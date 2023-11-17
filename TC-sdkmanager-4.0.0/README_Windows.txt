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
## Windows Desktop ##
1. Install Docker Desktop on Microsoft Windows 10 Professional or Enterprise 64-bit
    https://hub.docker.com/editions/community/docker-ce-desktop-windows/

2. Launch Docker Desktop
Check the notification menu for docker and open “Dashboard"

3. Verify docker installation
Open Windows PowerShell and type command “docker images”
If the installation is not proper or when the docker desktop application is not running in background, PowerShell console will throw out error


##########          INSTALL SDK MANAGER          ##########
## Windows PowerShell ##
1. Unzip TC-sdkmanager-x.x.x.zip and navigate to TC/sdkmanager/x.x.x directory from a Windows PowerShell.

2. Execute the following commands:
    # Windows PowerShell #
    # For RB5LU1.0,RB6,RB1,RB2 Platforms :Generate Ubuntu 18.04 docker image #
    $ rm .\Dockerfile
    $ cmd /c mklink Dockerfile Dockerfile_18.04
    $ docker build -t ubuntu:18.04-sdkmanager .
    # For Robotics RB5 LU2.0 and RB5N LU2.0 Platform :Generate Ubuntu 20.04 docker image #
    $ rm .\Dockerfile
    $ cmd /c mklink Dockerfile Dockerfile_20.04
    $ docker build -t ubuntu:20.04-sdkmanager .
---------------------------------------------------------------------------------------------------------------------
Make sure to include the "space" and "period" at the end of the command.
ubuntu:18.04-sdkmanager or ubuntu:20.04-sdkmanager: the name of docker image to be generated.


##########          LAUNCH SDK MANAGER          ##########
## Windows Desktop ##
1. Create Docker container
    # For RB5LU1.0,RB6,RB1,RB2 Platforms ?Generate Ubuntu 18.04 docker image #
    $ docker run -it -d --name sdkmanager_container ubuntu:18.04-sdkmanager
    # For Robotics RB5 LU2.0 and RB5N LU2.0 Platform ?Generate Ubuntu 20.04 docker image #
    $ docker run -it -d --name sdkmanager_container ubuntu:20.04-sdkmanager
---------------------------------------------------------------------------------------------------------------------
Above command will generate a docker container named “sdkmanager_container”

2. Launch sdkmanager
    $ docker exec -it sdkmanager_container sdkmanager


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
## Windows Desktop ##
Since you are using Docker container on Windows, you cannot use sdkmanager to flash the images on your Qualcomm Robotics RBx development kit.
You will need to copy the images to Windows 10 filesystem and use the MULTIDL_TOOL to flash the images.

1. Copy the full build from Docker container to Windows Host PC after the build is generated
From a new Windows PowerShell window:
$ docker cp sdkmanager_container:[target_directory]/[name_of_selected_release]/full_build [destionation path on Windows host PC]
---------------------------------------------------------------------------------------------------------------------
Example: docker cp sdkmanager_container:/home/hostPC/demo_0803/QRB5165.1.0.0-200731/full_build D:\
---------------------------------------------------------------------------------------------------------------------

2. Flashing RBx
2.1 Refer to https://www.thundercomm.com/product/qualcomm-robotics-rb5-development-kit/#doc for the MULTIDL_TOOL User Guide
2.2 Install the flashing tool MULTIDL_TOOL from the downloaded zip file. (Refer MULTIDL_TOOL_USER_GUIDE.pdf)
2.3 Follow these steps to make sure that device is in Emergency Download (EDL) mode
        Method 1: adb reboot edl
        Method 2: Press F_DL key to power on.
    Please check the Device Manager to make sure the device is detected as "Qualcomm HS-USB QLoader 9008 (COMx)"
    If the device is not detected, you might need to download and install the correct USB drivers.
    Refer to https://www.thundercomm.com/product/qualcomm-robotics-rb5-development-kit/#doc to download and install the correct USB drivers.

2.4 Use MULTIDL_TOOL to flash the full_build:
    1) Launch MULTIDL_TOOL.
    2) From the MULTIDL_TOOL window, click 'Options->Configuration' to set full_build path.
    3) Enter '123456' for the password prompt.
    4) Choose ‘Flat Build’, Flash Type as ‘ufs’, and select your local full_build path, and programmer file (prog_firehose_ddr.elf)
    5) Click ‘Load XML’ to load xml files. When prompted, select all the XML files and all the Patch files in the full_build\ufs folder.
        Keep other settings as default. Then click ‘OK’ to go back to main page.
    6) Disconnect the RB5 device from PC and power it off.
    7) Plug in the power on device. Press and hold F_DL key, then connect device to PC via a type-C usb cable.
    8) Release F_DL key after the board is connected to PC.
    9) Click ‘START’ button corresponding to your device port on MULTIDL_TOOL window, then the flash process will start.
    10) Wait for the flash to be done, and the device will reboot automatically.


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
