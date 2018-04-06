# Welcome to my Chromebook Journey!

Current setup environment (as reported by chrx):
* Model:       ASUS Chromebook C213NA
* Released:    2017
* CPU Family:  Intel Apollo Lake

Before you begin, please backup your data as this will wipeout your data.

### Developer Mode
Developer Mode is required for a few of the steps outlined here (e.g., install crouton or even run chrx and Mr.Chromebox's firmware script).

## Install Crouton

1. Make the folder:
```
sudo mkdir /usr/local/bin
```
2. Download crouton and set the execution bit:
```
sudo curl -L -# -o ~/Downloads/crouton \
https://github.com/dnschneid/crouton/raw/master/installer/crouton && \
sudo chmod +x ~/Downloads/crouton
```
3. Setup crouton:
```
sh ~/Downloads/crouton
```
4. Install Ubuntu with Xfce:
```
sudo sh ~/Downloads/crouton -t xfce,extension,xiwi,touch
```

> Other types of installation based on the UI/GUI:
>
> If installing Xfce:
> ```
> sudo sh ~/Downloads/crouton -t xfce,extension,xiwi,touch
> sudo startxfce4
> ```
>
> If installing cli only:
> ```
> sudo sh ~/Downloads/crouton -t cli-extra,xiwi,keyboard
> sudo enter-chroot
> ```
>
> If installing LXDE:
> ```
> sudo sh ~/Downloads/crouton -t lxde,extension,xiwi,keyboard
> sudo startlxde
> ```
>
> If installing Gnome:
> ```
> sudo sh ~/Downloads/crouton -t gnome,extension,keyboard
> sudo startgnome
> ```
>
> If installing KDE:
> ```
> sudo sh ~/Downloads/crouton -t kde,extension,keyboard
> sudo startkde
> ```
>
> If installing Unity:
> ```
> sudo sh ~/Downloads/crouton -t unity,extension,keyboard
> sudo startunity
> ```
>
> If installing xiwi after:
> ```
> sudo sh ~/Downlods/crouton -t xiwi -u -n chrootname
> ```

### Update Crouton

To update crouton in chroot:  `croutonversion -u -d -c`

To update crouton in crosh:  `sudo sh ~/Downloads/crouton -u -n chrootname`


## Install and Run Linux via Dual-Boot


### Legacy BIOS (SeaBIOS)
Using Mr.Chromebox to set the legacy boot (**RW_LEGACY** or SeaBIOS):

`cd; curl -LO https://mrchromebox.tech/firmware-util.sh && sudo bash firmware-util.sh`

Using **chrx** to resize partition:

`cd ; curl -Os https://chrx.org/go && sh go`

To install GalliumOS (latest) Linux:

`cd ; curl -Os https://chrx.org/go && sh go -d galliumos -H hostname -U username -p admin-misc`

### Sleep/Suspend Mode
If Chromebook enters sleep/suspend mode, there will be issues with the DeveloperMode flags (e.g., Legacy Boot `dev_boot_legacy`) being cleared.  **CTRL-L** will only beep and not let you boot via legacy boot.  To fix the legacy BIOS, boot back into ChromeOS (**CTRL-D**) and use **crosh**:

`sudo crossystem dev_boot_usb=1 dev_boot_legacy=1`

After, reboot and **CTRL-L** will now successfully let you boot via legacy boot (e.g., boot into the installed Linux if dual booting).

Currently, there does not seem to be a way to successfully suspend.  Therefore, it is better to disable suspend for the time being.  Otherwise every time the Chromebook suspends and wakes-up, it goes to the ChromeOS recovery screen.

### ChromeOS Recovery
To completely remove Linux created by chrx, it is necessary to perform a full recovery as a powerwash only deletes user data.  (The parition that was created after the resize would not be affected by a powerwash.)  Google provides a Chrome Application that can be downloaded from the Chrome Web Store called [Chromebook Recovery Utility](https://chrome.google.com/webstore/detail/chromebook-recovery-utili/jndclpdbaamdhonoechobihbbiimdgai), which will be used to create the recovery media with a USB drive or SD/microSD card.  For the ASUS C213NA Chromebook, an 8GB USB drive was used to create the recovery media.

1. To perform the recovery, make sure that the Chromebook is off.
2. Insert the recovery media (USB drive of SD/microSD card).
3. Press **ESC-Refresh-Power** 3-key combination to boot into recovery mode.

After the verification, the recovery process will start.  This entire process will take a few minutes to complete.

Note that the Developer Mode will still be enabled after this process is completed.  Press **CTRL-D** to put into ChromeOS (via Developer Mode).

### Other Useful Links:
* [Mr.Chromebox Firmware Script](https://mrchromebox.tech/#fwscript)
* [chrx](https://chrx.org/)
* [GalliumOS Linux](https://galliumos.org/)
* [GalliumOS on Edgar](https://gist.github.com/stupidpupil/1e88638e5240476ec1f77d4b27747c88)
* [GalliumOS to do list includes suspend/resume functionality for Apoolo Lake platform](https://github.com/GalliumOS/galliumos-distro/issues/364)
* [GalliumOS resets crossystem flags when suspending](https://www.reddit.com/r/GalliumOS/comments/7lini3/apollo_lake_support/)
* ~~[Suspend bug](https://bugs.chromium.org/p/chromium/issues/detail?id=221905)~~
* ~~[GalliumOS Bug for suspend](https://github.com/GalliumOS/galliumos-distro/issues/268)~~
* ~~[Issues related to suspend](https://github.com/GalliumOS/galliumos-distro/issues/198)~~
* ~~[Potential fix for Ubuntu for suspend](https://askubuntu.com/questions/110398/computer-turns-off-instead-of-suspending-sleeping)~~
* ~~[Restoring legacy boot](http://jrs-s.net/2014/04/01/restoring-legacy-boot-linux-boot-on-a-chromebook/)~~
