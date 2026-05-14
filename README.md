QuickStick: A bootable-USB utility
==================================

[![Licence](https://img.shields.io/badge/license-GPLv3-blue.svg?style=flat-square&label=License)](https://www.gnu.org/licenses/gpl-3.0.en.html)

QuickStick is a utility that formats and creates bootable USB flash drives. It's based on
[Rufus](https://github.com/pbatard/rufus) by Pete Batard, with a neon-green-on-black UI and
additional Windows-customization options.

Features
--------

* Everything Rufus does:
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
* QuickStick additions:
  * **Enable the built-in Administrator account** option in the Windows User Experience dialog
  * Neon-green-on-black UI theme, on by default
* Portable. No installation required. Secure Boot compatible.
* 100% [Free Software](https://www.gnu.org/philosophy/free-sw) ([GPL v3](https://www.gnu.org/licenses/gpl-3.0))

Compilation
-----------

Use Visual Studio 2022 (or newer) Build Tools with the MSVC v143 toolset and the
Windows 10/11 SDK. Open `rufus.sln` and build the `Release|x64` configuration, or
from a Developer Command Prompt:

```
msbuild rufus.sln /t:Build /p:Configuration=Release /p:Platform=x64
```

The MinGW build path inherited from Rufus (`configure` / `make`) still works.

Credits and licence
-------------------

QuickStick is based on Rufus, which is © 2011-2026 Pete Batard and released under
the GNU GPL v3. All original Rufus copyright headers are preserved in each source
file. The QuickStick modifications are also GPL v3, and must remain so for any
further distribution.

Issues
------

Please use the [GitHub issue tracker](https://github.com/rufusadds/QuickStick/issues)
for bug reports or feature requests specific to QuickStick. Bugs that affect
upstream Rufus too should also be reported at
[pbatard/rufus](https://github.com/pbatard/rufus/issues).
