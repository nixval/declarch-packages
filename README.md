# 📦 Declarch Packages Registry

packages registry for [declarch](https://github.com/nixval/declarch).

## Structure
Modules are organized by **Topic**. Inside each topic folder, files are named by **Distro** or `default` for universal packages.

```text
modules/
  ├── hyprland/
  │     ├── default.kdl   (Universal: Flatpak)
  │     ├── arch.kdl      (Arch Linux specific)
  │     └── debian.kdl    (Debian/Ubuntu specific)
```

## How to Use
```bash
declarch init modules/hyprland
```

## Contributing
1. Create a new folder in `modules/`.
2. Add `arch.kdl` (required) and `default.kdl` (optional).
3. Open a Pull Request.
