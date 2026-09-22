# Fun with electronics

This document focuses on simple circuits and beginner-friendly examples using the ESP8266.

## What you need

A basic setup can include:

- Breadboard
- Jumper wires
- LEDs
- Resistors
- Push button
- Potentiometer
- ESP8266 board

## How a breadboard works

A breadboard is a solderless tool that lets you build temporary electronic circuits.

The board has:

- Rows of connected holes
- Power rails on the side
- A central groove separating sections
- Labels that help you organize the layout

A simple way to think about it:

- The long power rails on the side are for power and ground
- Each row or group of holes is connected internally in a certain pattern
- Components are placed so that their pins connect to the correct groups

This makes it easy to build and test circuits without soldering.

## A simple LED circuit

The easiest beginner project is to blink one or more LEDs.

### Wiring

For each LED:

- Longer leg = anode = connect to a positive voltage through a resistor
- Shorter leg = cathode = connect to ground

Use a resistor to limit current so the LED does not burn out.

A common value for beginner circuits is 220 ohm.

### Example code

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

This is the simplest possible test. If it works, your wiring and GPIO setup are likely correct.

## Multiple LEDs

You can extend the same idea to several LEDs:

```python
import machine
import time

leds = [
    machine.Pin(5, machine.Pin.OUT),
    machine.Pin(4, machine.Pin.OUT),
    machine.Pin(14, machine.Pin.OUT),
    machine.Pin(12, machine.Pin.OUT),
]

while True:
    for led in leds:
        led.value(1)
        time.sleep(0.2)
        led.value(0)
        time.sleep(0.2)
```

This pattern is easy to understand and works well for learning loops and timing.

## Button-controlled LED

A push button can be used as an input to the ESP8266.

### Wiring idea

- One side of the button connects to ground
- The other side connects to a GPIO pin
- The GPIO pin uses a pull-up resistor so the input is stable when not pressed

### Example code

```python
import machine
import time

button = machine.Pin(0, machine.Pin.IN, machine.Pin.PULL_UP)
led = machine.Pin(2, machine.Pin.OUT)

while True:
    if button.value() == 0:
        led.value(1)
    else:
        led.value(0)
    time.sleep(0.05)
```

This is a classic beginner example: the LED is on when the button is pressed.

## Potentiometer example

A potentiometer changes resistance, and the ESP8266 can read that change with an analog input.

### Wiring

- One outer pin to 3.3V
- Other outer pin to GND
- Middle pin to an ADC input

### Example code

```python
import machine
import time

pot = machine.ADC(0)
led = machine.Pin(2, machine.Pin.OUT)

while True:
    value = pot.read()
    if value > 500:
        led.value(1)
    else:
        led.value(0)
    time.sleep(0.05)
```

This is a good example of using an analog value to control a digital output.

## Good beginner practices

- Always use a resistor with LEDs
- Double-check the polarity of the LED
- Keep wires short and clean
- Power the circuit from the correct voltage
- Read the datasheet before connecting a sensor or module
- Test one circuit at a time

## Important caution

Some GPIO pins on the ESP8266 have special functions during boot. If you are building a project, it is a good idea to use pins that are known to be safe for basic experiments and check the board documentation when needed.

## Summary

The best way to learn electronics with the ESP8266 is to start with simple circuits and build up slowly. An LED, a button, and a potentiometer are enough to start understanding how digital and analog inputs and outputs work together.

---

Return to [README.md](README.md).
