![honda acura](https://user-images.githubusercontent.com/37757984/81997732-7f1f9300-9605-11ea-96fc-54474d48889e.jpeg)

[◄ Home](https://github.com/commaai/openpilot/wiki)

One of the best supported makes for openpilot.

# Community Features

## comma pedal

Allows Nidec Hondas without full-range cruise control to gain stop-and-go using openpilot with a device plugged into the gas pedal.

# Honda-Specific Terms
Term | Abbreviation | Definition
--- | --- | ---
Honda Sensing | Sensing | What Honda calls their ADAS system which provides things such as adaptive cruise control and lane keeping assist.
Honda Bosch | Bosch | Bosch is a company Honda uses to provide their ADAS systems. Bosch cars don't support openpilot longitudinal, but often can steer down to a lower mph.
Honda Nidec | Nidec | Nidec is a company Honda uses to provide their ADAS systems. Nidec cars support openpilot longitudinal, and are considered a better option for openpilot.

# Limitations

openpilot currently controls only steering on Bosch models. Longitudinal control is provided by the stock system that came with those cars.

Depending on the model, openpilot will not support stop and go.