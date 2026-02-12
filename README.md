# liboqs-binaries

Pre-built binaries for [liboqs](https://github.com/open-quantum-safe/liboqs) - Open Quantum Safe's quantum-resistant cryptographic algorithms library.

The official liboqs repository doesn't provide pre-built binaries in their releases. This repository automatically builds and publishes binaries for multiple platforms, making it easier to integrate liboqs into projects.

## Supported Platforms

- **Linux**: x86_64, ARM64
- **macOS**: x86_64 (Intel), ARM64 (Apple Silicon)
- **Windows**: x64, ARM64
- **iOS**: XCFramework (device ARM64 + simulator ARM64/x86_64)
- **Android**: armeabi-v7a, arm64-v8a, x86, x86_64

## Download

Visit the [Releases](../../releases) page to download the latest binaries.

Each release is tagged with the corresponding liboqs version (e.g., `0.15.0`).

## File Structure

After extracting an archive, you'll find:

```
lib/          # Compiled libraries (.so, .dylib, .dll, or .a)
include/      # Header files
  oqs/
    oqs.h
    ...
```

## Version Sync

This repository automatically checks for new liboqs releases daily and builds binaries when a new version is detected. You can also manually trigger builds via GitHub Actions.

## Build Information

All binaries are built with:
- CMake build system
- Release configuration
- Shared libraries enabled (except iOS which uses static)
- OpenSSL support where available

### Build Configuration

- **Linux**: Built on Ubuntu 22.04
- **macOS**: Built on official GitHub runners (macOS 13 for x86_64, macOS 14 for ARM64)
- **Windows**: Built with MSVC and Ninja
- **iOS**: Minimum deployment target: iOS 13.0
- **Android**: Minimum API level: 21 (Android 5.0), NDK r26d

## Related Projects

- [liboqs](https://github.com/open-quantum-safe/liboqs) - The main library
- [oqs](https://github.com/bardiakz/oqs) - Dart ffi wrapper for liboqs
- [Open Quantum Safe](https://openquantumsafe.org/) - Project homepage

## Disclaimer
These are **unofficial** binary distributions. For production use, consider building from source or waiting for official binary releases from the Open Quantum Safe project.
