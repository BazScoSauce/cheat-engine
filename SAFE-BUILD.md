# Cheat Engine Safe Build

This branch creates a private, clean 64-bit Windows build from the public Cheat Engine source in this repository.

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
- Portable ZIP
- Standard uninstallable Windows installer
- SHA-256 checksums for the generated packages

The build is x64-only to keep the package simpler and avoid installing the separate 32-bit cross-compiler during CI.

## Downloading a build

Open the repository's Actions tab, select **Build Safe Windows Package**, open the latest successful run, then download the **Cheat-Engine-Safe-Windows-x64** artifact. The artifact contains both the installer and portable ZIP.

## Important notes

This repository currently contains the public 7.5-era source, not the full current 7.7 source.

Cheat Engine performs memory inspection, debugging and process manipulation. Antivirus products and Microsoft Defender can therefore flag a self-built copy even when it was compiled directly from the source in this repository. A detection is not, by itself, proof that the build contains malware.

The installer produced by this branch is not digitally signed, so Windows SmartScreen may warn that the publisher is unknown.

No attempt is made to build, package or enable the DBK kernel driver or DBVM.
