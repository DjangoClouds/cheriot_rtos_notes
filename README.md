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
* Connect the Sonata Board and makes ure that it's running the correct bitfile. We ran with V1.1, which works with the version of CHERIoT RTOS that we are currently using.
  * Connecting to the serial port

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
