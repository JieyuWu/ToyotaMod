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

# Requirements

Most GM vehicles with a front radar (ACC), LKAs, and an ASCM in the trunk.  
The radar will be hidden behind the flat Chevy logo:

<img src="https://media.discordapp.net/attachments/524611823090008065/572962897202774029/Cf8RfUjUkAEfliS.png" width="400">

ASCM in the trunk:

<img src="https://media.discordapp.net/attachments/642826052544233491/653393851813199883/20191208_163317.jpg" width="400">

## Unoffically supported vehicles

Any GM vehicle 2016+ with front camera and LKAs. These will only have ALC (aka lane centering), but not ACC via OpenPilot.
See [Unofficial GM fork](https://shulerent.com/openpilot-2019-chevy-bolt-port/) for more info.

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
* Replacement for ASCM (Advance Safety Control Module). Namely, one of:
    * [GM Giraffe](https://zoneos.com/shop/) - $300-$500
    * [ASCM wiring harness](https://leepauldinginc.square.site/product/gm-volt-harness-for-open-pilot/20?cs=true) - $210-$1000
    * ASCM connector [Amazon](https://www.amazon.com/dp/B01MULGCTM/) - $9 + Cam molex connector [digikey](https://www.digikey.com/product-detail/en/molex-llc/0348250124/WM10326-ND/4504599) - $10
* 3 meter long USB extension cable. Preferably 20awg or smaller (thicker). [Recommended](https://www.l-com.com/usb-premium-usb-cable-type-a-male-female-extension-cable-30m). - $20
* Short 30cm mini-usb left-angle cable. [Recommended](https://www.amazon.com/gp/product/B074C8ZLYC). - $9

## Installation

### Prerequisites

If using ASCM connector stub + cam connector stub, furnish the stubs via soldering.

1) Final ASCM 14-pin connector stub assembled:  

(TBD)

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
    * If using ASCM stub connector, disconnect the 14-pin ASCM connector and plug in the stub connector. Leave the 16-pin connector in ASCM plugged in.
2) Install Gray Panda in OBD II port.
    * Install Gray Panda GPS antenna on windshield.
3) Install EON centered on windshield.
    * Run a USB extension cable from Panda -> nearby EON.
    * Use short mini-usb left-angle USB cable from USB extension -> EON.
4) [Enjoy your first drive!](https://community.comma.ai/wiki/index.php/First_OpenPilot_Drive)

**For more detailed instructions see [Zoneos](https://zoneos.com/volt/)**