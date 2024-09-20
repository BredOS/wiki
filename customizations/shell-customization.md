---
title: BredOS Shell Customization Guide 🐚🎨
description: This guide will help you customize your BredOS experience by changing and enhancing your shell! 🚀 Whether you prefer Bash, Zsh, Fish, or Nushell, you'll find everything you need right here. Let’s dive in! 🌊
published: true
date: 2024-09-20T19:45:03.972Z
tags: customization, shell
editor: markdown
dateCreated: 2024-09-20T19:39:08.509Z
---

# BredOS Shell Customization Guide 🐚🎨

This guide will help you customize your BredOS experience by changing and enhancing your shell! 🚀 Whether you prefer Bash, Zsh, Fish, or Nushell, you'll find everything you need right here. Let’s dive in! 🌊

---

## 📚 Table of Contents
* Bash 🐢
* Zsh ⚡
* Fish 🐠
* Nushell 🧠

---

## Bash 🐢
Bash is the default shell in BredOS. Let’s start with setting it up or making it your default shell!

### Install Bash 🛠️
To install Bash, run:
```bash
sudo pacman -S bash
```

### Set Bash as Default Shell ⚙️
1. To list all installed shells, run:
   ```bash
   chsh -l
   ```
2. To set Bash as your default shell:
   ```bash
   chsh -s /usr/bin/bash
   ```
3. If you're using systemd-homed, run:
   ```bash
   homectl update --shell=/usr/bin/bash user
   ```
4. Log out and log back in to start using Bash as your shell. 🔄

### Oh My Bash 💡
Improve Bash with **Oh My Bash**, a framework that adds themes, plugins, and other cool enhancements! 🌟

---

## Zsh ⚡
Zsh is a powerful shell with many advanced features that make it more versatile than Bash.

### Install Zsh 🛠️
To install Zsh, run:
```bash
sudo pacman -S zsh
```

### Features 🌟
- **Better Tab Completion** ⌨️: Zsh shows only valid destinations when using commands like `cd`.  
- **Better History Search** 🔍: Type part of a previous command and press ⬆️ to search through your history.

### Oh My Zsh 🧩
**Oh My Zsh** is a community-driven framework that enhances Zsh with themes and plugins, giving you even more power and flexibility. ✨

### Set Zsh as Default Shell ⚙️
1. To list all installed shells, run:
   ```bash
   chsh -l
   ```
2. To set Zsh as your default shell:
   ```bash
   chsh -s /usr/bin/zsh
   ```
3. If you're using systemd-homed, run:
   ```bash
   homectl update --shell=/usr/bin/zsh user
   ```
4. Log out and log back in to switch to Zsh! 🔄

---

## Fish 🐠
**Fish** (the friendly interactive shell) focuses on ease of use and comes with great features out of the box.

### Install Fish 🛠️
To install Fish, run:
```bash
sudo pacman -S fish
```

### Features 🌟
- **Autosuggestions** 🤖: Fish suggests commands as you type, based on your history.
- **Web-Based Configuration** 🌐: Customize your shell’s appearance and behavior via a web interface.
- **Works Out of the Box** 🧰: Tab completion, syntax highlighting, and more without any extra setup!

### Oh My Fish 🎣
Use **Oh My Fish** to add plugins and themes to Fish, enhancing its functionality and aesthetics. 🌈

### Set Fish as Default Shell ⚙️
1. To list all installed shells, run:
   ```bash
   chsh -l
   ```
2. To set Fish as your default shell:
   ```bash
   chsh -s /usr/bin/fish
   ```
3. If you're using systemd-homed, run:
   ```bash
   homectl update --shell=/usr/bin/fish user
   ```
4. Log out and log back in to enjoy Fish! 🔄

---

## Nushell 🧠
**Nushell** takes a modern approach to shell scripting, treating all input as structured data, making it easier to handle.

### Install Nushell 🛠️
To install Nushell, run:
```bash
sudo pacman -S nushell
```

### Features 🌟
- **Everything is Data** 📊: Nu pipelines handle structured data for easy filtering, sorting, and selecting.
- **Powerful Plugins** 🔌: Easily extend Nushell with a wide range of plugins.
- **Great Error Messages** 🛠️: Nushell helps you catch errors early with helpful error messages.

### Set Nushell as Default Shell ⚙️
1. To list all installed shells, run:
   ```bash
   chsh -l
   ```
2. To set Nushell as your default shell:
   ```bash
   chsh -s /usr/bin/nu
   ```
3. If you're using systemd-homed, run:
   ```bash
   homectl update --shell=/usr/bin/nu user
   ```
4. Log out and log back in to switch to Nushell! 🔄
