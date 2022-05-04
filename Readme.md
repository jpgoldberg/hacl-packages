# The Cryspen HACL Packages

![][status]

The [HACL*] repository is a collection of high-assurance cryptographic algorithms developed as part of [Project Everest].
It includes source code written in [F*], generated code in C, verified assembly code
from the [Vale] project, and an agile multiplexed cryptographic provider called [EverCrypt].
As such, the full [HACL*] repository contains many software artifacts and a complicated build system
that can be intimidating to a crypto developer who simply wishes to use verified crypto.

This repository addresses this gap by presenting several usable crypto packages developed by Cryspen on top of HACL\*.
In particular, it contains a portable C crypto library that selects optimized implementations for each platform,
as well as Rust, OCaml, and JavaScript bindings for this library. Cryspen is in the process of adding more usable APIs for crypto
primitives, as well as extensive documentation for these APIs. Cryspen is also working on more optimized versions of some
algorithms.

## Build

We uses [cmake] to configure the C build and [ninja] to build.

Quick start: `./mach build --test`

Build dependencies

- [cmake]
- [ninja]
- [python]

## mach

All actions are driven by [mach].
See `./mach --help` for details.

## Platform Support

The HACL Packages are supported based on the following tiers.

### Tier 1

Tier 1 targets are guaranteed to work. These targets have automated testing to
ensure that changes do not break them.

- [x] x86_64 Linux (x86_64-unknown-linux-gnu)
- [x] x86 Linux (i686-unknown-linux-gnu)
- [x] x86_64 macOS (x86_64-apple-darwin)
- [x] x86_64 Windows
  - [x] x86_64-pc-windows-msvc
  - [x] x86_64-pc-windows-clang
- [ ] x86 Windows (i686-pc-windows-msvc)

### Tier 2

Tier 2 targets are guaranteed to build.
These targets have automated builds to ensure that changes do not break the
builds. However, not all of them are always tested.

- [x] arm64 macOS (aarch64-apple-darwin)
- [x] arm64 Linux (aarch64-unknown-linux-gnu)
- [x] arm64 Android (aarch64-linux-android)
- [x] arm64 iOS (aarch64-apple-ios)
- [x] s390x z14 Linux (s390x-unknown-linux-gnu)

### Tier 3

Tier 3 targets are supported by the code but there are no automated checks and
there is no guarantee that they work.

- ARMv7 Android (aarch64arm-linux-androideabi)
- arm64 iOS Simulator (aarch64-apple-ios-sim)
- x86_64 iOS (x86_64-apple-ios)
- PowerPC
- IBM Z15
- FreeBSD / x64

## Compiler support

When using the `c89` edition of HACL GCC 4.8 and up are supported.
In any other case a modern C compiler is expected.

## Algorithms

The following tables gives an overview over the algorithms supported by the HACL
packages.

| Family               | Algorithm         | Support                                 |
| -------------------- | ----------------- | --------------------------------------- |
| AEAD                 | AES-GCM 128       | AES-NI & CLMUL (x86 only)               |
| AEAD                 | AES-GCM 256       | AES-NI & CLMUL (x86 only)               |
| AEAD                 | Chacha20-Poly1305 | Portable \| vec128 \| vec256            |
| ECDH                 | Curve25519        | Portable \| BMI2 & ADX                  |
| ECDH                 | P-256             | Portable                                |
| Signature            | Ed25519           | Portable                                |
| Signature            | P-256             | Portable                                |
| Hash                 | SHA2-224          | Portable \| SHAEXT                      |
| Hash                 | SHA2-256          | Portable \| SHAEXT                      |
| Hash                 | SHA2-384          | Portable                                |
| Hash                 | SHA2-512          | Portable                                |
| Hash                 | SHA3              | Portable                                |
| Hash                 | Blake2            | Portable \| vec128 \| vec256            |
| Key Derivation       | HKDF              | Portable (depends on hash)              |
| Symmetric Encryption | Chacha20          | Portable \| vec128 \| vec256            |
| Symmetric Encryption | AES 128           | AES-NI & CLMUL (x86 only)               |
| Symmetric Encryption | AES 256           | AES-NI & CLMUL (x86 only)               |
| MAC                  | HMAC              | Portable (depends on hash)              |
| MAC                  | Poly1305          | Portable \| vec128 \| vec256 \| x64 ASM |

## Testing

Testing is done with [gtest] and requires a C++11 compiler (or C++20 MSVC).

### Dependencies

Tests require the [nlohmann_json] package to read json test files.
CMake takes care of pulling and building the package.

## Code Style

Handwritten C and CPP code is formatted with the Mozilla clang-format style.

## License

HACL packages are licensed under either of

- [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0)
- [MIT license](http://opensource.org/licenses/MIT)

at your option.

[//]: # "links"
[cmake]: https://cmake.org/
[ninja]: https://ninja-build.org/
[mach]: ./mach
[gtest]: https://google.github.io/googletest/
[nlohmann_json]: https://github.com/nlohmann/json
[hacl*]: https://hacl-star.github.io
[f*]: https://fstar-lang.org
[vale]: https://hacl-star.github.io/HaclValeEverCrypt.html
[evercrypt]: https://hacl-star.github.io/HaclValeEverCrypt.html
[status]: https://img.shields.io/badge/status-beta-orange.svg?style=for-the-badge
[project everest]: https://project-everest.github.io/
[python]: https://www.python.org/