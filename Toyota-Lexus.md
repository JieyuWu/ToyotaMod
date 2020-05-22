![toyota lexus](https://user-images.githubusercontent.com/37757984/81997758-90689f80-9605-11ea-98c5-cbdf92f49e30.jpeg)

[◄ Home](https://github.com/commaai/openpilot/wiki)

# Toyota-Specific Terms

For general terms, [go here](https://github.com/commaai/openpilot/wiki/General-Terms).

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

Toyotas have very good torque, and work well on local and highway roads.

### Steering Sensor

TSS2 Toyotas have a great angle sensor, as well as select 2019+ TSSP Toyotas.
Most TSSP Toyotas have a bad angle sensor. This results in jerky, non-precise steering. The worst culprit of this is the Prius. This can be fixed on some models with a ZSS.

## Longitudinal Control

Control over the gas and brakes.

### DSU

The Driver Support Unit is what controls AEB and longitudinal on TSSP cars. This unit must be unplugged to give openpilot control, although this removes AEB. A SDSU solves this problem, by passing through the correct AEB messages while allowing openpilot to control longitudinal.

### Non-DSU Cars

Non-DSU cars such as the Camry cannot use openpilot longitudinal control. They utilize a different radar unit that directly sends gas and brake commands, thus is impossible to intercept without a radar swap.

# Community Features

## comma pedal

Allows Toyotas without full-range cruise control to gain stop-and-go using openpilot with a device plugged into the gas pedal.

## SDSU / SmartenedDSU

Upgrades the Driver Support Unit to passthrough AEB and enable openpilot longitudinal control.

## Zorro Steering Sensor (ZSS)

Upgrades TSSP cars with a better angle sensor which allows more accurate steering with openpilot.