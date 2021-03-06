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
CX-5, CX-9, and Mazda 6 for model years 2017-2020. Depending on the country and the specific model, 2016/2017 might also work any may require a different a different connector from the one sold at the comma shop. The CX-3 most likely falls into the same 2017-2020 categoray of supported cars. Mazda 3 is supported up to 2018 model. Mazda 3 2019 and newer use a new driver assistance system and is not yet supported. 

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

# Custom solutions:
Note: Mazda harness is now available at comma shop. Look for "Mazda Development" when you select a vehicle. 
## Harness Connector parts:
* [OP connector](https://www.digikey.com/product-detail/en/molex/5016462600/WM6066-ND/1787767)
* [Camera side](https://www.digikey.com/product-detail/en/molex/0348240124/WM10324-ND/4504597)
* [Car Side](https://www.digikey.com/product-detail/en/molex/0348250124/WM10326-ND/4504599)
* [car connector crimps](https://www.digikey.com/product-detail/en/molex/5600230421/WM8745CT-ND/3178491)
* [OP connector crimps](https://www.digikey.com/product-detail/en/molex/5016471000/WM6057CT-ND/1787797)

Harness wiring:

  ![](https://media.discordapp.net/attachments/533836721541087242/669598201438928937/mazda-connector.png)

## Steering Lockout Mitigation
* [Steering Cover](https://www.amazon.com/gp/product/B07465843H/)
* [Weight](https://www.amazon.com/gp/product/B071WP8HGP/)

![](https://media.discordapp.net/attachments/533836721541087242/715957164098715718/steering_wheel_cover_weights.png)

# Developer TODOs 
* Steer down to zero
* Steer without lockout
* Find cruise set speed signal
* openpilot longitudinal control
* Fingerprinting 2.0 ([reference](https://github.com/commaai/openpilot/pull/1540))

# See Also

* https://medium.com/@to.jafar/how-to-setup-openpilot-on-mazda-3eb54c62fdc5

