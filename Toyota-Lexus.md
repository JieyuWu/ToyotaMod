![toyota lexus](https://user-images.githubusercontent.com/37757984/81997758-90689f80-9605-11ea-98c5-cbdf92f49e30.jpeg)

[◄ Home](https://github.com/VirtuallyChris/wikitest/wiki)

# Toyota-Specific Terms

For general terms, [go here](https://github.com/commaai/openpilot/wiki/Glossary-of-Terms).

Term | Abbreviation | Definition
--- | --- | ---
Driver Support Unit | DSU | This embedded system implements cruise control and Automatic Emergency Braking in some Toyota cars.
Toyota Safety Sense 2 | TSS2 | TSS2 builds on the previous TSS-C and TSS-P suites, and consists of six active safety and driver assistance systems: PCS, DRCC, LDA, AHB, RSA, and LTA. It has a better angle sensor, and supports full range ACC on all openpilot compatible models.
Toyota Safety Sense P | TSSP | An advanced active safety package for mid-size and large vehicles, and consists of six active safety and driver assistance systems: PCS, LDA, and AHB. Includes a DSU which does ACC and AEB.
Toyota Safety Sense C | TSSC | An advanced active safety package for compact vehicles, and consists of six active safety and driver assistance systems: PCS, DRCC, LDA, and AHB. It does not feature lane keep assist, thus is not compatible with openpilot.

# openpilot Capabilities

## Lateral Control

Control over the steering wheel.

### Torque

### Steering Sensor

## Longitudinal Control

Control over the gas and brakes.

### DSU

### Non-DSU Cars

# Community Features

## comma pedal

Allows Toyotas without full-range cruise control to gain stop-and-go using openpilot with a device plugged into the gas pedal.

## SDSU / SmartenedDSU

Upgrades the Driver Support Unit to passthrough AEB and enable openpilot longitudinal control.

## Zorro Steering Sensor (ZSS)

Upgrades TSSP cars with a better angle sensor which allows more accurate steering with openpilot.