![honda acura](https://user-images.githubusercontent.com/37757984/81997732-7f1f9300-9605-11ea-96fc-54474d48889e.jpeg)

[◄ Home](https://github.com/commaai/openpilot/wiki)

# Make-Specific Terms

For general terms, [go here](https://github.com/commaai/openpilot/wiki/General-Terms).

Term | Abbreviation | Definition
--- | --- | ---
Honda Sensing | Sensing | What Honda calls their ADAS system which provides things such as adaptive cruise control, lane keeping assist, road departure mitigation, and lane departure warning.
Honda Bosch | Bosch | Bosch is a company Honda uses to provide their ADAS systems. Bosch cars don't support openpilot longitudinal, but can sometimes (depending on model) steer down to a lower mph then Honda Nidec vehicles.
Honda Nidec | Nidec | Nidec is a company Honda uses to provide their ADAS systems. Nidec cars support openpilot longitudinal, and are considered a better option for openpilot. Nidec hardware is being phased out company-wide in favor of the Bosch system.
Rewrite Honda EPS | RWD | Part of the Honda Diagnostic System (HDS) software is a tool to flash firmware updates (J2534 Rewrite application) and a set of firmware update files. See https://github.com/gregjhogan/rwd-xray/blob/master/README.md

# openpilot Capabilities

## Lateral Control - steering


### Torque
Honda/Acura vehicles suffer from a low amount of steering torque that can be applied by openpilot. Hondas/Acuras with openpilot are best suited to highways and generally straight roads. They can typically make gradual turns at high speeds, but may require reduced speed to successfully navigate sharper turns.

### Minimum Speeds
Depending on the vehicle model, openpilot cannot steer the car at speeds below 3mph or 12mph. When traveling below the minimum steering speed, the driver must take control of the steering wheel.

## Longitudinal Control - gas and brakes

### Honda Bosch
openpilot doesn't yet control acceleration on Bosch ADAS based vehicles. The radar accepts commands and visual information from the factory windshield mounted camera assembly which then commands the vehicle's steering and acceleration accordingly. The factory Bosch radar does not output object data like other makes/models (including Honda Nidec).

### Honda Nidec
Depending on the model, openpilot will not support stop and go (titled "Low Speed Follow" by Honda/Acura). openpilot does not have direct control over forward acceleration like other models, so it instead uses the factory built-in control system by commanding the desired vehicle speed. If improved acceleration or acceleration control are desired, the community-only supported comma pedal interceptor is required (see below. Not sold or built by comma.ai). openpilot, however, does have full braking control on these cars.

# Community Features

## comma pedal

Allows Nidec Hondas without full-range cruise control to gain stop-and-go using openpilot with a device plugged into the gas pedal.