# Setting Up the Sonata Board & Development Environment on Windows 11
This is how I set-up my Sonata board. It's always being updated, so your experience may vary slightly. There were several changes between bitfile V0.2 and V1.0 - it possible that sort of thing could happen again.
This setup is using V1.1

# Pre-requistes
As metioned in the main instructions, please install the following packages before you start:
* [Visual Studio Code](https://apps.microsoft.com/detail/XP9KHM4BK9FZ7Q?hl=en-GB&gl=GB&ocid=pdpshare)
* [Windows Subsystem for Linux](https://learn.microsoft.com/en-us/windows/wsl/install)
* [Docker Desktop](https://docs.docker.com/desktop/setup/install/windows-install/)

# Updating the Sonata
Adapted from [these instructions](https://lowrisc.github.io/sonata-system/doc/guide/updating-system.html).
* DO NOT plug your Sonata board in until told to do so.
* Update the RP2040 with the latest firmware
  * Go [here](https://github.com/lowRISC/sonata-system/releases) and download your latest version (I used V1.1). The instructions here are really good so read them and you should be fine & you can skip the rest of this section.
  * The files I downloaded were:
    * `rpi_rp2_v1.1.uf2`
    * `snake_demo_v1.1.slot2.uf2`
    * `sonata-v1.1.bit.slot1.uf2`
    * `sonata-v1.1.bit.slot2.uf2`
    * `sonata-v1.1.bit.slot3.uf2`
    * `sonata_simple_demo_v1.1.slot1.uf2`
  * Take you Sonata Board and make sure the `bitstream` switch (also labelled `sw3` is set to `1`).
  * Also make sure the `SW App` switch (also labelled `sw7` is set to `1`).
  * Make sure you USB cable is not plugged into a PC yet.
  * Plug one end of your USB cable into your Sonata board. It's goes in theuSB C socket labelled `Main USB` (also labelled `J2`).
  * Hold down the `RP2040 Boot` button (also labelled `SW9`).
  * Whilst holding down the button, plug the other end of your USB cable into your Windows PC.
  * A drive will appear called "RPI-RP2".
  * Copy the file `rpi_rp2_v1.1.uf2` into it.
  * The drive should automatically dismount and be replaced with one called "SONATA".
* Loading a Bitfile
  * Open the "SONATA" drive.
  * Copy the file `sonata-v1.1.bit.slot1.uf2` onto the drive.
  * It should automatically load the file and reboot. The `CHERI` LED should light up and the `LEGACY` LED should turn off.
* Loading a Test App
  * Now we need something to run as a demo. Copy across the file `sonata_simple_demo_v1.1.slot1.uf2`.
* Reading the Debug Output
  * I used PuTTY to connect to the serial port but you can use any serial terminal.
  * When you plugin your Sonata board, 3 new COM Ports will be added. The best way to see this is to open Device Manager, look in the "Ports (COM & LPT)" section then plug in your Sonata board and see which new COM Ports get added. It will add 3 new COM ports, in my case, they were COM8, COM9 & COM10. I've found that the debig port is normally the middle of these 3 (COM9).
  * The Debug Port will output at 921600 baud, 8 data bits, 1 stop bit, no parity and no flow control.
  * If you press the `Reset` button on the Sonata board (also labelled `SW5`) you can watch the loading messages as they appar.

# Cloning the Repository and Building Examples
I'm going to use my fork but you could just clone the original repository. It's important that you use a recursive clone as there are submodules included.
* Open your WSL install (I used Ubuntu)
* In WSL, browse to where you want the code to go (I have a subfolder called "github" in my home folder.
* Do a recursive clone from your fork of the repo. For me it looks like this:
```
git clone --recurse https://github.com/DjangoClouds/cheriot-rtos
```
* If you don't have your own fork then clone the roiginal repo instead:
```
git clone --recurse https://github.com/CHERIoT-Platform/cheriot-rtos
```
* Wait for it to finish cloning.
* Before going further, make sure that Docker Desktop is running.
* Now we need to open VSCode using this repo. The easiest way is to launch it from the WSL terminal:
```
cd cheriot-rtos
code .
```
* VSCode should open and it will ask if you want to repoen the project in the container. You want to do this.
* Reopening in the container can take 5 minutes, depending on your computer.
* Once the project is opened in the container, we will be using the Terminal in VSCode to build, since that is in the container. The WSL instance is not open in the container, so we don't need it now.

# Building the Code Examples
I already have my serial port open.
* Having opened the repo in VSCode and in the container, we can build from the terminal is VSCode. If you can't see the terminal, turn it on from the View Menu.
* In the terminal window, we want to change directory to the specific example. For this example, I will build the first example.
```
cd examples/01.hello_world/
```
* Now we have 3 commands that we will issue:
  * The first command (`xmake config --sdk=/cheriot-tools --board=sonata-1.1`) sets the build environment. Here I am specifically targetting V1.1 (you can use `--board=sonata` if you want to use the deafult). This command only needs running the once after cloning or pulling the repo or if you wish to build on another target. It doesn't hurt to run it multiple times though.
  * The second command (`xmake`) actually builds the code and produces the `bin` file.
  * The final command (`xmake run`) converts the `bin` file into the `firmware.uf2` file that can be copied into the `SONATA` drive that appears when we plug the Sonata board into our PC. The `uf2` file can be found in the subfolder `build\cheeriot\cheeriot\release`, after running `xamke run`.
```
* These are the command in full:
xmake config --sdk=/cheriot-tools --board=sonata-1.1
xmake
xmake run
```
* Now copy the `firmware.uf2` file into the SONATA drive. The Sonata should reboot and you can follow the progress on the serial terminal.

  # HELP! I Copied firmware.uf2 onto SONATA and Nothing Happened
  * You've probably got a mismatch between the bitfile (in our case V1.1) and the frimware that you built for (notice how I explictly specified V1.1). Go back through these instructions and double check what you've done.
