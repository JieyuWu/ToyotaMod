![hyundai kia genesis](https://user-images.githubusercontent.com/37757984/82103626-983d4800-96c8-11ea-8062-e771da985755.jpeg)

[◄ Home](https://github.com/commaai/openpilot/wiki)

**This brand is community supported. Enable it with the toggle in Settings->Developer->Enable Community Features.**

# Harness Guide

Before purchasing a harness for an unsupported vehicle, make sure you are purchasing the correct type. 
### It's important to look where the notches are on your plug side, and ensure they match correctly.

You can find this connector plugged into your Lane-Keep camera which is located near your rear-view mirror. You will need to pull back some trim to expose the camera. Once you do, unplug the connector and compare it to the types below.

![Wire Key](https://user-images.githubusercontent.com/37757984/85790184-a6797d80-b6e4-11ea-8a86-01b6511cd190.png)

---
![Hyundai A](https://user-images.githubusercontent.com/37757984/85791441-ae3a2180-b6e6-11ea-8464-410c5fe6dc62.png)

This connector has a more square shape than the rest. It is also 6 holes across rather than 8.

---
![Hyundai B](https://user-images.githubusercontent.com/37757984/85791442-aed2b800-b6e6-11ea-8d26-29b8c1b238ac.png)

This connector is white, and has unique notches evenly in from the sides. It has the same connector as Hyundai C, but the wiring is different.

---
![Hyundai C](https://user-images.githubusercontent.com/37757984/85791443-aed2b800-b6e6-11ea-97ed-0d3cb5bbf092.png)

This connector is white, and has unique notches evenly in from the sides. It has the same connector as Hyundai B, but the wiring is different.

---
![Hyundai D](https://user-images.githubusercontent.com/37757984/85791444-af6b4e80-b6e6-11ea-8ba5-0d3210a6dce1.png)

This connector is light grey, and has unique notches with the left notch being flush with the left of the connector, while the right notch is inward. It has the same connector as Hyundai I, but the wiring is different.

---
![Hyundai E](https://user-images.githubusercontent.com/37757984/85791446-af6b4e80-b6e6-11ea-8877-74177385f578.png)

This connector is black with a white plug, and has unique notches being flush with the sides of the connector. It has the same connector as Hyundai F, but the wiring is different.

---
![Hyundai F](https://user-images.githubusercontent.com/37757984/85791448-b003e500-b6e6-11ea-893e-1da6bdec383c.png)

This connector is black with a white plug, and has unique notches being flush with the sides of the connector. It has the same connector as Hyundai E, but the wiring is different.

---
![Hyundai G](https://user-images.githubusercontent.com/37757984/85791451-b003e500-b6e6-11ea-9e21-d5707aea2920.png)

This connector is blue with a white plug, and has unique notches with the right notch being flush with the right of the connector, while the left notch is inward. It has the same connector as Hyundai H, but the wiring is different.

---
![Hyundai H](https://user-images.githubusercontent.com/37757984/85791452-b003e500-b6e6-11ea-87b0-6ea821a1f668.png)

This connector is blue with a white plug, and has unique notches with the right notch being flush with the right of the connector, while the left notch is inward. It has the same connector as Hyundai G, but the wiring is different.

---
![Hyundai I](https://user-images.githubusercontent.com/37757984/85791454-b09c7b80-b6e6-11ea-959d-30ce905041f1.png)

This connector is light grey, and has unique notches with the left notch being flush with the left of the connector, while the right notch is inward. It has the same connector as Hyundai D, but the wiring is different.

---
![Hyundai J](https://user-images.githubusercontent.com/37757984/85791455-b09c7b80-b6e6-11ea-9507-7c8c6b3076f6.png)

This connector is white, and has unique wings that protrude from the top of the connector. It is the same connector housing as a Toyota harness, although the wiring is different.

---

# Make-Specific Terms

For general terms, [go here](https://github.com/commaai/openpilot/wiki/General-Terms).

Abbreviation | Term | Definition
--- | --- | ---
SCC | Smart Cruise Control | A fancy way to say ACC, or adaptive cruise control.
HDA | Highway Driver Assist | Combines LFA and SCC with map data to create a more comfortable level 2 experience.
LFA | Lane Follow Assist | A fancier LKAS that centers but nags

# openpilot Capabilities

## Lateral Control

Control over the steering wheel.

For HKG cars that have critical damping (ping pong, oscillation, ziggy zaggies) no matter your settings, PID tuning may not be right for your car.  You can try INDI tuning instead by adding these five lines to your relevant car in `/car/hyundai/interface.py` :

```
ret.lateralTuning.init('indi')
ret.lateralTuning.indi.innerLoopGain = 3.0
ret.lateralTuning.indi.outerLoopGain = 2.0
ret.lateralTuning.indi.timeConstant = 1.0
ret.lateralTuning.indi.actuatorEffectiveness = 1.0
```

Comment out the lines containing Kp, Ki and Kf with a # at the beginning of the line.

The above is only a start point, and needs tuning like any variable parameter.  Raise and lower the LoopGain's by 0.1 at a time, both up or down, until your condition improves.  For Stinger and Genesis, the actuatorEffectiveness start point should be 1.5. 

## Longitudinal Control

Control over the gas and brakes.

At the moment, longitudinal control is provided by the stock system that came with the car.
In the future, we will be able to control longitudinally via openpilot for any vehicle whose trims _can_ support SCC, even if not equipped

## Harness Cable Car and Year Compatible Chart

![Connector](https://i.imgur.com/fKYkA4I.jpg)

![Chart](https://i.imgur.com/Kue6iFa.jpg)