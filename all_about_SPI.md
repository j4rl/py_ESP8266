# SPI 
The Serial Peripheral Interface (SPI) is a synchronous serial communication interface that is commonly used to communicate with external devices, such as sensors, displays, and memory chips. The SPI interface consists of four signal lines:
- **MISO (GPIO12)**: Master
- **MOSI (GPIO13)**: Slave
- **SCK (GPIO14)**: Clock
- **CS (GPIO15)**: Chip Select

The SPI interface is a full-duplex interface, which means that data can be sent and received at the same time. The SPI interface is also a master-slave interface, which means that one device (the master) controls the communication, while the other device (the slave) responds to the commands from the master. The SPI interface is a synchronous interface, which means that the master and slave devices must be synchronized in order to communicate with each other. The SPI interface is a high-speed interface, which means that it can transfer data at high speeds, up to several megabits per second.
## Using SPI with the Node MCU ESP8266
The Node MCU ESP8266 has built-in support for the SPI interface, which makes it easy to connect external devices to the Node MCU ESP8266 using the SPI interface. To use the SPI interface with the Node MCU ESP8266, you will need to connect the external device to the appropriate pins on the Node MCU ESP8266, and then write code to communicate with the device using the SPI protocol. The Node MCU ESP8266 has built-in support for the SPI protocol, which makes it easy to communicate with external devices using the SPI interface. The Node MCU ESP8266 also has built-in support for the I2C protocol, which is another common interface for communicating with external devices.
## Example
Here is an example of how to use the SPI interface with the Node MCU ESP8266:
```python
import machine
import time
# Define the SPI pins
spi = machine.SPI(1, baudrate=100000, polarity=0, phase=0) # SPI(1) is HSPI on ESP8266, polarity and phase are 0, baudrate is 100kHz
# Define the CS pin
cs = machine.Pin(15, machine.Pin.OUT) # GPIO15 is the CS pin
# Select the device
cs.value(0) # Select the device, CS is active low
# Read data from the device
data = spi.read(10) # Read 10 bytes of data from the device
# Write data to the device
spi.write(b'Hello, world!')
# Deselect the device
cs.value(1) # Deselect the device, CS is active low
```
## Different SPI modes
The SPI interface supports four different modes, which are defined by the polarity and phase of the clock signal. The four modes are:
- **Mode 0**: Clock is low when idle, data is sampled on the rising edge
- **Mode 1**: Clock is low when idle, data is sampled on the falling edge
- **Mode 2**: Clock is high when idle, data is sampled on the rising edge
- **Mode 3**: Clock is high when idle, data is sampled on the falling edge

The mode of the SPI interface is determined by the polarity and phase parameters when the SPI object is created. The default mode is Mode 0, which is the most common mode used in SPI communication. You can change the mode of the SPI interface by changing the polarity and phase parameters when you create the SPI object. The mode of the SPI interface must be set to match the mode used by the external device, otherwise the communication will not work correctly. How will I know which mode to use? You can find the mode in the datasheet of the external device that you are using. If the mode is not specified in the datasheet, you can try different modes until you find the one that works.
## Screen SS7735S with SPI
The SS7735S is a popular TFT display that can be connected to the Node MCU ESP8266 using the SPI interface. The SS7735S display has a resolution of 128x160 pixels, and can display up to 65,536 colors. The SS7735S display has built-in support for the SPI interface, which makes it easy to connect the display to the Node MCU ESP8266 using the SPI interface. To use the SS7735S display with the Node MCU ESP8266, you will need to connect the display to the appropriate pins on the Node MCU ESP8266, and then write code to communicate with the display using the SPI protocol. The SS7735S display has built-in support for the SPI protocol, which makes it easy to communicate with the display using the SPI interface. The SS7735S display also has built-in support for the I2C protocol, which is another common interface for communicating with external devices.
Methods to use the SS7735S display with the Node MCU ESP8266:
- **SPI**: The SS7735S display can be connected to the Node MCU ESP8266 using the SPI interface. This method is the fastest and most reliable way to communicate with the display, but it requires more pins on the Node MCU ESP8266.
- **I2C**: The SS7735S display can be connected to the Node MCU ESP8266 using the I2C interface. This method is slower than the SPI interface, but it requires fewer pins on the Node MCU ESP8266.
- **OneWire**: The SS7735S display can be connected to the Node MCU ESP8266 using the OneWire protocol. This method is the slowest and least reliable way to communicate with the display, but it requires only one pin on the Node MCU ESP8266.

