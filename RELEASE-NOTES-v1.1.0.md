# LightJS CLI v1.1.0 - Release Notes

**Release Date:** November 9, 2025

## 🎉 New Features

### Web Mode
- **Browser-based deployment** - Run your app in any browser without WebView dependency
- New command: `light start --web` (or `light start -w`)
- Python HTTP server on port 3000
- Automatic browser launch
- Perfect for web deployment and cross-platform testing

### Comprehensive Error Handling
- **Standardized exit codes** for programmatic error detection
- **User-friendly error messages** with context and actionable suggestions
- **Safe filesystem operations** with automatic error recovery
- Consistent error experience across all commands

## 🔧 Improvements

### Documentation
- **New developer-focused README.md** - Technical documentation for CLI development
- **Complete User Guide** (docs/USER-GUIDE.md) - Installation, usage, examples
- **Error Handling Guide** (docs/ERROR-HANDLING.md) - Comprehensive error system documentation

### Code Quality
- Modular error handling system (`error_handler.h`)
- Specialized error functions for common scenarios
- Better error context and suggestions
- Improved code organization

### Commands Updated
- **create** - Better error messages, safe filesystem operations
- **build** - Improved build failure reporting
- **start** - Three modes (dev/prod/web) with proper error handling
- **clean** - Safe directory removal with error handling

## 📋 Available Modes

### Desktop Mode (WebView)
```bash
light start --dev   # Development with hot reload
light start --prod  # Production executable
```

### Web Mode (Browser)
```bash
light start --web   # HTTP server + browser
```

## 🐛 Bug Fixes

- Fixed missing includes in start.cpp
- Fixed CreateProcessA parameter issues
- Fixed frontend directory path resolution
- Improved process cleanup on Ctrl+C
- Better error recovery in development mode

## 📦 Installation

### Windows Installer
`LightJS-1.1.0-win64.exe`
- Full installation with PATH setup
- Desktop shortcuts
- WebView2 dependency check
- Automatic updates support

### Portable Version
`lightJS-CLI-portable-v1.1.0.zip`
- No installation required
- Extract and run
- Perfect for USB drives or temporary setups

### macOS / Linux

**Pre-built binaries are not yet available.**

Users must build from source. See [BUILD-LINUX-MACOS.md](BUILD-LINUX-MACOS.md) for complete instructions.

Quick summary:
```bash
git clone https://github.com/alb0084/lightJs.git
cd lightJs/cli
mkdir build && cd build
cmake ..
cmake --build . --config Release
sudo cp bin/Release/light /usr/local/bin/
```

Future releases will include pre-built binaries for all platforms.

## 🔄 Upgrade from v1.0.1

1. **Backup your projects** (optional, CLI doesn't touch project files)
2. **Uninstall v1.0.1** (Windows: Control Panel → Programs)
3. **Install v1.1.0** using the new installer
4. **Verify installation**: `light --version`

Or simply replace `light.exe` with the new version (portable users).

## 📖 Documentation

- [User Guide](docs/USER-GUIDE.md) - Complete usage guide
- [Error Handling](docs/ERROR-HANDLING.md) - Error system documentation
- [Testing Guide](docs/TESTING-GUIDE.md) - Testing procedures
- [README](README.md) - Developer documentation

## 🚀 What's Next?

### v1.2.0 (Planned)
- `--verbose` flag for detailed logging
- `light doctor` command to check dependencies
- Configurable port for web mode
- Error log file (`~/.lightjs/errors.log`)
- Hot reload for web mode

### v1.3.0 (Future)
- Network error handling (port conflicts, downloads)
- Automatic error recovery and retries
- Plugin system for custom commands
- Multi-language support

## 🙏 Contributors

- **Alberto (Alb0084)** - Project lead and development

## 📄 License

See LICENSE.txt for details.

---

## Exit Codes Reference

For scripting and automation:

| Code | Name | Description |
|------|------|-------------|
| 0 | SUCCESS | Operation completed successfully |
| 1 | GENERIC_ERROR | Unexpected error |
| 2 | INVALID_ARGS | Invalid command-line arguments |
| 3 | PATH_NOT_FOUND | Required file/directory not found |
| 4 | DIRECTORY_EXISTS | Target directory already exists |
| 5 | COMMAND_FAILED | External command failed |
| 6 | DEPENDENCY_MISSING | Required dependency not installed |
| 7 | NOT_LIGHTJS_PROJECT | Not a valid LightJS project |
| 8 | PERMISSION_DENIED | Insufficient permissions |

## 🔗 Links

- **GitHub Repository**: https://github.com/alb0084/lightJs
- **Issue Tracker**: https://github.com/alb0084/lightJs/issues
- **Documentation**: https://github.com/alb0084/lightJs/tree/main/docs

---

**Thank you for using LightJS CLI!** 🎉

For questions or issues, please visit our GitHub repository.
