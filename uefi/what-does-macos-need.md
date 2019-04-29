# What does macOS need?

To understand where these sections come from, you need to understand what macOS is looking for in a disk drive for it to install "properly". macOS put some restrictions on the size and the possibility to even format a partition as HFS+ if some requirements are not fulfilled.

macOS looks for:

* a GPT formatted disk
* a EFI partition:
  * FAT32 formatted \(not that it matters for it\)
  * flagged as EFI System Partition \(hex: EF00 in gdisk\)
  * is 200MB at least
  * in the same disk where macOS should be installed.
* 60GB of free space

If any of these are in your target disk, you're good to go, if not, that's the point of this guide.

