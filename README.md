# ros-learning

## Sharing experience of setting up ubuntu 16.04 & ubuntu 18.04 as dual boot / VM

### VM on Macbook pro M1 2020 (failed on 18.04)

downloaded arm64 server version, then to install desktop graphics.

I tried UTM (version3.2.4), Parallel Desktop and VMWare Fusion.

UTM works for 16.04, while 18.04 has the error "no wifi adapter found". The <b>keypoint</b> is to choose "display-<b>console only</b>" before starting installation. and to click the button on the top right to <b>eject</b> the image <b>before</b> clicking 'continue' once installtion finishes.

Parallel Desktop and VMWare Fusion have the error of "CD-ROM Mounting" during installation.

I think parallel desktop and VMWare Fusion should be fine to support ubuntu after 20.

### Dual boot on Microsoft Surface laptop 5 (failed) - Win11

make a bootable USB drive by rufus - select the iso image then leave everything default

win+x opens disk management, shrink volume and leave it as unallocated.

reboot the laptop (press f4) to enter BIOS setup menu. Make USB as the top boot option, BUT it never boot from USB (weird).

I tried to directly boot USB. However, once ubuntu installation started, touchpad and keyboard were not working. I need bluetooth keyboard and mouse to go on. Even installation finished, ubuntu was still not able to be deteced, and grub never shows up. 

Gave up here.

### Dual boot on Dell Inspiration 15 7580 (worked) - Win11 Home & ubuntu 16.04
1. close BitLocker - quite annoying to enter recovery key
2. disable secure boot, change sata operation from raid to AHCI
3. make usb be the top boot option
4. start installing ubuntu by usb
5. windows in this case might be not working - because of AHCI. solution is here :(https://blog.csdn.net/qq_38664402/article/details/124085302)

### Dual boot on Dell XPS 13 9360 (worked) - Win10 Pro & ubuntu 18.04
everything is same as above.

### Install software on host computer:
This software is developed to run under Linux with Ubuntu 16.04 and ROS Kinetic. 
Installation steps are:
1. Unpack the htp_teleop.zip file into the source folder of a catkin workspace
2. Install dependencies:
    1. sudo apt-get install ros-kinetic-gazebo-ros-control
    2. sudo apt-get install ros-kinetic-joint-state-controller
    3. sudo apt-get install ros-kinetic-hector-gazebo-plugins
    4. sudo apt-get install ros-kinetic-hector-gazebo
    5. sudo apt-get install python-pygame
    6. sudo pip3 install -U scikit-fuzzy
3. Build all new ROS parts
    1. catkin_make
4. Set up the model path:
    1. export GAZEBO_MODEL_PATH=~/.gazebo/models:$GAZEBO_MODEL_PATH
### Run simulated environment on host:
1. Start the simulation
    1. roslaunch am_gazebo am_gazebo_hrp.launch gui:=true
2. launch different running nodes separately:
    1. source ~/catkin_ws/devel/setup.bash
    2. rosrun am_driver hrp_teleop_or_auto.py for mode 0 and 2
    3. rosrun am_driver teleop_or_slowdown.py for mode 0 and 3
    4. rosrun am_driver shared_control_slowdown.py for mode 5
    5. rosrun am_driver bumper_teleop.py for mode 1
    6. rosrun am_driver fuzzy_logic.py for mode  for mode 0,4,6,7
3. launch the interface:
    1. go to the directory and run python interface.py

