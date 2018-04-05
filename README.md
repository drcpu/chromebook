# Welcome to my Chromebook Joourney!

Using Mr.Chromebox to set the legacy boot (RW_LEGACY or SeaBIOS):

`cd; curl -LO https://mrchromebox.tech/firmware-util.sh && sudo bash firmware-util.sh`

Using chrx to resize partition:

`cd ; curl -Os https://chrx.org/go && sh go`

### Sleep/Suspend Mode
If Chromebook enters sleep/suspend mode, there will be issues with the legacy boot.  CTRL-L will only beep and not let you boot via legacy boot:

https://bugs.chromium.org/p/chromium/issues/detail?id=221905

To fix the legacy BIOS:

http://jrs-s.net/2014/04/01/restoring-legacy-boot-linux-boot-on-a-chromebook/

From crosh:

`sudo crossystem dev_boot_usb=1 dev_boot_legacy=1`

After, reboot and CTRL-L will now successfully let you boot via legacy boot (e.g., boot into the installed Linux if dual booting).

### Useful links:
* https://gist.github.com/stupidpupil/1e88638e5240476ec1f77d4b27747c88
* https://mrchromebox.tech/#fwscript
* https://chrx.org/
