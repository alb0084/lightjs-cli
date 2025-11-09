# Ì∫Ä LightJS CLI - Release Build Instructions

This directory is used to create distribution packages for LightJS CLI.

## Ì≥¶ What Gets Generated

1. **Portable ZIP** (`lightJS - CLI - portable v{VERSION}.zip`)
   - Contains: `light.exe`, `third_party/`, `README.md`
   - Size: ~500 KB
   - Usage: Extract and run directly, no installation needed

2. **NSIS Installer** (`build/LightJS-{VERSION}-win64.exe`)
   - Includes: Installation wizard
   - Features:
     - Automatic PATH addition
     - Desktop shortcut
     - Uninstaller
   - Size: ~1.1 MB

## Ìª†Ô∏è Quick Build (Automated)

Simply run:

```bash
./build-release.sh
```

This script will:
1. Extract version from source code
2. Copy latest `light.exe` from main build
3. Update `CMakeLists.txt` version
4. Clean build directory
5. Configure and build with CMake
6. Generate NSIS installer with CPack
7. Create portable ZIP package

## Ì≥ã Manual Build Process

If you need to build manually:

### 1. Update light.exe
```bash
cp "../lightJS - CLI/cli/build/bin/Release/light.exe" ./
```

### 2. Update Version
Edit `CMakeLists.txt`:
```cmake
set(CPACK_PACKAGE_VERSION "1.0.X")
```

### 3. Clean Build
```bash
rm -rf build && mkdir build && cd build
```

### 4. Configure CMake
```bash
cmake -G "Visual Studio 17 2022" -A x64 -DCMAKE_BUILD_TYPE=Release ..
```

### 5. Build
```bash
cmake --build . --config Release
```

### 6. Create Installer
```bash
cpack -C Release
```

### 7. Create Portable ZIP
```bash
cd ..
powershell -Command "Compress-Archive -Path 'light.exe', 'third_party', 'README.md' -DestinationPath 'lightJS - CLI - portable v1.0.X.zip' -Force"
```

## Ì≥Å Directory Structure

```
LightJS -CLI installer/
‚îú‚îÄ‚îÄ build-release.sh          ‚Üê Automated build script
‚îú‚îÄ‚îÄ BUILD-INSTRUCTIONS.md     ‚Üê This file
‚îú‚îÄ‚îÄ CMakeLists.txt            ‚Üê CPack configuration
‚îú‚îÄ‚îÄ README.md                 ‚Üê User documentation
‚îú‚îÄ‚îÄ light.exe                 ‚Üê CLI executable (copied from main build)
‚îú‚îÄ‚îÄ third_party/              ‚Üê Dependencies (webview)
‚îú‚îÄ‚îÄ build/                    ‚Üê Build artifacts (generated)
‚îÇ   ‚îî‚îÄ‚îÄ LightJS-{VERSION}-win64.exe
‚îî‚îÄ‚îÄ *.zip                     ‚Üê Portable releases

```

## ‚öôÔ∏è Requirements

- CMake 3.15+
- Visual Studio 2022
- NSIS (Nullsoft Scriptable Install System)
  - Path: `D:/Programmi/NSIS/makensis.exe` (configured in CMakeLists.txt)

## Ì∑™ Testing

### Test Portable Version
```bash
unzip "lightJS - CLI - portable v1.0.X.zip" -d test-portable
cd test-portable
./light.exe version
```

### Test Installer
```bash
start build/LightJS-1.0.X-win64.exe
```

After installation:
```bash
light version  # Should work from any directory
```

## Ì≥§ Publishing to GitHub

1. Create a new release on GitHub:
   ```
   https://github.com/alb0084/lightjs/releases/new
   ```

2. Tag format: `v1.0.X`

3. Upload both files:
   - `LightJS-{VERSION}-win64.exe` (Installer)
   - `lightJS - CLI - portable v{VERSION}.zip` (Portable)

4. Write release notes with changelog

## Ì¥ß Troubleshooting

### NSIS not found
Update the path in `CMakeLists.txt`:
```cmake
set(CPACK_NSIS_EXECUTABLE "C:/Path/To/NSIS/makensis.exe")
```

### light.exe not found
Build the main CLI first:
```bash
cd "../lightJS - CLI/cli/build"
cmake --build . --config Release
```

### Version mismatch
Ensure version in `cli/src/commands/version.cpp` matches `CMakeLists.txt`

---

**Author**: Alb0  
**Last Updated**: November 8, 2025
