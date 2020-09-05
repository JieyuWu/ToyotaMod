## Configuration Variations ##

![](http://justine-haupt.com/bolt/images/openpilot_BoltConfigurations.png)

To contribute to the above diagrams, download the [.svg file](http://www.justine-haupt.com/bolt/images/openpilot_systemdiagram.svg) and use Inkscape. The .svg file also includes a bunch of "general case" diagrams for openpilot not specific to the Bolt, but they may contain errors.

## Comma 2 ##
The Comma 2 has an onboard Panda and removes the need for the Giraffe by connecting directly to the car's buses.  To do this, you'll need a harness modified to connect properly to the right buses:

![Comma2 Harness Wiring](https://i.imgur.com/QGDNHLQ.png)
[Link to the Diagram on EasyEDA](https://easyeda.com/editor#id=76ac44b218d640e2bd9da8de83d87195)

To build this yourself you'll need the following parts:
1. [Male LKAS Connector](https://www.digikey.com/products/en?keywords=34825-0124%20)
2. [Female LKAS Connector](https://www.digikey.com/products/en?keywords=%2034824-0124)
3. [At least 12 crimp sockets for the Female Connector](https://www.digikey.com/product-detail/en/molex/5600230548/WM16762CT-ND/7428700)
4. 22-24 AWG wire.  Recommend PVC for abrasion resistance.
5. [Comma Dev Harness Wires](https://comma.ai/shop/products/comma-car-harness) (select Development Vehicle, only need a Black Panda if you have an Eon) or 6 & 7:
6. [26-socket Connector](https://www.digikey.com/products/en?keywords=5016462600)
7. [At least 18 crimp sockets](https://www.digikey.com/product-detail/en/molex/5016471000/WM6057CT-ND/1787797)  

To assemble, you'll need a crimping tool and a soldering kit.  Crimp the sockets onto the wires for the female connectors and insert to the proper slots.  Solder the wires to the male connector, wire directly to exterior pins. I shrink-wrapped the solder joints and I plan to reinforce the pins / solder joints with epoxy resin once I'm sure no more solder modifications are needed.

To connect the Comma Pedal we think you can tap into the ethernet run for the Comma Power using an ethernet splitter and extend it to the pedal.  (This configuration is untested on the Bolt).

## Pedal Interceptor ##
* Gerber files and BOM available [here](http://www.justine-haupt.com/bolt/pedalfab/)
* The vehicle-side TPS connector is [BWD P/N PT977 (AKA S-1478)](https://shop.advanceautoparts.com/p/bwd-electrical-connector-pt977/10433652-P?utm_medium=ymme)
* J. Shuler's 3D model for printing the mating connector housing for the TPS connector is [here](https://www.tinkercad.com/things/em6XUplxMTj). If you don't feel like making an Autocad account, the STL can be downloaded directly [here](http://justine-haupt.com/bolt/pedal_Mechanical/BoltMaleTPSConnectorHousing_jshuler.stl)
* The Pedal Interceptor wiki is [here](https://community.comma.ai/wiki/index.php/Comma_Pedal)
* Instructions for the initial installation of the firmware are [here](https://medium.com/@jfrux/flashing-the-comma-pedal-with-ubuntu-a83fb668f6e2)

## Installing firmware, updating, etc ##
This is the official wiki for configuring. Use the instructions to ssh into the Comma2 or Eon: [Configuring_OpenPilot](https://community.comma.ai/wiki/index.php/Configuring_OpenPilot)

(From Felger:) The first time you install a new fork that uses submodules (e.g. Panda or Pedal) you need to run:

`git submodule init`

`git submodule update`

Then to change panda code, for example, run
`pkill -f boardd`
Then in /data/openpilot/panda/board run
`make`


Wiring the comma.ai Pedal Interceptor for the Chevy Bolt:
![](http://justine-haupt.com/bolt/images/PedalBoltWiringDiagram.png)

## Alternate Single-Side Pedal Interceptor ## 
*This version is only slightly longer and has a much larger test point for entering DFU/programming mode*
* KiCad design files, Gerber Files and BOM available [here](http://justine-haupt.com/bolt/singlesidepedal/)
* The vehicle-side TPS connector is [BWD P/N PT977 (AKA S-1478)](https://shop.advanceautoparts.com/p/bwd-electrical-connector-pt977/10433652-P?utm_medium=ymme)
* J. Shuler's 3D model for printing the mating connector housing for the TPS connector is [here](https://www.tinkercad.com/things/em6XUplxMTj). If you don't feel like making an Autocad account, the STL can be downloaded directly [here](http://justine-haupt.com/bolt/pedal_Mechanical/BoltMaleTPSConnectorHousing_jshuler.stl)
* The Pedal Interceptor wiki is [here](https://community.comma.ai/wiki/index.php/Comma_Pedal)
* Instructions for the initial installation of the firmware are [here](https://medium.com/@jfrux/flashing-the-comma-pedal-with-ubuntu-a83fb668f6e2)

## Modding the EON ##
(Coming soon)


## Adding IR LEDs for improved night performance ##
(Coming soon)

## Info on an abortive effort to get OpenPilot running on an SBC ##
[Installing OpenPilot on an NVIDIA Jetson Nano](https://github.com/commaai/openpilot/wiki/Installing-OpenPilot-on-an-NVIDIA-Jetson-Nano)

## References ##
Giraffe Info:
[Gerber files](http://www.justine-haupt.com/bolt/giraffefab/)
[Parts list](http://www.justine-haupt.com/bolt/giraffeparts/)
[J. Shuler's design page](https://easyeda.com/jshuler/chevy-bolt-openpilot-giraffe-rev-3)
