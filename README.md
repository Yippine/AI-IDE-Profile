# AI-IDE-Profile

A centralized repository for managing user profiles and configurations across AI-powered IDE platforms, including Cursor, Kiro, and other VS Code-based development environments.

## 📋 Overview

This project serves as a comprehensive storage solution for:

- **Extension configurations** - Installed extensions and their settings
- **User settings** - IDE preferences and customizations
- **Keybinding configurations** - Custom keyboard shortcuts
- **MCP (Model Context Protocol) tool settings** - AI assistant configurations
- **Global extension settings** - Cross-project extension preferences
- **Workspace configurations** - Project-specific settings

## 🏗️ Project Structure

```
AI-IDE-Profile/
├── Cursor/                    # Cursor IDE configurations
│   └── User/
│       └── profiles/          # User profile settings
│           ├── extensions.json
│           ├── keybindings.json
│           └── settings.json
├── Kiro/                      # Kiro IDE configurations
│   ├── User/                  # User-specific settings
│   │   ├── keybindings.json
│   │   ├── settings.json
│   │   └── globalStorage/     # Global storage data
│   └── extensions/            # Installed extensions
└── README.md
```

## 🚀 Supported IDEs

### Cursor

- **Status**: Actively maintained
- **Features**: Full profile support with extensions, settings, and keybindings
- **Configuration Path**: `Cursor/User/profiles/`

### Kiro

- **Status**: Limited usage (potential future removal)
- **Features**: Basic settings and extension management
- **Configuration Path**: `Kiro/User/` and `Kiro/extensions/`

## 📦 Featured Extensions

The repository includes configurations for popular development extensions:

### Development Tools

- **Claude Code** - AI-powered coding assistant
- **GitLens** - Advanced Git integration
- **Prettier** - Code formatting
- **Docker** - Container development support
- **Remote SSH** - Remote development capabilities

### Language Support

- **Python** (with Pylance, Black formatter, isort)
- **JavaScript/TypeScript**
- **YAML** - Configuration file support
- **Dockerfile** - Enhanced Docker syntax

### Productivity

- **Todo Tree** - Task management in code
- **Rainbow CSV** - Enhanced CSV viewing
- **PDF Viewer** - In-editor PDF support
- **MongoDB** - Database integration

### Themes & UI

- **Catppuccin** - Modern color themes
- **Custom UI Style** - Interface customization

## 🔧 Configuration Management

### Extension Settings

Extensions are managed through `extensions.json` files that specify:

- Extension identifiers
- Version requirements
- Enable/disable status

### User Settings

Centralized in `settings.json` files containing:

- Editor preferences
- Theme configurations
- Language-specific settings
- Extension-specific options

### Keybinding Customizations

Custom shortcuts defined in `keybindings.json` files for:

- Editor commands
- Extension-specific actions
- Workflow optimizations

## 🔄 Synchronization

This repository enables:

- **Cross-platform sync** - Share configurations between different machines
- **IDE migration** - Easy transfer between different VS Code-based editors
- **Backup & restore** - Version-controlled configuration history
- **Team sharing** - Standardized development environments

## 📝 Usage

### Setting Up New Environment

1. Clone this repository
2. Copy relevant configuration files to your IDE's user directory
3. Install extensions from `extensions.json`
4. Restart IDE to apply settings

### Updating Configurations

1. Make changes in your IDE
2. Export updated configuration files
3. Commit changes to this repository
4. Sync across other environments

## 🤝 Contributing

This is a personal configuration repository, but contributions for:

- Configuration optimization suggestions
- Extension recommendations
- Documentation improvements

are welcome through issues and pull requests.

## 📄 License

This project contains personal configurations and settings. Feel free to use as reference for your own IDE setup.

## 🔗 Related Projects

- [Cursor IDE](https://cursor.sh/) - AI-powered code editor
- [Visual Studio Code](https://code.visualstudio.com/) - Base editor platform
- [Claude Code Extension](https://github.com/anthropics/claude-code) - AI coding assistant
