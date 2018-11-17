# 1 Disk + Winders/Loonix

For this recipe you'll need:

1. One USB drive
2. One Computer
3. One disk drive
4. A Linux/Windows installed on the drive
5. One Gparted amd64 ISO from here: [https://gparted.org/download.php](https://gparted.org/download.php)
6. Some time
7. A Good pinch of backed up data \(your loss if you mess up\)
8. Some brains
9. A Google/DuckDuckGo will always be handy and welcomed in the mix

Now let's get started to mix the whole thing :\)

1. Backup your important data. I take no responsibility of a disastrous loss, a missing assignment, an unfinished homework, a thermonuclear war plan or your grandma's old cat pics.
2. Make sure Windows or Linux are running in UEFI mode. To check
   1. For windows: [https://blogs.technet.microsoft.com/home\_is\_where\_i\_lay\_my\_head/2012/10/02/how-to-check-in-windows-if-you-are-using-uefi/](https://blogs.technet.microsoft.com/home_is_where_i_lay_my_head/2012/10/02/how-to-check-in-windows-if-you-are-using-uefi/)
   2. For linux: [https://unix.stackexchange.com/a/148366](https://unix.stackexchange.com/a/148366)
   3. If not, you'll have to convert it to UEFI:
      1. for windows [https://docs.microsoft.com/en-us/windows/deployment/mbr-to-gpt](https://docs.microsoft.com/en-us/windows/deployment/mbr-to-gpt) \(I'll make a guide on how to do it manually later one, it's ez\)
      2. for linux: add a partition \(anywhere on the disk, 200MB size, FAT32, flagged as "boot" or type as EF00\) and re-install grub-efi \(at this point you can just make another partition and install macOS lol\) and make sure the drive is GPT \(you can convert it with `gdisk`\)
3. Make a bootable disk for Gparted ISO:
   1. Format your USB as FAT32
   2. Mount the ISO:
      1. Double click on windows
      2. You can use `gnome-disks` or `mount -o loop` to mount
   3. Copy the insides of the ISO into the USB
   4. You're done.
4. Boot the USB
5. When you get to the Gparted screen, make sure you select your disk on the right side of the window
   1. Delete the MSR partition \(it's usually 16MB and Unformatted with a ⚠️icon\) \[WINDOWS ONLY\]
6. Pin point your EFI partition:
   1. it has 100MB \(if it has more than 200MB, then just resize your windows partition and format it for macOS, you dont need to resize the EFI, go directly to 12.\)
   2. it's flagged as `boot`
   3. fat32
7. Select the partition in front of it \(usually Windows/Linux partition\)
8. Select Resize/Move
   1. Resize it from the Left or type in the resizing amount in `Free space preceding` by 100MiB
   2. Confirm by pressing Resize/Move
9. Select your EFI partition
10. Select Resize/Move
    1. Fill in the space on the right
    2. Confirm by pressing Resize/Move
11. To this point no changes has been made, you can still go back and backup your data
12. Select your windows partition again
13. Select Resize/Move
    1. Resize it from the Right or type in the resizing amount in `Free space following` by at least 60GiB \(or 61440MiB\): THIS is your macOS partition size, resize it wisely, you'll have hard time doing so later one as it's not in the beginning of the disk.
    2. Confirm by pressing Resize/Move
14. Right click on the blank space &gt; New partition
    1. File System: hfs/hfsplus \(if not, then fat32\)
    2. Name/Label: whatever you want
    3. Confirm by pressing Add
15. Apply and wait for it to do its work \(it will take some time on HDDs, and a lot less on SSDs\)

You're now ready to boot macOS installer and do the rest from there, make sure you dont mess up by selecting the wrong partition.

