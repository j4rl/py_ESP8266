# All about SPI

SPI stands for Serial Peripheral Interface. It is a common way for microcontrollers to communicate with sensors, displays, memory chips, and other modules.

## What SPI is

SPI is a synchronous serial protocol. That means that the devices share a clock signal so they can transfer data in a controlled way.

The SPI bus usually has four main signals:

- MOSI: Master Out, Slave In
- MISO: Master In, Slave Out
- SCK: Clock
- CS: Chip Select

The master device controls the communication, and the slave device responds to the commands it receives.

## Typical SPI pins on the ESP8266

On the ESP8266, SPI is commonly used with pins such as:

- MOSI = GPIO13
- MISO = GPIO12
- SCK = GPIO14
- CS = GPIO15

The exact pins can vary depending on the board and the library you are using, so always check the documentation for your specific setup.

## Why SPI is useful

SPI is useful because it is:

- Fast
- Simple to understand at a basic level
- Common in sensors and displays
- Full-duplex, which means data can move in both directions at the same time

## SPI modes

SPI has four common modes, defined by clock polarity and phase:

- Mode 0: clock idle low, data sampled on rising edge
- Mode 1: clock idle low, data sampled on falling edge
- Mode 2: clock idle high, data sampled on rising edge
- Mode 3: clock idle high, data sampled on falling edge

The mode must match the device you are talking to. If the wrong mode is used, the communication will often fail in a confusing way.

The easiest rule is:

- Check the sensor or module datasheet
- Set the SPI mode to match the device
- Test with a simple read or write command

## A basic SPI example

This example shows the general idea of SPI communication on the ESP8266:

```python
import machine

spi = machine.SPI(1, baudrate=100000, polarity=0, phase=0)
cs = machine.Pin(15, machine.Pin.OUT)

cs.value(0)
spi.write(b'Hello from ESP8266!')
cs.value(1)
```

This code does not read any data back, but it shows the essential flow:

1. Create the SPI object
2. Select the slave device with CS
3. Send data
4. Deselect the device

## Important beginner note

SPI devices often need a chip-select pin for each connected module. If you connect multiple devices to the same SPI bus, each device usually gets its own CS line.

## How to choose the correct pins

When using an SPI module, check the datasheet for these values:

- Which pin is MOSI
- Which pin is MISO
- Which pin is SCK
- Which pin is CS
- Which SPI mode is required
- What voltage the module expects

This is the most important step when debugging a device that does not respond.

## Example of a common pattern

```python
import machine

spi = machine.SPI(1, baudrate=1000000, polarity=0, phase=0)
cs = machine.Pin(15, machine.Pin.OUT)

# select device
cs.value(0)

# send a byte
spi.write(b'\x01')

# read a response
response = spi.read(4)
print(response)

# deselect device
cs.value(1)
```

## Beginner tips

- Use short jumper wires for SPI signals
- Keep wiring neat and consistent
- Make sure ground is connected between devices
- Check whether your device is 3.3V or 5V tolerant
- If nothing works, verify the clock mode and chip select pin first

## Summary

SPI is one of the most useful interfaces on the ESP8266. It is fast and widely supported, but it is also easy to misconfigure. The key to success is matching the proper pins and mode to the specific device you are using.

---

The next document covers practical electronics and beginner circuits: [electronics.md](electronics.md).
