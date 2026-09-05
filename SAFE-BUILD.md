# Cheat Engine Safe Build

This branch creates a private, clean Windows build from the public Cheat Engine source in this repository.

## Safety profile

The packaging workflow intentionally excludes:

- Windows kernel driver files (`*.sys`)
- DBK kernel-mode helper files
- DBVM files
- `ceserver` binaries
- third-party bundled/recommended software

The package is intended for normal user-mode, offline/single-player debugging and modding.

## What is built

- Cheat Engine 64-bit, Release mode
- Cheat Engine 32-bit, Release mode
- Portable ZIP
- Standard uninstallable Windows installer
- SHA-256 checksums for the generated packages

## Important notes

This repository currently contains the public 7.5-era source, not the full current 7.7 source.

Cheat Engine performs memory inspection, debugging and process manipulation. Antivirus products and Microsoft Defender can therefore flag a self-built copy even when it was compiled directly from the source in this repository. A detection is not, by itself, proof that the build contains malware.

The installer produced by this branch is not digitally signed, so Windows SmartScreen may warn that the publisher is unknown.

No attempt is made to build, package or enable the DBK kernel driver or DBVM.
