SDK Manager User Guide
Current SDK manager version: 4.0.0


##########          HOW TO DOWNLOAD          ##########
1. A valid Thundercomm Account is mandatory, register on https://www.thundercomm.com/app_en/register.
2. SDK Manager Download link:
https://www.thundercomm.com/product/qualcomm-robotics-rb6-development-kit/#sdk-manager

##########          FEW THINGS TO BE AWARE OF           ##########
1. Ubuntu on libvirt KVM/QEMU is not supported.
2. For Docker users on any Ubuntu Desktop (18.04, 16.04, etc.), please follow the guide in "On Other Ubuntu Host" for all sections.
3. Docker desktop is only supported on Windows 10 professional or enterprise.
4. Enter a work directory with read-write permissions for sdkmanager. For Docker image user, create the work directory under /home/hostPC/.
5. The full process for image repack requires at least 40 minutes, depending on Internet speed.
6. For LU platform, generate image first before flashing full build.
7. Keep the internet connected during the image generation.
8. Recommend using USB3.0 port and USB3.0 cable for flashing the image.
9. If you are using a Linux desktop to flash the device, please run the following command before connecting the device to the desktop. 
   $ sudo systemctl stop ModemManager


##########          PREPARATION          ##########
## On Ubuntu Host ##
#For Robotics RB5 LU2.0 and RB5N LU2.0 Platform (required OS: Ubuntu 20.04)#
    Required packages (minimum version): coreutils 8.30, fakechroot 2.19, fakeroot 1.24, kmod 27-1ubuntu2.1, libc6-arm64-cross 2.31, python 2.7.18, qemu-user-static 1:7.2+dfsg-5ubuntu1, udev 245.4-4ubuntu3.20, unzip 6.0, wget 1.20.3.
    Run these commands to create soft links:
    $ sudo rm -rf /lib/ld-linux-aarch64.so.1
    $ sudo ln -sf /usr/aarch64-linux-gnu/lib/ld-2.31.so /lib/ld-linux-aarch64.so.1
    $ sudo ln -sf /bin/bash /bin/sh
    $ sudo dpkg -P qemu-user-static
    $ wget http://archive.ubuntu.com/ubuntu/pool/universe/q/qemu/qemu-userstatic_6.2+dfsg-2ubuntu6_amd64.deb
    $ sudo dpkg -i qemu-user-static_6.2+dfsg-2ubuntu6_amd64.deb

#For RB5LU1.0, RB6, RB1, RB2 Platforms (required OS: Ubuntu 18.04)#
    Required packages (minimum version): coreutils 8.28, fakechroot 2.19, fakeroot 1.22, kmod 24-1ubuntu3.2, libc6-arm64-cross 2.27, python 2.7.15, qemu-user-static 1:2.11+dfsg-1ubuntu7.28, udev 237-3ubuntu10.42, unzip 6.0, wget 1.19.4.

1. Install the dependency libraries to the host computer
   $ sudo apt-get install coreutils fakechroot fakeroot kmod libc6-arm64-cross python2.7 qemu-user-static wget udev openssh-server -y

## Generate Ubuntu Docker Image ##
NOTE: Different OS versions require different Docker images.
#Robotics RB5 LU2.0 and RB5N LU2.0 Platform#
For an Ubuntu 16.04 or 18.04 host, an Ubuntu 20.04 Docker image is required.

#RB5LU1.0, RB6, RB1, and RB2 Platforms#
For an Ubuntu 16.04 or 20.04 host, an Ubuntu 18.04 Docker image is required.

1. Install qemu-user-static, openssh-server and udev to the host PC.
   $sudo apt-get install qemu-user-static openssh-server udev -y

2. Install Docker
   Follow the steps in "Install using the repository" on Docker website: 
   https://docs.docker.com/engine/install/ubuntu/

