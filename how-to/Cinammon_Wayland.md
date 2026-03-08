---
title: Cinnamon Wayland with GPU Acceleration on RK3588
description: Switching Cinnamon from X11 to Wayland with hardware-accelerated rendering on RK3588 boards
published: true
date: 2026-03-08T15:58:02.631Z
tags: cinnamon, wayland, gpu, panthor, rk3588
editor: markdown
dateCreated: 2026-03-07T16:06:02.388Z
---

# 1. Introduction

Cinnamon supports Wayland sessions starting from version `6.4`. On RK3588 boards, switching from X11 to Wayland requires extra configuration because the SoC exposes two separate DRM devices: one for display output and one for GPU rendering. Without proper setup, Cinnamon's compositor (`Muffin`) falls back to `llvmpipe` software rendering, resulting in poor desktop performance.

This guide walks you through enabling a fully GPU-accelerated Cinnamon Wayland session on BredOS.

# 2. Prerequisites

## 2.1 Required Packages

- Verify that all required packages are installed:

```
sudo pacman -S --needed cinnamon muffin wayland xorg-xwayland libinput pipewire mesa libdrm
```

## 2.2 Kernel and GPU Driver

This guide assumes you already have the Panthor GPU driver enabled. If you are still using Panfork (the default on BredOS for RK35xx), follow the [Setup Panthor on Mali GPUs with RK3588](/en/how-to/how-to-setup-panthor) guide first, then return here.

- Verify that the `panthor` module is loaded:

```
lsmod | grep panthor
```

You should see `panthor` in the output. If not, load it manually:

- Load the module:

```
sudo modprobe panthor
```

> Panthor requires a BredOS kernel `6.12` or later. If the module is not available, update your kernel.
{.is-warning}

## 2.3 User Permissions

Your user must belong to the `render` and `video` groups to access the GPU render node. Without these permissions, applications silently fall back to software rendering.

- Check your current groups:

```
groups
```

If `render` or `video` are missing from the output, add your user to both groups:

```
sudo usermod -aG render,video $USER
```

- Log out and log back in for the group change to take effect.

- Verify that the GPU render node exists and is accessible:

```
ls -la /dev/dri/
```

You should see at least `card0`, `card1`, and `renderD128`. The `renderD128` device should be owned by group `render` with permission `crw-rw----`.

> If `/dev/dri/renderD128` is missing entirely, the Panthor driver failed to initialize. Check `dmesg | grep -i panthor` for errors.
{.is-warning}

# 3. Understanding the Dual-GPU Setup

On RK3588 boards, the kernel exposes two DRI card devices. This is the root cause of most GPU acceleration issues with Cinnamon Wayland.

- The following table shows the role of each device:

| Device | Driver | Role |
|--------|--------|------|
| `/dev/dri/card0` | `rockchip-drm` | Display controller (HDMI/DP output). No 3D rendering. |
| `/dev/dri/card1` | `panthor` | GPU (Mali-G610). Handles all 3D rendering. |
| `/dev/dri/renderD128` | `panthor` | GPU render node (used by applications for 3D). |
{.dense}

The problem: `Muffin` (Cinnamon's compositor, a fork of GNOME's Mutter) tries to use `card0` for rendering by default. Since `rockchip-drm` has no 3D capabilities, it falls back to `llvmpipe` (CPU-based software rendering).

The solution: tell Muffin to use the `panthor` render node for GPU acceleration while keeping `rockchip-drm` for display output.

- Verify your device layout:

```
ls -l /dev/dri/
```

- Check which driver is behind each card:

```
udevadm info -q property -n /dev/dri/card0 | grep DRIVER
udevadm info -q property -n /dev/dri/card1 | grep DRIVER
```

# 4. Configure GPU Selection

## 4.1 Create a Udev Rule

The most reliable method is a `udev` rule that tells Muffin which device to prefer for rendering.

- Create the udev rule file:

```
sudo nano /etc/udev/rules.d/61-mutter-panthor.rules
```

- Add the following content:

```
# RK3588: mark Panthor render node as preferred GPU for Mutter/Muffin
SUBSYSTEM=="drm", KERNEL=="card1", DRIVERS=="panthor", TAG+="mutter-device-preferred-primary"
```

- Reload udev rules:

```
sudo udevadm control --reload
sudo udevadm trigger
```

- Verify that the tag was applied:

```
udevadm info -q all -n /dev/dri/card1 | grep mutter
```

You should see `mutter-device-preferred-primary` in the output.

## 4.2 Set Environment Variables

