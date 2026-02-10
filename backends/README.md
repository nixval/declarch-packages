# Declarch Backend Registry

This directory contains backend configuration files for various package managers. Each `.kdl` file defines how declarch interacts with a specific package manager.

## Available Backends

### System Package Managers

| Backend | Description | Platforms |
|---------|-------------|-----------|
| `pacman` | Native Arch Linux package manager | Linux |
| `paru` | Feature-packed AUR helper (Rust) | Linux |
| `yay` | Alternative AUR helper (Go) | Linux |
| `aur` | Meta backend with auto-fallback (paru→yay→pacman) | Linux |
| `apt` | Advanced Package Tool (Debian/Ubuntu) | Linux |
| `dnf` | Dandified YUM (Fedora/RHEL) | Linux |
| `flatpak` | Universal Linux app distribution | Linux |
| `snap` | Universal packages by Canonical | Linux |
| `nix` | Purely functional package manager | Linux, macOS |
| `soar` | Static binary package manager | Linux |
| `brew` | Homebrew (macOS/Linux) | macOS, Linux |

### Language-Specific Package Managers

| Backend | Description | Platforms |
|---------|-------------|-----------|
| `npm` | Node.js package manager | Linux, macOS, Windows |
| `yarn` | Fast, reliable dependency management | Linux, macOS, Windows |
| `pnpm` | Fast, disk space efficient package manager | Linux, macOS, Windows |
| `bun` | Fast JavaScript toolkit | Linux, macOS |
| `pip` | Python package installer | Linux, macOS, Windows |
| `cargo` | Rust package manager | Linux, macOS, Windows |
| `gem` | Ruby package manager | Linux, macOS, Windows |
| `go` | Go tool installer | Linux, macOS, Windows |

## Meta Fields

Each backend has a `meta` section with the following fields:

| Field | Description | Example |
|-------|-------------|---------|
| `title` | Display name of the backend | `"NPM"` |
| `description` | Brief description | `"Node.js package manager"` |
| `version` | Backend config version | `"-"` (placeholder) |
| `author` | Original author | `"-"` (placeholder) |
| `maintained` | Current maintainer | `"nixval"` |
| `tags` | Search tags | `"nodejs" "javascript"` |
| `url` | Source code URL | `"-"` (placeholder) |
| `homepage` | Official website | `"https://www.npmjs.com"` |
| `license` | Software license | `"-"` (placeholder) |
| `created` | Creation date | `"2026-02-08"` |
| `platforms` | Supported platforms | `"linux" "macos"` |
| `requires` | Required dependencies | `"nodejs"` |
| `install-guide` | Installation instructions | `"-"` (placeholder) |

**Note:** Fields with value `"-"` are placeholders and will not be displayed during `init`.

## Backend Configuration Format

```kdl
backend "name" {
    meta {
        title "Backend Name"
        description "Description here"
        maintained "nixval"
        tags "tag1" "tag2"
        url "-"
        homepage "https://example.com"
        license "-"
        created "2026-02-08"
        platforms "linux"
        requires "dependency"
        install-guide "-"
    }
    
    binary "command"
    sudo "true"  // or "false"
    
    list "list command" {
        format tsv  // tsv, json, whitespace, regex, plain
        name_col 0
        version_col 1
    }
    
    install "install command {packages}"
    remove "remove command {packages}"
    update "update command"
    upgrade "upgrade command"
    
    noconfirm "-y"
    
    search "search command {query}" {
        format tsv
        name_col 0
        desc_col 1
    }
}
```

### Important Notes

- Use `"true"` / `"false"` (strings) for boolean values like `sudo`, not bare `true` / `false`
- The `{packages}` placeholder in commands will be replaced with actual package names
- The `{query}` placeholder in search commands will be replaced with the search term

## Using Backends

### In your declarch.kdl

```kdl
// Import backends
imports {
    "backends/paru.kdl"
    "backends/flatpak.kdl"
    "backends/npm.kdl"
}

// Use packages with specific backends
packages {
    // Backend-specific packages
    paru:google-chrome
    flatpak:com.spotify.Client
    npm:typescript
}

// Or use blocks
packages:paru {
    visual-studio-code-bin
    discord
}
```

### Command Line

```bash
# Install with specific backend
dcl install paru:google-chrome
dcl install npm:eslint

# Sync specific backend only
dcl sync --backend paru
dcl sync --backend flatpak

# Search in specific backend
dcl search firefox --backends paru,flatpak

# Initialize multiple backends
dcl init --backend apt,aur,paru -y

# List available backends
dcl init --list backends
```

## Backend Priority / Fallback

The `aur` backend is special - it provides automatic fallback:

1. **paru** - Tries to use paru first
2. **yay** - Falls back to yay if paru unavailable  
3. **pacman** - Falls back to pacman for official repos

## Creating Custom Backends

### Basic template:

```kdl
backend "mybackend" {
    meta {
        title "My Backend"
        description "Description of my backend"
        maintained "nixval"
        tags "package-manager" "custom"
        url "-"
        homepage "-"
        license "-"
        created "2026-02-08"
        platforms "linux"
        requires "mybinary"
        install-guide "-"
    }
    
    binary "mycommand"
    sudo "false"
    
    list "mycommand list" {
        format whitespace
        name_col 0
    }
    
    install "mycommand install {packages}"
    remove "mycommand remove {packages}"
}
```

## Contributing

To add a new backend:

1. Create a new `.kdl` file in this directory
2. Use `"-"` for unknown meta fields (they will be hidden in output)
3. Set `maintained "nixval"` (or your name if maintaining)
4. Test the backend with `declarch check validate`
5. Submit a PR

## License

All backend configurations are provided under MIT License unless otherwise specified.
