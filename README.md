# Circuit-python


---
# Table of Contents

* [Table of Contents](#Table-of-Contents)
* [Hello Circuit Python](#Hello-Circuit-Python)
* [Circuit Python Servo](#circuit-python-servo)
* [Circuit Python LCD](#circuit-python-LCD)
* [Circuit Python Distance Sensor](#circuit-python-distance-sensor)
* [Circuit Python Photointerrupters](#circuit-python-photointerrupters)
* [Circuit Python Classes, Object, Modues](#Classs,-Objects,-Modules)
* [Fancy LED](#fancy-LED)
* [PID Box](#PID-Box)
* [Robot Arm](#Robot-Arm)

# Hello Circuit Python

### Description 
Introduction to circuit python. uploading Caret and begel term and using the metro express board. 

### Evidence
```import board
import neopixel
import time

dot= neopixel.NeoPixel(board.NEOPIXEL,1)

while True:
    print("Make it blue!")
    dot.fill((0,0,255))
    time.sleep (.5)
    print("Make it yellow!")
    dot.fill((255,255,0))
    time.sleep(.5)
```
### Image
[![LED Blink](/photos/LED_Blink_Preview.png)](photos/ledblink.mp4)
### Reflection
This was very confusing and it is hard to make the code work on my board, I am not sure if I am doing this right. 
My beagel term does not do the same thing as it shows in the video. I am not sure how to load an image of the work I have done. 
When I opened my caret ap, it did not have the main.py file, not sure what I may be doing wrong. 

# Circuit python servo

### Description- 

### Evidence
```import time
import board
import pulseio
from adafruit_motor import servo
 
# create a PWMOut object on Pin A2.
pwm = pulseio.PWMOut(board.A2, duty_cycle=2 ** 15, frequency=50)
 
# Create a servo object, my_servo.
my_servo = servo.Servo(pwm)
 
while True:
    for angle in range(0, 180, 10):  # 0 - 180 degrees, 5 degrees at a time.
        my_servo.angle = angle
        time.sleep(0.05)
    for angle in range(180, 0, -10): # 180 - 0 degrees, 5 degrees at a time.
        my_servo.angle = angle
        time.sleep(0.05)
```        
### Image

### Reflection

# Circiut python LCD

### Description 

### Evidence
```
import time
import board
import analogio
from lcd.lcd import LCD
from lcd.i2c_pcf8574_interface import I2CPCF8574Interface
# some LCDs are 0x3f... some are 0x27.
lcd = LCD(I2CPCF8574Interface(0x27), num_rows=2, num_cols=16)
count = 0 # initialize count
input1_touched = False
input2_touched = False

# define inputs used for touch
AI1 = analogio.AnalogIn(board.A1) # upcounter input
AI2 = analogio.AnalogIn(board.A2) # downcounter input

while True:
    if AI1.value > 45000 and not input1_touched:
        count += 1
        input1_touched = True
    elif AI1.value < 45000:
        input1_touched = False
    if AI2.value > 45000 and not input2_touched:
        count -= 1
        input2_touched = True
    elif AI2.value < 45000:
        input2_touched = False
    msg = "Count:" + str(count)
    lcd.print(msg)
    time.sleep(1)
    lcd.clear()
```
### Image

### Reflection


# Circiut python distance sensor

### Description 
* when your hand is 27.5cm away from the ultorsoundic sencor then the light is teal
* when your hand is 30cm away from the ultorsoundic sencor then the light is green\teal
* when your hand is 35cm away from the ultorsoundic sencor then the light is green

### Evidence
```# Write your code here :-)
import time
import board
import simpleio
import neopixel
import adafruit_hcsr04

sonar = adafruit_hcsr04.HCSR04(trigger_pin=board.D5, echo_pin=board.D6)
RED = 0;
GREEN = 0;
BLUE = 0;

pixel = neopixel.NeoPixel(board.NEOPIXEL,1)

while True:
    #pixel.fill((RED,GREEN,BLUE))
    if sonar.distance >=5 and sonar.distance <=20:
        RED = simpleio.map_range(sonar.distance,5,20,255,0)
        GREEN = 0
        BLUE = simpleio.map_range(sonar.distance,5,20,0,255)
    elif sonar.distance > 20 and sonar.distance <= 35:
        RED = 0
        GREEN = simpleio.map_range(sonar.distance,20,35,0,255)
        BLUE = simpleio.map_range(sonar.distance,20,35,255,0)
    else:
       RED = 255
       GREEN = 255
       BLUE = 255
    pixel.fill((RED,GREEN,BLUE))
    print(sonar.distance)
    time.sleep(0.5)
```    
### Image
[![distance sensor wiring](/photos/Ultrasonic-Sensor-Cirucit-Schematics-04.png)](/photos/IMG_0079.MOV)

### Reflection
I learrned that we needed make sure we had cases for all distances frorm the sensor or else the board would not work.

# Classs, Objects, Modules 

### Description
when your hand is 5cm away from the ultorsoundic sencor then the light is red 
when your hand is 7.5cm away from the ultorsoundic sencor then the light is orange 
when your hand is 10cm away from the ultorsoundic sencor then the light is pink
when your hand is 15cm away from the ultorsoundic sencor then the light is purppple 
when your hand is 20cm away from the ultorsoundic sencor then the light is blue
when your hand is 25cm away from the ultorsoundic sencor then the light is medium blue
when your hand is 27.5cm away from the ultorsoundic sencor then the light is teal
when your hand is 30cm away from the ultorsoundic sencor then the light is green\teal
when your hand is 35cm away from the ultorsoundic sencor then the light is green

### Evidence
```# you don't need an __init__ method, but it is common for stuff that runs at instantiaion
     def __init__(self, red, green, blue):
          self.led1 = DigitalInOut(red)
          self.led1.direction = Direction.OUTPUT
          self.led2 = DigitalInOut(green)
          self.led2.direction = Direction.OUTPUT
          self.led3 = DigitalInOut(blue)
          self.led3.direction = Direction.OUTPUT

     #
     def red(self):
          self.led1.value = True
          self.led2.value = False
          self.led3.value = False

     def green(self):
          self.led1.value = False
          self.led2.value = True
          self.led3.value = False

    def blue(self):
          self.led1.value = False
          self.led2.value = False
          self.led3.value = True

    def cyan(self):
          self.led1.value = False
          self.led2.value = True
          self.led3.value = True

    def magenta(self):
          self.led1.value = True
          self.led2.value = False
          self.led3.value = True

    def yellow(self):
          self.led1.value = True
          self.led2.value = True
          self.led3.value = False
 ```
### Image
[![RGD Project](/photos/IMG_0081_Preview.png)](/photos/IMG_0081.MOV)
### Reflection
I learrned that we needed make sure we had cases for all distances frorm the sensor or else the board would not work.

# Fancy LED

### Description
first the 2 outer red lights turn on 
then the middle red light turnn on 
then the 2 outter redlights turn on
then the middle red light turnn on 
then the 2 outter redlights turn on
then the middle red light turnn on 
then the 2 outter redlights turn on
then the middle red light turnn on 
then the 2 outter redlights turn on
then the middle red light turnn on 
then the middle red light turnn on abd the 3 blue lights 
then the middle red light turnn on abd the 3 blue lights 
then the middle red light turnn on abd the 3 blue lights 
then the middle red light turnn on abd the 3 blue lights 
then the middle red light turnn on abd the 3 blue lights 
then the red light on the right turns on 
then the middle red light turns on 
then the left red light turns on 
then the red light on the right turns on 
then the middle red light turns on 
then the left red light turns on 
then the red light on the right turns on 
then the middle red light turns on 
then the left red light turns on 
then the red light on the right turns on 
then the middle red light turns on 
then the left red light turns on 
then the red light on the right turns on 
then the middle red light turns on 
then the left red light turns on 
then the 3 blue light and the red light on the left turn on
then the midle blue light and the left red light turn on 
then the 2 outer blue light and the left red light turn on 
then the right blue light and the left red light turn on 
then the left blue light and the left red light turn on 
then the 2 inner blue lights and the right red light turns on 
then the right blue light and the left red light turns on 
then the 2 inner blue lights and the left red light turn on
then the 2 outer bule lights and the left red light turs on 
then all blue lights and the left red light turns on 
then the right blur light and the left red light turns on 
then the 2 outter blue light and the left red light turns on 
then the left red light turns on 
then the left blue light and the left red light turns on 
then the middle blue light and the left red light turns on  
then the left red light turns on
then the 2 outer blue lights and the left red light turns on 
then the left blue and the left red light turns on 
### Evidence
```from fancyLED import FancyLED
import board

fancy1 = FancyLED(board.D2,board.D3,board.D4)
#fancy2 = FancyLED(board.D5,board.D6,board.D7)

while True:
    fancy1.alternate()
    #fancy2.blink()
    fancy1.chase()
    #fancy2.sparkle()
```
```from digitalio import DigitalInOut, Direction
import board
import time
import random

a = 0
b = 0
c = 0
d = 0
option = [True, False]

class FancyLED(object):
    def __init__(self, one, two, three):
    # the two sets of LEDs are initalized with the three pins of the individual LEDs
        self.LED1 = DigitalInOut(one)
        self.LED1.direction = Direction.OUTPUT
        self.LED2 = DigitalInOut(two)
        self.LED2.direction = Direction.OUTPUT
        self.LED3 = DigitalInOut(three)
        self.LED3.direction = Direction.OUTPUT

    def alternate(self):
        for a in range (0, 5, 1):
            self.LED1.value = True
            self.LED2.value = False
            self.LED3.value = True
            time.sleep(0.5)
            self.LED1.value = False
            self.LED2.value = True
            self.LED3.value = False
            time.sleep(0.5)
            a = a + 1

    def blink (self):
        for b in range (0, 5, 1):
            self.LED1.value = True
            self.LED2.value = True
            self.LED3.value = True
            time.sleep (0.5)
            self.LED1.value = False
            self.LED2.value = False
            self.LED3.value = False
            time.sleep (0.5)
            b = b + 1

    def chase (self):
        for c in range (0, 5, 1):
            self.LED1.value = True
            self.LED2.value = False
            self.LED3.value = False
            time.sleep (0.5)
            self.LED1.value = False
            self.LED2.value = True
            self.LED3.value = False
            time.sleep (0.5)
            self.LED1.value = False
            self.LED2.value = False
            self.LED3.value = True
            time.sleep (1)
            c = c + 1

    def sparkle (self):
        for d in range (0, 20, 1):
        # loop runs 20 times instead of 5
            self.LED1.value = random.choice (option)
            self.LED2.value = random.choice (option)
            self.LED3.value = random.choice (option)
            time.sleep (0.3)
            self.LED1.value = False
            self.LED2.value = False
            self.LED3.value = False
            d = d + 1
```            

### Image
[![Fancy LED Project](/photos/IMG_0081_Preview.png)](/photos/IMG_0081.MOV)
### Reflection
It was really hard to code so i used google and it helped a lot. The wiring was also kinda hard so i used google to help me wire. 

# PID Box

### Description

### Evidence

### Image

### Reflection

# Robot Arm

### Description

### Evidence

### Image

### Reflection


