# UEFI + GPT = BFF
To understand how it works, unlike the old legacy days where there was a sector that the bios had to read to load the bootloader, UEFI systems need an `EFI program/application` that is either the bootloader or the one that will load the bootloader (like clover, clover is not a real bootloader most of the time, it loads macOS's `boot.efi` which is the real macOS bootloader) which is presented as a `file` instead of a sector. This eases fixing boot issues and can help save and recover boot elements by simply copying them else where and can be edited. All the files are in a FAT32 formatted partition, mostly EFI partition on system disks, or any FAT32 partitions even on MBR formatted disks.

So what's makes it that easy? If you take the example of grub2 and winloader in a legacy system, to use one you need to replace the other with it, so you can't just switch from grub2 to winloader (or the opposite) without replacing the boot sector of the other, but in UEFI systems (mostly desktop setups, and some laptops, like ASUSs and MSIs...) you can "choose" which file to load, so you can boot directly to windows by loading `bootmgfw.efi` in your EFI partition or load GRUB2 or even CLOVER by selecting their respective files. This way, you can have all the booting files, without the need to replace them, and thanks to clover you can load these applications and files directly from it.

What's the issue then? The issue is not in the files in the EFI partitions, the issue is how the disk is partitioned and how the systems will react to it. For example, macOS disk utility cannot (for whatever reason) format a partition on a GPT disk if the EFI partition is not at least 200MB, while windows and linux are satisfied with whatever size you give them, as long as it can hold the boot files, usually, if you format the disk from within their respective installers, they automatically make a 100MB EFI partition, which is fine for them but not for macOS. This is where it gets tricky and where macOS becomes a bit bitchy about.

So I'll divide this guide into these situations:

* I have 2 disks and I use each OS on a disk
* I have 1 disk with windows/linux already installed in it
* I have blank disk or with macOS installed already in it and I want to add windows/linux
