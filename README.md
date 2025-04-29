# CHERIoT RTOS Notes

These are just my notes on installing and using CHERIoT RTOS on the [Sonata development board](https://lowrisc.github.io/sonata-system/) and building the code under Windows.

## General Notes
I'm not going to answer all these questions - instead I'll just link to places that explain it all.
* What is [CHERI](https://en.wikipedia.org/wiki/Capability_Hardware_Enhanced_RISC_Instructions)?
* What is [CHERI in more detail](https://www.cl.cam.ac.uk/research/security/ctsrd/cheri/)?
* What is the [CHERIoT Platform](https://github.com/CHERIoT-Platform)?
* What is [CHERIoT RTOS](https://github.com/CHERIoT-Platform/cheriot-rtos)?
* [Why did they write a new RTOS for CHERIoT?](https://cheriot.org/rtos/philosophy/history/2024/10/24/why-new-rtos.html)
* What is the [Sonata Development Platform](https://lowrisc.github.io/sonata-system/)?
* Where can a get a [Sonata board](https://www.mouser.co.uk/ProductDetail/NewAE/NAE-SONATA-ONE?qs=wT7LY0lnAe1k3dLvmL42Eg%3D%3D)?

## Setting Up The Building Platform on Windows 11
### Before You Start
* Make sure that you have installed:
  * [Visual Studio Code](https://apps.microsoft.com/detail/XP9KHM4BK9FZ7Q?hl=en-GB&gl=GB&ocid=pdpshare)
  * [Windows Subsystem for Linux](https://learn.microsoft.com/en-us/windows/wsl/install)
  * [Docker Desktop](https://docs.docker.com/desktop/setup/install/windows-install/)
* Update the Sonata and Run Some Firmware
  * In the examples below they will suggest cloning the [CHERIoT RTOS](https://github.com/CHERIoT-Platform/cheriot-rtos) but you will likely write something that can be used as an example and you may want to commit back so I would suggest forking the repo and working from that. [My fork](https://github.com/DjangoClouds/cheriot-rtos) is where I'm workong on finishing the CAN driver conversion that I started as an [open source project in a previous job](https://github.com/GrassHopper1977/cheriot-rtos-sonata-hardware/) (& I now work on just for fun).
  * [Update the Sonata Firmware and bit file](https://lowrisc.github.io/sonata-system/doc/guide/updating-system.html) We ran with V1.1, which works with the version of CHERIoT RTOS that we are currently using.
  * [From zero to CHERIoT in two minutes with Sonata](https://cheriot.org/fpga/ibex/2024/06/10/sonata-quick-start.html) This is a little out of date now as it was using V0.2 of the bitfile but it hasn't changed that much so it's not a bad example. The part about automatically upload the compiler code to the Sonata doesn't seem to work under Windows (there have been several attempts to get it working but, honestly, it's easy to just copy th files accross). 
  * Connecting to the serial port
 
### Building the Code
I keep forgetting the exact commands required, so here they are:
```sh
$ xmake config --sdk=/cheriot-tools --board=sonata
$ xmake
$ xmake run
```
You only need to run the first line once per project or if you've changed the project config. The `--board` can be changed to target a specific build of the hardware. The processor is an FPGA so the hardware can change, these fiels are released as the bitfiles that we loaded at the beginning. If you look in the code you find the available boards list and you will notice that sonata.json is actually a link to a json file with a specific version number specified. You can change the target board to try out code for new version of the bitfile that are not yet the default.
TODO! Add an example here.

### Checkout the Git Repo
* Make sure that Docker for Desktop is running
* Open WSL
* I created a "github" folder to put everything into
* Checkout the cheriot-rtos repo.
* Build the examples
* Copy the files across to the Sonata Board
* Watch the magic work

## FAQs
### Are There Other Example Repos?
[Yes, look here.](https://github.com/CHERIoT-Platform)

### Where Can I Ask Questions?
There's 3 places that I've found:
1. [The CHERIoT Public Chat group on Signal](https://signal.group/#CjQKIElxAs3t3MUEMOEmQEuMHRK4rErUk2xVeFzjAjFXAShzEhCK9qQwEMFKGLGZnCjrQ7zm)
2. [CHERIoT Platofrm Discussions on Github](https://github.com/orgs/CHERIoT-Platform/discussions)
3. There is a Slack channel for CHERI in general but I don't use it as most of the CHERIoT specific conversations take place on Signal.

## Are the hardware peripherals protected against from other threads?
Not yet. See [this example](https://github.com/GrassHopper1977/cheriot-rtos-sonata-hardware/tree/main/examples/15.testing). A solution is currrently under development.
