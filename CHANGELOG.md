# Changelog

All notable changes to this project will be documented in this file.

## [2.0.1] - 2026-08-08
### Changed 
- macos-13 runner to macos-15-intel
- mac arm runner to macos-latest

## [2.0.0] - 2026-08-08

### Breaking
- Release tags now use a `<liboqs_version>-<build_revision>` scheme (e.g.
  `0.16.0-v2`) instead of the bare liboqs version, so this pipeline can
  never overwrite or collide with a pre-2.0.0 release. Existing releases
  on bare version tags (e.g. `0.16.0`) are unaffected and remain available,
  marked as legacy.
- Combined `all-platforms` archive layout changed to per-platform,
  per-architecture subfolders (`linux/x86_64/`, `macos/arm64/`,
  `windows/x86_64/`, `android/<abi>/`, `ios/`) to fix a bug where builds
  sharing a filename (all Android ABIs, all desktop libs) silently
  overwrote each other during archive assembly. The combined archive from
  prior releases only ever contained one platform's binary in practice.

### Added
- Native Linux ARM64 build via hosted `ubuntu-24.04-arm` runner, replacing
  slow/flaky QEMU emulation.
- macOS x86_64 (Intel) build restored, on `macos-13` (last Intel-based
  hosted runner; `macos-12` was retired).
- `SHA256SUMS.txt` published with every release for integrity verification.
- README.txt bundled inside the combined archive explaining the new layout
  and noting that Android/iOS integration still requires manually placing
  files into `jniLibs/<abi>/` or embedding the `.xcframework` in Xcode —
  this is not done automatically.

### Changed
- `OQS_USE_OPENSSL=OFF` and `OQS_DIST_BUILD=ON` applied consistently across
  all platforms (previously desktop builds used OpenSSL-backed primitives
  while mobile builds didn't, an unintentional inconsistency).
- Consolidated four overlapping/partially-broken workflow files into a
  single canonical `build-liboqs.yml`.

## [1.0.0]

### Added
- Initial setup of automated binary builds
- Support for Linux (x86_64, ARM64)
- Support for macOS (x86_64, ARM64)
- Support for Windows (x64, ARM64)
- Support for iOS (XCFramework)
- Support for Android (armeabi-v7a, arm64-v8a, x86, x86_64)
- Automated daily checks for new liboqs releases
