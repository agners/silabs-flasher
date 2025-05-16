> [!NOTE]  
> This project is dormant, please use the much more capable utilty called [Universal Silicon Labs
Flasher](https://github.com/NabuCasa/universal-silabs-flasher).


# Silicon Labs Firmware flashing utility

The `silabs-flasher` utility allows to flash products using the Silicon Labs
Wireless Gecko Series 1 and 2 chips. It makes use of the zigpy bellows library 
to communicate using the EmberZNet Serial Protocol over serial port.

## Install

Silicon Labs Flasher is available from PyPI:
```
$ pip install silabs-flasher
```

To use GPIOs to reset the chip (useful on Home Assistant Yellow) make sure to
install with gpiod from PyPI as extra dependency:
```
$ pip install "silabs-flasher[gpio]"
```

## Usage

Use the info command to check communication with the device and get
information about the current firmware and the bootloader:
```
$ silabs-flasher --device /dev/ttyUSB4 info
Manufacturer: 
Board name: 
EmberZNet version: 6.7.9.0 build 405
bootloader version: 0x1902, nodePlat: 0x04, nodeMicro: 0x18, nodePhy: 0x0f
```

The firmware can be flashed using the `flash` command:
```
$ silabs-flasher --device /dev/ttyUSB4 flash --firmware ncp-uart-sw_679_115200.gbl 
Trying to connect using EZSP...
Launching bootloader in mode recovery mode via EZSP.
Bootloader detected successfully.
Bootloader version: 1.9.2
Starting firmware upload...
Firmware update  [####################################]  100%          
Bootloader reported successful upload.
```

To reset the chip using GPIO use the following arguments:
```
$ silabs-flasher --device /dev/ttyAMA1 --baudrate 115200 flash \
                 --no-ezsp-reset --cm4-gpio-reset \
                 --firmware NabuCasa_EZSP_v6.10.3.0_PA32_ncp-uart-hw_115200.gbl
```
