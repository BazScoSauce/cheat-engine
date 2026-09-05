# Cheat Engine Safe Build

This branch creates a private, minimal 64-bit Windows build from the public Cheat Engine source in this repository.

## Safety profile

The final package uses an explicit allowlist. It contains only:

- `cheatengine-x86_64.exe`
- `lua53-64.dll`
- `BUILD-INFO.txt`

The build intentionally omits the normal `bin` directory extras, including autorun scripts, Java/.NET agents, injection helpers, Direct3D/overlay hook DLLs, 32-bit helpers, DBK kernel drivers, DBVM, `ceserver`, the tiny compiler/include tree, bundled Lua command-line executables, and third-party installer offers.

This means some advanced Cheat Engine features will not be available. The goal of this branch is a small user-mode build for basic offline/single-player memory scanning and editing.

## Packaging

The installable package is a standard Windows Installer (`.msi`) created with WiX Toolset 3.14.1. It no longer uses the Inno Setup EXE wrapper that triggered a `Trojan:Win32/Malgent` detection on an `is-*.tmp` installer temporary file.

The MSI installs per-user under Local AppData and creates a Start Menu shortcut. It does not contain custom actions or scripts that execute during installation.

A portable ZIP containing the same three files is also produced.

## Build chain

- Lazarus 2.2.2 / FPC 3.2.2 x64
- Lazarus installer downloaded from the official Lazarus mirror and SHA-256 verified before use
- WiX Toolset 3.14.1 for MSI creation
- GitHub Actions Windows Server 2022 runner
- SHA-256 checksums generated for final artifacts

## Important notes

This repository contains the public 7.5-era source, not the full current 7.7 source.

Removing optional helpers does not make Cheat Engine inherently benign. The main executable is specifically designed to inspect and modify other processes' memory. Microsoft Defender or another antivirus may therefore still classify the actual Cheat Engine executable as a hacking/debugging tool or malware-like program.

If Defender flags the new MSI or the installed `cheatengine-x86_64.exe`, do not automatically whitelist it. Check which exact file is detected first.

The MSI is not digitally signed, so Windows may report an unknown publisher.
