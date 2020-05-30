![Mazda](https://user-images.githubusercontent.com/37757984/82703104-287b1000-9c28-11ea-989e-6d9e691dd60f.png)

[◄ Home](https://github.com/commaai/openpilot/wiki)

# Overview

Mazda is community supported and available in dashcam mode only in OP due to a steer lockout if the driver does not touch the steering wheel for more than 5 seconds. Currently, the only workaround for this issue is to use a weight on the steering wheel. If you want to use OP with Mazda in non-dashcam mode you have to make changes to the source code and use it at your own risk. To do that change the line in `selfdrive/car/mazda/interface.py` [[here]](https://github.com/commaai/openpilot/blob/master/selfdrive/car/mazda/interface.py#L24)
from:
```
ret.dashcamOnly = True
```
to 
```
ret.dashcamOnly = False
```

Remember that you have to keep your hands on the wheel at all times, or use a steering lockout mitigation such as a weight on the steering wheel, otherwise the car does not respond to steer commands from OP.

# Make-Specific Terms

For general terms, [go here](https://github.com/commaai/openpilot/wiki/General-Terms).

Mazda I-ACTIVSENSE is an umbrella term that Mazda uses to describe a series of advanced safety and driver assistance technologies such as ACC, LKAS, Blind-spot monitoring, Smart City brakes and so on. Most models/trims from 2017 and newer come with ACC and LKAS as standard options. 

Term | Abbreviation | Definition
--- | --- | ---
Mazda Radar Cruise Control  | MRCC | Mazda Adaptive Cruise Control - ACC
Lane-Keep Assist System | LAS | Mazda LKAS

# Supported models
CX-5, CX-9, and Mazda 6 for model years 2017-2020. Other car/year models might work but have not been tested.  Mazda 3 2019 and newer use a new driver assistance system and is not yet supported. 

# openpilot Capabilities

## Lateral Control

Mazda LKAS is not available on low speeds. In particular, LKAS is not available until the car drives above 32mph/52kph. LKAS gets disabled when the speed goes below 28mpg/45kph. OP will NOT allow initial engagement if LKAS is not available. If OP is already engaged and LKAS becomes unavailable, OP will continue to be engaged but will not steer and will display a warning about steering being unavailable. 

### Torque
Available steering torque is adequate for most highway driving conditions. City driving requires driver intervention on sharp turns. 

### Minimum Speeds

* LKAS is allowed when the car drives above 32mph
* LKAS is not allowed when the speed dips below 28mph
* LKAS must be allowed for OP to do the initial engagement

## Longitudinal Control

Longitudinal control is not supported by OP with Mazda. OP relies on the stock MRCC to control speed. MRCC support follow-to-stop to 0mph and automatic resume if the stop is less than three seconds. OP improve on that by allowing the car to resume without driver intervention after longer delays. Even though MRCC works down to 0mph, the lowest allowed set speed is 19mph. 

Note that OP takes control of the engagement process and will not allow the MRCC to engage if LKAS is not available, i.e, when used with OP you will not be able to engage ACC on low speeds. That behavior is required by OP safety model.

# Developer TODOs 
* Steer down to zero
* Steer without lockout
* Find cruise set speed signal
* openpilot longitudinal control
* Fingerprinting 2.0 ([reference](https://github.com/commaai/openpilot/pull/1540))