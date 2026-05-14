QuickStick: A bootable-USB utility
==================================

[![Licence](https://img.shields.io/badge/license-GPLv3-blue.svg?style=flat-square&label=License)](https://www.gnu.org/licenses/gpl-3.0.en.html)
[![Status](https://img.shields.io/badge/status-preview-orange.svg?style=flat-square)](https://github.com/rufusadds/QuickStick)

QuickStick is a utility that formats and creates bootable USB flash drives.
It's a fork of [Rufus](https://github.com/pbatard/rufus) by Pete Batard,
re-skinned with a clean white-and-electric-blue UI and extended with a few
Windows-customization options that haven't been accepted upstream.

> **Preview build.** QuickStick is a single rolling preview — there is no
> stable release line yet. Expect rough edges, and don't use it on drives
> you care about until the project is past the preview phase.

Features
--------

Everything Rufus 4.15 does:

* Format USB, flash card and virtual drives to FAT/FAT32/NTFS/UDF/exFAT/ReFS/ext2/ext3
* Create DOS bootable USB drives using [FreeDOS](https://www.freedos.org) or MS-DOS
* Create BIOS or UEFI bootable drives, including [UEFI bootable NTFS](https://github.com/pbatard/uefi-ntfs)
* Create bootable drives from bootable ISOs (Windows, Linux, etc.) and from disk images
* Create Windows 11 installation drives for PCs without TPM or Secure Boot
* [Windows To Go](https://en.wikipedia.org/wiki/Windows_To_Go) drives
* VHD/DD, VHDX and FFU images of an existing drive
* Persistent Linux partitions
* MD5, SHA-1, SHA-256 and SHA-512 checksums
* Runtime validation of UEFI bootable media
* Bad blocks checks, including detection of fake flash drives
* Download Microsoft Windows 8/10/11 retail ISOs and [UEFI Shell](https://github.com/pbatard/UEFI-Shell) ISOs
* Portable. Secure Boot compatible. No installation required.
* 100% [Free Software](https://www.gnu.org/philosophy/free-sw) ([GPL v3](https://www.gnu.org/licenses/gpl-3.0))

QuickStick additions on top of Rufus:

* **Enable the built-in Administrator account** — a new checkbox in the
  Windows User Experience customization dialog (shown when starting a
  Windows 11 install). When ticked, QuickStick adds a `FirstLogonCommand`
  that runs `net user Administrator /active:yes` to activate the dormant
  SID-500 Administrator on first sign-in. Off by default and persisted
  across sessions; the account has no password set by default, so use
  with care.
* **Clean light theme** — white dialog background, hairline grey
  borders, electric blue (`#0066FF`) accents on focus/hover, electric
  blue progress bar. Forced light title bar regardless of the Windows
  system theme. Inspired by the Apple / Stripe / Linear visual language.
* **Phantom test device** — a permanent `[TEST] Phantom drive (no disk
  will be written)` entry at the end of the device dropdown lets you
  exercise the full pre-format pipeline (including the Windows User
  Experience dialog and unattend.xml generation) without a real USB
  drive plugged in. The format aborts safely after the dialog and
  reports the path of the generated unattend.xml for inspection.

Building from source
--------------------

QuickStick builds with Visual Studio 2022 (or newer) Build Tools using the
MSVC v143 toolset and the Windows 10/11 SDK. The `Release|x64` configuration
is the one that's actively tested.

From a Developer Command Prompt:

```
msbuild rufus.sln /t:Build /p:Configuration=Release /p:Platform=x64
```

Or, if you don't have a Developer Command Prompt in your PATH:

```
"C:\Program Files (x86)\Microsoft Visual Studio\<edition>\<year>\BuildTools\MSBuild\Current\Bin\MSBuild.exe" ^
    rufus.sln /t:Build /p:Configuration=Release /p:Platform=x64
```

The output binary lands at `x64\Release\rufus.exe` (the in-tree project file
name still says `rufus`; the binary identifies itself to Windows as
QuickStick via its version-info metadata).

The MinGW build path inherited from Rufus (`configure` / `make`) is
preserved and should still work, but is not actively tested.

Running the preview build
-------------------------

QuickStick requires administrator privileges, like Rufus. Right-click
`rufus.exe` and select **Run as administrator**, or accept the UAC prompt
when launching it normally.

To verify the new WUE option without burning a real drive:

1. Launch QuickStick.
2. In the **Device** dropdown, pick `[TEST] Phantom drive (no disk will be written)`.
3. In **Boot selection**, point at a Windows 11 ISO.
4. Click **START**. The Windows User Experience dialog opens.
5. Tick **Enable the built-in Administrator account**, click OK.
6. A popup reports the path of the generated `unattend.xml`. Open that
   file in Notepad and confirm the `<CommandLine>net user Administrator
   /active:yes</CommandLine>` line is present.

No disk is ever modified.

Credits and licence
-------------------

QuickStick is derived from Rufus, which is
**© 2011-2026 Pete Batard** and released under the
[GNU GPL v3](https://www.gnu.org/licenses/gpl-3.0.html). All original
Rufus copyright headers are preserved in every source file. The
QuickStick modifications layered on top are also released under GPL v3
and any further redistribution must remain so. See `LICENSE.txt` for
the full licence text.

QuickStick is not affiliated with, endorsed by, or in any way associated
with Pete Batard or the upstream Rufus project. If you want the original
Rufus, get it from [rufus.ie](https://rufus.ie).

Issues
------

For bugs or feature requests specific to QuickStick, please open an
issue on the [GitHub tracker](https://github.com/rufusadds/QuickStick/issues).
Bugs that also affect upstream Rufus should be reported at
[pbatard/rufus](https://github.com/pbatard/rufus/issues) so that everyone
benefits from the fix.
