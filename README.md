# Dexcavater v1.0.0-beta.1

**Dexcavater** is a desktop Android reverse-engineering workbench built with **Rust**, **Tauri 2**, **React**, and **CodeMirror 6**. All analysis in this release is **pure-static** (no AI/LLM dependencies).

> **Pre-release build** — intended for testing and security auditing. Compiled installers only; source code is not distributed in this release.

---

## What's Included in v1.0.0-beta.1

### 1. React Native / Hermes Studio & `libhermes.so` Native Bridge
- **Pure-Static `libhermes.so` & Native Bridge Profiler (`05_libhermes_vm_and_native_bridge.md`)**
  - Parses `libhermes*.so`, `libappmodules.so`, `libreactnativejni.so`, `libjsi.so`, and `libturbomodule*` in `lib/<abi>/` directly in Rust (`goblin` + `cpp_demangle`) without external `readelf` or `nm`.
  - Extracts ELF virtual addresses (`0x...`) for VM entry points (`makeHermesRuntime` / `createHermesRuntime`, `evaluateJavaScript`, `prepareJavaScript`, `BCProviderFromBuffer`, `isHermesBytecode`, `JNI_OnLoad`).
  - Demangles and classifies JSI `HostFunction` / `HostObject`, `TurboModule`, `Fabric UI`, and `Java_*` JNI symbols, plus `.rodata` Hermes version clues and native security indicators.
  - Flags compiled-in Hermes Inspector / CDP Debug APIs (`HERMES_INSPECTOR_CDP_EXPOSED`) in the Audit Notebook.
  - Cross-references bundle module/hook strings against native `.so` symbols and Smali `ReactContextBaseJavaModule` / `@ReactMethod` classes.
- **HBC `v99+` Rich Static Fallback**
  - When encountering newer Hermes bytecode versions (`v99+`) whose opcodes are not lifted, extracts HBC header metadata, function directory entries, and structured string literals (`01_decompiled_bundle.js`).
- **Pre-Flight Decompression & Sourcemaps**
  - Decompresses GZIP, ZLIB, and ZIP-wrapped bundles in memory and extracts inline Base64 sourcemaps into `decompiled_src/original_sources/`.

### 2. Unity IL2CPP Studio
- Parses `global-metadata.dat` + `libil2cpp.so` for C# class and metadata reconstruction.
- Gracefully detects and reports encrypted or obfuscated `global-metadata.dat` files via `metadata/global_metadata_info.json` and `00_summary.md`.

### 3. Flutter & Native ELF Studio
- **Flutter / Dart AOT:** Static `libapp.so` snapshot inspection and Dart class/library recovery.
- **Native ELF Studio:** Pure-Rust ELF header, section, symbol, and hardening mitigation checks.

### 4. Android DEX / Smali / JADX Pipeline
- Apktool + Manifest XML + Smali + JADX decompilation with undecompiled DEX coverage auditing across primary and embedded DEX files.

### 5. Cross-Platform Parity & Security Hardening
- **Windows:**
  - `CREATE_NO_WINDOW` (`0x08000000`) applied to background subprocesses (`java`, `jadx`, `apktool`, `adb`, `readelf`).
  - Extended-length UNC (`\\?\`) prefix normalization for `explorer.exe /select,` and `dex_audit_controller.rs`.
  - Cross-platform `beforeBuildCommand` / `beforeDevCommand` in `tauri.conf.json`.
- **Linux:**
  - Fixed `reveal_in_explorer` (`xdg-open`) by removing the unsupported `--` argument.
- **Archive & Path Safety:**
  - Replaced external `tar` CLI calls with bounded pure-Rust `tar.gz` extraction (`flate2`).
  - Enforced path-traversal confinement in `elf_analysis_controller.rs`, `hermes_analysis_controller.rs`, and `dex_audit_controller.rs`.
- **UI Responsiveness:**
  - Portaled editor tab context menus cleanly (`FrameworkStudioView.tsx`) and kept heavy analysis asynchronous off the UI thread.

---

## Installers

| Platform | Installer Format | Architecture |
| :--- | :--- | :--- |
| **Linux (Debian / Ubuntu)** | `.deb` | `amd64` |
| **Linux (Fedora / RHEL / openSUSE)** | `.rpm` | `x86_64` |
| **Windows** | `.exe` (NSIS) | `x64` |
| **macOS** | `.dmg` | Apple Silicon / Universal |

---

## Integrity Verification

Verify downloaded installers against the attached `SHA256SUMS.txt`:
```bash
sha256sum -c SHA256SUMS.txt
```

## Runtime Requirements
- **Java JDK 17+** must be installed on your machine for JADX / Apktool decompilation.

---
_Compiled binaries only. Source code is not distributed in this release._
