![toyota lexus](https://user-images.githubusercontent.com/37757984/81997758-90689f80-9605-11ea-98c5-cbdf92f49e30.jpeg)

[◄ Home](../wiki)

Table of Contents
=================

   * [Supported Toyota/Lexus Vehicles](#supported-toyotalexus-vehicles)
      * [Toyota Camry Support](#toyota-camry-support)
   * [Make-Specific Terms](#make-specific-terms)
   * [openpilot Capabilities](#openpilot-capabilities)
      * [Lateral Control](#lateral-control)
         * [Torque](#torque)
         * [Steering Sensor](#steering-sensor)
      * [Longitudinal Control](#longitudinal-control)
         * [TSS2 Vehicles](#tss2-vehicles)
         * [TSSP Vehicles](#tssp-vehicles)
         * [Stock vs openpilot Longitudinal Control Differences](#stock-vs-openpilot-longitudinal-control-differences)
   * [Community Features](#community-features)
      * [comma pedal](#comma-pedal)
      * [SDSU (SmartDSU/SmartenedDSU)](#sdsu-smartdsusmarteneddsu)
      * [Zorro Steering Sensor (ZSS)](#zorro-steering-sensor-zss)
   * [Common Toyota/Lexus Questions:](#common-toyotalexus-questions)
      * [How can I find out what version of Toyota Safety Sense (TSS) or other features my car has?](#how-can-i-find-out-what-version-of-toyota-safety-sense-tss-or-other-features-my-car-has)

# Supported Toyota/Lexus Vehicles

The most up-to-date list of supported vehicles is on the [openpilot main page](https://github.com/commaai/openpilot#supported-cars).  Please take careful note of the following columns and **pay attention to and read any footnotes**:
* <u>Supported Package</u> - Mandatory trim levels or options required for openpilot to work, if any.  All means all versions of this model work.
* <u>ACC</u> - What is in charge of [longitudinal control](https://github.com/commaai/openpilot/wiki/Toyota-Lexus#longitudinal-control). This can be either Stock (your vehicle's cruise control system) or openpilot. 
  * Footnote 3 applies to a number of Toyota vehicles.  See discussion of [Disconnecting DSU](#).
* <u>No ACC accel below</u> - The car will not provide any gas below these speeds.  0 mph means that the vehicle is capable of stop-and-go driving.
  * Footnote 1, see the [comma pedal](https://github.com/commaai/openpilot/wiki/Toyota-Lexus#comma-pedal).
  * For footnote 4 see [openpilot Camry Support](https://github.com/commaai/openpilot/wiki/Toyota-Lexus#toyota-camry-support).
* <u>No ALC below</u> - No [lateral control](https://github.com/commaai/openpilot/wiki/Toyota-Lexus#lateral-control), this doesn't apply to any supported Toyota/Lexus vehicles currently.

## Toyota Camry Support
For 2018-2020 Camry models which don't have Full-Speed Range Dynamic Radar Cruise Control <u>openpilot will not function below 25mph</u> this includes the 4CYL L, 4CYL LE and 4CYL SE non-hybrid models.  There is no currently known solution for this, these vehicles **cannot** use a comma pedal to solve this issue.  This is because these models use a Continental radar not used on other vehicles and messages from the radar cut out completely below 25mph.

This limitation does not apply to Camry models with Full-Speed Range Dynamic Radar Cruise Control including the (2018-2020 XLE, XSE, LE HV, XLE HV, and SE HV)

# Make-Specific Terms

The following terms are specific to Toyota and Lexus vehicles and are often used in discussions. 

For general terms, [go here](../wiki/General-Terms).

Term | Abbreviation | Definition
--- | --- | ---
Driver Support Unit | DSU | This embedded system implements cruise control and Automatic Emergency Braking in some Toyota cars.
Toyota Safety Sense 2 | TSS2 | TSS2 builds on the previous TSS-C and TSS-P suites, and consists of six active safety and driver assistance systems: PCS, DRCC, LDA, AHB, RSA, and LTA. It has a better angle sensor, and supports full range ACC on all openpilot compatible models.
Toyota Safety Sense P | TSSP | An advanced active safety package for mid-size and large vehicles, and consists of six active safety and driver assistance systems: PCS, LDA, and AHB. Includes a DSU which does ACC and AEB.
Toyota Safety Sense C | TSSC | An advanced active safety package for compact vehicles, and consists of six active safety and driver assistance systems: PCS, DRCC, LDA, and AHB. It does not feature lane keep assist, thus is not compatible with openpilot.

# openpilot Capabilities

## Lateral Control

Control over the steering wheel.  openpilot handles lateral control for all supported Toyota/Lexus vehicles.  However, some TSSP vehicles may have jerky non-precise steering as noted in [Steering Sensor](https://github.com/commaai/openpilot/wiki/Toyota-Lexus#steering-sensor).

### Torque

Toyotas have very good torque, and work well on local and highway roads.

### Steering Sensor

TSS2 Toyotas have a great angle sensor, as well as select 2019+ TSSP Toyotas.
Most TSSP Toyotas have a bad angle sensor. This results in jerky, non-precise steering. The worst culprit of this is the Prius. This can be fixed on some models with a ZSS.

## Longitudinal Control

Control over the gas and brakes.

### TSS2 Vehicles

openpilot handles longitudinal control for these vehicles without any additional modifications.  AEB and blindspot warning will continue to function as they did on the original vehicle.  There is no option on these vehicles to use Stock ACC while using openpilot.

### TSSP Vehicles

The Driver Support Unit is what controls AEB and longitudinal on TSSP cars. This unit must be unplugged to give openpilot control, although this removes AEB.  Users are strongly discouraged from disconnecting their DSU and abandoning AEB.  Instead, a [SDSU](https://github.com/commaai/openpilot/wiki/Toyota-Lexus#sdsu-smartdsusmarteneddsu) solves this problem, by passing through the correct AEB messages while allowing openpilot to control longitudinal.

TSSP vehicle owners have the benefit of choosing to use openpilot or stock ACC, this is not an option for TSS2 vehicle owners.  SmartenedDSU owners may also have the option to switch between stock and openpilot for each drive.

### Stock vs openpilot Longitudinal Control Differences

Both systems work well and there are numerous people who prefer one system over the other.  Generally, the stock ACC is slower to accelerate from a stop and will keep a larger following distance as low speed.  openpilot on the other hand accelerates more aggressively and maintains a closer distance at low speeds but a larger distance as high (freeway) speeds.  Some hybrid owners prefer the stock system because its gentler acceleration profile means less use of the internal combustion engine in traffic.

# Community Features

## comma pedal

A [comma pedal](../wiki/comma-pedal) allows Toyotas without full-range cruise control to gain stop-and-go using openpilot with a device plugged into the gas pedal.

## SDSU (SmartDSU/SmartenedDSU)

Upgrades the Driver Support Unit to passthrough AEB and enable openpilot longitudinal control.  [SDSU](https://github.com/wocsor/panda/tree/smart_dsu) was first sold as an external, harness-style contraption, and later the [SmartenedDSU](https://discord.com/channels/469524606043160576/532179801474203649/687669433145229385) (DSU modified by forwarding a severed CAN connection back into the network by way of an onboard, stripped down, reflashed Panda) and became preferred, with quick creation/installation.

## Zorro Steering Sensor (ZSS)

Upgrades TSSP cars with a [better angle sensor](https://github.com/zorrobyte/betterToyotaAngleSensorForOP) which allows more accurate steering with openpilot.

# Common Toyota/Lexus Questions:

## How can I find out what version of Toyota Safety Sense (TSS) or other features my car has?
> A couple of helpful links.  You can lookup you vehicle details using your VIN on the [Toyota Vehicle Information Lookup](https://www.toyota.com/owners/my-vehicle/vehicle-specification).  You can also review this handy [TSS Applicability Chart](https://cdn.discordapp.com/attachments/524327905937850394/669113172489404416/TSS_Features.pdf)