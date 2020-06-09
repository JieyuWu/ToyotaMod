![hyundai kia genesis](https://user-images.githubusercontent.com/37757984/82103626-983d4800-96c8-11ea-8062-e771da985755.jpeg)

[◄ Home](https://github.com/commaai/openpilot/wiki)

**This brand is community supported. Enable it with the toggle in Settings->Developer->Enable Community Features.**

# Harness Guide

Before purchasing a harness for an unsupported vehicle, make sure you are purchasing the correct type. 
### It's important to look where the notches are on your plug side, and ensure they match correctly.

You can find this connector plugged into your Lane-Keep camera which is located near your rear-view mirror. You may need to pull back some trim to expose the camera. Once you do, unplug the connector and compare it to the types below. If it doesn't match, we don't yet sell the correct harness for your vehicle.

---
![Hyundai A](https://user-images.githubusercontent.com/37757984/82007923-4d67f580-9620-11ea-8e5f-8167e2051f02.png)

This connector has a more square shape than the rest. It is also 6 holes across rather than 8.

---
![Hyundai B](https://user-images.githubusercontent.com/37757984/82935518-06dc9a00-9f42-11ea-996c-e83166c0c89e.png)

This connector is white, and has unique notches evenly in from the sides. It has the same connector as Hyundai C, but the wiring is different.

---
![Hyundai C](https://user-images.githubusercontent.com/37757984/82935522-07753080-9f42-11ea-85d1-8f104693f41c.png)

This connector is white, and has unique notches evenly in from the sides. It has the same connector as Hyundai B, but the wiring is different.

---
![Hyundai D](https://user-images.githubusercontent.com/37757984/82935524-07753080-9f42-11ea-88cd-3691be085b66.png)

This connector is light grey, and has unique notches with the left notch being flush with the left of the connector, while the right notch is inward. It has the same connector as Hyundai I, but the wiring is different.

---
![Hyundai E](https://user-images.githubusercontent.com/37757984/82935525-080dc700-9f42-11ea-809a-cedd72f97112.png)

This connector is black with a white plug, and has unique notches being flush with the sides of the connector. It has the same connector as Hyundai F, but the wiring is different.

---
![Hyundai G](https://user-images.githubusercontent.com/37757984/83704485-0e95e180-a5c7-11ea-9f11-cae40a675728.png)

This connector is blue with a white plug, and has unique notches with the right notch being flush with the right of the connector, while the left notch is inward. It has the same connector as Hyundai H, but the wiring is different.

---
![Hyundai H](https://user-images.githubusercontent.com/37757984/83704572-3e44e980-a5c7-11ea-90d7-f0dd64635b17.png)

This connector is blue with a white plug, and has unique notches with the right notch being flush with the right of the connector, while the left notch is inward. It has the same connector as Hyundai G, but the wiring is different.

---
# Not Yet Released Harness Types

![Hyundai F](https://user-images.githubusercontent.com/37757984/82935527-080dc700-9f42-11ea-9d7c-c4383e72da57.png)

This connector is black with a white plug, and has unique notches being flush with the sides of the connector. It has the same connector as Hyundai E, but the wiring is different.

---
![Hyundai I](https://user-images.githubusercontent.com/37757984/83458885-2da24100-a418-11ea-8131-64b4af87f82d.png)

This connector is light grey, and has unique notches with the left notch being flush with the left of the connector, while the right notch is inward. It has the same connector as Hyundai D, but the wiring is different.

---

# Make-Specific Terms

For general terms, [go here](https://github.com/commaai/openpilot/wiki/General-Terms).

Term | Abbreviation | Definition
--- | --- | ---
Smart Cruise Control | SCC | A fancy way to say ACC
Lane Following Assist | LFA | A fancier LKAS that centers but nags
Highway Driver Assist | HDA | Combines LFA and SCC with map data to create a more comfortable level 2 experience.

# openpilot Capabilities

## Lateral Control

Control over the steering wheel.

For HKG cars that have critical damping (ping pong, oscillation, ziggy zaggies) no matter your settings, PID tuning may not be right for your car.  You can try INDI tuning instead by adding these five lines to your relevant car in ./car/hyundai/interface.py:

ret.lateralTuning.init('indi')
ret.lateralTuning.indi.innerLoopGain = 3.0
ret.lateralTuning.indi.outerLoopGain = 2.0
ret.lateralTuning.indi.timeConstant = 1.0
ret.lateralTuning.indi.actuatorEffectiveness = 1.0

Comment out the lines containing Kp, Ki and Kf with a # at the beginning of the line.

The above is only a start point, and needs tuning like any variable parameter.  Raise and lower the LoopGain's by 0.1 at a time, both up or down, until your condition improves.  For Stinger and Genesis, the actuatorEffectiveness start point should be 1.5. 

## Longitudinal Control

Control over the gas and brakes.

At the moment, longitudinal control is provided by the stock system that came with the car.
In the future, we will be able to control longitudinally via openpilot for any vehicle whose trims _can_ support SCC, even if not equipped