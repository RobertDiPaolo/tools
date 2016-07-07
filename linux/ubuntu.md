# Ubuntu Specific
All this is known to work on Ubuntu 16.04

## Useful Links
* [Kernel PPA](http://kernel.ubuntu.com/~kernel-ppa/mainline/)
* [Firmware Updates](http://archive.ubuntu.com/ubuntu/pool/main/l/linux-firmware/)

## Update Kernel
For newer hardware it can be a good idea to install a more up to date kernel. You can download the .deb file from the Kernel PPA link above and install it. Take the generic kernel and headers for relevant architecture (amd64 in most cases) and install both then restart.

## Update firmware
If you need to update to the latest firmware to support newer hardware or fix bugs. You can download a later version from the link above and install, like so;

    curl -O http://de.archive.ubuntu.com/ubuntu/pool/main/l/linux-firmware/linux-firmware_X.Y_all.deb
    dpkg -i linux-firmware_X.Y_all.deb
    sudo update-initramfs -u -k all

Where X.Y is the firmware version you want to use.

## UI Tweaks
See [here](http://ubuntuforums.org/showthread.php?t=2211863) for how to setup a decent task switcher. And [here](http://askubuntu.com/questions/22207/quickly-place-a-window-to-another-screen-using-only-the-keyboard) to setup a shortcut to move window to another screen.

## HiDPI Display Support
To get apps looking good with HiDPI displays.

### Unity
In the 'Screen Display' setting, set 'Scale for menu and title bars' to 1.65 and 'Scale all window conents to match' to 'Display with smallest controls'.

### Grub
To avoid small fonts on grup screen;
- Add GRUB_GFXMODE=1024x768 to /etc/default/grub
- Run 'sudo update-grub'

### QT & GTK
Create a file '/etc/profile.d/hidpi.sh' with the following in it;

    QT_DEVICE_PIXEL_RATIO=2
    QT_SCREEN_SCALE_FACTORS=1.75
    GDK_SCALE=2
    GDK_DPI_SCALE=0.5

These enviroment vars should fix a lot of apps.

## Power Managment
Install powertop the add the following to /etc/rc.local

    # Make powertop tuning persistant
    powertop --auto-tune

    # Make powertop tuning persistant
    powertop --auto-tune

Depending on your hardware you might then want to explicitly turn back on some stuff.

## Dell XPS15 9550 Tweaks
There is a very good [forum thread](http://ubuntuforums.org/showthread.php?t=2317843) with details on how to setup ubuntu on the XPS15. I've listed what I ended up 

### Kernel
Update to the 4.6 or 4.7 Kernel for better support for Skylake.

### Grub
Update /etc/default/grub so that;

    GRUB_CMDLINE_LINUX_DEFAULT="quiet splash drm.vblankoffdelay=1"
    GRUB_CMDLINE_LINUX="reboot=efi"

This adds a power tweak and makes reboot work correctly.

### Bluetooth
Bluetooth firmware is missing, you can donload it from [here](https://www.dropbox.com/s/8goc4omhnzxij93/BCM-0a5c-6410.hcd?dl=0) and copy it to /lib/firmware/brcm/ then reboot.

### Sensors
To load the sensors (cpu temp, etc);

    apt-get install lm-sensors
    sensors-detect

Follow the instructions and say yes to adding to /etc/modules.

### Dell USB-C Dock
Doesn't always get detected after resume or if it's uplugged and re-plugged, you can rescan as follows;

    sudo sh -c "echo 1 > /sys/bus/pci/rescan"

To get the display port working with the dock, you can download the drivers from [Display Link](http://www.displaylink.com/downloads/ubuntu) and it should work.

## Nvidia
Install the binary drivers from the 'Additional Drivers' app. Also install 'prime-indicator' and add 'prime-indicator&' to the end of /etc/rc.local' so it auto starts.
