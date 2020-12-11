This page is about Volkswagen PQ35/PQ46 platforms. For MQB platform, see [Volkswagen page](https://github.com/commaai/openpilot/wiki/Volkswagen). Usernames are from Discord (User:Name).

There is work in progress on PQ35/PQ46 (November 2020). Currently these cars are being tested:
* Golf Mk6 1.2 TSI DSG (User:Edgy)
* Golf Estate (EU) | Jetta Sportwagen (NA) MK6 2.0 TDI DSG (User:Khonsu)
* Passat B6 R36 (User:Kamold with retrofits from B7, User:Redragon_101)
* Sharan Mk2 7N2 (User:Kubsztal)

# Drive-by-wire capabilities

## Lateral Control (steering)

VW LKAS message (HCA) is used for steering currently, but HCA wont work down to 0 km/h. Gen 3 steering rack should work and SHOULD be possible being retrofited to older vehicles (replacing generation 1 and 2 racks). 

When steering via HCA then after 6 minutes (300 sec) the steering will fail for 3 seconds and then HCA can be resumed again. This timeout can be prevented - after 5.5 minutes terminate HCA message for 1.05 seconds and the 300 sec timeout will reset (counting new 300 period).

There is another steering CAN message being worked on - DSR (Driver Steering Recommendation). This message could help circumvent the timeout of HCA message (using it intentionaly for a while to reset the HCA timeout). DSR should allow for more torque than HCA and possibly replace HCA completely, but that is yet to be explored.

Parking assist can be used for steering up to 20 km/h but is commanded by steering angle rather than torque (as HCA and DSR is). For steering in all speeds a combination of Park assist and HCA/DSR could be used but the transition to/from PA has to be solved (probably nothing quite simple).

Rack part numbers
* 1K0909144E (HCA steering down to 50 km/h, no steering 50-0) - SW2501
* 1K0909144M (HCA steering down to 20 km/h, no steering 20-0) - SW3201
* 1K0909144R (HCA steering down to 20 km/h, no steering 20-0) - SW3501

SW2xxx steers down to 50 kmh. SW3xxx steers down to 20 kmh.

EEPROM of the racks can be accessed over OBD. Rack can be flashed to different ROM (partial FW updates only though). Any SW2XXX can be flashed to R SW3501. Contact Edgy#0385 on discord for flash files.

## Longitudinal Control (gas+brakes)

### Gas

Comma pedal is likely to be used for acceleration on cars not supporting ACC, ACC supported cars can and should be controlled trough mACC_System message on CAN.

### Brakes
Braking should be supported through given ABS pump that has ACC braking capability:
* MK60EC1 H31 or newer for ACC support (part number 1K0907379)
* MK60EC1 H46 for EPB, BSD, RTA and PLA 3.0 support (part number 1K0907379BM)
* Other ABS pumps not yet tested

Currently there is no braking below 15 km/h with MK60EC1 H31+ pump. The MK60EC1 H46 pump which supports EPB should allow braking with ACC messages down till 0 km/h but code has to be written yet.

A car with stock stop&go ACC functionality should naturally be able to brake down till 0 with ACC message.

#### Golf
ACC was not factory fitted to Golf Mk5 and Mk6.

EPB retrofit - it should be able to retrofit EPB to at least Golf Mk6. Following are the parts needed for a Golf Mk6 1.2 TSI DSG:

* MK60EC1 H46 ABC pump (1K0907379BM)
* EPB ECU (56D907801A) - from Chinese VW Magotan
* EPB button (5GG927225)
* Golf Mk7 rear brake calipers (8v0615423 + 8v0615424)
* following may also be needed (depends on your brake disc dimensions etc.):
    * rear brake discs 272 mm (1K0615601AA)
    * front calipers (8v0615124 + 8v0615123)
    * front discs 312 mm (1K0615301AA)
      *Note: Golf Estate | Jetta Sportwagen Mk6 does not need modification to front brakes. Only rear.

#### Passat B6/B7
All B6+B7 had EPB by default. On B6 there was ACC but without F2S (follow-to-stop = braking till 0) and B7 had ACC with F2S. It is possible to retrofit B7 ACC to B6 ([Kamold's Passat B6 retrofit guide](https://www.vwwatercooled.com.au/forums/f234/adaptive-cruise-retrofit-118949.html)) - you should not need to touch the brakes (discs+calipers).

# Possible Retrofits
PQ Vehicles can be retrofitted with allot of the latest MQB features if done in correct order.
The first retrofits to consider if wanting to go to 2015-2017 assist systems:
* 3D Instruments Cluster (This offers support for display of those functions including matching CP items)
* A 2017 ABS pump (For the MK60EC1 abs it requires H46 flashed to CC Firmware)

After this retrofits you can go ahead and retrofit:
* 5Q0 Side assist with Rear Traffic Alert
* 3Q0 Lane assist with Sign Assist and High Beam Assist
* 7N0 Adaptive Cruise Control
* Park Assist 3.0

It's also possible to not retrofit some one those newer MQB assists but the Passat B7 assists this may be possible after checking some requirements. An overview of systems you could possibly retrofit:
* 3AA Adaptive Cruise Control
* 3AA Lane Assist with Sign Assist and High Beam Assist
* 3AA Side Assist
* Park Assist 1.5 and with a supported ABS Park Assist 2.0

# Code

There are various OpenPilot forks tuned for particular PQ platforms.

### PQ35

Discord user Edgy (Golf Mk6): https://github.com/CineXWorm/openpilot (which branch to use?)

### Passat

#### Guide by Discord user Redragon_101

2010 Passat B6 PQ46 with factory ACC on powertrain setup for OP with White Panda.

J533 Harness pinout:

All connections are made by taps. ie make a 3 way junction, no need to cut wires.

Example: gateway pin6, vehicle pin6, and Panda pin 14 should all be wired together
* Pin 14 on Panda goes to 6 of J533 harness
* pin 6 on Panda goes to 16 of J533 harness
* pin 4 on panda goes to 11 of J533 harness
* pin 16 on panda goes to 1 of J533 harness
* pin 8 on panda goes to 14 of J533 harness

1. Install jyoungs8607 0.7.4 vw-community-private-pq branch onto EON.
2. Add your fingerprint of your car by using Workbench. This program has a Get fingerprint command built in and add it into 
  /data/openpilot/selfdrive/car/volkswagen/values.py of the EON using WinSCP or similar.
3. Using WinSCP log into the EON and find /data/openpilot/selfdrive/car/volkswagen/interface.py
4. Find this line:  https://github.com/jyoung8607/openpilot/blob/6201db04268c930f30ed025b9e0851ae7248eaeb/selfdrive/car/volkswagen/interface.py#L113
5. comment it out and add a line below saying ret.canValid = True
6. Reboot EON and take it for a test drive.   Hope this helps someone out.

# Diverse notes

Extended CAN is defined for PQ since the very beginning and is still used in today’s PQ verhicles (Caddy, Sharan, Alhambra). MQB and PQ have completely different CAN messaging schemes which can’t be mixed. But there do exist units that can be corded to either PQ or MQB (e.g. 3Q0 camera, 5Q0 side assist radar, many PLA units, ...) The manufacturer simply programmed both messaging schemes (PQ or MQB) selectable. Thus the same partnumber can be used on either platform. That’s probably why people talk about a PQ-MQB-mix which is technically very wrong. Either the unit is in PQ mode or in MQB mode. (by carlos_ddd)