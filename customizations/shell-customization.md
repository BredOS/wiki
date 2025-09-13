---
title: BredOS Shell Customization Guide 🐚🎨
description: This guide will help you customize your BredOS experience by changing and enhancing your shell! 🚀 Whether you prefer Bash, Zsh, Fish, or Nushell, you'll find everything you need right here. Let’s dive in! 🌊
published: true
date: 2025-09-13T10:30:59.488Z
tags: customization, shell
editor: markdown
dateCreated: 2024-09-20T19:39:08.509Z
---

# BredOS Shell Customization Guide 🐚🎨

This guide will help you customize your BredOS experience by changing and enhancing your shell! 🚀 Whether you prefer Bash, Zsh, Fish, or Nushell, you'll find everything you need right here. Let’s dive in! 🌊


## 1. Bash 🐢
> Bash is the default shell in BredOS. 
{.is-info}

Let’s start with setting it up or making Bash your default shell!

### 1.1 Install Bash 🛠️
To install Bash, run:
```bash
sudo pacman -S bash
```

### 1.2 Set Bash as Default Shell ⚙️
1. To list all installed shells, run:
   ```bash
   chsh -l
   ```
2. To set Bash as your default shell:
   ```bash
   chsh -s /usr/bin/bash
   ```
3. Log out and log back in to start using Bash as your shell. 🔄

### 1.3 Oh My Bash 💡
Improve Bash with **Oh My Bash**, a framework that adds themes, plugins, and other cool enhancements! 🌟

---

## 2. Zsh ⚡
Zsh is a powerful shell with many advanced features that make it more versatile than Bash.

### 2.1 Install Zsh 🛠️
To install Zsh, run:
```bash
sudo pacman -S zsh
```

### 2.2 Features 🌟
- **Better Tab Completion** ⌨️: Zsh shows only valid destinations when using commands like `cd`.  
- **Better History Search** 🔍: Type part of a previous command and press ⬆️ to search through your history.

### 2.3 Set Zsh as Default Shell ⚙️
1. To list all installed shells, run:
   ```bash
   chsh -l
   ```
2. To set Zsh as your default shell:
   ```bash
   chsh -s /usr/bin/zsh
   ```
3. Log out and log back in to switch to Zsh! 🔄

### 2.4 Oh My Zsh 🧩
**Oh My Zsh** is a community-driven framework that enhances Zsh with themes and plugins, giving you even more power and flexibility. ✨

---

## 3. Fish 🐠
**Fish** (the friendly interactive shell) focuses on ease of use and comes with great features out of the box.

### 3.1 Install Fish 🛠️
To install Fish, run:
```bash
sudo pacman -S fish
```

### 3.2 Features 🌟
- **Autosuggestions** 🤖: Fish suggests commands as you type, based on your history.
- **Web-Based Configuration** 🌐: Customize your shell’s appearance and behavior via a web interface.
- **Works Out of the Box** 🧰: Tab completion, syntax highlighting, and more without any extra setup!

### 3.3 Set Fish as Default Shell ⚙️
1. To list all installed shells, run:
   ```bash
   chsh -l
   ```
2. To set Fish as your default shell:
   ```bash
   chsh -s /usr/bin/fish
   ```
3. Log out and log back in to enjoy Fish! 🔄

### 3.4 Oh My Fish 🎣
Use **Oh My Fish** to add plugins and themes to Fish, enhancing its functionality and aesthetics. 🌈

---

## 4. Nushell 🧠
**Nushell** takes a modern approach to shell scripting, treating all input as structured data, making it easier to handle.

### 4.1 Install Nushell 🛠️
To install Nushell, run:
```bash
sudo pacman -S nushell
```

### 4.2 Features 🌟
- **Everything is Data** 📊: Nu pipelines handle structured data for easy filtering, sorting, and selecting.
- **Powerful Plugins** 🔌: Easily extend Nushell with a wide range of plugins.
- **Great Error Messages** 🛠️: Nushell helps you catch errors early with helpful error messages.

### 4.3 Set Nushell as Default Shell ⚙️
1. To list all installed shells, run:
   ```bash
   chsh -l
   ```
2. To set Nushell as your default shell:
   ```bash
   chsh -s /usr/bin/nu
   ```
3. Log out and log back in to switch to Nushell! 🔄
