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
sudo startxfce4
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

### Install Applications

```
sudo apt update
sudo apt upgrade
sudo apt-get install -y curl lynx mc vim wget python python-pip python-httplib2
```

Install Google Chrome Browser
```
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
echo 'deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main' | sudo tee /etc/apt/sources.list.d/google-chrome.list
sudo apt-get update
sudo apt-get install -y google-chrome-stable
```

Install Visual Studio Code
```
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
sudo apt-get update
sudo apt-get install -y code
```

Install rkt to run docker containers:
```
sudo apt install -y iptables libnfnetlink0
gpg --recv-key 18AD5014C99EF7E3BA5F6CE950BDD3E0FC8A365E
wget https://github.com/rkt/rkt/releases/download/v1.29.0/rkt_1.29.0-1_amd64.deb
wget https://github.com/rkt/rkt/releases/download/v1.29.0/rkt_1.29.0-1_amd64.deb.asc
gpg --verify rkt_1.29.0-1_amd64.deb.asc
sudo dpkg -i rkt_1.29.0-1_amd64.deb
```

```
# Use container for now
# Install Couchbase
# curl -O http://packages.couchbase.com/releases/couchbase-release/couchbase-release-1.0-4-amd64.deb
# sudo dpkg -i couchbase-release-1.0-4-amd64.deb
# sudo apt-get update
# sudo apt install -y couchbase-server
# sudo iptables -I INPUT -p tcp --dport 4369 -j ACCEPT
# sudo iptables -I INPUT -p tcp --dport 8091 -j ACCEPT
# sudo iptables -I INPUT -p tcp --dport 8092 -j ACCEPT
# sudo iptables -I INPUT -p tcp --dport 8093 -j ACCEPT
# sudo iptables -I INPUT -p tcp --dport 8094 -j ACCEPT
# sudo iptables -I INPUT -p tcp --dport 9100 -j ACCEPT
# sudo iptables -I INPUT -p tcp --dport 9101 -j ACCEPT
# sudo iptables -I INPUT -p tcp --dport 9102 -j ACCEPT
# sudo iptables -I INPUT -p tcp --dport 9103 -j ACCEPT
# sudo iptables -I INPUT -p tcp --dport 9104 -j ACCEPT
# sudo iptables -I INPUT -p tcp --dport 9105 -j ACCEPT
# sudo iptables -I INPUT -p tcp --dport 9998 -j ACCEPT
# sudo iptables -I INPUT -p tcp --dport 9999 -j ACCEPT
# sudo iptables -I INPUT -p tcp --dport 11207 -j ACCEPT
# sudo iptables -I INPUT -p tcp --dport 11209 -j ACCEPT
# sudo iptables -I INPUT -p tcp --dport 11210 -j ACCEPT
# sudo iptables -I INPUT -p tcp --dport 11211 -j ACCEPT
# sudo iptables -I INPUT -p tcp --dport 11214 -j ACCEPT
# sudo iptables -I INPUT -p tcp --dport 11215 -j ACCEPT
# sudo iptables -I INPUT -p tcp --dport 18091 -j ACCEPT
# sudo iptables -I INPUT -p tcp --dport 18092 -j ACCEPT
# sudo iptables -I INPUT -p tcp --dport 18093 -j ACCEPT
# sudo iptables -I INPUT -p tcp --dport 21100:21299 -j ACCEPT
# sudo iptables -L
# /opt/couchbase/bin/couchbase-server -- -noinput -detached
# /opt/couchbase/bin/couchbase-server -k
```

List chroot
```
sudo edit-chroot -a
```

Backup a chroot to ~/Downloads
```
sudo edit-chroot -b chrootname
```

Backup a chroot to an SD Card
```
sudo edit-chroot -f /media/removable/SD\ Card/ -b chrootname (assumes the name of your SD Card is "SD Card")
```

Backup a chroot to a USB drive
```
sudo edit-chroot -f /media/removable/your_path_on_drive -b chrootname
```

Restore from a backup
```
sudo edit-chroot -f /media/removable/your_path_on_drive -r chrootname
sudo sh ~/Downloads/crouton -f backupTarBall.tar.gz
```

Remove chroot
```
sudo delete-chroot chrootname (default is xenial)
sudo delete-chroot xenial
```

Run Couchbase Container
```
sudo rkt run --net=host docker://couchbase --insecure-options=image
sudo rkt stop {UUID}
sudo rkt rm {UUID}
# sudo rkt run --net=host docker://hello-world --insecure-options=image
```

Bash into Container
```
sudo rkt enter {UUID}
sudo rkt enter --app=couchbase {UUID}
```

Run Apps via Xiwi (from crosh)
```
sudo startxiwi -b google-chrome
sudo startxiwi -b code
```

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
