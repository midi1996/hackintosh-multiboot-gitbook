# Fix Clovy Clovy

On some cases, especially laptops, they are hard coded to start `\EFI\Microsoft\Boot\bootmgfw.efi` instead of `\EFI\BOOT\BOOTX64.EFI`, and this to lock the computer \(somewhat\) to M$'s botnet OS. To fix that you can:

* Mount EFI partition, rename `bootmgfw.efi` in `EFI > Microsoft > Boot` to anything else than `bootmgfw.efi` \(like bootmgfww.efi or something\). Remember that naming. Now, the computer will not find `bootmgfw.efi` and look for `bootx64.efi` or whatever is the next boot option.
* Rename `CLOVERX64.EFI` to `bootmgfw.efi` then rename M$'s `bootmgfw.efi` to anything else, then copy the fake `bootmgfw.efi` to `EFI > Microsoft > Boot`. On some laptops it is needed to force load anything named `bootmgfw.efi` to boot anything.
* On _**SOME**_ UEFI systems, like AMI Aptio, you can add and change boot options from the firmware setup \(aka, BIOS setup\) and change boot file priority, use this instead of renaming if you have this option. If you can do this, no need to configure clover any further.
* Manually Add Clover Entry:
  * Enter EFI Shell.
  * As shell loads, note the label of the HDD/SSD your EFI and macOS/OSX are installed on, or type `map` to see it
  * Then `bcfg boot dump` it will output your actual boot entries.  
  * VERY CAREFULLY add a new entry after the highest one in the list. I had to type `bcfg boot add XX FSX:\EFI\CLOVER\CLOVERX64.EFI "CloverBoot"`, where `FSX` is your macOS/OSX EFI, `XX` is the new entry and `"CloverBoot"` is the name of the entry, can be changed to anything as long as it's between `" "`
* Then you can delete old `bcfg` entry that points to `/BOOT/BOOTX64.EFI` with `bcfg boot rm XX` where `XX` is the number identifier seen when you do `bcfg boot dump`
* _Optional:_ You can then boot into macOS/OSX and rename /BOOT to /BOOT.bak, leave it as it is if you're using windows/linux or delete it if you had it there for clover boot anyways.

_Source:_ [_https://sourceforge.net/p/cloverefiboot/tickets/226/\#d1a9/0222/8cc1_](https://sourceforge.net/p/cloverefiboot/tickets/226/#d1a9/0222/8cc1)

_\(Credits to /u/corpnewt and /u/Ressetkk for mentioning this to me, maybe I'll add `efibootmgr` guide too, most linux users know how to use google tho\)_

**Keep in mind:**

* On ANY windows cumulative or seasonal update/upgrade, your fake `bootmgfw.efi` will be replaced by a new one, or if you renamed it, a new one will be copied over, so you will need to rename/replace that file.
* If you like to use Grub2 to load linux, make sure you load GRUB2 from Clover and not the opposite \(feasible, works sometimes, not recommended\).

Now you will get to CLOVER screen but without windows access mostly \(I'm sure you dont need to rename grubx64 for linux users, as most OEMs dont lock the firmware on it\). So to add ANY EFI program to the boot list, you need to add this `Custom Entry` to clover's `config.plist` as shown here:

```markup
    <key>GUI</key>
    <dict>
     ...
      <key>Custom</key>
      <dict>
        <key>Entries</key>
        <array>
          <dict>
            <key>Path</key>
            <string>\EFI\path\to\file.efi</string>
            <key>Title</key>
            <string>*insert title here*</string>
            <key>Type</key>
            <string>Windows OR Linux</string>
            <key>Volume</key>
            <string>*Insert partition GUID here if on different DISK*</string>
          </dict>
           ... to other entries ...
        </array>
      </dict>
     ...
    </dict>
```

So for example `bootmgfw.efi` renamed to `bootmgfww.efi`

```markup
    <key>GUI</key>
    <dict>
     ...
      <key>Custom</key>
      <dict>
        <key>Entries</key>
        <array>
          <dict>
            <key>Path</key>
            <string>\EFI\Microsoft\Boot\bootmgfww.efi</string>
            <key>Title</key>
            <string>Windows Bootloader</string>
            <key>Type</key>
            <string>Windows</string>
            <key>#Volume</key>
            <string>I DONT NEED IT</string>
            <key>#Comment</key>
            <string>When I add a "#" before the naming of the key, it's disabled</string>
          </dict>
        </array>
      </dict>
      ...
    </dict>
```

Save your config.plist and try it out. You can replace path with `\EFI\grub\grubx64.efi` to load GRUB2 or look where `lilo` file is located and add it too.

_To know more, go to:_

[http://www.insanelymac.com/forum/topic/298027-guide-aio-guides-for-hackintosh/?p=2029540](http://www.insanelymac.com/forum/topic/298027-guide-aio-guides-for-hackintosh/?p=2029540)

[https://clover-wiki.zetam.org/configuration/gui\#gui\_custom](https://clover-wiki.zetam.org/configuration/gui#gui_custom)

