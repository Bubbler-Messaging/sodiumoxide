# sodiumoxide

Maintained fork of [sodiumoxide](https://github.com/sodiumoxide/sodiumoxide) — type-safe Rust bindings for [libsodium](https://github.com/jedisct1/libsodium).

This fork uses [Bubbler's libsodium fork](https://github.com/Bubbler-Messaging/libsodium) as the native backend, built statically from source.

## What changed from upstream

- **No longer deprecated** — actively maintained for [Bubbler Messaging](https://github.com/Bubbler-Messaging)
- Rust edition 2024
- Updated dependencies (ed25519 2.2.3, serde 1.x, rmp-serde 1.x)
- libsodium submodule points to Bubbler's fork

## Building

A C compiler (`cc`, `clang`, ...) is required to build libsodium from source.

```
git clone https://github.com/Bubbler-Messaging/sodiumoxide.git
cd sodiumoxide
git submodule update --init --recursive
cargo build
```

The first build compiles libsodium from source (1–3 minutes). Subsequent builds use the cached result.

## Testing

```
cargo test
```

## Linking

By default, libsodium is built from source and linked **statically**. This is the recommended approach for all platforms including iOS and Android.

Alternative linking options via environment variables:

| Variable | Description | Notes |
| :------- | :---------- | :---- |
| `SODIUM_LIB_DIR` | Path to a precompiled libsodium | Directory containing `.so`, `.a`, `.la`, `.dll` or `.lib` |
| `SODIUM_SHARED` | Link dynamically instead of statically | Only works with `SODIUM_LIB_DIR` |
| `SODIUM_USE_PKG_CONFIG` | Find system library via pkg-config | |
| `SODIUM_DISABLE_PIE` | Build with `--disable-pie` | Non-Windows only, when building from source |

## Features

| Feature | Default | Description |
| :------ | :------ | :---------- |
| `std` | enabled | When disabled, builds with `#![no_std]` |
| `serde` | enabled | Serialization/deserialization of keys, tags, etc. |
| `benchmarks` | disabled | Compile benchmark tests (requires nightly) |

## Platform compatibility

- Linux
- macOS
- Windows (MSVC)
- iOS
- Android

## License

Licensed under either of

- [Apache License, Version 2.0](LICENSE-APACHE)
- [MIT License](LICENSE-MIT)

at your option.
