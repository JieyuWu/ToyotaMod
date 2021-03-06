![VW](https://user-images.githubusercontent.com/37757984/82105487-5ca67c00-96d0-11ea-80ef-ba6bbff61d2a.jpg)

[◄ Home](https://github.com/commaai/openpilot/wiki)

**This brand is community supported. Enable it with the toggle in Settings->Developer->Enable Community Features.**

# Overview
Comma AI currently has no official support for Volkswagen brands besides certain Golfs, but a community port is available, with plans to upstream for official support in the near future. The community port is designed to support any Volkswagen MQB vehicle with ACC radar. Check the Vehicle Support section for details and caveats. For more detailed information ask at #volkswagen on comma.ai Discord.

This article is about MQB platform. There is a development going on for the PQ platform - for more information see [Volkswagen PQ](https://github.com/commaai/openpilot/wiki/Volkswagen-PQ).

# Supported Vehicles

<details><summary>Fully Tested and Supported</summary>
<p>

These vehicles are confirmed supported by the community Volkswagen port, because they have been tested on at least one representative car in the wild. Both automatic and manual transmissions are supported.
The vehicle must have ACC (radar-based cruise control).
For vehicles without factory Lane Assist, a custom harness (Dream Harness - integrates at J533) will be required to use modern Comma Two hardware, and a diagnostic tool (VCDS/OBD11/etc.) will be needed to make minor coding changes to the steering rack in order for OP to steer, and coding changes to the instrument cluster will be needed to receive feedback and status information.
- 2012-2019 Mk3 Audi A3 (tested variants only) [Wiki]
	- A3
	- A3 e-tron
- 2014-current Mk3 Audi TT / TTRS [Wiki]
- 2017-current Mk1 Audi Q2 [Wiki]
- 2018-current Mk2 Audi Q3 [Wiki]
- 2016-current Mk1 SEAT Ateca [Wiki]
- 2013-current Mk3 Škoda Octavia [Wiki]
- 2019-current Mk1 Škoda Scala [Wiki]
- 2015-current B8 Škoda Superb [Wiki]
- 2018-2019 Mk1 Volkswagen Atlas (Teramont in some markets) [Wiki]
- 2012-2019 Mk7 and Mk7.5 Volkswagen Golf (tested variants only) [Wiki]
	- Please note the MY changeover from Mk6 to Mk7 varied by market, USA did not get Golf 7 until MY 2014!
	- e-Golf
	- Golf
	- Golf GTE (sport hybrid)
	- Golf GTI
	- Golf R
- 2019-current Volkswagen Jetta (except GLI) and Sagitar (Mk7) [Wiki]
	- The GLI variant is architecturally compatible, but factory ACC appears unavailable (thanks for nothing VW)
- 2015-current B8 Volkswagen Passat [Wiki]
	- This is NOT the Passat currently available in North America, which is based on the currently unsupported NMS platform
- 2015-current Mk2 Volkswagen Touran [Wiki]
</p>
</details>

<details><summary>Supportable but Untested</summary>
<p>

These vehicle-classes should work fine with openpilot, to the best of our information, but have not yet been tested. Minor tweaks or other support may be needed. Be cautious if making an openpilot or vehicle purchase decision based on this information. If in doubt, ask on Discord.
- All MQB vehicles not listed above, with ACC radar
	- 2012-current Mk3 Audi A3 variants not explicitly tested so far
		- Audi S3
		- Audi RS3
	- 2012-current Mk3 SEAT León [Wiki]
	- 2019-current Mk1 SEAT Tarraco [Wiki]
	- 2019-current Mk1 Škoda Kamiq [Wiki]
- 2017-current Mk1 Škoda Karoq [Wiki]
	- 2017-current Mk1 Škoda Kodiaq [Wiki]
	- 2018-current Mk1 Volkswagen Arteon [Wiki]
	- 2018-current Mk4 Volkswagen Bora [Wiki]
	- 2013-2019 Volkswagen Golf variants not explicitly tested so far (Mk7 and Mk7.5) [Wiki]
		- Golf Alltrack
		- Golf GTD (sport diesel)
		- Golf GTI TCR
		- Golf Sportsvan / SV
		- Golf SportWagen
	- 2017-current Mk2 Volkswagen Crafter [Wiki]
	- 2015-current Mk1 Volkswagen Lamando [Wiki]
		-Made in China, limited info available, unable to fully verify
	- 2018-current Mk3 Volkswagen Lavida [Wiki]
		-Made in China, limited info available, unable to fully verify
	- 2018-current Mk1 Volkswagen Tayron [Wiki]
		-Made in China, limited info available, unable to fully verify
	- 2016-current Mk2 Volkswagen Tiguan [Wiki]
		-In North America, all 2016-2017 Tiguans and the 2018 Tiguan "Limited" are still Mk1 PQ46 Mk1 (see PQ46 below); all other 2018 and all 2019-forward are MQB Mk2
	- 2018-current Mk1 Volkswagen Tharu / Tarek [Wiki]
		-Made in China, limited info available, unable to fully verify
</p>
</details>

<details><summary>Long Term Roadmap</summary>
<p>

We think these vehicles can be supported at some point, but they are not supported just yet. Code changes will be required. There are no firm dates for any of these items. If you have a vehicle in this section and are interested in testing with openpilot, please ask on Discord before proceeding.
- Longitudinal control using visiond to drive known ACC messaging, for vehicles without radar. It's not yet known specifically what retrofits we'll need for vehicles with cruise control only, but we'll probably need to change out the steering wheel buttons or control stalk as applicable.
- All MQB-A0 vehicles. We think these SHOULD work, but ran into unknown issues with the ones we tested and were not able to complete troubleshooting with the owners. Contact us on Discord if you have access to a legitimate VCDS interface for diagnostics and are interested in trying. Especially if you have factory LKAS.
	- 2018-current Mk2 Audi A1 [Wiki]
	- 2017-current SEAT Arona [Wiki]
	- 2017-current SEAT Ibiza [Wiki]
	- 2018-current Mk6 Volkswagen Polo [Wiki]
	- 2019-current Mk1 Volkswagen T-Cross [Wiki]
- All PQ35/PQ46/NMS vehicles. We hope and plan to provide some level of official support in the long-term future, and we are having good success in early testing. Vehicles in this set may or may not be supportable. Most if not all should have electric power steering racks, but earlier vehicles may or may not have configurable support for Lane Assist commands. Do not purchase a vehicle based solely on this list.
	- PQ35: https://en.wikipedia.org/wiki/Volkswagen_Group_A_platform#PQ35_(A5)
	- PQ46, including New Midsize Sedan (NMS): https://en.wikipedia.org/wiki/Volkswagen_Group_B_platform#PQ46_(A6)
- All MLB and MLBevo vehicles (requires FlexRay support, VERY long term future)
	- 2018-current Volkswagen Touareg
	- All modern Audi not listed as MQB: A4, A5, A6, A7, A8, R8, Q5, Q7, Q8, e-Tron SUV and all variants thereof
- All MEB (new electric mass-market platform ID3,ID4,...) vehicles, big question marks here until we see one, but we have cautious optimism.
- All MQBevo vehicles (the new Golf Mk8 and all future refreshed MQBs), big question marks here until we see one, but we have cautious optimism.
- All New Small Family (NSF) vehicles, supportability status totally unknown at this time. Contact us if you are interested in testing and you have a legitimate VCDS interface for diagnostics and settings changes.
	- 2011-current SEAT Mii [Wiki]
	- 2011-current Škoda Citigo [Wiki]
	- 2011-current Volkswagen Up! [Wiki]
</p>
</details>

<details><summary>Unsupportable</summary>
<p>

These vehicles either don't have electric power steering, or we don't have a known control channel, or there is no factory option or ability to retrofit the necessary ACC and steering components. Support could be reexamined if new information comes to light, but at this time we have no plans to investigate further.
- Volkswagen Touareg prior to 2018 (hydraulic power steering, lane departure warning only via steering wheel haptic)
- Volkswagen Phaeton (hydraulic power steering, lane departure warning only via steering wheel haptic)
- NSF (New Small Family) supermini models without factory options for ACC or LKAS.
</p>
</details>

# What to buy for MQB vehicles
Purchasing the comma two (c2) is the easiest way to get started. It is also possible to build your own eon and save some $$.

## If your car has LKAS & ACC
1. [comma two DevKit](https://comma.ai/shop/products/comma-two-devkit)
2. Select MQB Development Harness
<sub><sup>(VW Golf and MQB development car harness's are the same)</sup></sub>

## If your car only has ACC
1. [comma two DevKit](https://comma.ai/shop/products/comma-two-devkit)
2. Make your own [VAG J533 Harness](https://github.com/commaai/openpilot/wiki/VW-j533-cable). There's also a Dream Harness made in a Chinese factory thanks to Saber422#9277. Currently it's a group buy, so if you are interested, ask in the Discrod.
3. Recode the steering rack and instrument cluster to believe the car has lane assist (this allows lateral control via CAN messages to the steering rack). Use VCDS to modify control module 17 (instruments) and module 44 (steering assist). See this [video](https://www.youtube.com/watch?v=XSzJU31zXuE) for instructions.

## If your car has neither ACC nor LKAS

This has not been explored very much yet. Theoretically, you could retrofit ACC ([example guide](https://mqb.pl/en/adaptive-cruise-control-retrofit-acc-on-mqb/)) and then continue as "If your car only has ACC". It may also be possible just to do the coding of other parts for ACC (according to mqb.pl article) without the physical radar. However, this has not been tried and it is possible that an ACC fault will arise from the missing radar and other parts (engine, brakes) would stop responding to ACC commands.

# Installing the Community Port

### Black Panda / Comma Two / Grey Panda 
To run the Community port, you MUST [install stock openpilot](https://github.com/commaai/openpilot/wiki/Installing-openpilot#install-openpilot) first. 

> Newer C2 ship with NEOS 15. You must have NEOS 14 for the Community port to work. To downgrade use the following command via SSH:
cd /data && rm -rf openpilot && git clone -b release2 https://github.com/jyoung8607/openpilot && cd /data/openpilot/installer/updater && rm update.json && wget https://cdn.discordapp.com/attachments/538741329799413760/774123747257876480/update.json && reboot


**Automatic URL Install**
(currently broken due to the NEOS update - use the method above until the fork is updated)  
If you're at the EON/Comma Two installer prompt and it's asking for a download URL, then use `https://volkswagen.opcfork.org/` instead of the comma URL. Continue the install using the normal methods and instructions. 

**Manual Install**  
Alternatively, you can install the Community Port manually. Enable developer and SSH in the setting menu. Then, [connect via SSH](https://github.com/commaai/openpilot/wiki/SSH) and run the following command:  
  
`cd /data && mv openpilot backup-openpilot && git clone https://github.com/jyoung8607/openpilot.git -b release2 && reboot`  

**Integration Location**  
Once installed, C2/BP owners default to integrating at the camera(official comma harness), grey Panda owners default to integrating at the gateway(Dream Harness/J533). If this isn't what you have, you need to SSH in and do the following as appropriate for where you are wired:  
  
`echo -n "gateway" > /data/params/d/ForceNetworkLocation`
or
`echo -n "camera" > /data/params/d/ForceNetworkLocation`  
 

### White Panda
If you are using a white panda, you will have to run the last compatible version of openpilot: 0.7.4. In order to do this, run the following command to install 0.7.4 with white panda support:

`cd /data && mv openpilot backup-openpilot && git clone https://github.com/jyoung8607/openpilot.git -b vw-community-devel && reboot`

# openpilot Capabilities

## Lateral Control
Control over the steering wheel is provided by openpilot. All MQB vehicles tested to-date support steering down to 0mph.

### Torque
Available steering torque is adequate for most highway driving conditions. All MQB models support the exact same amount of commanded torque, but the different steering rack and suspension geometry between models can result in different effective performance. 

[Torque Demonstration video](https://www.youtube.com/watch?v=8TZAY3am8E4)
### Minimum Speeds
The minimum ACC setpoint is 20mph/30kph. 

## Longitudinal Control
Longitudinal control remains with stock ACC, although OP takes control of the engagement process for additional safety and feature needs. The exact behavior depends on whether the vehicle has "ACC High" or "ACC Low" from the factory.

[Stop & Go Demonstration video](https://www.youtube.com/watch?v=Il5zqZj2-58)

### Stock ACC High: 
These vehicles support follow-to-stop and automatic resume if the stop is less than three seconds, from the factory. OP can improve on that by resuming on behalf of the driver after longer delays by emulating repeated RES presses at standstill. "ACC high" requires an electronic parking brake, and does make use of it under certain conditions. If the vehicle in question has an EPB, chances are good it supports "ACC high".

### Stock ACC Low: 
These vehicles generally support follow-to-stop (XXX review this: maybe near-stop only) but will require the driver to take over and hold the brake after a very short delay. Resume from stop is moot as "ACC low" vehicles will not hold themselves at a stop. Any vehicles with a manual parking brake, either foot or hand-operated, will fall into this category.

# PQ platform

See [Volkswagen PQ](https://github.com/commaai/openpilot/wiki/Volkswagen-PQ) page.

# Make-Specific Terms

For general terms, [go here](https://github.com/commaai/openpilot/wiki/General-Terms).

Term | Abbreviation | Definition
--- | --- | ---
Modularer Querbaukasten / Modular Transverse Matrix | MQB | Strategy for shared modular design between VAG group makes and models. MQB cars with ACC work with Openpilot.
Electronic Parking Brake | EPB |  A handbrake system powered by electric motors. [Wiki](https://en.wikipedia.org/wiki/Electronic_parking_brake)
Component Protection | CP | Component Protection is required on some newer parts to unlock them in working in that vehicle.
Adaptive cruise control | ACC| Control of the speed of the car; usually through use of radar in factory systems
Longitudinal| long | basically ACC but usually in the OP context
Lateral | lat| Control of the steering wheel
Lane keep assist| LKAS | Same as lat but usually in the context of the factory system
jyoung8607 | jyoung | First to make OP work in VW
Edgy | Edgy | First to make OP long work in VW PQ

# Useful links

* [Adaptive Cruise Control retrofit – ACC on MQB](https://mqb.pl/en/adaptive-cruise-control-retrofit-acc-on-mqb/)
* [Tutorial – Retrofiting Lane Assist | Sign Assist | Light Assist – 5Q0980653](https://mqb.pl/en/tutorial-retrofiting-lane-assist-sign-assist-light-assist-5q0980653/)

# Known issues / FAQ

-Set point creep: On cars where the RES button increases the cruise speed set point by 1, the set point will often go up, especially when the car in front is already moving but we aren't moving yet. Will probably be fixed in a future update by incorporating ["ESP_21"]['ESP_Haltebestaetigung'] as a condition for emulating RES presses when at a standstill.

-Radar/Vision Fusion for OP long control: Unlike some other cars, MQB cars don't give much raw Radar data. Because of this the radar fusion won't be as easy. Once OP long control is as reliable as stock radar based ACC it can still be implemented.

-Fingerprinting: On VW cars we currently only use FPv1. The current V2 is WIP.