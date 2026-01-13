# 📦 Declarch Packages Registry

Community-maintained package configurations for [declarch](https://github.com/nixval/declarch).

## 🚀 Quick Start

```bash
# Install declarch (if you haven't)
curl -fsSL https://raw.githubusercontent.com/user/declarch/main/install.sh | sh

# Initialize with a module from this registry
declarch init hyprland      # Hyprland window manager setup
declarch init gaming        # Gaming setup
declarch init dev-rust      # Rust development setup

# Sync your system
declarch sync
```

## 📁 Structure

Modules are organized as **flat files** for simplicity:

```
modules/
├── hyprland.kdl          ← Full Hyprland setup
├── gaming.kdl            ← Gaming setup
├── dev-rust.kdl          ← Rust development setup
├── waybar.kdl            ← Waybar configuration
└── ...
```

Each `.kdl` file contains **cross-distro packages**:
- `aur-packages {}` - Arch Linux AUR (auto-skipped on non-Arch)
- `packages {}` - Soar packages (works on all distros)
- `flatpak-packages {}` - Flatpak apps (works on all distros)

## 🎯 Usage Examples

### Basic Usage

```bash
# Install Hyprland setup
declarch init hyprland

# This downloads modules/hyprland.kdl and:
# - Adds it to ~/.config/declarch/modules/hyprland.kdl
# - Auto-injects import into your declarch.kdl
# - Ready to sync!

declarch sync
```

### Multiple Modules

```bash
# Install multiple modules
declarch init hyprland
declarch init gaming
declarch init dev-rust

# All configs are now imported
declarch check --verbose  # See what will be installed
```

### Module Content

Each module file contains all package types:

```kdl
// Example: hyprland.kdl

// AUR packages (Arch Linux only)
aur-packages {
    hyprland
    waybar
    rofi-wayland
}

// Soar packages (all distros)
packages {
    bat
    exa
    ripgrep
}

// Flatpak packages (all distros)
flatpak-packages {
    org.mozilla.firefox
    com.spotify.Client
}
```

## 🌍 Cross-Distro Support

### Arch Linux
```bash
declarch init hyprland
declarch sync
# Installs: AUR packages + Soar packages + Flatpak packages
```

### Debian/Ubuntu
```bash
declarch init hyprland
declarch sync
# Installs: Soar packages + Flatpak packages (AUR skipped)
```

### Fedora
```bash
declarch init hyprland
declarch sync
# Installs: Soar packages + Flatpak packages (AUR skipped)
```

## 📝 Available Modules

### Window Managers
- **hyprland** - Hyprland wayland compositor + essential tools
- **sway** - Sway i3-compatible wayland compositor

### Development
- **dev-rust** - Rust development environment
- **dev-python** - Python development environment
- **dev-node** - Node.js development environment

### Gaming
- **gaming** - Steam, Lutris, launchers, and tools

### Terminal Tools
- **term-tools** - Modern CLI tools (bat, exa, fd, etc.)

### Desktop Applications
- **waybar** - Waybar status bar
- **rofi** - Rofi launcher/dmenu replacement

## 🤝 Contributing

Contributions are welcome! Here's how to add a module:

### 1. Create Module File

```bash
# Clone this repo
git clone https://github.com/nixval/declarch-packages
cd declarch-packages

# Create your module
cat > modules/your-module.kdl << 'EOF'
// Your Module Description
// Usage: declarch init your-module

aur-packages {
    package1
    package2
}

packages {
    package3
    package4
}

flatpak-packages {
    com.example.app
}
