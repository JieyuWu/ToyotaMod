![honda acura](https://user-images.githubusercontent.com/37757984/81997732-7f1f9300-9605-11ea-96fc-54474d48889e.jpeg)

[◄ Home](https://github.com/commaai/openpilot/wiki)

# Make-Specific Terms

For general terms, [go here](https://github.com/commaai/openpilot/wiki/General-Terms).

Term | Abbreviation | Definition
--- | --- | ---
Honda Sensing | Sensing | What Honda calls their ADAS system which provides things such as adaptive cruise control and lane keeping assist.
Honda Bosch | Bosch | Bosch is a company Honda uses to provide their ADAS systems. Bosch cars don't support openpilot longitudinal, but often can steer down to a lower mph.
Honda Nidec | Nidec | Nidec is a company Honda uses to provide their ADAS systems. Nidec cars support openpilot longitudinal, and are considered a better option for openpilot.

# openpilot Capabilities

## Lateral Control

Control over the steering wheel.

### Torque
Hondas suffer from low torque, so they can only make gradual turns on a highway.

### Minimum Speeds
Depending on the model, openpilot will stop steering under 3mph, or 12mph. During this the driver must resume steering control.

## Longitudinal Control

Control over the gas and brakes.

### Honda Bosch
openpilot doesn't take over control on gas and brakes on Bosch models.

### Honda Nidec
Depending on the model, openpilot will not support stop and go.

# Community Features

## comma pedal

Allows Nidec Hondas without full-range cruise control to gain stop-and-go using openpilot with a device plugged into the gas pedal.