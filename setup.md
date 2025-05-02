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
  * Plug one end of your USB cable into your Sonata board. It's goes in tehuSB C socket labelled `Main USB` (also labelled `J2`).
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
  * When you plugin your Sonata board, 3 new COM Ports will be added. Teh best way to see this is to open Device Manager, look in the "Ports (COM & LPT)" section then plug in your Sonata board and see which new COM Ports get added.
  * The Debug Port will output at 921600 baud, 8 data bits, 1 stoip bit, no parity and no flow control.
  * If you press teh `Reset` button on teh Sonata board (also labelled `SW5`) you can watch teh laoding messages as they appar.

