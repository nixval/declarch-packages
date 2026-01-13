# 📦 Declarch Packages Registry

Community-maintained package configurations for [declarch](https://github.com/nixval/declarch).

## 🚀 Quick Start

```bash
# Install declarch (if you haven't)
curl -fsSL https://raw.githubusercontent.com/user/declarch/main/install.sh | sh

# Import a module from this registry
declarch init hyprland/niri-nico

# Sync your system
declarch sync
```

## 📁 Structure

Modules are organized by **category/contributor** to allow multiple configurations per topic:

```
modules/
├── hyprland/                    ← Hyprland WM category
│   ├── niri-nico.kdl           ← @niri-nico's setup
│   ├── minimal-setup.kdl       ← @minimalist's setup
│   └── another-contrib.kdl     ← Other contributor's setup
├── gaming/                      ← Gaming category
│   ├── steam-setup.kdl         ← @gamer123's setup
│   └── competitive-setup.kdl   ← Competitive gaming setup
└── dev/                        ← Development category
    ├── rust-toolchain.kdl      ← @rustacean's setup
    └── python-env.kdl          ← Python environment
```

Each `.kdl` file contains **cross-distro packages**:
- `aur-packages {}` - Arch Linux AUR (auto-skipped on non-Arch)
- `packages {}` - Soar packages (works on all distros)
- `flatpak-packages {}` - Flatpak apps (works on all distros)

## 🎯 Usage Examples

### Import a Module

```bash
# Import Hyprland setup by @niri-nico
declarch init hyprland/niri-nico

# This downloads modules/hyprland/niri-nico.kdl and:
# - Auto-creates ~/.config/declarch/ if not exists
# - Adds it to ~/.config/declarch/modules/hyprland/niri-nico.kdl
# - Auto-injects import into your declarch.kdl

# Sync to install
declarch sync
```

### Multiple Modules

```bash
# Import multiple configurations
declarch init hyprland/niri-nico
declarch init gaming/steam-setup
declarch init dev/rust-toolchain

# All configs are now imported
declarch check --verbose  # See what will be installed
```

### Discover Available Modules

```bash
# Browse the registry
# https://github.com/nixval/declarch-packages/tree/main/modules

# Or list categories:
ls modules/
# hyprland/  gaming/  dev/
```

## 🌍 Cross-Distro Support

### Arch Linux
```bash
declarch init hyprland/niri-nico
declarch sync
# Installs: AUR packages + Soar packages + Flatpak packages
```

### Debian/Ubuntu
```bash
declarch init hyprland/niri-nico
declarch sync
# Installs: Soar packages + Flatpak packages (AUR skipped)
```

### Fedora
```bash
declarch init hyprland/niri-nico
declarch sync
# Installs: Soar packages + Flatpak packages (AUR skipped)
```

## 📝 Module Format

Each module file contains all three package types:

```kdl
// hyprland/niri-nico.kdl

// AUR Packages (Arch Linux only)
aur-packages {
    hyprland
    waybar
    rofi-wayland
}

// Soar Packages (all distros)
packages {
    bat
    exa
    ripgrep
}

// Flatpak Packages (all distros)
flatpak-packages {
    org.mozilla.firefox
    com.spotify.Client
}
```

## 📂 Available Categories

### Window Managers (`hyprland/`)
- **niri-nico.kdl** - Complete Hyprland setup with Waybar, Rofi, theming
- **minimal-setup.kdl** - Bare-bones Hyprland essentials only

### Gaming (`gaming/`)
- **steam-setup.kdl** - Steam, Lutris, Heroic, launchers + tools
- **competitive-setup.kdl** - Optimized for competitive gaming

### Development (`dev/`)
- **rust-toolchain.kdl** - Complete Rust development environment
- **python-env.kdl** - Python development with data science tools

## 🤝 Contributing

Contributions are welcome! This is a **community registry** where everyone can share their configurations.

### How to Contribute

#### 1. Choose Your Module Path

```
category/your-name.kdl
```

- **category**: `hyprland`, `gaming`, `dev`, etc.
- **your-name**: Your unique identifier (username, nickname, etc.)

Examples:
- `hyprland/niri-nico.kdl` - Your Hyprland setup
- `gaming/steam-gamer.kdl` - Your gaming config
- `dev/rust-dev.kdl` - Your Rust development setup

#### 2. Create Your Module

```bash
# Fork and clone this repo
git clone https://github.com/YOUR_USERNAME/declarch-packages
cd declarch-packages

# Create your module file
cat > modules/hyprland/your-name.kdl << 'EOF'
// Your Name's Hyprland Setup
// Contributor: @yourusername
// Category: hyprland
//
// Usage:
//   declarch init hyprland/your-name

aur-packages {
    hyprland
    waybar
}

packages {
    bat
    exa
}

flatpak-packages {
    org.mozilla.firefox
}
