![VW](https://user-images.githubusercontent.com/37757984/82105487-5ca67c00-96d0-11ea-80ef-ba6bbff61d2a.jpg)

[◄ Home](https://github.com/commaai/openpilot/wiki)

**This brand is community supported. Enable it with the toggle in Settings->Developer->Enable Community Features.**

# Make-Specific Terms

For general terms, [go here](https://github.com/commaai/openpilot/wiki/General-Terms).

Term | Abbreviation | Definition
--- | --- | ---
Modularer Querbaukasten / Modular Transverse Matrix | MQB | Strategy for shared modular design between VAG group makes and models. MQB cars with ACC work with Openpilot.

# openpilot Capabilities

## Lateral Control
Control over the steering wheel is provided by openpilot. All MQB vehicles tested to-date support steering down to 0mph.

### Torque
Available steering torque is adequate for most highway driving conditions. All MQB models support the exact same amount of commanded torque, but the different steering rack and suspension geometry between models can result in different effective performance. 

### Minimum Speeds
The minimum ACC setpoint is 20mph/30kph. 

## Longitudinal Control
Longitudinal control remains with stock ACC, although OP takes control of the engagement process for additional safety and feature needs. The exact behavior depends on whether the vehicle has "ACC High" or "ACC Low" from the factory.

### Stock ACC High: 
These vehicles support follow-to-stop and automatic resume if the stop is less than three seconds, from the factory. OP can improve on that by resuming on behalf of the driver after longer delays. "ACC high" requires an electronic parking brake, and does make use of it under certain conditions. If the vehicle in question has an EPB, chances are good it supports "ACC high".

### Stock ACC Low: 
These vehicles generally support follow-to-stop (XXX review this: maybe near-stop only) but will require the driver to take over and hold the brake after a very short delay. Resume from stop is moot as "ACC low" vehicles will not hold themselves at a stop. Any vehicles with a manual parking brake, either foot or hand-operated, will fall into this category.
