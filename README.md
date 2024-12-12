# Python for the ESP8266
This repository contains a collection of Python scripts that can be run on the ESP8266. The scripts are written in MicroPython, which is a lean and efficient implementation of Python 3 that includes a small subset of the Python standard library. The scripts are intended to be run on the ESP8266 microcontroller, which is a low-cost Wi-Fi microcontroller with a full TCP/IP stack and a microcontroller unit (MCU) based on the Node MCU architecture.
- [About the Node MCU ESP8266](about_node-mcu.md)
- [All about SPI](all_about_SPI.md)
- [Fun with electronics](electronics.md)
- [Getting started with MicroPython](getting_started.md)

## Which editor to use?
The scripts can be written and run on any text editor that supports MicroPython. Some popular editors that support MicroPython include:
- Thonny
- Mu
- Visual Studio Code
- PyCharm
- Arduino IDE
Personally i like to use Mu Editor with my Node MCU ESP8266. It is a simple editor that is easy to use and has a built-in serial console for debugging. It also has a built-in file manager that allows you to upload files to the ESP8266. You may use any editor of your choice.
## Getting started
To get started with MicroPython on the ESP8266, you will need to install the MicroPython firmware on the ESP8266. You can download the firmware from the MicroPython website and flash it onto the ESP8266 using a tool like esptool.py. Once you have flashed the firmware onto the ESP8266, you can connect to the ESP8266 using a serial terminal and start running Python scripts on it.
## MicroPython website
You can find more information about MicroPython on the MicroPython website: [https://micropython.org/](https://micropython.org/)
On that website you can find the firmware for the ESP8266 and other microcontrollers, as well as documentation and tutorials on how to get started with MicroPython.
## Electronics components and tools
To run the scripts in this repository, you will need som electronic components other than the ESP8266. 
**Here is a list of components that you may need:**
- Breadboard
- Jumper wires
- LEDs
- Resistors
- Push buttons
- Various sensors (e.g. temperature sensor, light sensor, motion sensor)
- any SPI or I2C devices

**Tools that you may need:**
- Soldering iron
- Multimeter (optional)
- Oscilloscope (optional, pro users)
- Cutters, wire strippers, pliers, tweezers, etc.
- Coffee (optional)

**Bare minimum components that you will need to run the scripts in this repository are:**
- ESP8266 and a USB cable
- Computer with a USB port