In addition to the udev rule, set environment variables that help Muffin and Mesa select the correct GPU.

- Create the environment configuration file:

```
sudo nano /etc/environment.d/90-rk3588-gpu.conf
```

- Add the following content:

```
# RK3588 GPU selection for Mutter/Muffin Wayland
MUTTER_ALLOW_HYBRID_GPUS=1
```

> Do not set `WLR_DRM_DEVICES` - that variable is for wlroots-based compositors (Sway, Hyprland), not for Muffin. Setting it has no effect on Cinnamon.
{.is-warning}

## 4.3 Remove Incorrect Configuration

If you previously created a `/etc/environment.d/gpu-wayland.conf` with variables like `WLR_DRM_DEVICES`, `MESA_LOADER_DRIVER_OVERRIDE`, or `MUTTER_DEBUG_FORCE_EGL_STREAM`, remove or rename it. These variables do not apply to Muffin and may cause unexpected behavior.

- Check for stale configuration:

```
ls /etc/environment.d/
```

- Remove any incorrect files:

```
sudo rm /etc/environment.d/gpu-wayland.conf
```

# 5. Select the Wayland Session

## 5.1 From the Login Screen

Most display managers (LightDM, GDM, SDDM) allow choosing the session type from the login screen.

- Look for a gear icon or session selector on the login screen
- Select `Cinnamon (Wayland)` instead of `Cinnamon`
- Log in normally

## 5.2 Verify the Session Type

After logging in:

- Confirm you are running a Wayland session:

```
echo $XDG_SESSION_TYPE
```

The output should be `wayland`.

# 6. Verify GPU Acceleration

## 6.1 Check the Renderer

On Wayland, you must use `eglinfo` to check GPU acceleration. The `glxinfo` command goes through XWayland and may incorrectly show `llvmpipe` even when the compositor is GPU-accelerated.

- Install `eglinfo` if not present:

```
sudo pacman -S --needed mesa-utils
```

- Check the EGL renderer:

```
eglinfo -B 2>/dev/null | grep -A2 "Device platform"
```

You should see `Mali-G610` or `panthor` in the output, not `llvmpipe`.

- Alternatively, check what Muffin reports in its logs:

```
journalctl --user -b -u cinnamon-session | grep -i "renderer\|gpu\|egl\|drm"
```

## 6.2 Check Compositing Status

- Open Cinnamon's System Settings, navigate to `General` and check that `Compositing` is enabled
- Alternatively, check from terminal:

```
dconf read /org/cinnamon/muffin/compositing-manager
```

The output should be `true`.

# 7. Troubleshooting

## 7.1 glxinfo Still Shows llvmpipe

This is expected on Wayland. The `glxinfo` command uses the GLX protocol which goes through XWayland. Even with a fully GPU-accelerated Wayland session, `glxinfo` may report `llvmpipe` because XWayland may not have access to the GPU render node.

