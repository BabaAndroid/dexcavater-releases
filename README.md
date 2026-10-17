# ⛏️ Dexcavater Desktop Releases

Welcome to the official download repository for **Dexcavater** — a high-performance, modern Android APK reverse engineering, decompilation, and security analysis workbench.

---

## 📦 Download Latest Version

👉 **[Go to Latest Releases](https://github.com/BabaAndroid/dexcavater-releases/releases/latest)** to download installers for your operating system:

| Platform | Package Format | Download Link |
| :--- | :--- | :--- |
| **Ubuntu / Debian / Mint** | `.deb` (64-bit) | [Download .deb](https://github.com/BabaAndroid/dexcavater-releases/releases/latest) |
| **Fedora / RHEL / CentOS** | `.rpm` (64-bit) | [Download .rpm](https://github.com/BabaAndroid/dexcavater-releases/releases/latest) |
| **Windows 10 / 11** | `.exe` (NSIS Setup) | [Download .exe](https://github.com/BabaAndroid/dexcavater-releases/releases/latest) |

---

## 🚀 Installation Instructions

### 🐧 Linux (Ubuntu / Debian / Linux Mint)
Download the `.deb` file and install it via terminal:
```bash
sudo dpkg -i dexcavater_*_amd64.deb
```
*(If missing system dependencies, run `sudo apt-get install -f`)*

### 🎩 Linux (Fedora / RHEL)
Download the `.rpm` file and install it:
```bash
sudo rpm -i dexcavater-*.x86_64.rpm
```

### 🪟 Windows (10 / 11)
1. Download `dexcavater_*_x64-setup.exe`.
2. Double-click the installer and follow the setup wizard.
3. Launch Dexcavater from your Start Menu or Desktop shortcut.

---

## ✨ Features at a Glance

* **Blazing Fast In-Memory Analysis**: Built in pure Rust & Tauri for instant file navigation and memory efficiency.
* **CodeMirror 6 Editor**: High-speed syntax highlighting for Java, Smali, JavaScript, and XML.
* **Semantic Code Navigation**: Instant *Go to Definition*, *Find Callers*, *Find Callees*, and *Find Usages*.
* **Hermes Decompiler Engine**: Dedicated in-process extraction and deep decompilation for React Native Hermes bytecode.
* **Native ELF & Shared Library Analyzer**: Inspect symbols, JNI bridge signatures, and security flags (`readelf`).
* **Interactive X-Ray Call Graphs**: Explore call hierarchies and dependencies visually.

---

## 🔐 Verifying Downloads
Every release includes a `SHA256SUMS.txt` file. You can verify the integrity of your download:

```bash
sha256sum -c SHA256SUMS.txt
```

---

## 🐛 Feedback & Bug Reports
Found a bug or have a feature request? Please [open an issue](https://github.com/BabaAndroid/dexcavater-releases/issues) in this repository!
