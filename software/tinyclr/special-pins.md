# Special Pins
---

There are five pins that have special functionality. They are also predefined on the SITCore line of products: 
* RESET (NRST)
* LDR (PE3)
* APP (PB7)
* MOD (PD7)
* WKUP (PA0)

All special pins except RESET can be used as GPIO or peripheral pins, however it is up to you to make sure your use of these pins does not interfere with their use as special pins if needed. We strongly recommend exposing all special pins in your SITCore designs.

## RESET

The SITCore chip is held in reset while the reset pin is low. Releasing RESET and allowing it to go high will begin the system startup process. When designing your own circuit board, the RESET pin must be pulled high for the processor to start running. On our SITCore Modules and Dev Boards we pull RESET high through a 10K resistor, allowing RESET to be pulled low by the RESET button. When using the SITCore chipsets, you will have to pull RESET high yourself.

## LDR

The LDR pin is used to enter the GHI Electronics bootloader mode. The LDR pin is normally pulled high during startup or reset, allowing the managed application to execute. When the LDR pin is pulled low during startup or reset, the device enters GHI Electronics bootloader mode, which is used to load the SITCore firmware. There is no need for a pull up resistor on the LDR pin as the LDR pin is pulled high through a pull up resistor internal to the processor.

## APP

The APP pin is used to prevent the application from running. The APP pin is checked shortly after startup and reset. When the APP pin is high your application will run normally. If the APP pin is low when the bootloader is finished, the bootloader will not transfer execution to your application. There is no need for an external pull up on the APP pin as it is pulled high by an internal pull up.

## MOD

The MOD pin is used to select the debugging/deployment interface. The MOD pin is pulled high by an internal pull up resistor -- there is no need to add a pull up resistor to the MOD pin when designing a custom circuit board.

By default, the MOD pin is pulled high during reset allowing for deployment and debugging over USB. Pulling the MOD pin low during startup or reset allows for deployment and debugging over UART. Note that our SITCore Dev Boards include a FT232R USB to serial converter chip to provide a convenient way to connect a PC to the board's serial debug/deploy port.

## WKUP

The WKUP pin can be used to wake up the processor from special power saving modes. The WKUP pin can be configured to use an internal pull-up or pull-down, so no external pull resistor is needed. When WKUP functionality is not needed, this pin can be used as a GPIO or peripheral pin. See the [Power Management](../../software/tinyclr/tutorials/power-management.md) page for more information.

## Debug Interface

Don't forget to expose either the USB client or UART interface (or both) that you plan on using to deploy and debug your application code. All SITCore products built around a 100 pin chip (SC20100x) use UART1 for the serial debug interface. All SITCore products built around the 260 pin SC20260B chip use UART5 for the serial debug interface.

## Other Recommended Pin Usage

When designing your own board, we recommend that you add the following peripherals using the stated pins to maintain consistency with our dev boards and sample software.

| Peripheral | Recommended SITCore I/O Assignment |
|--|--|
| User LED | 100 pin devices: PE11 |
|  | 260 pin devices: PB0 |
| Buzzer | PB1 |
|  |  |
| SPI Display | SPI = SPI4 |
|  | BL = PA15 |
|  | CS = PD10 |
|  | RS = PC4 |
|  | RST = PE15 |
|  |  |
| Parallel Display | Backlight = PA15 |
|  | Touch I2C = I2C1 |
|  | Touch IRQ = PJ14 |
|  |  |
| WiFi | SPI = SPI3 |
|  | IRQ = PA10 |
|  | CS = PD15 |
|  | EN = PA8 |
|  | RST = PA9 |

