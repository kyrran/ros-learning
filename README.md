# ros-learning

## Sharing experience of setting up ubuntu 16.04 & ubuntu 18.04 as dual boot / VM

### VM on Macbook pro M1 2020 (failed on 18.04)

downloaded arm64 server version, then to install desktop graphics.

I tried UTM (version3.2.4), Parallel Desktop and VMWare Fusion.

UTM works for 16.04, while 18.04 has the error "no wifi adapter found". The <b>keypoint</b> is to choose "display-<b>console only</b>" before starting installation. and to click the button on the top right to <b>eject</b> the image <b>before</b> clicking 'continue' once installtion finishes.


Parallel Desktop and VMWare Fusion have the error of "CD-ROM Mounting" during installation.

I think parallel desktop and VMWare Fusion should be fine to support ubuntu after 20.

### Dual boot on Microsoft Surface laptop 5 (failed)

make a bootable USB drive by rufus - select the iso image then leave everything default

win+x opens disk management, shrink volume and leave it as unallocated.

reboot the laptop (press f4) to enter BIOS setup menu. Make USB as the top boot option, BUT it never boot from USB (weird).

I tried to directly boot USB. However, once ubuntu installation started, touchpad and keyboard were not working. I need bluetooth keyboard and mouse to go on. Even installation finished, ubuntu was still not able to be deteced, and grub never shows up. 

Gave up here.

### Dual boot on Dell Inspiration 15 7580 (worked)
1. close BitLocker - quite annoying to enter recovery key
2. disable secure boot, change sata operation from raid to AHCI
3. make usb be the top boot option
4. start installing ubuntu by usb
5. windows in this case might be not working - because of AHCI. solution is here :(https://blog.csdn.net/qq_38664402/article/details/124085302)

### Dual boot on Dell XPS 13 9360 (worked)
everything is same as above.

