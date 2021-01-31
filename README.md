# Circuit-python-


---
## Table of Contents
* [Table of Contents](#Table-of-Contents)
* [Hello Circuit python](hello circuit python)
* [Circuit python servo](#circuit python servo)
* [circuit python LCD](#circuit python LCD)
* [circuit python distance sensor](#circuit python distance sensor)
* [circuit python photointerrupters](#circuit python photointerrupters)
* [circuit python Classes, Object, Modues](#Classs, Objects, Modules)
* [fancy LED](#fancy LED)




## Hello Circuit Python

### Description- Introduction to circuit python. uploading Caret and begel term and using the metro express board. 

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
![ledblink](circuit-python-/ledblink.mp4)


### Reflection
This was very confusing and it is hard to make the code work on my board, I am not sure if I am doing this right. 
My beagel term does not do the same thing as it shows in the video. I am not sure how to load an image of the work I have done. 
When I opened my caret ap, it did not have the main.py file, not sure what I may be oding rong. 


## Circuit python servo

### Description- 

### Evidence


### Image



### Reflection


# Circiut python LCD

### Description- 

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

### Description- 
when your hand is 27.5cm away from the ultorsoundic sencor then the light is teal
when your hand is 30cm away from the ultorsoundic sencor then the light is green\teal
when your hand is 35cm away from the ultorsoundic sencor then the light is green

### Evidence

### Image
![distance sensor wiring](/photos/Ultrasonic-Sensor-Cirucit-Schematics-04.png)



### Reflection


# Classs, Objects, Modules 

### Description- 

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

