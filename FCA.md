![FCA](https://user-images.githubusercontent.com/37757984/82703103-2749e300-9c28-11ea-914c-b7a21074640f.png)

[◄ Home](https://github.com/commaai/openpilot/wiki)

**This brand is community supported. Enable it with the toggle in Settings->Developer->Enable Community Features.**

# Make-Specific Terms

For general terms, [go here](https://github.com/commaai/openpilot/wiki/General-Terms).

Term | Abbreviation | Definition
--- | --- | ---
LaneSense | LKAS | Stock lane keeping system (can turn the wheel, you need this.)
Adaptive Cruise Control | ACC | Stock cruise control system with radar that paces the vehicle in front of you (you need this.) 
Fiat Chrysler of America | FCA | You'll see this term a lot.  It just groups Ram, Jeep, Chrysler, Dodge, Fiat, etc into one.

## Current community supported vehicles: (must have ACC and LaneSense)
### 2017-2018 Jeep Grand Cherokee (all trims including SRT, Trackhawk)
### 2019+ Jeep Grand Cherokee (all trims including SRT, Trackhawk) * minimum steer speed 39 mph 
### 2017-2018 Chrysler Pacifica (all trims and powertrains)
### 2019+ Chrysler Pacifica (all trims and powertrains) * minimum steer speed 39 mph
### 2019+ Jeep Cherokee (KL) (all trims) * minimum steer speed 39 mph 
To add Openpilot to one of the above vehicles, a Comma two (c2) is required, and FCA Harness.  The official Openpilot releases from Comma work with the above vehicles.  

# openpilot Capabilities

## Lateral Control

Control over the steering wheel.

### Torque

### Minimum Speeds

Chrysler Pacifica and Jeep Grand Cherokee models years 2017-2018 can steer down to 9 mph. 

Model years 2019 and later can start steering once reaching 39 mph, and then steer down to approximately 30 mph.

## Longitudinal Control

Control over the gas and brakes.

Longitudinal control is provided by the stock system that came with the car.  

## 2019+ Ram 1500 with ACC and LaneSense

Ram 1500's with ACC and LaneSense may work with Openpilot.  A car port has not yet been completed for Ram 1500's, although a bit of data has been collected from them.  It appears, with the information gathered so far, that it "should" work.  Owners of Ram 1500's interested in making Openpilot work with their trucks would need a Comma two (c2) and Dev Harness, outfitted with connectors as found in this document: https://1drv.ms/b/s!AhlEjIwibjKfiZojQ_EU934HfcvMHA?e=mOVWBh.

## 2014-2018 Chrysler 200, 2014-2018 Jeep Cherokee, late model Jeep Renegade, late model Jeep Compass, 2014-2018 Dodge Chargers, 2014-2018 Chrysler 300 equipped with ACC and LaneSense 

These vehicles work with Openpilot via a fork maintained by Discord member, Tunder.  Those interested should contact Tunder directly, as the fork is highly experimental and in active development.  It can be found, and forked, from https://github.com/Tundergit/openpilot.git, branch: devel.  *** This implementation does NOT conform to safety standards enforced by Comma.  Installing and using this fork is at your own risk.  Owners are encouraged to contribute to further development of this fork.  

Owners of the above vehicles will need a Comma two (c2) and Dev Harness, outfitted with the connectors found in this document: https://1drv.ms/b/s!AhlEjIwibjKfiZoczAAEKfpPBOIE-w?e=SjJmJQ 