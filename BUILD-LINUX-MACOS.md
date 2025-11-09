# Building LightJS CLI for Linux and macOS

The Windows installer and portable version only work on Windows. For **Linux** and **macOS**, you need to build the CLI from source.

---

## 📋 Prerequisites

### Linux (Ubuntu/Debian)

```bash
# Update package lists
sudo apt update

# Install build tools
sudo apt install -y build-essential cmake git

# Install WebKitGTK (required for WebView)
sudo apt install -y libwebkit2gtk-4.0-dev

# Install Python and Node.js (for dev/web modes)
sudo apt install -y python3 nodejs npm

# Verify installation
cmake --version
gcc --version
python3 --version
node --version
```

### Linux (Fedora/RHEL)

```bash
# Install build tools
sudo dnf install -y gcc gcc-c++ cmake git

# Install WebKitGTK
sudo dnf install -y webkit2gtk3-devel

# Install Python and Node.js
sudo dnf install -y python3 nodejs npm
```

### macOS

```bash
# Install Xcode Command Line Tools
xcode-select --install

# Install Homebrew (if not already installed)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install CMake
brew install cmake

# Install Python and Node.js
brew install python node

# Verify installation
cmake --version
clang --version
python3 --version
node --version
```

**Note:** macOS includes WebKit framework by default.

---

## 🔨 Building from Source

### 1. Clone the Repository

```bash
git clone https://github.com/alb0084/lightJs.git
cd lightJs
```

### 2. Navigate to CLI Directory

```bash
cd cli
```

### 3. Create Build Directory

```bash
mkdir build
cd build
```

### 4. Configure with CMake

```bash
cmake ..
```

**Expected output:**
```
-- The C compiler identification is GNU/Clang
-- The CXX compiler identification is GNU/Clang
-- Configuring done
-- Generating done
-- Build files have been written to: .../lightJs/cli/build
```

### 5. Compile

```bash
cmake --build . --config Release
```

**This will take 1-2 minutes.** You'll see compilation progress:
```
[ 10%] Building CXX object CMakeFiles/light.dir/src/main.cpp.o
[ 20%] Building CXX object CMakeFiles/light.dir/src/commands/create.cpp.o
...
[100%] Linking CXX executable bin/Release/light
```

### 6. Verify Build

```bash
./bin/Release/light --version
```

**Expected output:**
```
LightJS CLI v1.1.0
  ✓ Desktop mode (WebView2/WebKit)
  ✓ Web mode (Browser)
  ✓ Dev mode (Hot reload)
```

---

## 📦 Installation

### Option 1: Local Installation (User Only)

```bash
# Create local bin directory
mkdir -p ~/.local/bin

# Copy binary
cp bin/Release/light ~/.local/bin/

# Add to PATH (add to ~/.bashrc or ~/.zshrc)
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

# Verify
light --version
```

### Option 2: System-Wide Installation (All Users)

```bash
# Copy binary to system location
sudo cp bin/Release/light /usr/local/bin/

# Make executable
sudo chmod +x /usr/local/bin/light

# Verify
light --version
```

### Option 3: Manual Execution (No Installation)

```bash
# Run from build directory
./bin/Release/light --version

# Create alias (add to ~/.bashrc or ~/.zshrc)
alias light='/path/to/lightJs/cli/build/bin/Release/light'
```

---

## 🚀 Quick Start

After installation:

```bash
# Create a new project
light create my-app

# Navigate to project
cd my-app

# Build the project
light build

# Run in development mode (desktop)
light start --dev

# Or run in web mode (browser)
light start --web
```

---

## 🐧 Platform-Specific Notes

### Linux

**WebKitGTK Versions:**
- Ubuntu 20.04+: WebKitGTK 4.0
- Ubuntu 18.04: WebKitGTK 4.0 (older version)
- Fedora 34+: WebKitGTK 4.0

**Wayland vs X11:**
LightJS works on both Wayland and X11 display servers.

**App Execution:**
```bash
# Desktop mode uses WebKitGTK
light start --dev   # GTK window with WebView

# Web mode uses browser
light start --web   # Opens in default browser
```

### macOS

**WebKit Framework:**
macOS includes WebKit framework by default (no installation needed).

**Apple Silicon (M1/M2/M3):**
The build works natively on ARM64 Macs. CMake detects the architecture automatically.

**Code Signing (Optional):**
For distribution, you may want to sign the binary:
```bash
codesign -s "Developer ID" ./bin/Release/light
```

**App Execution:**
```bash
# Desktop mode uses WebKit
light start --dev   # Cocoa window with WebView

# Web mode uses browser
light start --web   # Opens in Safari/default browser
```

---

## 🔧 Troubleshooting

### Build Errors

**"CMake not found"**
```bash
# Linux
sudo apt install cmake

# macOS
brew install cmake
```

**"webkit2gtk-4.0 not found" (Linux)**
```bash
sudo apt install libwebkit2gtk-4.0-dev
```

**"C++ compiler not found"**
```bash
# Linux
sudo apt install build-essential

# macOS
xcode-select --install
```

### Runtime Errors

**"Python not found" (Web mode)**
```bash
# Linux
sudo apt install python3

# macOS
brew install python
```

**"npm not found" (Dev mode)**
```bash
# Linux
sudo apt install nodejs npm

# macOS
brew install node
```

**"libwebkit2gtk-4.0.so: cannot open shared object file"**
```bash
# Install WebKitGTK runtime
sudo apt install libwebkit2gtk-4.0-37
```

---

## 🔄 Updating

To update to a newer version:

```bash
cd lightJs
git pull
cd cli/build
cmake --build . --config Release

# Reinstall
sudo cp bin/Release/light /usr/local/bin/
```

---

## 🗑️ Uninstallation

### User Installation
```bash
rm ~/.local/bin/light
```

### System Installation
```bash
sudo rm /usr/local/bin/light
```

### Remove Build Files
```bash
cd lightJs/cli
rm -rf build
```

---

## 📚 Additional Resources

- **User Guide:** [docs/USER-GUIDE.md](../cli/docs/USER-GUIDE.md)
- **Error Handling:** [docs/ERROR-HANDLING.md](../cli/docs/ERROR-HANDLING.md)
- **Testing Guide:** [docs/TESTING-GUIDE.md](../cli/docs/TESTING-GUIDE.md)
- **GitHub Repository:** https://github.com/alb0084/lightJs

---

## 💡 Tips

### Development Build

For development with debug symbols:
```bash
cmake -DCMAKE_BUILD_TYPE=Debug ..
cmake --build .
```

### Clean Build

If you encounter issues:
```bash
cd cli
rm -rf build
mkdir build && cd build
cmake ..
cmake --build . --config Release
```

### Build with Verbose Output

To see detailed compilation commands:
```bash
cmake --build . --config Release --verbose
```

---

## 🆘 Getting Help

If you encounter issues:

1. **Check Prerequisites:** Ensure all dependencies are installed
2. **Clean Build:** Remove `build/` and rebuild
3. **GitHub Issues:** https://github.com/alb0084/lightJs/issues
4. **Documentation:** Read the User Guide in `docs/`

---

**LightJS CLI v1.1.0** | Built with ❤️ in C++
