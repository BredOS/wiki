---
title: Configuring Governors
description: Using govctl to manage system governors
published: true
date: 2025-09-15T06:42:25.101Z
tags:
editor: markdown
dateCreated: 2025-05-07T12:47:49.033Z
---

# 1. 簡介

BredOS ships by default the tool `govctl` in package `bredos-govctl`.
It is enabled by default and will set the performance according to available battery power.

This should be installed by default. If not, install it with

```
sudo pacman -S bredos-govctl
```

The tool will continuously set the governor to the specified settings, overrides or other tools will not function.
Uninstall the package if this is a problem for your workflow.

```
sudo pacman -R bredos-govctl
```

## 1.1 Default behaviour

GovCtl will by default ensure maximum performance across all attached devices, if there is no onboard battery, or the system is plugged in.

If the system holds sufficient charge, but it's not plugged in, it'll maintain most of the performance, limiting GPU speed and cpu boost.

If the system does not hold a sufficient charge (20% is the default point at which this is determined),
the system will minimize power draw, at the detriment of performance and response time.
This for example will make RK3588 boards only run at 300mHz.

If you do not like the defaults, they can all be changed.

## 1.2 Viewing governor state

To view the currently applied governor, just run `govctl`, root access is not required.

```
govctl
```

```
---------------------------------------
Currently applied governor: performance
---------------------------------------

usage: govctl [-h] [-g {powersave,conservative,performance}]
              [-b {powersave,conservative,performance}] [-e] [-d]
              [-p POWERSAVE_PERCENT]

Governor configuration tool

options:
  -h, --help            show this help message and exit
  -g, --set-governor {powersave,conservative,performance}
                        Set desired governor
  -b, --set-battery-governor {powersave,conservative,performance}
                        Set desired governor while running on battery power
  -e, --enable-battery-detection
                        Enable battery state detection
  -d, --disable-battery-detection
                        Disable battery state detection
  -p, --powersave-percent POWERSAVE_PERCENT
                        Percentage at which powersave triggers
```

## 1.3 Setting a different powersave point

As the help menu states, using option `-p` will allow you to reconfigure the point at which the governor `powersave` will be applied at. By default this is 20%, and can be set to be 1% to 80%.

Reconfigure as follows:

```
sudo govctl -p 30
```

This would set it to trigger at 30%.

## 1.4 Changing the applied governor

By default, when plugged in or no batteries are present, the system will maintain maximum performance.
The flag `-g` sets the governor used when plugged in. If you want it to be `conservative` while your system is running of of power run:

```
sudo govctl -g conservative
```

The flag `-b` sets the governor used when **NOT** plugged in. If you want it to be `performance` while your system is running of of battery run:

```
sudo govctl -b performance
```

## 1.5 Disabling battery detection

Disabling battery detection with:

```
sudo govctl -d
```

Will ensure that at all times the "plugged in" governor is applied at all times.

To undo this, run:

```
sudo govctl -e
```