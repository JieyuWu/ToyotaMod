![Nissan](https://user-images.githubusercontent.com/37757984/82703105-2913a680-9c28-11ea-8130-ce67221dd568.png)

[◄ Home](https://github.com/commaai/openpilot/wiki)

**This brand is community supported. Enable it with the toggle in Settings->Developer->Enable Community Features.**

# Install Locations

The Nissan harness needs to be plugged into the ADAS module (NOT the lane keep assist camera). This module can be in a wide range of locations, which is why the Nissan harness ships with a 3 meter USB-C cable.

Below are locations the community has found for their cars. Please note, if your car isn't below you will need to locate the ADAS module. Join others on [discord.comma.ai](https://discord.comma.ai) in the #nissan channel to get tips and tricks. [Techinfo](https://www.nissan-techinfo.com/) can help.

## Leaf 2018-20

There are two known locations. Check your glovebox first as this is really easy to access compared to the instrument cluster. Below are confirmed locations. Please keep it up to date.

**Glovebox**
* Everything else

**Instrument Cluster**
* 2nd Zero Edition (01/18 - 02/18)

### Glovebox
![image](https://user-images.githubusercontent.com/37757984/94322928-da18ad80-ff48-11ea-9aaa-b4fde9783a7f.png)

It is just above the glove box location once removed. The picture is taken with the camera pointed up into the cavity - not directly head on. To access the glovebox remove the screws, directly above and below the glovebox. You can then gently pull the glovebox out and access everything needed behind it.

### Instrument Cluster
To access the instrument cluster you can follow this video [https://youtu.be/gkA1WDu8cq0](https://youtu.be/gkA1WDu8cq0). You do NOT need to disconnect the instrument cluster itself as shown in the video. Just put it to the side. The cable is long enough. 

The ADAS module is on the right side as marked by the arrow. Pay extra attention as the adapter marked with the X also fits the nissan leaf car harness provided by comma ai.

![image](https://razem.io/blog/20/12/19/OpenpilotNissanLeafICPart1/assets/leaf_ic_instruction.jpg)

With the instrument cluster out of your way, you can also remove the screw shown below. Which should then give easy access to the adapter.

![image](https://razem.io/blog/20/12/19/OpenpilotNissanLeafICPart1/assets/leaf_ic_ads.jpg)

## Rogue 2018-19
![image](https://user-images.githubusercontent.com/37757984/94323035-2368fd00-ff49-11ea-8b42-3fc9c40cf2cb.png)

There is no need to disassemble anything. Remove the luggage floor cover, and expose the spare tire. The ADAS can be reach by hand, and the harness wire disconnects with minimal effort. This may require a [USB-C 3.1 Gen 2 extender](https://www.amazon.com/gp/product/B07KK9QXPM/) to reach the comma device.

![image](https://user-images.githubusercontent.com/37757984/94323063-3bd91780-ff49-11ea-8637-7a4ca4745b0c.png)

# Make-Specific Terms

For general terms, [go here](https://github.com/commaai/openpilot/wiki/General-Terms).

Term | Abbreviation | Definition
--- | --- | ---
ProPILOT | | Nissan's driver assistance system

# openpilot Capabilities

## Lateral Control

Control over the steering wheel.

### Torque

Nissans have great torque, and can take most turns in normal driving situations.

### Minimum Speeds

Nissans control the wheel down to 0mph.

## Longitudinal Control

Control over the gas and brakes.

Longitudinal control is provided by the stock system that came with the car.