3. Generate Ubuntu 18.04/20.04 docker image:
   # Ubuntu terminal #
   # Generate Ubuntu 18.04 docker image #
   $ ln -sf Dockerfile_18.04 Dockerfile
   $ sudo docker build -t ubuntu:18.04-sdkmanager .
   # Generate Ubuntu 20.04 docker image #
   $ ln -sf Dockerfile_20.04 Dockerfile
   $ sudo docker build -t ubuntu:20.04-sdkmanager .


##########          INSTALL SDK MANAGER          ##########
## On Ubuntu Host ##
1. Unzip TC-sdkmanager-x.x.x.zip and navigate to TC-sdkmanager-x.x.x directory from a terminal window, install or re-install sdkmanager
   $ sudo dpkg -i tc-sdkmanager-vx.x.x_amd64.deb

## On Ubuntu Docker ##
1. Generate Ubuntu 18.04/20.04 docker image
Unzip TC-sdkmanager-x.x.x.zip, navigate to TC-sdkmanager-x.x.x directory from a new terminal window (on Ubuntu Desktop), and execute the following commands:
   # Ubuntu terminal #
   # Generate Ubuntu 18.04 docker image #
   $ ln -sf Dockerfile_18.04 Dockerfile
   $ sudo docker build -t ubuntu:18.04-sdkmanager .
   # Generate Ubuntu 20.04 docker image #
   $ ln -sf Dockerfile_20.04 Dockerfile
   $ sudo docker build -t ubuntu:20.04-sdkmanager .

---------------------------------------------------------------------------------------------------------------------
Make sure to include the "space" and "period" at the end of the command.
ubuntu:18.04-sdkmanager or ubuntu:20.04-sdkmanager: the name of docker image to be generated.


##########          LAUNCH SDK MANAGER          ##########
## On Ubuntu Host ##
1. Launch sdkmanager
    $ sdkmanager

## On Ubuntu Docker ##
1. Create Docker container
    # Ubuntu 18.04 docker image #
    $ sudo docker run -v /home/${USER}:/home/hostPC/ --privileged -v /dev/:/dev -v
    /run/udev:/run/udev -d --name sdkmanager_container -p 36000:22 ubuntu:18.04-sdkmanager
    # Ubuntu 20.04 docker image #
    $ sudo docker run -v /home/${USER}:/home/hostPC/ --privileged -v /dev/:/dev -v
    /run/udev:/run/udev -d --name sdkmanager_container -p 36000:22 ubuntu:20.04-sdkmanager

---------------------------------------------------------------------------------------------------------------------
Host PC's /home/${USER} is mounted on /home/hostPC in Docker container
Above command will generate a docker container named sdkmanager_container.

2. Launch sdkmanager in Docker container
$ sudo docker exec -it sdkmanager_container sdkmanager


##########          RUNNING SDK MANAGER          ##########
## General ##
1. Provide Thudercomm login credentials 
	Credential Checking ...
	Enter your Thundercomm username:
	Enter your Thundercomm password:
2. Provide a working directory when asked for target directory (for example "/home/user")
Enter absolute target directory for SDK (overwrites existing files, default: /home/user): 

Note: For Docker users, provide the work directory as /home/hostPC/[working directory]

3. Select a desired product
        Select your product:
	1: RB1
	2: RB2
	3: RB5
	4: RB5N(Non-Pop)
	5: RB6
	Select one number of product( 1 | 2 | 3 ...) to continue with:

4. Select a desired platform for Robotics RBx device
	Choose a platform for Robotics RBx device
	Enter 1 to use LU platform, 2 to use LE platform:

## LU PLATFORM ##
1. Type the number of available version for image repack, for example, "1"
        You chose LU platform
        Enter 1 to use LU1.0 platform, 2 to use LU2.0 platform:

2. Type the number of available version for image repack, for example, "1"
        You chose LU1.0 platform

	Checking current version of release ...
	Available versions: 
	1: QRB5165.UBUN.x.x-xxxxxx (latest version)

	Recommended version: QRB5165.UBUN.x.x-xxxxxx

	Select one number of available version ( 1 ) to continue with: 

