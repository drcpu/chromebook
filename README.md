# Welcome to my Chromebook Joourney!

Current setup environment (as reported by chrx):
* Model:       ASUS Chromebook C213NA
* Released:    2017
* CPU Family:  Intel Apollo Lake

Before you begin, please backup your data as this will wipeout your data.

Enable Developer Mode.

Using Mr.Chromebox to set the legacy boot (**RW_LEGACY** or SeaBIOS):

`cd; curl -LO https://mrchromebox.tech/firmware-util.sh && sudo bash firmware-util.sh`

Using **chrx** to resize partition:

`cd ; curl -Os https://chrx.org/go && sh go`

To install GalliumOS (latest, e.g., GalliumOS 2.2) Linux:

`cd ; curl -Os https://chrx.org/go && sh go -d galliumos -H hostname -U username -p admin-misc`

To install GalliumOS 2.1 Linux:

`cd ; curl -Os https://chrx.org/go && sh go -d galliumos -r 2.1 -H hostname -U username -p admin-misc`


### Sleep/Suspend Mode
If Chromebook enters sleep/suspend mode, there will be issues with the legacy boot.  **CTRL-L** will only beep and not let you boot via legacy boot.  To fix the legacy BIOS, boot back into ChromeOS (**CTRL-D**) and use **crosh**:

`sudo crossystem dev_boot_usb=1 dev_boot_legacy=1`

After, reboot and **CTRL-L** will now successfully let you boot via legacy boot (e.g., boot into the installed Linux if dual booting).

Potentially changing the BIOS (with the removal of the write-protect screw and with Mr.Chromebox's BOOT_STUB firmware) would allow the wake to bootup Legacy BIOS/SeaBIOS by default allowing the suspend-wake functionality to work.

Currently, there does not seem to be a way to successfully suspend.  Therefore, it is better to disable suspend for the time being.  Otherwise every time the Chromebook suspends and wakes-up, it goes to the ChromeOS recovery screen.

### Useful links:
* [Mr.Chromebox Firmware Script](https://mrchromebox.tech/#fwscript)
* [chrx](https://chrx.org/)
* [GalliumOS Linux](https://galliumos.org/)
* [GalliumOS on Edgar](https://gist.github.com/stupidpupil/1e88638e5240476ec1f77d4b27747c88)
* [Suspend bug](https://bugs.chromium.org/p/chromium/issues/detail?id=221905)
* [GalliumOS Bug for suspend](https://github.com/GalliumOS/galliumos-distro/issues/268)
* [Issues related to suspend](https://github.com/GalliumOS/galliumos-distro/issues/198)
* [Potential fix for Ubuntu for suspend](https://askubuntu.com/questions/110398/computer-turns-off-instead-of-suspending-sleeping)
* [Restoring legacy boot](http://jrs-s.net/2014/04/01/restoring-legacy-boot-linux-boot-on-a-chromebook/)
