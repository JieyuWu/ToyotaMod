![Chevy](https://user-images.githubusercontent.com/37757984/82255575-ba71d880-9909-11ea-9143-d4670684426e.jpg)

[◄ Home](https://github.com/commaai/openpilot/wiki)

**This brand is community supported. Enable it with the toggle in Settings->Developer->Enable Community Features.**

# GM Terms

[Also see general terms](https://github.com/commaai/openpilot/wiki/General-Terms).

Term | Abbreviation | Definition
--- | --- | ---
Advanced Safety Control Module | ASCM | Car computer/module that does sensor fusion from Radar and Camera to create ACC and LKA messages to PCM (powertrain control module). Typically located in the trunk.
Calibration | n/a | Packaged adjustments to running parameters of firmware running on GM vehicles. Updates available from SPS within [TIS2Web](https://www.acdelcotds.com)
Firmware | n/a | Base operating system for various devices throughout the vehicle. Updates available from SPS within [TIS2Web](https://www.acdelcotds.com)
GDS2 | Global Diagnostic System 2 | GM system for advanced diagnostics and firmware flashing
GMLAN | GM Local Area Network | Single wire propriety interface present on the CAN connector in GM vehicles.
MDI | Multiple Diagnostic Interface | GM service device connecting the vehicle to a computer. Lower price generics exist such as vxdiag.
SPS | Service Programming System | Firmware and calibrations within the TIS2Web application. Updates can be seen for vehicles by VIN without cost [here](https://tis2web.service.gm.com/tis2web).
Tech2Win | Tech2 for Windows | Emulated legacy diagnostic interfaces for Windows. Runs in an emulated terminal.
TIS2Web | Techline Information System | [ACDelco site](https://www.acdelcotds.com) providing diagnostics and firmware for cars on a subscription basis. Interacts with vehicle via GM MDI. Java webstart application.

# Vehicle Requirements

Most GM 2016-2020 vehicles with ACC, LKA.
 
Radar is behind flat Chevy logo:

<img src="https://media.discordapp.net/attachments/524611823090008065/572962897202774029/Cf8RfUjUkAEfliS.png" width="400">

ASCM in the trunk:

<img src="https://media.discordapp.net/attachments/642826052544233491/653393851813199883/20191208_163317.jpg" width="400">

## Unofficial Vehicles

Any GM vehicle 2016+ with front camera and LKA. These will only have ALC, not ACC. With a comma pedal, limited ACC is possible.
See [Unofficial GM fork](https://shulerent.com/openpilot-2019-chevy-bolt-port/) for more info.

For the Chevy Bolt specifically, see the [openpilot Bolt wiki](https://github.com/commaai/openpilot/wiki/Chevy-Bolt).

# Capabilities

### Minimum Speeds

All: 8 mph for lateral control. First engagement must be above 18 mph.

2017: 8 mph for longitudinal control

2018+: 0 mph for longitudinal control

### Auto-Resume

2017: Auto-resumes from stop at 0mph.

2018+: Must press RESUME to resume from stop.

# Hardware

* openpilot device and harness, choose one of:
  * two + ODB-II harness: [$1000](https://comma.ai/shop/products/comma-two-devkit)
    * comma ODB-II harness: $200
    * or homebuilt harness: $40
  * EON + grey panda: $300-$600 used #for-sale
    * Long 3 m usbcable. 20 awg or better. [Recommended](https://www.l-com.com/usb-premium-usb-cable-type-a-male-female-extension-cable-30m). - $20
    * Short 0.3 m mini-usb left-angle cable. [Recommended](https://www.amazon.com/gp/product/B074C8ZLYC). - $9
* Bypass ASCM and power the radar, choose one of:
    1. [GM Giraffe](https://zoneos.com/shop/) - $300-$500
    <br><img src="https://cdn.discordapp.com/attachments/524611823090008065/715799632176742440/20200210_231051.jpg" width="300">
    2. [ASCM wiring harness](https://leepauldinginc.square.site/product/gm-volt-harness-for-open-pilot/20?cs=true) - $210-$240
    <br><img src="https://cdn.discordapp.com/attachments/524611823090008065/578723742100881409/Volt_Wiring_Without_Giraffe.png" width="600">
    3. ASCM connector [Amazon](https://www.amazon.com/gp/product/B000UF24KE/) / [Amazon alt](https://www.amazon.com/dp/B01MULGCTM/) - $7-10 + Cam molex connector [digikey](https://www.digikey.com/product-detail/en/molex-llc/0348250124/WM10326-ND/4504599) - $10
    4. 0.1" header [homebrew harness](https://zoneos.com/volt/#manual-radar)

## Harness Examples

ASCM 14-pin stub

<img src="https://cdn.discordapp.com/attachments/631935882756358174/716016754509480056/20200529_1250562.jpg" width="300">
<img src="https://cdn.discordapp.com/attachments/631935882756358174/716016757436973056/20200529_1251122.jpg" width="300">
<img src="https://cdn.discordapp.com/attachments/631935882756358174/716016758405988402/20200529_1251432.jpg" width="300">

Camera stub

<img src="https://cdn.discordapp.com/attachments/643098390363766798/650085947395801102/20190928_134009.jpg" width="400">

Connect switched +12V (e.g. ignition on, rearview mirror connector or driver fusebox) to pin 9 (radar power) of cam connector. This will turn on the front radar when the car is powered on.

**Original instructions from [Zoneos](https://zoneos.com/volt/)**

# Homebuilt ODB-II to ODB-C Harness
  Map ODB-II to [OBD-C female (at comma two) schematic](https://github.com/commaai/neo/blob/master/car_harness/OBD-C.sch.pdf)
  May require the intercept relays in black and two pandas to be disabled:
  * `panda/board/main.c:`
  * Add `case SAFETY_GM:` fall-through after `case SAFETY_ELM327:`

|   | OBD-II |   | OBD-C |
|---|---|---|---|
| 4 | GND | GND | |
| 6 | CAN1H | A2 | CAN0H |
| 14 | CAN1L | A3 | CAN0L |
| 3 | CAN2H | A11 | CAN1H |
| 11 | CAN2L | A10 | CAN1L |
| 12 | CAN3H | B2 | CAN2H 
| 13 | CAN3L | B3 | CAN2L 
| 16 | 12V | VBUS | |
| | | B8 | SBU2 1kΩ to GND |
