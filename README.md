# GuardianPipeOrgan

[<img src = "https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/4da7ebca-186f-412e-8aa4-d7fcf4fde7b9/de98lke-fb39619d-336d-4663-add4-e0f87b19a37b.png?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOiIsImlzcyI6InVybjphcHA6Iiwib2JqIjpbW3sicGF0aCI6IlwvZlwvNGRhN2ViY2EtMTg2Zi00MTJlLThhYTQtZDdmY2Y0ZmRlN2I5XC9kZTk4bGtlLWZiMzk2MTlkLTMzNmQtNDY2My1hZGQ0LWUwZjg3YjE5YTM3Yi5wbmcifV1dLCJhdWQiOlsidXJuOnNlcnZpY2U6ZmlsZS5kb3dubG9hZCJdfQ.55sYyvbvFXvSWeLJUF-AZFiEDiaG3U3LSn7FCi4E5nI" alt = "Terrako by rongs1234 on DeviantArt" width = "" height = "">](https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.deviantart.com%2Frongs1234%2Fart%2FTerrako-862044206&psig=AOvVaw2PNPe1dH_EVHYLI62axwsY&ust=1612890263248000&source=images&cd=vfe&ved=0CAIQjRxqFwoTCMC378vi2u4CFQAAAAAdAAAAABAD)

Pardon the dust as we keep updating this README!

ins Table of Contents

### Project Pre-Planning
ins Pre-planning Document

[Link](https://docs.google.com/document/d/1uND1lurYmUpj-_9FQsYxZuwOPflugXZLaDDHEH4wFzs/edit?usp=sharing)

### Pseudocode
Link to code [here.](GuardianPipeOrganOutPseudoCode)
```python
# Bob Kammauff
# 2/4/2021
# Guardian Pipe Organ - Output
# pseudocode

# at the top here, put all of the libraries we'll be using

import time

import digitalio
import touchio
import busio
import board
import usb_midi
import neopixel


import adafruit_midi

from adafruit_midi.note_on          import NoteOn
from adafruit_midi.control_change   import ControlChange
from adafruit_midi.pitch_bend       import PitchBend

# + some others that I don't know about

# set up any serial port communication we'll need

# using some type of shift register or port thingy to get more pins
# so initialize that

# Read any incoming MIDI messages (events) over USB
# looking for note on, note off messages

# Our organ will have 32 notes starting at middle C (C4) and going up to G6
# Each time a note on value is detected, write the pin connected to that note's solonoid high
# Each time theres a note off value, write the pin low

# there will be transistors in between every solonoid to supply the correct voltage
```

## Working on the Code
So, I do not have the transistors or the shift registers or any of that fancy stuff yet; all I got is a Circuit Python and some LED's, but the coding will be the same either way. Let's set up a circuit python to read Midi Data coming from my computer to light up some led's.

The wiring is easy. a bunch of LED's and resistors. Iet's get working on the code for it.

Ok so I've already run into a couple problems about how to write the code. The code I'm taking it from sets all of the pins using a for loop. But, I can't find a way to do that with digital pins because they require a 2nd initialization to tell the pin whether to be input or output. Brute forcing it might just be the correct solution, but the idea of having the pins in an array just makes the code so much simpler.

Now that I've described the problem, the solution seems clear: do a mix

This didn't work

```python
pins = [board.D13,
        board.D12,
        board.D11,
        board.D10,
        board.D9,
        board.D8,
        board.D7,
        board.D6,
        board.D5,
        board.D4,
        board.D3,
        board.D2]


# add LED's
# ledG = digitalio.DigitalInOut(board.D1)
# ledG.direction = digitalio.Direction.OUTPUT
# n
# or do it like this

noteLEDs = []
x = 0
for pin in pins:
    noteLEDs = [digitalio.DigitalInOut(pin)]
    print(str(pin))

del pins, x  # done with that
noteLEDs.direction = digitalio.Direction.OUTPUT
```

Lets try this now: set the pins each to a variable, then set each variable to a list.

```python
pinD13 = digitalio.DigitalInOut(board.D13)
pinD12 = digitalio.DigitalInOut(board.D12)
pinD11 = digitalio.DigitalInOut(board.D11)
pinD10 = digitalio.DigitalInOut(board.D10)
pinD9 = digitalio.DigitalInOut(board.D9)
pinD8 = digitalio.DigitalInOut(board.D8)
pinD7 = digitalio.DigitalInOut(board.D7)
pinD6 = digitalio.DigitalInOut(board.D6)
pinD5 = digitalio.DigitalInOut(board.D5)
pinD4 = digitalio.DigitalInOut(board.D4)
pinD3 = digitalio.DigitalInOut(board.D3)
pinD2 = digitalio.DigitalInOut(board.D2)

pinD13.direction = digitalio.Direction.OUTPUT
pinD12.direction = digitalio.Direction.OUTPUT
pinD11.direction = digitalio.Direction.OUTPUT
pinD10.direction = digitalio.Direction.OUTPUT
pinD9.direction = digitalio.Direction.OUTPUT
pinD8.direction = digitalio.Direction.OUTPUT
pinD7.direction = digitalio.Direction.OUTPUT
pinD6.direction = digitalio.Direction.OUTPUT
pinD5.direction = digitalio.Direction.OUTPUT
pinD4.direction = digitalio.Direction.OUTPUT
pinD3.direction = digitalio.Direction.OUTPUT
pinD2.direction = digitalio.Direction.OUTPUT


noteLEDs = [pinD13,
            pinD12,
            pinD11,
            pinD10,
            pinD9,
            pinD8,
            pinD7,
            pinD6,
            pinD5,
            pinD4,
            pinD3,
            pinD2]

# Brute forced
```
### Schedule

| 1st week |  Get midi working with the circuit pythons  |  Feb. 22nd-26th |
|:--------:|:-------------------------------------------:|:---------------:|
| 2nd week | Order all of the parts we’ll need           | Mar. 1st-5th    |
| 3rd week | Design the organ pipes and the valve system | Mar. 8th-12th   |
| 4th week | Design the Shell to put the organ into      | Mar. 15th-19th  |
| 5th week | Fabrication                                 | Mar.22nd-26th   |
| 6th week | Troubleshooting (buffer week)               | Mar. 29th-Apr.2 |


#### 3rd Week

Bob Goal: Finish the design for the organ pipes. Design the Valve system. 

Justyn Goal: Fix up the github, Add pictures, cad, toc. Lay out the valves once Bob Has made the valves


### CAD

[Link to Onshape](https://cvilleschools.onshape.com/documents/e358e4e3ba9e07c5ae938246/w/c6c09eac29318e33af1bc1ef/e/29cbd6e08dd43a0f8d613074)
