# ⚡ LightJS

A lightweight **C++ runtime** for building cross-platform desktop apps with modern web frontends.  
Inspired by **Electron**, powered by **libwebview**, built for **performance and modularity**.

---

## ✨ Features

- 🧠 **Native-light core** — no Chromium, no Node  
- 🔄 **JS ↔ C++ Bridge** — works like Electron’s preload layer  
- 🧩 **Modular architecture** — process, audio, HID, and more  
- 🌍 **Cross-platform ready** — Windows, macOS, Linux  
- ⚙️ **Built-in CLI** — create, build, and launch projects easily  

---

# ⚙️ Setting up LightJS CLI on Windows

Follow these steps to configure **LightJS CLI (`light.exe`)** and make sure it can locate your app and the WebView runtime correctly.

---

## 1️⃣ Prerequisites

Before running any `light` command, ensure you have the following installed:

- **CMake ≥ 3.15**  
  👉 [Download here](https://cmake.org/download/) and make sure it’s added to your system `PATH`.

- **Microsoft Visual Studio Build Tools 2022**  
  (select the “C++ Build Tools” workload)  
  👉 [Download here](https://visualstudio.microsoft.com/visual-cpp-build-tools/)

Verify setup:
```bash
cmake --version
cl
```
Both commands should print version information.

---

## 2️⃣ (Optional) Create a .env file

In your project root, create a .env file to store environment variables:

```bash
type nul > .env
```

---

## 3️⃣ Set required environment variables

In Command Prompt (cmd) or PowerShell, set:

```bash
set LIGHTJS_APP_PATH=C:\path\to\your\app
set LIGHTJS_DEBUG=true
```

Or add them directly inside `.env`:

```bash
LIGHTJS_APP_PATH=C:\path\to\your\app
LIGHTJS_DEBUG=true
```

---

## 4️⃣ Place the WebView engine next to light.exe

Make sure your folder structure looks like this:

```
C:\Program Files\LightJS\
├─ light.exe
└─ third_party\
   └─ webview\
```

This ensures LightJS can properly load the embedded WebView runtime.

---

## 5️⃣ Apply environment variables

Restart your terminal (or your computer) and verify:

```bash
echo %LIGHTJS_APP_PATH%
echo %LIGHTJS_DEBUG%
```

---

## 6️⃣ Run LightJS

Once everything is set up, you can create and launch a project:

```bash
light create myApp
light build
light start
```

This will:

🧱 Create a new LightJS project (`light create`)  
🛠️ Build it using CMake (`light build`)  
🚀 Launch the app window (`light start`)

---

## 🧠 Manual Build (for developers)

If you prefer to build the runtime manually:

```bash
mkdir build && cd build
cmake .. && make
./LightJS
```

---

## 🚀 Quick Install (Portable CLI)

You can also use LightJS as a portable CLI:

1. Download the latest `LightJS_CLI_Windows.zip` from GitHub Releases  
2. Extract it anywhere, for example:

```
D:\Programmi\LightJS\
├─ light.exe
└─ third_party\
    └─ webview\
```

3. (Optional) Add the folder to your PATH:

```bash
setx PATH "%PATH%;D:\Programmi\LightJS"
```

4. Open a new terminal and type:

```bash
light --help
```

---

## 🔮 Future (Planned)

In future versions, LightJS will include a precompiled runtime,  
so you can simply run:

```bash
light create myApp
light start
```

...without needing CMake or Visual Studio Build Tools —  
just a single executable. 🔥

---

## 🧩 About

LightJS was created for developers who want native performance  
with the freedom of web technologies.  
A minimal, modern bridge between HTML, CSS, JS, and C++.

© 2025 LightJS — Designed and developed with ⚡ passion for the next era of hybrid apps.
