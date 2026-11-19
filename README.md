# WMCL · EasyTier

A trimmed fork of [EasyTier](https://github.com/EasyTier/EasyTier) used by the **WMCL launcher**
on both desktop and Android. Single branch: `wmcl`.

## What this branch keeps

- `easytier/` — EasyTier core, with the `easytier-core` and `easytier-cli` binaries
- `easytier-rpc-build/` — build-time dependency
- `easytier-contrib/easytier-ffi/` — C FFI wrapper used by WMCL on Android
  (`DllImport("easytier_ffi")`, TUN fd injection)
- `.github/workflows/wmcl-android.yml` — cross-compiles and publishes Android arm64 artifacts

Removed to keep the repository and build small: GUI, web console, magisk/ohrs/uptime/android-jni
contribs, nix files, frontend assets, upstream CI and docs.

## Artifacts

Android release: [`wmcl-android-v2.6.4`](https://github.com/wenxiangL521/EasyTier/releases/tag/wmcl-android-v2.6.4)

- `easytier-cli` — NAT test for WMCL (`-o json stun`)
- `libeasytier_ffi.so` — EasyTier runtime for WMCL (C FFI)

Both files are downloaded by the WMCL build (CI or local script) and packaged into the APK;
they are never committed to the WMCL repository.

## Desktop build

```bash
cargo build --release --bin easytier-core --bin easytier-cli
```

The resulting binaries are used by the WMCL desktop launcher (Windows / Linux / macOS).

## Android build

Requires Rust and Android NDK r26b:

```bash
rustup target add aarch64-linux-android
export NDK_HOME=/path/to/ndk
export PATH="$NDK_HOME/toolchains/llvm/prebuilt/linux-x86_64/bin:$PATH"
export CC_aarch64_linux_android="$NDK_HOME/toolchains/llvm/prebuilt/linux-x86_64/bin/aarch64-linux-android26-clang"
export CARGO_TARGET_AARCH64_LINUX_ANDROID_LINKER="$CC_aarch64_linux_android"

cargo build --release --target aarch64-linux-android --bin easytier-cli
cargo build --release --target aarch64-linux-android -p easytier-ffi
```

## Differences from upstream

- TCP STUN server list extended with China-reachable nodes (`easytier/src/common/stun.rs`)
- Workspace reduced to the crates needed by WMCL

## License

Same as upstream, see [LICENSE](LICENSE).
