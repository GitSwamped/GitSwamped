# React Native (Bare) + Android Studio + Room + C++ Integration = Dev Setup (Windows + VS Code)

**Status:** final • **Last updated:** 2025-09-18 20:10 • **Target OS:** Windows 10/11 • **Focus:** _React Native frontend with Android-native Room database and C++ integration via JNI/NDK_

Expect 
---

## 🔑 Glossary

- **SDK (Software Development Kit)** → tools (compilers, debuggers, APIs) to build apps.  
- **LTS (Long Term Support)** → stable version (e.g., Node.js) supported for years.  
- **JDK (Java Development Kit)** → toolkit Android uses for Java/Kotlin.  
- **Temurin JDK 17** → Eclipse distribution of Java, stable and Android-compatible.  
- **NDK (Native Development Kit)** → toolkit to write Android code in C/C++.  
- **ORM (Object-Relational Mapping)** → programming technique (+library/framework) that lets you interact with a database. 
- **Room** → Android ORM over SQLite, type-safe and migration-friendly.  
- **SQLite** → lightweight database built into Android/iOS devices.  
- **JNI (Java Native Interface)** → lets Java/Kotlin call into C++ code.  
- **Metro** → React Native’s JavaScript bundler.  
- **AVD (Android Virtual Device)** → emulator (virtual phone) that runs on your machine.
- **CLI (Command Line Interface)** → interacting with a program through a terminal with text commands (versus using a GUI).
- **DAO (Data Access Object)** → a design pattern used in Room that defines how code talks to the database (one specific tool inside the ORM toolbox).

---

## 0) What you’ll install (quick checklist)

- [ ] **Node.js (LTS)** — JavaScript runtime for React Native  
- [ ] **JDK 17 (Temurin)** — required by Android Gradle Plugin  
- [ ] **Android Studio** — for SDK, emulator, platform tools, **NDK** and **CMake**  
- [ ] **VS Code** — your editor  
- [ ] **VS Code extensions** — React Native Tools, Prettier, Java pack, C/C++, SQLite  
- [ ] **Python 3** — for algorithm prototyping (no Anaconda)  
- [ ] **MSYS2 toolchain** — for C++ development and builds  

---

## 1) Core downloads (official links) IN THIS ORDER

- **Node.js LTS**: https://nodejs.org/en  
- **JDK 17 (Temurin)**: https://adoptium.net/temurin/releases/?version=17  
- **Android Studio**: https://developer.android.com/studio  
- **Visual Studio Code**: https://code.visualstudio.com/  

> Install Node **before** creating any React Native project. Android Studio provides SDK, NDK, Gradle, emulator, and build tools.

---

## 2) Android Studio — SDK components to install

Open **Android Studio → Options Menu (gear icon, bottom left) → Settings → type 'SDK' in the search bar (top left) → SDK Tools** and install:

- **Android SDK Command-line Tools** (API 34 or newer) + Google APIs  
- **Android SDK Build-Tools** (latest)  
- **Android SDK Platform-Tools** (adb, fastboot)  
- **Android Emulator**
- **Android Emulator hypervisor driver**  
- **Google Play services**
- **Google Repository**
- **NDK (Side by side)** (required for C++)  
- **CMake** (required for C++ builds)  

Then open **AVD Manager** and create a device (Pixel 7, API 34/35). Verify it boots.

---

## 3) VS Code extensions (IDs for quick install)

- **React Native Tools** — `msjsdiag.vscode-react-native`  
- **Prettier – Code formatter** — `esbenp.prettier-vscode`  
- **Java Extension Pack** — `vscjava.vscode-java-pack`  
- **C/C++** — `ms-vscode.cpptools`  
- **SQLite** — `alexcvzz.vscode-sqlite`  
- **Python** — `ms-python.python`  

From VS Code, press **Ctrl+P** → type: `ext install <id>`.

---

## 4) Verify core tools

Open a new terminal and check:  

```powershell
node -v
npm -v
java -version
adb --version
```

You should see versions. If `adb` isn’t found, re-check PATH and Android SDK.

---

## 5) Create and run a fresh React Native app (Android)

Use `npx` (do not install old global CLI).

```powershell
npx react-native@latest init ScreenBrake --version latest
cd ScreenBrake

# Start Metro
npm start

# In another terminal: run Android app
npx react-native run-android
```

Troubleshooting: ensure emulator is running or physical device is authorized (`adb devices`).

---

## 6) Room + C++ Integration

- **Room (Java/Kotlin)**  
  - Define entities with `@Entity`.  
  - Define DAOs with `@Dao` + queries.  
  - Room auto-generates boilerplate SQL.  

- **C++ (via NDK + JNI)**  
  - Implement performance-heavy logic in `.cpp` files.  
  - Expose C++ functions to Java with JNI.  
  - Java/Kotlin layer passes data between Room and C++.  

- **React Native Bridge**  
  - Java/Kotlin native module connects Room + C++ functions to React Native.  
  - RN JS calls the module, receives results.  

This architecture ensures all features can be backed by Room, while C++ handles algorithms and performance-critical tasks.

---

## 7) If we're going to incorporate C++, we must have shared Standards and Build Settings

We should target **C++17** for this project.

- Fully supported in Android NDK r23+ (stable).  
- Modern features available: lambdas, smart pointers, `auto`, range-based loops, etc.  
- Avoid C++20/23 features — not guaranteed portable on all Android devices yet.  

📄 `CMakeLists.txt` (We need to find, maybe at project root or cpp folder, and ensure):

```cmake
cmake_minimum_required(VERSION 3.10.2)

...

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
```

This ensures everyone compiles with the same C++ standard.

---

## 8) Sanity test checklist

- [ ] `node -v` and `npm -v` work  
- [ ] `java -version` shows JDK 17  
- [ ] `adb --version` works  
- [ ] Emulator boots (or device visible with `adb devices`)  
- [ ] `npx react-native run-android` launches app 
- [ ] Room + JNI test function compiles and runs (e.g., `addNumbers` in C++)  

---

## 9) What this setup covers

- Bare React Native with Android Studio toolchain  
- Room for on-device database storage  
- C++ integration through NDK/JNI  
- Standardized build on **C++17**  
- Do we want team to split roles (Java/Kotlin dev + C++ dev + JS/React Native devs)  

---

**Next step with the team:** Verify everyone installs the same versions, then implement a **Room + C++ JNI “hello world”** (add two numbers in C++, store result in Room, display in RN).  

We need to look into the GitHub integration found in Android Studio settings.
