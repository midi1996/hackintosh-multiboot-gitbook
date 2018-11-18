---
description: This section will gather known issues and will to fix them.
---

# InS - QnA

> I try to install windows, but it says that I have an MBR disk, but macOS is already installed, so it should GPT, right?

Yes and No. Apparently, your disk has been changed to **Hybrid MBR**, and to fix it, have a good read here [http://www.insanelymac.com/forum/topic/298027-guide-aio-guides-for-hackintosh/?p=2098111](http://www.insanelymac.com/forum/topic/298027-guide-aio-guides-for-hackintosh/?p=2098111).

> I lost `bootmgfw.efi`, am I retarded?

Maybe, hopefully not, how did you even lose it? But to get it back you need to make a windows installer disk, and follow **Step number 4** in this guide [http://www.insanelymac.com/forum/topic/298027-guide-aio-guides-for-hackintosh/?p=2098111](http://www.insanelymac.com/forum/topic/298027-guide-aio-guides-for-hackintosh/?p=2098111).

> I'm on an MBR partitioned disk, and my `$(setup)` supports UEFI, why was I stupid enough not to install it as UEFI? and how can I make it UEFI bootable and not lose anything?

[http://www.insanelymac.com/forum/topic/298027-guide-aio-guides-for-hackintosh/?p=2098111](http://www.insanelymac.com/forum/topic/298027-guide-aio-guides-for-hackintosh/?p=2098111) &lt;&lt; ok ? There is a specific paragraph for that.

> ... but dude! I'm the laziest shit on this earth, and I have the Fall Creators Update!

[https://docs.microsoft.com/en-us/windows/deployment/mbr-to-gpt](https://docs.microsoft.com/en-us/windows/deployment/mbr-to-gpt) &lt;&lt; Good news! No need for extra steps!

> I have clover in legacy and I have a GPT formatted disk, I want to install winblows and it wont saying it's GPT and needs MBR! HOW?

\(Win10 only, maybe will work on win8.1, win 7 is harder\) Make your USB in the UEFI way \(8GB FAT32 USB, copy the contents of the ISO into the USB, or use bootcamp to make it on macOS\). In Clover GUI, if you see "Boot bootx64.efi from &lt;something that hints to USB", go for it, if it doesn't load, or does nothing

1. Hit "S" to open shell command
2. Follow this album [https://imgur.com/a/U4lgW](https://imgur.com/a/U4lgW) \(note: these pics were taken when I made a guide for Win7/8.X installation on Legacy to UEFI \(quite the complicated stuff\), and we had to download `bootx64.efi`, on Windows 10 installer, you dont need to download it, it's already in its folder\)

> I'm stuck in windows and I need to edit stuff on EFI, how do I do that?

1. Open Command Prompt as administrator \(or PowerShell if you're "modern"\)
2. Type `mountvol X: /s`. This will mount the EFI partition to `X:`, you can change the letter to anything else as long as it's not used
3. Download Explorer++ \(9oo9le 1t\)
4. Run it as administrator
5. ...
6. Edit

> ... but I need to edit my config.plist dude! How can I do that????

1. Copy your config.plist somewhere else than the EFI partition
2. Use either:
   * Geany \(9oo9le\)
   * Sublime Text \(9oo9le\)
   * jsPlistor [http://tustin2121.github.io/jsPlistor/](http://tustin2121.github.io/jsPlistor/) \(a JS plist editor, you need to open the config and copy its contents to the "Import" box\)
   * CCE [http://cloudclovereditor.altervista.org/cce/index.php](http://cloudclovereditor.altervista.org/cce/index.php) \(A better alternative to CC and it's used on the wed directly, you'll just need to upload your file\)
3. Save
4. Replace your old one using Explorer++
5. Hope you didnt break it.

