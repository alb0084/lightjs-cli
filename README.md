# ⚡ LightJS CLI

A lightweight **C++ framework** for building **cross-platform desktop applications** and **web applications** with modern frontends.  
Inspired by Electron, powered by **WebView2** (Windows) / **WebKit** (macOS/Linux), built for performance and modularity.

**Write once, deploy everywhere**: Desktop (Windows, macOS, Linux) and Web (standard browsers).

---

## ✨ Features

- 🧠 **Native-light core** (no Chromium bundle, no Node.js)
- 🌐 **Dual-mode deployment**: Desktop app (WebView2/WebKit) OR Web app (standard browser)
- 🔄 **JS ↔ C++ Bridge** (similar to Electron's preload API)
- 🧩 **Modular architecture** (process, audio, HID modules)
- 🌍 **Truly cross-platform** (Windows, macOS, Linux)
- ⚙️ **Built-in CLI** for project scaffolding and automation
- 📦 **Hidden CMake** - users only see `lightjs.config.json`
- 🎨 **Automatic code formatting** with `.clang-format` (K&R style)
- 🚀 **Web export** - deploy the same codebase to standard web browsers

---

## 📥 Installation

### Windows

1. **Download** the installer or portable version from [Releases](https://github.com/alb0084/lightJs/releases)
2. **Install** (installer) or extract (portable) to your preferred location
3. **Add to PATH** (recommended):
   - Right-click "This PC" → Properties → Advanced System Settings
   - Environment Variables → System Variables → Path → Edit
   - Add: `C:\Program Files\LightJS\` (or your install path)
4. **Verify installation**:
   ```bash
   light --version
   ```

### macOS / Linux

**Pre-built binaries are not yet available for macOS/Linux.**

Please build from source. See **[BUILD-LINUX-MACOS.md](BUILD-LINUX-MACOS.md)** for complete instructions.

Quick build:
```bash
git clone https://github.com/alb0084/lightJs.git
cd lightJs/cli/build
cmake ..
cmake --build . --config Release
sudo cp bin/Release/light /usr/local/bin/
```

# Verify
light --version
```

### Prerequisites

LightJS CLI requires these tools to build projects:

**All Platforms:**
- **CMake ≥ 3.15**  
  👉 [Download here](https://cmake.org/download/) and add to PATH

**Windows:**
- **Microsoft Visual Studio Build Tools 2022**  
  (with "Desktop development with C++" workload)  
  👉 [Download here](https://visualstudio.microsoft.com/visual-cpp-build-tools/)

- **WebView2 Runtime** (usually pre-installed on Windows 10/11)  
  👉 [Download here](https://developer.microsoft.com/en-us/microsoft-edge/webview2/) if needed

**macOS:**
- **Xcode Command Line Tools**  
  ```bash
  xcode-select --install
  ```

**Linux:**
- **GCC/G++ ≥ 7** or **Clang ≥ 5**
- **WebKitGTK** (for WebView support)
  ```bash
  # Ubuntu/Debian
  sudo apt install build-essential libwebkit2gtk-4.0-dev
  
  # Fedora/RHEL
  sudo dnf install gcc-c++ webkit2gtk3-devel
  
  # Arch
  sudo pacman -S base-devel webkit2gtk
  ```

**Verify prerequisites**:
```bash
cmake --version
# Windows: cl
# macOS/Linux: gcc --version or clang --version
```

---

## 🚀 Quick Start

### 1️⃣ Create a New Project

```bash
light create myApp
cd myApp
```

This generates a complete project structure:

```
myApp/
├── src/
│   ├── main.cpp              # C++ application entry point
│   ├── frontend/
│   │   ├── index.html        # Your UI
│   │   ├── style.css
│   │   └── app.js
│   └── bridge.cpp            # JS ↔ C++ communication
├── lightjs.config.json       # User-friendly configuration
├── .clang-format             # Code style (K&R)
├── .gitignore                # Pre-configured for LightJS
└── .lightjs/                 # Hidden CMake configuration (auto-managed)
    └── CMakeLists.txt
```

### 2️⃣ Build Your Project

```bash
light build
```

This automatically:
- Configures CMake from hidden `.lightjs/` folder
- Compiles C++ code
- Links WebView2 runtime
- Generates executable in `build/Release/`

**Build configurations**:
```bash
light build              # Release build (default)
light build --debug      # Debug build with symbols
light build --clean      # Clean before building
```

### 3️⃣ Run Your App

**Desktop mode** (native window with WebView):
```bash
light start
```

**Web mode** (standard browser):
```bash
light start --web
```

This opens your application:
- **Desktop**: Native window with WebView2 (Windows) / WebKit (macOS/Linux)
- **Web**: Your default browser at `http://localhost:3000`

The same codebase works in both modes! 🎉

---

## 📝 Configuration

### `lightjs.config.json`

This is the **only configuration file** you need to edit:

```json
{
  "name": "myApp",
  "version": "1.0.0",
  "build": {
    "outputDir": "build",
    "configuration": "Release",
    "platforms": ["windows", "macos", "linux"]
  },
  "frontend": {
    "entry": "src/frontend/index.html",
    "devServer": {
      "port": 3000,
      "autoReload": true
    }
  },
  "window": {
    "width": 1280,
    "height": 720,
    "title": "My LightJS App",
    "resizable": true
  },
  "deployment": {
    "desktop": true,
    "web": true,
    "webOutputDir": "dist/web"
  }
}
```

**Deployment modes**:
- `desktop: true` - Build native desktop app with WebView
- `web: true` - Export to standard web app (runs in any browser)
- Both can be `true` - same codebase, dual deployment!

**Note**: CMake configuration is hidden in `.lightjs/` folder - you don't need to touch it!

---

## 🛠️ CLI Commands

### Project Management

```bash
light create <project-name>   # Create new project
light build                    # Build project (all platforms)
light build --platform windows # Build for specific platform
light start                    # Run desktop app
light start --web              # Run in browser mode
light clean                    # Clean build artifacts
light export --web             # Export for web deployment
```

### Version & Help

```bash
light --version                # Show CLI version
light --help                   # Show help information
```

---

## 📂 Project Structure Details

### `.ljs` Files (LightJS Framework)

LightJS uses `.ljs` extension with `~...~` syntax for embedding JavaScript in C++:

```cpp
// preload.ljs
#include "webview.h"

void setupBridge(webview::webview& w) {
    w.eval(~
        window.api = {
            greet: (name) => window.chrome.webview.invoke('greet', name)
        };
    ~);
}
```

### Cross-Platform Rendering

LightJS automatically selects the best rendering engine per platform:

| Platform | Desktop Mode | Web Mode |
|----------|-------------|----------|
| **Windows** | WebView2 (Edge) | Any browser |
| **macOS** | WebKit | Any browser |
| **Linux** | WebKitGTK | Any browser |

**Same codebase** - the framework handles platform differences automatically!

---

## 🎨 Code Formatting

All projects include `.clang-format` with **K&R style**:

```c
BasedOnStyle: LLVM
BreakBeforeBraces: Attach
IndentWidth: 2
PointerAlignment: Left
```

**To format your code**:
```bash
clang-format -i src/*.cpp
```

Or install the VS Code extension for automatic formatting.

---

## 🐛 Troubleshooting

### "CMake not found"
```bash
# Add CMake to PATH, then restart terminal
cmake --version
```

### Windows: "cl.exe not found" 
```bash
# Open "Developer Command Prompt for VS 2022"
# Or add VS Build Tools to PATH
```

### Windows: "WebView2 Runtime missing"
- Download from: https://developer.microsoft.com/microsoft-edge/webview2/
- Or use evergreen installer (recommended)

### macOS: "webkit not found"
```bash
xcode-select --install
```

### Linux: "webkit2gtk not found"
```bash
# Ubuntu/Debian
sudo apt install libwebkit2gtk-4.0-dev

# Fedora
sudo dnf install webkit2gtk3-devel
```

### Build fails with CMake errors
```bash
light clean          # Clean build artifacts
light build          # Rebuild from scratch
```

### Application window doesn't open
```bash
light build --debug  # Build with debug symbols
light start          # Check console for error messages
```

### Web mode doesn't start
```bash
# Check if port 3000 is already in use
# Edit lightjs.config.json to change port
```

---

## 🔧 Advanced Usage

### Manual CMake Build

If you need to customize the build:

```bash
cd .lightjs                           # Hidden CMake folder
cmake -S . -B ../build -G "Visual Studio 17 2022"
cmake --build ../build --config Release
```

### Custom Build Configuration

Edit `.lightjs/CMakeLists.txt` (advanced users only):

```cmake
set(PROJECT_ROOT "${CMAKE_CURRENT_SOURCE_DIR}/..")
set(CMAKE_CXX_STANDARD 17)
add_executable(${PROJECT_NAME} ${PROJECT_ROOT}/src/main.cpp)
```

---

## 📚 Examples

### Hello World (Desktop)

```cpp
// src/main.cpp
#include "webview.h"

int main() {
    webview::webview w(false, nullptr);
    w.set_title("Hello LightJS");
    w.set_size(800, 600, WEBVIEW_HINT_NONE);
    w.set_html("<h1>Hello from LightJS!</h1>");
    w.run();
    return 0;
}
```

### Hello World (Web)

The same frontend code works in web mode automatically:

```html
<!-- src/frontend/index.html -->
<!DOCTYPE html>
<html>
<head>
    <title>Hello LightJS</title>
</head>
<body>
    <h1>Hello from LightJS!</h1>
    <p>This works in both desktop and web mode!</p>
</body>
</html>
```

Run with:
```bash
light start        # Desktop mode
light start --web  # Web mode (browser)
```

### JS ↔ C++ Bridge

```cpp
// C++ side (desktop mode only)
w.bind("add", [](std::string args) -> std::string {
    // Parse args, calculate sum
    return "{\"result\": 42}";
});

// JavaScript side (frontend/app.js)
if (window.chrome && window.chrome.webview) {
    // Desktop mode - use native bridge
    window.add(10, 32).then(result => {
        console.log(result); // 42
    });
} else {
    // Web mode - use fallback or API
    console.log("Running in web mode");
}
```

---

## 🌟 Roadmap

### Current (v1.0.x)
- ✅ CLI with hidden CMake
- ✅ Project scaffolding
- ✅ Build/start commands
- ✅ Cross-platform support (Windows, macOS, Linux)
- ✅ Dual-mode deployment (Desktop + Web)
- ✅ `.ljs` syntax support
- ✅ Auto-formatting with `.clang-format`

### Coming Soon (v1.1.x)
- 🔄 Hot reload for frontend development
- 🔄 Better error messages
- 🔄 VS Code extension for `.ljs` syntax highlighting
- 🔄 Template system for different project types
-   Web export optimization and bundling
-   Progressive Web App (PWA) support

### Future (v2.0+)
- 🔮 Advanced module system (plugins)
- 🔮 Mobile support (iOS/Android via WebView)
- 🔮 One codebase → Desktop + Web + Mobile
- 🔮 Cloud deployment templates
- 🔮 Native performance profiling tools

---

## 🤝 Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📄 License

LightJS CLI is open-source software.  
WebView2 components are subject to Microsoft's license terms.

---

## 🔗 Links

- **GitHub**: https://github.com/alb0084/lightJs
- **Issues**: https://github.com/alb0084/lightJs/issues
- **WebView2 Docs**: https://learn.microsoft.com/en-us/microsoft-edge/webview2/

---

**Made with ⚡ by Alb0 **
