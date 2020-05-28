![Chevy](https://user-images.githubusercontent.com/37757984/82255575-ba71d880-9909-11ea-9143-d4670684426e.jpg)

[◄ Home](https://github.com/commaai/openpilot/wiki)

**This brand is community supported. Enable it with the toggle in Settings->Developer->Enable Community Features.**

# Make-Specific Terms

For general terms, [go here](https://github.com/commaai/openpilot/wiki/General-Terms).

Term | Abbreviation | Definition
--- | --- | ---
Calibration | n/a | Packaged adjustments to running parameters of firmware running on GM vehicles. Updates available from SPS within [TIS2Web](https://www.acdelcotds.com)
Firmware | n/a | Base operating system for various devices throughout the vehicle. Updates available from SPS within [TIS2Web](https://www.acdelcotds.com)
GDS2 | Global Diagnostic System 2 | GM system for advanced diagnostics and firmware flashing
GMLAN | GM Local Area Network | Single wire propriety interface present on the CAN connector in GM vehicles.
MDI | Multiple Diagnostic Interface | GM service device connecting the vehicle to a computer. Lower price generics exist such as vxdiag.
SPS | Service Programming System | Firmware and calibrations within the TIS2Web application. Updates can be seen for vehicles by VIN without cost [here](https://tis2web.service.gm.com/tis2web).
Tech2Win | Tech2 for Windows | Emulated legacy diagnostic interfaces for Windows. Runs in an emulated terminal.
TIS2Web | Techline Information System | [ACDelco site](https://www.acdelcotds.com) providing diagnostics and firmware for cars on a subscription basis. Interacts with vehicle via GM MDI. Java webstart application.

# openpilot Capabilities

## Lateral Control

Control over the steering wheel.

### Torque

### Minimum Speeds

8mph minimum speed for lateral control

## Longitudinal Control

Control over the gas and brakes.
Longitudinal control is provided by OpenPilot.

### Minimum Speeds

2017 MY:
8mph minimum speed for longitudinal control

2018+ MY:
0mph minimum speed for longitudinal control

### AutoResume

2017 MY:
Auto-resumes from stop at 0mph.

2018+ MY:
Does not autoresume. Must press RESUME to resume from stop.