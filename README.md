Scripts for adding stuff to a RattlesnakeOS ROM

Currently only contains a script with patches that adds Magisk to a RattlesnakeOS build

IMPORTANT - READ BEFORE USING
---
- This was uploaded from my private repository at the request of another GitHub user. Since this works on my device, I don't intend to offer much support to this repository.
- **Use at your own risk.**
- This is only compatible with Android 10 builds.
- This does not add Magisk Manager to the build. Unlike official Magisk installations, you will need to install Magisk Manager manually. It will function normally afterwards, however.
- You CANNOT install a **factory** image patched in this way. If you try to, ***you will fail to boot.***
- You MUST install this as either a background OTA update, or as an `adb sideload` OTA image installed from recovery mode.
- ***NEVER PERFORM A FACTORY RESET WITH MAGISK INSTALLED LIKE THIS.***
   - If you perform a Factory Reset with Magisk installed like this, ***you will fail to boot.***
   - If you fail to boot, the Boot Control HAL will mark the failing slot(s) as "unbootable" until it is flashed over with a replacement.
   - Since the engineers at Google no longer have functioning brains, on Android 10, the `boot.img` responsible for booting the system is the same `boot.img` responsible for booting into recovery. Therefore, if your *system* is ever unbootable, then so is your *recovery mode* as well as your *rescue mode* (what's the point of a recovery at that point, then, Google???).
   - As a consequence, if you ever fail to boot, such as after performing a Factory Reset with Magisk installed, you will be unable to boot into Recovery or Rescue mode, meaning you can't flash an unpactched OTA image.
   - If you have locked your bootloader with a custom AVB key, ***YOU WILL BRICK YOUR DEVICE*** if the above ever happens to you unless you have left OEM unlocking enabled and are able to run `fastboot flashing unlock`. If you have not left OEM unlocking enabled and you end up in this situation, you are screwed, because you will have no way to update/replace the failing `boot.img`.
   - To be clear - you *can* lock your bootloader and use your device comfortably with Magisk installed like this. However, be sure that you ***never factory reset your device***, or otherwise put yourself in a situation where it is **possible** to factory reset your device, without ensuring that "OEM unlocking" is enabled in your Developer Options.
   - You may want to consider patching your recovery menu to remove the "factory reset" option to ensure this isn't possible for someone in possession of your device to do.

Also, please be aware that line 21 of `0001-patch_core_makefile.patch` has not been tested by me. I've added it for convenience, but my current method of acheiving the equivalent is changing the `initramfs.c` file of my kernel before compiling my kernel. I'm supplying my own custom kernel patches to my RattlesnakeOS build anyway, so that method has been sufficient for my needs. The line of that patch *probably* works, but it needs to be tested first.

Credit for `0002-patch_mkbootfs.patch` goes to GitHub user CaseyBakey.