3. Type "1" when below message was shown to start downloading LU resources and image repacking, or type "help" for more information

	--------------------------------------------------------
	SDK has been successfully set up and is ready to be used
	Type 'help' for commands
	--------------------------------------------------------
	> help

	commands:
	help = Show usage help for LU platform
	1 = Download LU resources and generate system.img with current release
	2 = Flash full build (require system.img generation first)
	q = exit sdk manager


	You will see the following message once the images are built successfully
	--------------------------------------------------------
	Move sparse images to full_build ...done
	You may proceed to flash full_build to your device
	--------------------------------------------------------

NOTE: The repack process might take up to 40 minutes. 

4. After the completion of repack process, system image is generated in the working directory
Note: For Docker users, the system image is generated in /home/hostPC/[working directory]

## LE PLATFORM ##
1. Type the number of available version to contiue, for example, "2"
        You chose LE platform

	Checking current versions of release ...
	Available versions: 
	1: QRB5165.LE.x.x-xxxxxx (latest version)

	Recommended version: QRB5165.LE.x.x-xxxxxx

	Select one number of available version ( 1 ) to continue with: 

2. Type "1" when below message was shown to download LE resources, or type "help" for more information

	--------------------------------------------------------
	SDK has been successfully set up and is ready to be used
	Type 'help' for commands
	--------------------------------------------------------
	> help

	commands:
	help = Show usage help for LE platform
	1 = Download LE resources
	2 = Flash full build
	3 = Download LE SDK toolchain
	q = exit sdk manager


    You will see the following message once the resource is downloaded successfully
	Download LE resources ... Done


##########          FLASH RBx DEVICE          ##########
## On Ubuntu Host and On Ubuntu Docker ##
1. Disconnect the device from PC before flashing full build, and follow the operation steps below:
    1) Power off the device (unplug power cable and USB cable)
    2) Plug in the power on device (12V)
    3) Press and hold F_DL key, and connect board to PC via a type-C USB (It will switch the device to EDL mode)
    4) Release F_DL key after the board is connected to PC
    5) Start flashing process from the SDK manager (command 2: "Flash full build")
    6) SDK manager will detect the device and start flash process automatically
    7) Wait for the flashing process to be finished, the board will reboot automatically.

2. Enter the command below in a new terminal window on Host PC after the device successfully boots up:
$ adb wait-for-device shell


##########          TROUBLESHOOT          ##########
1. Internet Timeout Issue
Internet timeout issue may happen during the image generation process. If issues like "Unable to fetch" are encountered, try to run command 1 again.

2. Apt Source issue
If the download fails, check the internet connection and the source list.

3. Device Boots Up
The device reboots after the flashing process is completed. If the sdkmanager does not detect the device, execute the followings:
    1) If Ubuntu 18.04/20.04 is used on Docker, check whether "adb kill-server" is entered on the host PC before flashing image.
    2) Reboot the device manually, open a new terminal window and enter 'adb shell' to check device.
    3) Check if any debian packages are modified.

4. If flash process on Ubuntu systems does not work properly, copy full-build folder to a Windows PC and use Thundercomm MULTIDL_TOOL to flash the image.
Refer to https://www.thundercomm.com/product/qualcomm-robotics-rb5-development-kit/#doc for the tool and user guide.


For additional reference please refer to:
## Robotics RB5 Platform ##
1. Quick Start Guide: https://developer.qualcomm.com/qualcomm-robotics-rb5-kit/quick-start-guide
2. Hardware Reference Guide: https://developer.qualcomm.com/qualcomm-robotics-rb5-kit/hardware-reference-guide
3. Software Reference Manual: https://developer.qualcomm.com/qualcomm-robotics-rb5-kit/software-reference-manual
## Robotics RB6 Non-pop Platform ##
1. Quick Start Guide: https://developer.qualcomm.com/qualcomm-robotics-rb6-kit/quick-start-guide
2. Hardware Reference Guide: https://developer.qualcomm.com/qualcomm-robotics-rb6-kit/hardware-reference-guide
3. Software Reference Manual: https://developer.qualcomm.com/qualcomm-robotics-rb6-kit/software-reference-manual
