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

If you want to get fancy, this will enable printf to uart2 (with conversion of \n into \r\n) 
in main.c, add this at USER CODE BEGIN 4

    /* USER CODE BEGIN 4 */

    // This maps normal print output to the serial tx/rx (in this case, uart2)
    int __io_putchar(int ch) {
        // Code to write character 'ch' on the UART
      switch (ch)
      {
        case '\n' : { HAL_UART_Transmit(&huart2, (uint8_t*)"\r\n", 2 , 1000); break;	};			// cr/lf translation
        default:  {HAL_UART_Transmit(&huart2, (uint8_t*)&ch, 1 , 1000); break; 	};
      }

      return 1;
    }

    int __io_getchar(void) {
        // Code to read a character from the UART
      return 1;
    }


    /* USER CODE END 4 */

# EXAMPLE
The example in the example directory is generated from this ioc, with some additional simple tools added
* The printf is directed to uart2.  scanf is NOT directed to uart2, but could be.
* A very simple task scheduler is connected, and demonstrates doing very simple tasks on a time base.  Doing printf from these tasks "it a really bad idea" - it's occuring in the system tick interrupt context. This is only to demonstrated that the tasks are executing.
