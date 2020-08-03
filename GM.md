![Chevy](https://user-images.githubusercontent.com/37757984/82255575-ba71d880-9909-11ea-9143-d4670684426e.jpg)

[◄ Home](https://github.com/commaai/openpilot/wiki)

**This brand is community supported. Enable it with the toggle in Settings->Developer->Enable Community Features.**

# Make-Specific Terms

For general terms, [go here](https://github.com/commaai/openpilot/wiki/General-Terms).

Term | Abbreviation | Definition
--- | --- | ---
Advanced Safety Control Module | ASCM | Car computer/module that does sensor fusion from Radar and Camera to create ACC and LKAs messages to PCM (powertrain control module). Typically located in the trunk.
Calibration | n/a | Packaged adjustments to running parameters of firmware running on GM vehicles. Updates available from SPS within [TIS2Web](https://www.acdelcotds.com)
Firmware | n/a | Base operating system for various devices throughout the vehicle. Updates available from SPS within [TIS2Web](https://www.acdelcotds.com)
GDS2 | Global Diagnostic System 2 | GM system for advanced diagnostics and firmware flashing
GMLAN | GM Local Area Network | Single wire propriety interface present on the CAN connector in GM vehicles.
MDI | Multiple Diagnostic Interface | GM service device connecting the vehicle to a computer. Lower price generics exist such as vxdiag.
SPS | Service Programming System | Firmware and calibrations within the TIS2Web application. Updates can be seen for vehicles by VIN without cost [here](https://tis2web.service.gm.com/tis2web).
Tech2Win | Tech2 for Windows | Emulated legacy diagnostic interfaces for Windows. Runs in an emulated terminal.
TIS2Web | Techline Information System | [ACDelco site](https://www.acdelcotds.com) providing diagnostics and firmware for cars on a subscription basis. Interacts with vehicle via GM MDI. Java webstart application.

# Requirements

Most GM 2016-2020 vehicles with a front radar (ACC), LKAs, and an ASCM in the trunk.  
The radar will be hidden behind the flat Chevy logo:

<img src="https://media.discordapp.net/attachments/524611823090008065/572962897202774029/Cf8RfUjUkAEfliS.png" width="400">

ASCM in the trunk:

<img src="https://media.discordapp.net/attachments/642826052544233491/653393851813199883/20191208_163317.jpg" width="400">

## Unoffically supported vehicles

Any GM vehicle 2016+ with front camera and LKAs. These will only have ALC (aka lane centering), but not ACC via OpenPilot.
See [Unofficial GM fork](https://shulerent.com/openpilot-2019-chevy-bolt-port/) for more info.

For the Chevy Bolt specifically, see the [openpilot Bolt wiki](https://github.com/commaai/openpilot/wiki/Chevy-Bolt).

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

### Auto-Resume

2017 MY:
Auto-resumes from stop at 0mph.

2018+ MY:
Does not auto-resume. Must press RESUME to resume from stop.

# openpilot Installation

## Required hardware
* Comma EON (EON OLED or EON Gold, 64GB or 128GB) - $250-$400
* Gray Panda + GPS antenna - $50-$200
* Replacement for ASCM. Namely, one of:
    1. [GM Giraffe](https://zoneos.com/shop/) - $300-$500
    <br><img src="https://cdn.discordapp.com/attachments/524611823090008065/715799632176742440/20200210_231051.jpg" width="300">
    2. [ASCM wiring harness](https://leepauldinginc.square.site/product/gm-volt-harness-for-open-pilot/20?cs=true) - $210-$240
    <br><img src="https://cdn.discordapp.com/attachments/524611823090008065/578723742100881409/Volt_Wiring_Without_Giraffe.png" width="600">
    3. ASCM connector [Amazon](https://www.amazon.com/gp/product/B000UF24KE/) / [Amazon alt](https://www.amazon.com/dp/B01MULGCTM/) - $7-10 + Cam molex connector [digikey](https://www.digikey.com/product-detail/en/molex-llc/0348250124/WM10326-ND/4504599) - $10
* 3 meter long USB extension cable. Preferably 20awg or smaller (thicker). [Recommended](https://www.l-com.com/usb-premium-usb-cable-type-a-male-female-extension-cable-30m). - $20
* Short 30cm mini-usb left-angle cable. [Recommended](https://www.amazon.com/gp/product/B074C8ZLYC). - $9

## Installation

### Prerequisites

If using ASCM connector stub + cam connector stub, furnish the stubs via soldering.

1) Final ASCM 14-pin connector stub assembled:  

<img src="https://cdn.discordapp.com/attachments/631935882756358174/716016754509480056/20200529_1250562.jpg" width="300">
<img src="https://cdn.discordapp.com/attachments/631935882756358174/716016757436973056/20200529_1251122.jpg" width="300">
<img src="https://cdn.discordapp.com/attachments/631935882756358174/716016758405988402/20200529_1251432.jpg" width="300">

2) Final cam connector stub assembled:  
<img src="https://cdn.discordapp.com/attachments/643098390363766798/650085947395801102/20190928_134009.jpg" width="400">

3) Connect a wire from switched +12V (e.g. ignition on) to pin 9 of cam connector. This will turn on the front radar when the car is powered on.
Examples of switched +12V locations:
* Rearview mirror assembly
* Driver footwell fusebox

### Hardware Installation

1) Replace ASCM with one of the 3 ASCM replacements above.
    * If using GM Giraffe, simply swap out the ASCM for the GM Giraffe.
    * If using ASCM wiring harness, connect the harness inline with ASCM and run the wires to the dash.
    * If using ASCM stub connector, disconnect the 14-pin ASCM connector and plug in the stub connector. Leave the 16-pin connector in ASCM plugged in. Also unplug the front camera connector from the camera, and plug in the cam molex stub. Finally, make sure you're powering your radar with +12v (see #3 above).
2) Install Gray Panda in OBD II port.
    * Install Gray Panda GPS antenna on windshield.
3) Install EON centered on windshield.
    * Run a USB extension cable from Panda -> nearby EON.
    * Use short mini-usb left-angle USB cable from USB extension -> EON.
4) [Enjoy your first drive!](https://community.comma.ai/wiki/index.php/First_OpenPilot_Drive)

**For more detailed instructions see [Zoneos](https://zoneos.com/volt/)**

# comma two support

* Like the EON, bypass the ASCM, and power the radar.
* Disable intercept relays
  * `panda/board/main.c:`
  * Add `case SAFETY_GM:` fall-through after `case SAFETY_ELM327:`
  * (TODO: git patch or commit ref this step)
* OBD-II to OBD-C Harness
  * Buy the [`OBD-II Harness` from the comma shop!](https://comma.ai/shop/products/comma-car-harness)! Supports GMLAN.
  * Or, map to [OBD-C female (at comma two) schematic](https://github.com/commaai/neo/blob/master/car_harness/OBD-C.sch.pdf)

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
