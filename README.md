# @tsclang/wasm — official toolchain bundles

This repository hosts the downloadable toolchain bundles consumed by the
[`@tsclang/wasm`](https://github.com/tsclang/tsclang/tree/develop/packages/platforms/wasm)
platform package of the [TSClang](https://github.com/tsclang/tsclang) compiler.

The packages' `platform.toolchains.<name>.downloads["<os>-arch>"]` entries point
at [Releases](../../releases) of this repository — never at raw upstream
downloads. This is the **sha256 contract**: a pinned hash ships with the
package manifest, so upstream re-uploads cannot silently change what users
execute, and availability is under our control.

## Bundles

| Tag | Toolchain | OS-arch | Origin | License |
|-----|-----------|---------|--------|---------|
| `toolchains-v1` | emcc 7.0.0 | win32-x64 | [Emscripten SDK](https://github.com/emscripten-core/emsdk) wasm-binaries + portable python/node | Emscripten (MIT/ULIM), CPython (PSF), Node (MIT) |

The emcc bundle is **composite**: the bare emsdk wasm-binaries archive is not
self-sufficient, so the bundle ships portable python and node in `bin/`, a
relocatable `.emscripten` config (paths resolved via `__file__`) and an
`emcc`/`emcc.py` runpy shim. Linux/macOS bundles are assembled the same way by
this repository's CI — see `.github/workflows/`.

Every archive carries a `TSC_BUNDLE_NOTICE.txt` stating the upstream sources
and licenses. Layout contract: a `bin/` directory on top.

Release assets are immutable. A new toolchain version ships as a **new tag**
(`toolchains-v2`, …) plus a package manifest bump.
