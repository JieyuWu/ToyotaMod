![Subaru](https://user-images.githubusercontent.com/37757984/82103719-fbc77580-96c8-11ea-99d7-6697f1a3ef6f.jpg)

[◄ Home](https://github.com/commaai/openpilot/wiki)

# Make-Specific terms

For general terms, [go here](https://github.com/commaai/openpilot/wiki/General-Terms).

Term | Abbreviation | Definition
--- | --- | ---
EyeSight | ES | Subaru's vision based adaptive cruise / emergency braking / lane keeping system
Global Platform | Global | Subaru's current unified platform, allowing a consistent core between different models. Lowering cost, and improving ease of development. Models using Global Platform include 2017+ Impreza, 2018+ Crosstrek, 2020+ Legacy and 2020+ Outback
Pre-Global Platform | Pre-Global | Refers to models with ES predating Global Platform, for example 2015-2019 Outback, 2015-2019 Legacy, 2017-2019 Forester

# Supported models
**Subaru is community supported. Enable it with the toggle in Settings->Developer->Enable Community Features.**
## Global
| Make      | Model (US Market Reference)   | Supported Package | ACC              | No ACC accel below | No ALC below |
| ----------| ------------------------------| ------------------| -----------------| -------------------| -------------|
| Subaru    | Crosstrek 2018-19             | EyeSight          | Stock            | 0mph               | 0mph         |
| Subaru    | Impreza 2017-20               | EyeSight          | Stock            | 0mph               | 0mph         

# Community supported models
## Pre-global
| Make      | Model (US Market Reference)   | Supported Package | ACC              | No ACC accel below | No ALC below |
| ----------| ------------------------------| ------------------| -----------------| -------------------| -------------|
| Subaru    | Forester 2017                 | EyeSight          | Stock            | 0mph               | 0mph         |
| Subaru    | Legacy 2015-18                | EyeSight          | Stock            | 0mph               | 0mph         |
| Subaru    | Outback 2015-18               | EyeSight          | Stock            | 0mph               | 0mph         |

Community supported models are available in custom fork at https://github.com/bugsy924/openpilot

# openpilot capabilities

## Lateral control

Control over the steering wheel.

### Torque

Subarus have very good torque, and works well on local and highway roads.

### Minimum speeds

0 mph minimum speed for lateral control

## Longitudinal control

Control over the gas and brakes.

Longitudinal control is provided by the stock system that came with the car.

### Stop and go support

Eyesight ACC stops the car, and on supported models<sup>1</sup> will engage brake hold for up to 2 minutes, after which, the park brake will be engaged. *Resuming ACC is a manual operation at this time. Automatic resume is not implemented yet.*

<sup>1 - Supported models include those with an electic park brake. If your vehicle has a traditional handbrake, your hold will only last for a couple seconds before the vehicle will begin to coast.</sup>

# Community videos
Subaru harness install
- [2018 Subaru Crosstrek (global)](https://www.youtube.com/watch?v=LD7qiOcPFtU)
- [2018 Subaru Legacy (pre-global)](https://www.youtube.com/watch?v=-1Snpp3cQEg)

Drives
- [2018 Subaru Crosstrek City Drive Timelapse](https://www.youtube.com/watch?v=1iNOc3cq8cs)
- [2018 Subaru Impreza City Drive Timelapse](https://www.youtube.com/watch?v=LMCTiQE_Ado)