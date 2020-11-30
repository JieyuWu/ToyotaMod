### Explanation
The Zorro Steering Sensor (ZSS) is a modification that adds an additional steering sensor in order to improve Open Pilot's (OP) lateral control. The stock sensor on some vehicles are very imprecise. Adding a better sensor provides OP with a much more accurate picture of the state of the steering wheel, thus a much smoother straight-line experience is achieved with this modification.

Under the hood, OP controls steering on a vehicle by sending torque commands to the steering system in order to achieve the desired lane keeping.  On vehicle's with imprecise sensors, the steering commands end up overshooting how much to steer, thus it's easy for a ping-ponging effect to occur going down a straight lane. By improving the sensor, the steering movements become less exaggerated, resulting in a much straighter driving result.

More technical details are available at the github [repo](https://github.com/zorrobyte/betterToyotaAngleSensorForOP)

### Compatibility

* Toyota vehicles with a Driver Support Unit (DSU).
  * This can be further verified by checking [Toyota Parts](https://parts.toyota.com/) and seeing if your vehicle has an 88150-xxxxx part number. (e.g. [example](https://parts.toyota.com/p/Toyota__/COMPUTER-ASSEMBLY---DRIVING-SUPPORT/66837622/8815047110.html))
  * Unfortunately, Camrys DO NOT have DSUs, thus can not have a SDSU added, and the ZSS mod added.
  * Originally, this modification was intended for pre-2018 Priuses.  The 2019+ Prius already has a better steering sensor, so this modification provides marginal improvement.
* It's also used for retro-fitting on certain vehicles that do not have this sensor.

Likely, other DSU based Toyota's are supported if they have the 88150-xxxxx part number.  Check your vehicle:

* [Toyota Parts](https://parts.toyota.com)
* [Lexus Parts](https://parts.lexus.com)

### Purchasing
* ZSS is sold by a community member @erich. [The Ad](https://discordapp.com/channels/469524606043160576/532179801474203649/687679573042921593)
* This is also a side-project for @erich, so availability may be limited.

### Caveats/Considerations

* There's a limited amount of technical support.
* If your vehicle doesn't ping pong down a straight lane, there's little to gain from this modification.
* A [Smart DSU](https://github.com/commaai/openpilot/wiki/Smart-DSU) is required.
* ZSS is only supported via a custom fork. (See first point) [zss_080 branch](https://github.com/ErichMoraga/openpilot/tree/080_zss)

### Installation

Taken from ZSS Ad

1. Remove dust cap from EPS to access shaft to which you adhere a small magnet holder (with 6x2.5mm diametric magnet) using Permatex silicone adhesive or similar (do NOT use super glue).  After initial installation videos, I revised that magnet holder design to have a pointed tip for easier centering.
2. Attach the ZSS sensor (doesn't require adhesive anymore, now that I include an "installation buddy") to the ZSS, as seen in the relevant video.
3. ZSS box can be located wherever you want.  Initial recommendation was on the A/C ducts, but I prefer the driver side ECU compartment, behind the access panel.
4. Connect ethernet cable from DSU/SDSU (uses fake eth. spec 1, to avoid fragmentation across userbase).  Do NOT try connecting to CPv2 directly (if you have a Comma Harness), or via splitter (it's OK if you connect a Pedal that way, though).
5. Load a ZSS-enabled branch to your EON/C2...
```cd /data && rm -rf openpilot && git clone -b 0710_zss https://github.com/ErichMoraga/openpilot && cd params/d && rm -f *aram* && reboot```