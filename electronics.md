# Having fun with electronics
## Introduction
When coding with MicroPython and the ESP8266, you will need some electronic components to run the scripts in this repository. Here is a list of components that you may need:
- Breadboard
- Jumper wires
- LEDs
- Resistors
- Push buttons
- Various sensors (e.g. temperature sensor, light sensor, motion sensor)
- TTL or CMOS logic chips
## How the breadboard works
The breadboard is a tool that allows you to connect electronic components together without soldering. The breadboard has a grid of holes that are connected together in rows and columns. The rows are connected horizontally, while the columns are connected vertically. The breadboard also has power rails on the sides that are used to provide power to the components on the breadboard. The power rails are usually labeled with the voltage that they provide, such as 3.3V or 5V. The breadboard also has a gap in the middle that is used to separate the power rails into two sections. This gap is called the "dip" or "ditch" and is used to prevent short circuits between the power rails. The breadboard also has a set of holes in the middle that are used to connect components together. These holes are usually labeled with letters and numbers to help you keep track of which holes are connected together. The breadboard also has a set of holes on the sides that are used to connect the breadboard to other components, such as the ESP8266 or a power supply. The breadboard is a versatile tool that can be used to build a wide variety of electronic circuits, from simple LED blinkers to complex microcontroller projects.
## Simple LED blinking with five LEDs
Setting it up on a breadboard:
- Connect the ESP8266 to the breadboard
Place the ESP8266 on the breadboard so that the pins are aligned with the rows on the breadboard. Make sure that the pins are inserted into the holes on the breadboard so that they make a good connection. You can use jumper wires to connect the ESP8266 to the breadboard if the pins do not align with the rows on the breadboard.
- Connect the LEDs and resistors to the breadboard
Place the LEDs on the breadboard so that the longer leg (the anode) is connected to the positive power rail, and the shorter leg (the cathode) is connected to a resistor. Connect the other end of the resistor to a pin on the ESP8266. You can use jumper wires to connect the LEDs to the breadboard if the legs do not align with the rows on the breadboard. We use resistors to limit the current flowing through the LEDs and prevent them from burning out. The value of the resistor depends on the voltage and current rating of the LED, but a good rule of thumb is to use a 220 ohm resistor for a 3.3V power supply.
- Write the code
- Run the code (duh)
Example code:
```python
import machine
import time
# Define the pins
led1 = machine.Pin(16, machine.Pin.OUT) # GPIO16 is the internal LED on the ESP8266
led2 = machine.Pin(5, machine.Pin.OUT) # GPIO5 is the pin for the first external LED
led3 = machine.Pin(4, machine.Pin.OUT) # GPIO4 is the pin for the second external LED
led4 = machine.Pin(0, machine.Pin.OUT) # GPIO0 is the pin for the third external LED
led5 = machine.Pin(2, machine.Pin.OUT) # GPIO2 is the pin for the fourth external LED
led6 = machine.Pin(14, machine.Pin.OUT) # GPIO14 is the pin for the fifth external LED
# Blink the LEDs
while True:
    led1.value(1) # Turn the internal LED on
    led2.value(1) # Turn the first external LED on
    led3.value(1) # Turn the second external LED on
    led4.value(1) # Turn the third external LED on
    led5.value(1) # Turn the fourth external LED on
    led6.value(1) # Turn the fifth external LED on
    time.sleep(1) # Wait for 1 second
    led1.value(0) # Turn the internal LED off
    led2.value(0) # Turn the first external LED off
    led3.value(0) # Turn the second external LED off
    led4.value(0) # Turn the third external LED off
    led5.value(0) # Turn the fourth external LED off
    led6.value(0) # Turn the fifth external LED off
    time.sleep(1) # Wait for 1 second
```
Example code of using the five LEDs like a Knight Rider light, and the internal LED blinks independently:
```python
import machine
import time
# Define the pins
led1 = machine.Pin(16, machine.Pin.OUT) # GPIO16 is the internal LED on the ESP8266
led2 = machine.Pin(5, machine.Pin.OUT) # GPIO5 is the pin for the first external LED
led3 = machine.Pin(4, machine.Pin.OUT) # GPIO4 is the pin for the second external LED
led4 = machine.Pin(0, machine.Pin.OUT) # GPIO0 is the pin for the third external LED
led5 = machine.Pin(2, machine.Pin.OUT) # GPIO2 is the pin for the fourth external LED
led6 = machine.Pin(14, machine.Pin.OUT) # GPIO14 is the pin for the fifth external LED
# Blink the LEDs using a Knight Rider light pattern and putting the leds in a list to make it easier to loop through them
leds = [led2, led3, led4, led5, led6]
while True:
    led1.value(1) # Turn the internal LED on
    for led in leds:
        led.value(1) # Turn the external LEDs on
        time.sleep(0.1) # Wait for 0.1 second
        led.value(0) # Turn the external LEDs off
    time.sleep(0.1) # Wait for 0.1 second
    led1.value(0) # Turn the internal LED off
    for led in reversed(leds):
        led.value(1) # Turn the external LEDs on
        time.sleep(0.1) # Wait for 0.1 second
        led.value(0) # Turn the external LEDs off
    time.sleep(0.1) # Wait for 0.1 second
```
## Using a push button to control the LEDs
Setting it up on a breadboard:
- Connect the push button to the breadboard
Place the push button on the breadboard so that the legs are connected to two different rows on the breadboard. Connect one leg of the push button to a pin on the ESP8266, and connect the other leg to the ground rail on the breadboard. You can use jumper wires to connect the push button to the breadboard if the legs do not align with the rows on the breadboard.
- Write the code
- Run the code (duh)
Example code:
```python
import machine
import time
# Define the pins
led1 = machine.Pin(16, machine.Pin.OUT) # GPIO16 is the internal LED on the ESP8266
led2 = machine.Pin(5, machine.Pin.OUT) # GPIO5 is the pin for the first external LED
led3 = machine.Pin(4, machine.Pin.OUT) # GPIO4 is the pin for the second external LED
led4 = machine.Pin(0, machine.Pin.OUT) # GPIO0 is the pin for the third external LED
led5 = machine.Pin(2, machine.Pin.OUT) # GPIO2 is the pin for the fourth external LED
led6 = machine.Pin(14, machine.Pin.OUT) # GPIO14 is the pin for the fifth external LED
button = machine.Pin(12, machine.Pin.IN, machine.Pin.PULL_UP) # GPIO12 is the pin for the push button
# every push of the button will turn the next LED on, and turn the previous LED off while the internal led indicates button down
# Put the leds in a list to make it easier to loop through them
leds = [led2, led3, led4, led5, led6]
i = 0
while True:
    led1.value(button.value()) # Turn the internal LED on when the button is pressed
    if not button.value(): # Check if the button is pressed
        leds[i].value(1) # Turn the current LED on
        time.sleep(0.5) # Wait for 0.5 seconds
        leds[i].value(0) # Turn the current LED off
        i = (i + 1) % len(leds) # Increment the index and wrap around
        while not button.value(): # Wait for the button to be released
            pass
```
## Using a potentiometer to control how many LEDs are on
Setting it up on a breadboard:
- Connect the potentiometer to the breadboard
Place the potentiometer on the breadboard so that the legs are connected to three different rows on the breadboard. Connect one leg of the potentiometer to the positive power rail on the breadboard, and connect the other leg to the ground rail on the breadboard. Connect the middle leg of the potentiometer to a pin on the ESP8266. You can use jumper wires to connect the potentiometer to the breadboard if the legs do not align with the rows on the breadboard.
- Write the code
- Run the code (duh)
Example code:
```python
import machine
import time
# Define the pins
led1 = machine.Pin(16, machine.Pin.OUT) # GPIO16 is the internal LED on the ESP8266
led2 = machine.Pin(5, machine.Pin.OUT) # GPIO5 is the pin for the first external LED    
led3 = machine.Pin(4, machine.Pin.OUT) # GPIO4 is the pin for the second external LED
led4 = machine.Pin(0, machine.Pin.OUT) # GPIO0 is the pin for the third external LED
led5 = machine.Pin(2, machine.Pin.OUT) # GPIO2 is the pin for the fourth external LED
led6 = machine.Pin(14, machine.Pin.OUT) # GPIO14 is the pin for the fifth external LED
pot = machine.ADC(0) # ADC(0) is the pin for the potentiometer
# Read the value of the potentiometer and turn on the corresponding number of LEDs
while True:
    value = pot.read() # Read the value of the potentiometer
    leds = [led1, led2, led3, led4, led5, led6]
    for i, led in enumerate(leds):
        led.value(i < value) # Turn on the LED if the index is less than the value
    time.sleep(0.1) # Wait for 0.1 second
```
