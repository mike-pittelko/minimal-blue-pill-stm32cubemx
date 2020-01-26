# minimal-blue-pill-stm32cubemx

What you get:
This configuration 
* sets up the default clock for 72Mhz
* UART2 (!!) for 115200 baud, N,8,1 with TX on PA2, and RX on PA3.
* Heartbeat LED on PC13 (called LEDHB)
* Single Wire Debug mode

HOWTO:

Install STM32CubeIDE, STM32CubeMX, and STM32CubePrg

Download this .ioc file, load it with STM32CubeMX.

On the "Project Manager" page, set the project name, the project location.

Save the "project".  Then click the big "Generate" button on the top right of the CubeMX window.

You will be prompted to open the project in STM32CubeIDE, do so, you should be able to build the program, then program your blue pill.  It won't look like anything is happening, but it's running and properly configured to get you going.

