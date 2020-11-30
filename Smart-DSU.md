### Explanation
The SmartDSU (SDSU) is used to provide longitudinal control on Toyota vehicles that otherwise do not have Openpilot (OP) supported longitudinal control.

Depending on the vehicle, OP will run in one of the following modes:

* OP controls longitudinal (gas/brake) & lateral (steering)
* OP controls lateral (steering) only.

In vehicles where OP controls lateral only, OP relies on the vehicle's adaptive cruise control (ACC) for longitudinal control. It is possible to disconnect the DSU unit on some Toyotas to enable OP longitudinal, however this comes at the expense of disabling automatic emergency braking (AEB). The SDSU is installed between the DSU & DSU harness connector. It filters the traffic between the DSU & powertrain CAN bus thus enabling longitudinal control without removing AEB.

More technical explanation is available at the github [repo](https://github.com/wocsor/panda/tree/smart_dsu)

### Compatibility

* Toyota vehicles with a Driver Support Unit (DSU).
** This can be further verified by checking [Toyota Parts](https://parts.toyota.com/) and seeing if your vehicle has an 88150-xxxxx part number. (e.g. [example](https://parts.toyota.com/p/Toyota__/COMPUTER-ASSEMBLY---DRIVING-SUPPORT/66837622/8815047110.html))
* Unfortunately, Camrys DO NOT have DSUs, thus can not have a SDSU added, thus they will only work in lateral mode only.

Some cars that are supported:

|   Year   |   Model   |
|:----     |   :----   |
|2017-2019 |Corolla    |
|2016-2018 |Rav4       |
|2016-2018 |Rav4 Hybrid|
|2016-2020 |Prius      |
|2017-2020 |Prius Prime|
|2017-2019 |Highlander |
|2018-2019 |Sienna     |

Likely, other DSU based Toyota's are supported if they have the 88150-xxxxx part number.  Check your vehicle:

* [Toyota Parts](https://parts.toyota.com)
* [Lexus Parts](https://parts.lexus.com)

### Versions & Purchasing
There are 2 versions around the community:

* One available via a Chinese seller on [Taobao.com](https://item.taobao.com/item.htm?spm=a312a.7700824.w4004-21830160926.16.4f167c33SU8Tfg&id=624782255202) for around ~$125 shipped.  Install the Google Translate extension to navigate the site.  People also purchase through superbuy.com.  For US buyers, purchasing directly from Taobao is a 2 part process:
  * Purchase item from taobao.com
  * Wait 2-3 days for item to ship to an intermediary.  Navigate to the taobao page to pay the intermediary ~$15 for them to ship item to the US.
* Another developed by community member @erich named [Smartened DSU](https://discord.com/channels/469524606043160576/532179801474203649/687669433145229385).  This is definitely slicker, as the SDSU is integrated into the DSU casing, thus maintaining a stock appearance. However it is generally unavailable as this is a temporary project for @erich, however his features include everything the SDSU has plus the following:
  * Switch mode to change between regular DSU & SDSU mode (for when the car goes to the dealer)
  * Soldered on cat6 cable for comma-pedal & Zorro Steering Sensor installation.

### Installation

Upon locating the DSU, install the SDSU between the DSU and its connector.

TODO: Add links to locations for various DSUs on various vehicles:

* Lexus IS (US): DSU is located above the driver's right knee when seated in the driver's seat. 
* Toyota Corolla: Through the glove box behind the head unit.

After the SDSU is installed, some may also need to connect the SDSU to a Comma Pedal for some vehicles that do not provide stop and go with a SDSU only setup.

If a [ZSS](https://github.com/commaai/openpilot/wiki/Zorro-Steering-Sensor) also needs to be installed, this [splitter](https://www.amazon.com/gp/product/B07NYWKJS9) also allows ZSS + Pedal to be installed.

#### Installation - Comma Pedal w/ SDSU

The Pedal needs access to power and the CAN bus.  While the Pedal can be connected to power and CAN via the ODB-II port, the DSU provides the additional benefit of providing ignition-controlled power so that the pedal does not drain the car's battery when the car is off.