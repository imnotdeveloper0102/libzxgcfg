# libzxgcfg (v0.1.0)

Prebuilt binaries, one folder per operating system. Each folder holds a shared
library, a static library, and a command-line tool for every supported chip,
all built from the same release with hardening enabled (see below).

## Folders

| Folder | Contents |
|---|---|
| `libzxgcfg-linux/` | Linux (glibc): x86_64, aarch64, armv7, i686, riscv64, loongarch64, powerpc64le, s390x |
| `libzxgcfg-android/` | Android (API 21): arm64-v8a, armeabi-v7a, x86, x86_64 |
| `libzxgcfg-windows/` | Windows: x86_64, x86, aarch64 |
| `libzxgcfg-macos/` | macOS: x86_64, aarch64 |
| `libzxgcfg-wasm/` | WebAssembly: wasm32 (`libzxgcfg-wasm32.wasm`) |

File names follow the pattern `libzxgcfg-<os>-<chip>` plus `.so`, `.dll`,
`.dylib`, `.a`, or `.lib` as appropriate; command-line tools have no suffix
except `.exe` on Windows. Windows `.lib` files are static archives.

## Verification status

Every file was checked for correct file type, stripped symbols, absence of
build-machine paths, and the expected exported symbol set. Only the Linux
x86_64 build was run and tested (full test suite: 922 passed, 0 failed,
13 ignored); all other targets were verified by file type and symbols only,
and were not executed. Two known limitations remain: the macOS shared
libraries export additional internal symbols and keep a reduced symbol table
(the cross toolchain used cannot restrict them further), and the Linux armv7
command-line tool exports a set of libc helper symbols.

## Hardening

Binaries are built with link-time optimization, stripped symbols, and
remapped source paths, making casual reverse engineering harder. No
hardening can make reverse engineering impossible.
