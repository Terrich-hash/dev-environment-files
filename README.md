 # **dev-environment-files** 

Reproducible macOS development environment

Minimal • Keyboard-driven • Performance-focused

This repository contains my complete macOS development setup built around a tiling window manager, terminal-first workflow, and automation.

# System Architecture
```
                ┌──────────────────────────┐
                │          macOS           │
                └─────────────┬────────────┘
                              │
                 ┌────────────┴────────────┐
                 │        Homebrew         │
                 │   (package manager)     │
                 └────────────┬────────────┘
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
   ┌────┴────┐           ┌────┴────┐           ┌────┴────┐
   │  Kitty  │           │  yabai  │           │  skhd   │
   │Terminal │           │  WM     │           │ Hotkeys │
   └────┬────┘           └────┬────┘           └────┬────┘
        │                     │                     │
        └──────────────┬──────┴──────────────┬──────┘
                       │                     │
                 ┌─────┴─────┐         ┌─────┴─────┐
                 │ Monitoring │         │  UI Layer  │
                 │ btop/htop  │         │ spicetify  │
                 └────────────┘         └────────────┘

```

# Repository Structure
```
.
├── .config/
│   ├── btop/
│   ├── htop/
│   ├── kitty/
│   ├── ncspot/
│   ├── neofetch/
│   ├── skhd/
│   ├── spicetify/
│   └── yabai/
├── Brewfile
├── bootstrap.sh
└── README.md
```
# Core Components
Terminal
- Kitty — GPU-accelerated terminal

Window Management
- yabai — Tiling window manager for macOS
- skhd — Keyboard shortcut daemon

 Monitoring
- btop
- htop
- neofetch

UI Customization
- spicetify
- ncspot

# Quick Start (New Machine Setup)

Clone Repository
```
git clone git@github.com:Terrich-hash/dev-environment-files.git
cd dev-environment-files
```

Run Bootstrap Script
```
chmod +x bootstrap.sh
./bootstrap.sh
```

This will:
- Install Homebrew (if missing)
- Install required packages via Brewfile
- Symlink configs into ~/.config
- Prepare environment automatically

Brewfile

Create a file named **Brewfile** in the root:
```
brew "kitty"
brew "yabai"
brew "skhd"
brew "btop"
brew "htop"
brew "neofetch"
brew "spicetify-cli"
brew "ncspot"
```
Install all packages:
```
brew bundle
```

# bootstrap.sh

Create this file in the root of the repo:
```
#!/bin/bash

set -e

echo " Setting up development environment..."

# Install Homebrew if missing
if ! command -v brew &> /dev/null; then
  echo "Installing Homebrew..."
  /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
fi

# Update brew
brew update

# Install packages from Brewfile
brew bundle

# Ensure config directory exists
mkdir -p ~/.config

# Symlink all configs
for dir in .config/*; do
  name=$(basename "$dir")
  ln -sf "$(pwd)/.config/$name" "$HOME/.config/$name"
done

echo " Setup complete."
```

# Daily Workflow
Update Configurations

```
git add .
git commit -m "Update configuration"
git push
```

Sync on New Machine

```
git pull
./bootstrap.sh
```
# Dotfiles Philosophy
```
           Clean Setup
                │
                ▼
      Version-Controlled Config
                │
                ▼
       Reproducible Machines
                │
                ▼
        Zero Setup Friction
```


# Uses :
- Instant productivity on new machines
- No manual reconfiguration
- Clean engineering workflow
- Reproducible environment
