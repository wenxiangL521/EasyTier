# WMCL · EasyTier (Desktop branch)

A trimmed fork of [EasyTier](https://github.com/EasyTier/EasyTier) used by the
**WMCL launcher** on desktop platforms.

## What this branch keeps

- `easytier/` — EasyTier core, with the `easytier-core` and `easytier-cli` binaries
- `easytier-rpc-build/` — build-time dependency

Removed to keep the repository and build small: GUI, web console, FFI/JNI/uptime/magisk
contribs, nix files, frontend assets, upstream CI and docs.

## Differences from upstream

- TCP STUN server list extended with China-reachable nodes (`easytier/src/common/stun.rs`)
- Workspace reduced to the crates needed by the WMCL desktop launcher

## Local build

```bash
cargo build --release --bin easytier-core --bin easytier-cli
```

## License

Same as upstream, see [LICENSE](LICENSE).
