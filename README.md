

## 🔧 Backends

Package manager backends are now external and loaded from `~/.config/declarch/backends/`.

### Available Backends

#### Node.js Package Managers
- **npm** - Official Node.js package manager
- **yarn** - Fast, reliable, secure by Facebook  
- **pnpm** - Fast, disk space efficient
- **bun** - Incredibly fast JavaScript toolkit

#### Language-Specific
- **pip** - Python package installer
- **cargo** - Rust package manager

#### System Package Managers
- **brew** - Homebrew for macOS/Linux
- **flatpak** - Universal Linux apps
- **soar** - Static binary package manager

### Installing Backends

```bash
# Install specific backends
declarch init --backend npm,cargo,brew

# This copies backends from ../declarch-packages to:
# ~/.config/declarch/backends/npm.kdl
# ~/.config/declarch/backends/cargo.kdl
# ~/.config/declarch/backends/brew.kdl
```

### Backend Format

Each backend includes metadata and configuration:

```kdl
backend "npm" {
    meta {
        title "Node Package Manager"
        description "Official package manager for Node.js"
        version "1.0.0"
        author "declarch-community"
        tags "nodejs" "javascript" "npm"
        homepage "https://www.npmjs.com"
        license "MIT"
        platforms "linux" "macos" "windows"
        requires "nodejs"
        examples "typescript" "eslint" "prettier"
    }
    
    binary "npm"
    list "npm list -g --json" { format json }
    install "npm install -g {packages}"
    remove "npm uninstall -g {packages}"
}
```

### Creating Custom Backends

1. Copy an existing backend as template
2. Modify commands and metadata
3. Place in `~/.config/declarch/backends/`
4. No Rust code needed!

## 🤝 Contributing Backends

Add new backends to `backends/` directory:

```bash
# Create your backend
cat > backends/mybackend.kdl << 'EOF'
backend "mybackend" {
    meta {
        title "My Backend"
        description "Description of my backend"
        version "1.0.0"
        author "your-name"
        tags "tag1" "tag2"
    }
    
    binary "mybackend"
    list "mybackend list" { format json }
    install "mybackend install {packages}"
    remove "mybackend remove {packages}"
}
EOF

# Submit PR
```