Example of using the SS7735S display with the Node MCU ESP8266 using the SPI interface:
```python
import machine
import ssd1331  # Import the ssd1331 library, which is compatible with the SS7735S display (I hope)
# Define the SPI pins
spi = machine.SPI(1, baudrate=1000000, polarity=0, phase=0) # SPI(1) is HSPI on ESP8266, polarity and phase are 0, baudrate is 1MHz
# Define the CS pin, CS is active low (CS: Chip Select)
cs = machine.Pin(15, machine.Pin.OUT) # GPIO15 is the CS pin
# Define the DC pin (DC: Data/Command)
dc = machine.Pin(2, machine.Pin.OUT) # GPIO2 is the DC pin
# Define the RST pin (RST: Reset)
rst = machine.Pin(0, machine.Pin.OUT) # GPIO0 is the RST pin
# Create the display object
display = ssd1331.SSD1331(spi, cs, dc, rst)
# Clear the display
display.fill(0)
# Draw a rectangle
display.rect(10, 10, 50, 50, 0xFFFF)
# Draw a line
display.line(10, 10, 50, 50, 0xFFFF)
# Draw a circle
display.circle(50, 50, 20, 0xFFFF)
# Update the display
display.show()
```
## To use the temperature sensor BMP180 with SPI
The BMP180 is a popular temperature sensor that can be connected to the Node MCU ESP8266 using the SPI interface. The BMP180 sensor has built-in support for the SPI interface, which makes it easy to connect the sensor to the Node MCU ESP8266 using the SPI interface. To use the BMP180 sensor with the Node MCU ESP8266, you will need to connect the sensor to the appropriate pins on the Node MCU ESP8266, and then write code to communicate with the sensor using the SPI protocol. The BMP180 sensor has built-in support for the SPI protocol, which makes it easy to communicate with the sensor using the SPI interface. The BMP180 sensor also has built-in support for the I2C protocol, which is another common interface for communicating with external devices.

Example of using the BMP180 sensor with the Node MCU ESP8266 using the SPI interface:
```python
import machine
import bmp180  # Import the bmp180 library
# Define the SPI pins
spi = machine.SPI(1, baudrate=100000, polarity=0, phase=0) # SPI(1) is HSPI on ESP8266, polarity and phase are 0, baudrate is 100kHz
# Define the CS pin
cs = machine.Pin(15, machine.Pin.OUT) # GPIO15 is the CS pin
# Create the sensor object
sensor = bmp180.BMP180(spi, cs)
# Read the temperature
temperature = sensor.temperature() # Temperature is in degrees Celsius
# Read the pressure
pressure = sensor.pressure() # Pressure is in Pascals
print('Temperature: {} degrees Celsius'.format(temperature))
print('Pressure: {} Pascals'.format(pressure))
# convert to mmHg
pressure_mmHg = pressure / 133.322
print('Pressure: {} mmHg'.format(pressure_mmHg))
```
## Conclusion
The SPI interface is a powerful and versatile interface that can be used to communicate with a wide variety of external devices. The Node MCU ESP8266 has built-in support for the SPI interface, which makes it easy to connect external devices to the Node MCU ESP8266 using the SPI interface. By using the SPI interface, you can communicate with external devices at high speeds, and transfer data between the Node MCU ESP8266 and the external devices with ease. The SPI interface is a popular choice for IoT projects because of its high speed, reliability, and ease of use. By using the SPI interface with the Node MCU ESP8266, you can create a wide variety of IoT projects that communicate with external devices using the SPI protocol.


