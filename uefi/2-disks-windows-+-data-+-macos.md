# 2 Disks: Windows + Data + macOS

Some users may have a setup where they dedicate a disk for Windows another for data, and want to put macOS on the data drive.

To fix that, make sure that:

* the DATA disk is GPT formatted, if not, **convert it** with gdisk
* the DATA disk has a EFI partition:
  * if not, then create a 200MB \(or a bit more\) partition \(it doesnt matter where it is\)
  * format it as FAT32
  * set its flag as EFI System Partition \(or EF00 in `gdisk`\)
  * you can do that on diskpart by 
    * resizing the existent partition, leaving a space where you will have macOS + EFI partition \(&gt;=61GB\), then run in diskpart: 
    * `create partition efi size=200`
    * `format fs=fat32 quick label="EFI"`
    * and that's it
* the DATA disk has a **partition** formatted \(NTFS/FAT32/whatever\) that will receive macOS, Disk Utility in macOS does not play well with empty space.
* Boot and install macOS on the target disk.

Notes:

* it doesnt matter where you install clover, be it on the windows disk's EFI \(to make one EFI to rule them all\) or the target's EFI \(to separate them\)
* Some systems may limit the bootable drives options \(especially on laptops, desktops can have it easy\)

