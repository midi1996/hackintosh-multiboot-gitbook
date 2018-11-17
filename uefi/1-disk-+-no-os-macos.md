# 1 Disk + No OS/macOS

For this situation:

1. Install macOS first and partition your drives to HFS+/APFS partitions. _**DO NOT MAKE A FAT32 DISK FOR EITHER WINDOWS OR LINUX, KEEP IT HFS+/APFS \(better HFS+, highly recommended\).**_ _Reason:_ stupidly from Apple, when you make a FAT32 partition, it converts the GPT to a hybrid MBR, and it's meant usually for Bootcamp purposes, since Windows \(on pre-2016 Apple device\) is generally installed in legacy, and windows is picky so it prefers MBR on legacy and strictly GPT on UEFI. So keep in mind not to make a FAT32 partition.
   1. if you already installed macOS, just open Disk Utility, select your disk, select Partition and add a new partition \(HFS+ or APFS\).
2. Once done and it's all prepared, make your Windows install by mounting the ISO, formatting the USB to MS-DOS \(FAT32\) and copy the inside of the ISO into the root of that USB, or use unetbootin for linux \(or do both\). Also remember your 2nd partition's size.
3. Boot to your second OS installer
4. On windows installer, usually in the disk selection step, you'll a 619MB partition \(if on HFS+, on APFS, you'll just see a block with your macOS partition size\), that's your macOS Recovery HD, and right after it, you'll see a partition with the size you wanted to give to windows, select it, select "Delete" \(you can choose format, but it wont make some extra partitions for windows, nor recommended\), then choose the unallocated space, hit next and it will automatically make needed partitions and install windows. On Linux, if you want to dualboot, just make sure you choose the correct partition, format/resize/swap and everything you need on linux. If you want to triple boot with both macOS and Windows, make sure you leave Linux to the last, and do as you usually prefer.
5. Profit.

