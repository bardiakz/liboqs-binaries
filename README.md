# liboqs-binaries
Pre-built binaries for [liboqs](https://github.com/open-quantum-safe/liboqs) - Open Quantum Safe's quantum-resistant cryptographic algorithms library.
The official liboqs repository doesn't provide pre-built binaries in their releases. This repository automatically builds and publishes binaries for multiple platforms, making it easier to integrate liboqs into projects.
## Supported Platforms
- **Linux**: x86_64, ARM64
- **macOS**: x86_64 (Intel), ARM64 (Apple Silicon)
- **Windows**: x64
- **iOS**: XCFramework (device ARM64 + simulator ARM64/x86_64)
- **Android**: armeabi-v7a, arm64-v8a, x86, x86_64
## Download
Visit the [Releases](../../releases) page to download the latest binaries.
Each release is tagged as `<liboqs_version>-<build_revision>` (e.g., `0.16.0-b1`). The build revision only increments if a release needs to be re-published for the same liboqs version (packaging fix, not a new upstream version).
You can download either:
- An individual platform archive (e.g. `liboqs-0.16.0-linux-x86_64.tar.gz`), or
- The combined `liboqs-<version>-all-platforms.tar.gz`, which bundles every platform/architecture in one archive under separate subfolders.
### Verifying downloads
Every release includes `SHA256SUMS.txt`. Verify with:
```
sha256sum -c SHA256SUMS.txt
```
## File Structure
An individual platform archive extracts to:
```
lib/          # Compiled libraries (.so, .dylib, .dll, or .a)
include/      # Header files
  oqs/
    oqs.h
    ...
```
The combined archive keeps every platform/arch in its own subfolder so nothing overwrites anything else:
```
include/oqs/*.h
linux/x86_64/liboqs.so
linux/aarch64/liboqs.so
macos/x86_64/liboqs.dylib
macos/arm64/liboqs.dylib
windows/x86_64/oqs.dll
android/arm64-v8a/liboqs.so
android/armeabi-v7a/liboqs.so
android/x86_64/liboqs.so
android/x86/liboqs.so
ios/liboqs.xcframework/...
```
**Android/iOS note:** Flutter/native mobile builds can't load a library directly from this extracted path. You still need to copy the Android `.so` into `android/app/src/main/jniLibs/<abi>/` and add the iOS `.xcframework` to your Xcode project's embedded frameworks yourself.
## Version Sync
This repository automatically checks for new liboqs releases daily and builds binaries when a new version is detected. You can also manually trigger builds via GitHub Actions.
## Build Information
All binaries are built with:
- CMake build system
- Release configuration
- Shared libraries enabled (except iOS which uses static, packaged as an XCFramework)
- OpenSSL disabled on all platforms, for consistent cryptographic primitives across builds
### Build Configuration
- **Linux x86_64**: Built on Ubuntu (hosted runner)
- **Linux ARM64**: Built natively on Ubuntu ARM64 (hosted runner, no emulation)
- **macOS x86_64**: Built on `macos-15-intel` (GitHub is deprecating Intel macOS runners; this may need to change again before Apple/GitHub drop x86_64 support entirely around fall 2027)
- **macOS ARM64**: Built on macOS 14
- **Windows**: Built with MSVC and Ninja
- **iOS**: Minimum deployment target: iOS 13.0
- **Android**: Minimum API level: 21 (Android 5.0), NDK r27c
## Legacy Releases
Releases published before v2.0.0 of this repo used a bare `<liboqs_version>` tag (e.g. `0.15.0`) and a flat combined-archive layout that could silently overwrite files sharing a filename across platforms. Those releases and their download links are left untouched and still work, but the combined archive in them may not contain what its README claims. If you're on a legacy release, either move to a current one or use the individual per-platform archives, which were never affected.
## Related Projects
- [liboqs](https://github.com/open-quantum-safe/liboqs) - The main library
- [oqs](https://github.com/bardiakz/oqs) - Dart ffi wrapper for liboqs
- [Open Quantum Safe](https://openquantumsafe.org/) - Project homepage
## Disclaimer
These are **unofficial** binary distributions. For production use, consider building from source.