- Use `eglinfo` instead to verify the Wayland renderer (see [section 6.1](#h-61-check-the-renderer))
- To fix `glxinfo` specifically for X11 applications running under XWayland, try:

```
DRI_PRIME=1 glxinfo -B
```

## 7.2 Panthor Loaded but No GPU Rendering

If `lsmod | grep panthor` shows the module is loaded but applications still use `llvmpipe`, work through these checks in order:

**Check 1: Render node exists**

```
ls -la /dev/dri/
```

If `renderD128` is missing, Panthor failed to initialize. Check the kernel log:

```
dmesg | grep -i panthor
```

Common causes:
- Missing firmware: check `dmesg | grep -i firmware | grep -i mali`. The `mali-G610-firmware` package must be installed and the firmware files must be in `/lib/firmware/arm/mali/arch10.8/`
- Device tree overlay not enabled: follow the [Setup Panthor](/en/how-to/how-to-setup-panthor) guide to enable the `rockchip-rk3588-panthor-gpu` DTBO

**Check 2: User permissions**

```
ls -la /dev/dri/renderD128
groups
```

If `renderD128` exists but your user is not in the `render` group, see [section 2.3](#h-23-user-permissions).

**Check 3: Mesa detects the GPU**

```
eglinfo -B 2>/dev/null | grep -A5 "Device platform"
```

If the output shows empty devices or only `llvmpipe`, Mesa is not finding the Panthor driver. Verify that you are using the standard `mesa` package (not `mesa-panfork-git`):

```
pacman -Q mesa
```

If it shows `mesa-panfork-git`, replace it:

```
sudo pacman -S mesa
```

**Check 4: No conflicting libMali**

```
pacman -Q | grep -i mali
```

You should see `mali-G610-firmware` only. If any `libmali-valhall-g610` package is installed, it conflicts with Mesa's open source driver:

```
sudo pacman -R libmali-valhall-g610
```

**Check 5: Environment variable overrides**

Stale or incorrect environment variables can force Mesa to use the wrong driver:

```
env | grep -iE "mesa|gallium|dri|gpu|libgl|egl"
```

If any of `MESA_LOADER_DRIVER_OVERRIDE`, `LIBGL_ALWAYS_SOFTWARE`, `GALLIUM_DRIVER`, or `__GLX_VENDOR_LIBRARY_NAME` are set, unset them or remove them from your environment configuration files.

## 7.3 Vulkan Errors (VK_ERROR_INCOMPATIBLE_DRIVER)

If you see errors like `ZINK: vkCreateInstance failed (VK_ERROR_INCOMPATIBLE_DRIVER)` when running graphical applications:

- This means Mesa is trying to use the Zink driver (OpenGL-over-Vulkan) but no Vulkan driver is available. Install the Vulkan packages:

```
sudo pacman -S --needed vulkan-icd-loader vulkan-panfrost
```

- Verify that PanVK is detected:

```
vulkaninfo --summary 2>/dev/null | grep -A3 "GPU"
```

You should see `Mali-G610` or `panvk` in the output.

> This error does not prevent GPU-accelerated OpenGL from working. If Panthor is correctly set up, Mesa uses the native Gallium driver for OpenGL without going through Zink/Vulkan. However, installing PanVK is recommended for applications that require Vulkan.
{.is-info}

## 7.4 Cinnamon Falls Back to Software Rendering

If you have confirmed that Panthor works (the checks in [section 7.2](#h-72-panthor-loaded-but-no-gpu-rendering) all pass) but Cinnamon's compositor still uses software rendering:

- Verify the udev rule is applied (see [section 4.1](#h-41-create-a-udev-rule)):

```
udevadm info -q all -n /dev/dri/card1 | grep mutter
```

- Check that `MUTTER_ALLOW_HYBRID_GPUS=1` is set (see [section 4.2](#h-42-set-environment-variables))

- Check Muffin's log for errors:

```
journalctl --user -b | grep -i muffin
```

- Make sure compositing is not disabled:

```
dconf read /org/cinnamon/muffin/compositing-manager
```

If the output is `false` or empty, enable it:

```
dconf write /org/cinnamon/muffin/compositing-manager true
```

## 7.5 Black Screen or Login Loop


If the Wayland session fails to start:

- Switch to a TTY with `Ctrl+Alt+F2` and log in
- Check the session log:

```
journalctl --user -b -u cinnamon-session
```

- As a workaround, fall back to the X11 session from the login screen and verify your configuration

## 7.6 Screen Tearing or Poor Performance

If the session starts but performance is poor:

- Verify compositing is enabled (see [section 6.2](#h-62-check-compositing-status))
- Check that no Flatpak or Snap version of Cinnamon is overriding the system session
- Try adding `CLUTTER_PAINT=disable-clipped-redraws:disable-culling` to `/etc/environment.d/90-rk3588-gpu.conf` if you see rendering artifacts

## 7.7 Reverting to X11

If Wayland does not work correctly, you can always switch back to X11 from the login screen by selecting the `Cinnamon` session (without the "Wayland" label).

# 8. Summary

- The following table summarizes the changes needed:

| What | File | Content |
|------|------|---------|
| Udev rule | `/etc/udev/rules.d/61-mutter-panthor.rules` | Tag `card1` as `mutter-device-preferred-primary` |
| Environment | `/etc/environment.d/90-rk3588-gpu.conf` | `MUTTER_ALLOW_HYBRID_GPUS=1` |
| Session | Login screen | Select `Cinnamon (Wayland)` |
{.dense}

# 9. References

- [Muffin source code](https://github.com/linuxmint/muffin) - Linux Mint
- [Mutter multi-GPU support](https://gitlab.gnome.org/GNOME/mutter) - GNOME
- [Mesa Panthor driver](https://docs.mesa3d.org/drivers/panthor.html) - Mesa
- [Setup Panthor on Mali GPUs with RK3588](https://wiki.bredos.org/en/how-to/how-to-setup-panthor) - BredOS Wiki
- [Armbian RK3588 GPU acceleration discussion](https://forum.armbian.com/topic/56374-expected-default-graphics-acceleration-for-rk3588/) - Armbian Forum