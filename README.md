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


///3.2
# Why is bit-banging impractical on your laptop, despite it having a much faster processor than the RP2040?
Because PIO state machines allow for repeated readings and writes from GPIOs. Furthermore, it performs data transfer operations 
more efficiently than "Bit-Bangling."


# What are some cases where directly using the GPIO might be a better choice than using the PIO hardware? 
We can use Bit-Bangling in tasks that require slower protocols. We can use IRQ-based bit banging on simpler embedded systems. LEDs and push buttons are the most common applications for software GPIO access.

# How do you get data into a PIO state machine?
The OSR serves as a holding place for data entering the state machine through the TX FIFO. Data is loaded into the OSR one 32-bit 
chunk at a time from the TX FIFO. When an out instruction is issued, the OSR can divide the data into smaller chunks by shifting to 
the left or right and sending the bits that fall off the end to one of a few potential destinations, such as the pins.


# How do you get data out of a PIO state machine? 
GPIO mapping logic enables each state machine to see and manipulate up to 30 GPIOs. Here, we must define the GPIO Pins and PIO 
instances that will be synchronized for data to exit the PIO state machine.

# In the example, which low-level C SDK function is directly responsible for telling the PIO to set the LED to a new color? 
put_pixel() helper method above to output a sequence of pixel values while setting LED to a new color value.

# How is this function accessed from the main “application” code?
The PIO file we just looked at, WS2812.pio, is automatically turned (we'll learn how later) into a header containing our built 
PIO program binary, any assistance functions we put in the file, and other valuable program information. This is coded as 
WS2812.pio.h.

# What role does the pioasm “assembler” play in the example, and how does this interact with CMake?
Our.pio file's assembly program is converted into a binary program. Assembler programs are those that handle the task of 
converting assembly code into binary. A CMake file explains how to compile them into a binary that can be loaded into your 
Raspberry Pi Pico or other RP2040-based board. The CMake function pico generate pio header(TARGET PIO FILE) handles executing 
pioasm and putting the resulting header to the target TARGET's inclusion path. 






///3.3 WS2812.pio's annotations
![ ](https://github.com/unlim-int-soumya/Lab-2A/blob/main/PIO/Untitled_1.png)
<br>
![ ](https://github.com/unlim-int-soumya/Lab-2A/blob/main/PIO/Untitled_2.png)
<br>
![ ](https://github.com/unlim-int-soumya/Lab-2A/blob/main/PIO/Untitled_3.png)
<br>
![ ](https://github.com/unlim-int-soumya/Lab-2A/blob/main/PIO/Untitled_4.png)
<br>
![ ](https://github.com/unlim-int-soumya/Lab-2A/blob/main/PIO/Untitled_5.png)


//3.3 .WS2812.c File anotation
![ ](https://github.com/unlim-int-soumya/Lab-2A/blob/main/C/Untitled_1.png)
<br>
![ ](https://github.com/unlim-int-soumya/Lab-2A/blob/main/C/Untitled_2.png)
<br>
![ ](https://github.com/unlim-int-soumya/Lab-2A/blob/main/C/Untitled_3.png)
<br>
![ ](https://github.com/unlim-int-soumya/Lab-2A/blob/main/C/Untitled_4.png)
<br>
![ ](https://github.com/unlim-int-soumya/Lab-2A/blob/main/C/Untitled_5.png)


/////3.4
[This](https://github.com/unlim-int-soumya/Lab-2A/blob/main/3.4%20Spreadsheet%201.xlsx) is the link of the spreadsheet that I have prepared for this portion of the answer
# Which PIO instance is being used? Which state machine is being used with this PIO instance?
In this code, 0 instace of PIO and 0 instance of State machine were used.

# Which pin is this state machine configured to control? (you can either use settings from the example program, or for the Qt Py LED pin yours will be connected to)
Here WS2812_PIN was used by state machine to control.

# How long is the state machine's clock cycle? How much is this state machine’s clock scaled down relative to the system clock? 
State machines clock cycle is 48MHz. The clock divider can be configured to slow down the execution of the state machine: a clock divisor of n indicates that one 
instruction is performed every n system clock cycles. SDK's system clock frequency is set at 125MHz by default.

# In which direction will this state machine shift bits out of its “output shift register”?
Output Shift Register receives the input from the TX FIFO register bit-wise and shifts the output to the other output pins using OUT
command.

# What basic circuitry does a WS2812 LED need to operate?
Green, Red, and Blue are represented by three cascaded blocks on the WS2812. Each block has I/O ports such as (Power supply LED), Vdd, Gnd, Data output (DOUT), Data input (DIN), Power supply Control circuit (VCC), and Ground (VSS). Data bits indicating RGB brightness are serially sent into the Din pin, after which the chip strips out the first 24 bits (8 bits for R,G,B) and sends the remaining bits out the Dout pin. By connecting the LEDs in a string, with the Dout from one LED flowing to the Din of the next LED, each LED strips off the bits it requires from the front of the data stream and transmits the remainder of 
the data stream to the next LED. The number of LEDs you can drive with a single data line is theoretically unlimited; the only constraint is that the time it takes 
to update all the LEDs in the string rises linearly with the number of LEDs in the string. This results in a highly creative and 
effective method of addressing unique RGB data to any number of LEDs linked in a string.



//3.5
# How do you connect a WS2812 to a microcontroller?
WS2812 is connected to Microcontroller by Connecting with PCB Board with soldering.

# How does a WS2812 translate bits to color values?
When serial data is supplied to the LED's input, it takes the first three bytes (red, green, blue) and passes the remainder to its 
serial data output. These LEDs are frequently connected in a single continuous chain, with each LED connected to a common power 
source and its data output connected to the next LED's input.

# How do you send a single 1 or 0 bit to the WS2812?
WS2812 line format. Here, Wide positive pulse is used for 1 and narrow positive pulse for 0.

# How many bits does it take to send a single color value?
In WS2812, each color is represented by 24 bits of data.

# What happens if you send more bits than this in a packet? When we try to send more than one bits than this in a packet, the packet is divided into multiple packets and sent. How do you tell a WS2812 you’re done sending data?
To fill the vacuum, the out instruction pushes data out of the OSR and zeroes in from the other end. Because the OSR is 32 bits wide, you will begin to see zeroes after shifting out a total of 32 bits. A pull instruction explicitly removes data from the TX FIFO and places it in the OSR (stalling the state machine if the FIFO is empty).

# How do you send data to more than one WS2812 in a chain?
We are using TX FIFO registers for sending data more than one WS2812 in a chain. The data that we are moving out of the OSR comes from the state machine's TX FIFO, which is more extensively documented in the RP2040 Datasheet. The TX FIFO is a data buffer between the state machine and the rest of the RP2040 that may be filled 
either directly from the CPU or through system DMA, which is substantially quicker.
