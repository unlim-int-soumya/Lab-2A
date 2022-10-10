This lab's prelab section covered how to become familiar with the various terminals and text editors available.

Putty Installation:
To find out which port the board is utilizing, we'll utilize Windows Device Manager. To discover which port the board is utilizing, check without the board plugged in first. Launch Device Manager. Select Ports (COM & LPT). 0*

Now plug in your board. The Device Manager list will refresh and a new item will appear under Ports (COM & LPT). We found a different (COM#) after this item in the list.

Sometimes the item will refer to the name of the board. Other times it may be called something like USB Serial Device, as seen in the image above. Either way, there is a new (COM#) following the name. This is the port your board is using. 1*

As we're using Windows, we had to download a terminal program. We're going to use PuTTY. 2*

Now we had to open PuTTY.

Under Connection type: We chose the button next to Serial.
In the box under the Serial line, We entered the serial port you found that your board is using.
In the box under Speed, entered 115200. This is called the baud rate, which is the speed in bits per second that data is sent over the serial connection. For boards with built in USB it doesn't matter so much but for ESP8266 and other boards with a separate chip, the speed required by the board is 115200 bits per second. So you might as well just use 115200!

If we want to save those settings for later, We should use the options under Load, save or delete a stored session. Enter a name in the box under Saved Sessions, and click the Save button on the right. 3*

Once the settings are entered, Now we're ready to connect to the serial console. We clicked "Open" at the bottom of the window. So, A new window was opened. 4*

C/C++ SDK Installation:


However, in this lab, we had to install the SDK (Software Development Kits) for C/C++ in order to configure our PC for RP2040 development using Pico.

Since we used a Windows PC, we had to follow the steps below to install the C/C++ SDK, browse the pico-examples repository, and successfully run our first "hello_usb.c"  program.

To install C/C++ SDK on Windows 11, we needed to install the following additional tools:

1. [Arm GNU Toolchain](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads)
2.  [CMake](https://cmake.org/download/)
3.  [Build Tools for Visual Studio 2022](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2022)
4.  [Python 3.10](https://www.python.org/downloads/windows/)
5.  [Git](https://git-scm.com/download/win)



1.ARM GNU Toolchain

- We downloaded the file 'arm-gnu-toolchain-12.2.MPACBTI-Bet1-mingw-w64-i686-arm-none-eabi.exe' mentioned below. 1*
- We move to the next stage while the download is being completed by clicking the next button and accepting the licensing agreement. 2*
- The next step is to set the path and select a few more permissions in the checklists to configure the environment for ARM GNU. 3*
-  Now installation of ARM GNU Toolchain is done.

2. CMake

- We downloaded the file '[cmake-3.24.2-windows-x86_64.msi](https://github.com/Kitware/CMake/releases/download/v3.24.2/cmake-3.24.2-windows-x86_64.msi)' mentioned below. 1*
- Next, after accepting the licensing agreement we moved forwarded to path setting as shown below. 2*
- After that this the installation process occurred smoothly. 3*

4. Build Tools for Visual Studio 2022

- In next step of our process, We downloaded the file "[Build Tools for Visual Studio 2022](https://aka.ms/vs/17/release/vs_BuildTools.exe)" mentioned below. 1*
- Following the download, we choose the modules to be installed, as seen below. We selected to install Windows 11 SDK because we use Windows 11 Operating systems. 2*
- After this the installation procedure was completed. 

6. Python 3.10

- In next step, We downloaded the file [Latest Python 3 Release - Python 3.10.7](https://www.python.org/downloads/release/python-3107/) 1*
- Following after downloading this file while installing it we chose "Add to Path" option. Because Adding Python to PATH makes it possible for you to run (use) Python from your command prompt (also known as command-line or cmd). 2* 

8. Git
- To follow the last step in Toolchain installation, We downloaded Git named as [64-bit Git for Windows Setup](https://github.com/git-for-windows/git/releases/download/v2.38.0.windows.1/Git-2.38.0-64-bit.exe). for our 64-bit PC. *1
- Following the download, we chose a few checklists depending on our preferences. *2
- And in the next step we chose, Notepad as Git's default editor. *3
- Following the preceding step, we enabled Git to be used from the command line as well as third-party software. *4
- Next, We selected the check box "Checkout as is, commit as-is" stating how Git would treat line endings in the text files. *5
- Here, We selected the terminal emulator we want to use with Git Bash. *6
- Lastly, we enabled experimental support for pseudo consoles. * 7

The Toolchain installation was finally done.


9.2.2. Getting the SDK and examples
After that we executed the below commands in the command line. *Command_1

Then, from the Windows menu, we launched the Developer Command Prompt window by selecting Windows > Visual Studio 2022 > Developer Command Prompt for VS 2023 and and set the path as below. *2

Before proceeding, we closed our current Command Prompt window and opened a second Developer Command Prompt session where this environment variable will now be appropriately configured.

To construct the target, we proceeded to the pico-examples folder and generated the 'Hello World' example, as seen below. This generated elf, bin, and uf2 targets, which we can see within the build directory in the hello world/serial and hello world/usb directories. The UF2 binaries may be dragged and dropped straight onto an RP2040 board connected via USB to your PC. *3


 to build the target. This will produce elf, bin  and uf2 targets, you can find these in the hello_world/serial and
hello_world/usb directories inside your build directory. The UF2 binaries can be dragged-and-dropped directly onto a
RP2040 board attached to your computer using USB*3
 
 
