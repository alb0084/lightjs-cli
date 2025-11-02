 ⚡ LightJS

A lightweight C++ runtime for building cross-platform desktop apps with modern web frontends.  
Inspired by Electron — powered by **libWebView**, written in pure C++.

---

## 🚀 Features

- 🧩 **Native-light core** (no Chromium, no Node.js)
- 🔁 **JS ↔ C++ Bridge** (similar to Electron preload)
- 🖥️ **Cross-platform ready** (Windows / macOS / Linux)
- ⚙️ **Modular architecture** for process, audio, HID, etc.
- 🧠 **CLI included** (`light.exe`) for project automation

---

## ⚙️ Setting up LightJS on Windows

Follow these steps to install and use **LightJS CLI** (`light.exe`) to create, build, and run projects.

---

### 1. 📁 Install the LightJS engine

Place your `light.exe` binary and its dependencies in a single directory, for example:

C:\Program Files\LightJS
├─ light.exe
└─ third_party
└─ webview
├─ core
│ ├─ include\webview.h
│ └─ Release\webview_static.lib

r
Copia codice

Then add that path to your **system PATH** so you can call `light` globally:

```powershell
setx PATH "%PATH%;C:\Program Files\LightJS"
Now open a new terminal and verify:

bash
Copia codice
where light
You should see something like:

makefile
Copia codice
C:\Program Files\LightJS\light.exe
2. 🧱 Create a new project
From any directory:

bash
Copia codice
light create myApp
This generates a new folder myApp containing:

css
Copia codice
myApp/
├─ CMakeLists.txt
├─ render/
│  ├─ index.html
│  ├─ js/app.js
│  └─ preload.js
└─ src/
   ├─ main.cpp
   ├─ preload.cpp
   ├─ process_manager.cpp
   ├─ include/
   │  └─ bridge.h
   └─ utils/
      └─ logger.cpp
3. 🏗️ Build the project
bash
Copia codice
cd myApp
light build
The CLI will:

Create the build folder

Run cmake ..

Compile the runtime (lightjs.exe)

When completed, you’ll find your executable in:

bash
Copia codice
myApp/build/Release/lightjs.exe
4. ▶️ Run your app
bash
Copia codice
light start
This launches a native window loading your render/index.html, or if missing, falls back to a dev server (e.g. http://localhost:3000).

5. 🧹 Clean build artifacts
bash
Copia codice
light clean
Removes and recreates the build/ directory.

🧩 Developer Info
If you wish to rebuild the LightJS runtime manually:

bash
Copia codice
mkdir build && cd build
cmake .. && cmake --build . --config Release
This compiles the runtime with the embedded webview_static.lib and links it to the lightweight core engine.

🧠 Notes
The engine path (third_party/webview/) is automatically detected based on where light.exe is located.
You don’t need to define any custom environment variable.

Ensure CMake ≥ 3.15 and Visual Studio Build Tools are installed.

For Linux or macOS, replace the backslashes with / and install the appropriate WebView backend (WebKit2Gtk / WKWebView).

Author: Alb0