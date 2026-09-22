# Getting started with MicroPython on the ESP8266

This is the best place to begin if you are new to the ESP8266.

## Why use the ESP8266?

The ESP8266 is a low-cost Wi-Fi microcontroller that is popular for small IoT projects, sensors, automation, and learning electronics. It is cheap, easy to find, and works well with MicroPython.

You can use the ESP8266 to:

- Blink LEDs
- Read button and sensor input
- Control relays or motors
- Connect to Wi-Fi
- Communicate with other devices over SPI, I2C, and UART

## What you need

Before you start, make sure you have:

- An ESP8266 board
- A USB cable
- A computer with a USB port
- A way to upload files to the board
- A basic breadboard and jumper wires

## What is MicroPython?

MicroPython is a compact version of Python designed for microcontrollers. It gives you a Python-like programming experience, but it runs on tiny hardware with limited memory and processing power.

The ESP8266 can be programmed in several languages, but in this project we focus on MicroPython.

## Step 1: Install the firmware

To run MicroPython on the ESP8266, the board must first have the MicroPython firmware installed.

The typical process is:

1. Download the correct ESP8266 firmware from the MicroPython website
2. Connect the ESP8266 to your computer using USB
3. Put the board into flash mode if needed
4. Use a tool such as esptool.py to flash the firmware

This step is important because without the firmware the board will not run MicroPython code.

## Step 2: Connect to the board

After flashing, you can connect to the board using a serial terminal or an editor with a serial console. This lets you:

- See printed output from your scripts
- Debug errors
- Read sensor values
- Test code interactively

## Step 3: Upload and run a script

Once the board is running MicroPython, you can upload a Python file and run it.

A simple first test is to blink an LED:

```python
import machine
import time

led = machine.Pin(2, machine.Pin.OUT)

while True:
    led.value(1)
    time.sleep(0.5)
    led.value(0)
    time.sleep(0.5)
```

This is a great beginner test because it confirms that:

- The ESP8266 is running
- The board is connected properly
- The code is being uploaded successfully

## Step 4: Learn the basics of electronics

To work with ESP8266 projects, it helps to understand a few basic concepts:

- Voltage
- Current
- Resistance
- Ground
- GPIO pins
- Pull-up and pull-down resistors

You do not need to be an expert right away. A basic understanding is enough to begin with simple circuits.

## Step 5: Learn the most common protocols

The ESP8266 can work with different communication protocols, including:

- GPIO
- SPI
- I2C
- UART

SPI and I2C are especially important when connecting sensors and modules to the board.

## Good beginner habits

- Start with one small circuit at a time
- Test one sensor or component at a time
- Use a resistor with LEDs
- Check pin numbers carefully
- Read the datasheet for external devices
- Keep the circuit simple before adding complexity

## Recommended reading order

If you want to learn in a logical order, read these documents next:

- [About the Node MCU ESP8266](about_node-mcu.md)
- [All about SPI](all_about_SPI.md)
- [Fun with electronics](electronics.md)

## Final reminder

The best way to learn the ESP8266 is by building small projects and testing them step by step. The board is friendly to beginners, but you should always double-check wiring and pin numbers before power-up.

---

Next: [About the Node MCU ESP8266](about_node-mcu.md).
