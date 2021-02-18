# Comma 2
By far the most common device that can run openpilot is currently the Comma 2. Here are some basics about how it works. 

## Average ADAS architecture
Let's first take a look at the architecture of an average car's ADAS (advanced driver assistance system). 

![Drive not working](https://docs.google.com/drawings/d/e/2PACX-1vRJvj_ssim7KSOgPG5onb-GFgVqQoSaLpz257PikgjywXXRFtbZXgh60rbn1NRCKy-1E_qXy6_1LwUx/pub?w=1440&h=1080)

The ADAS ususally controlls many safety systems but the most important for us are lane keep assist (LKA, keeps the vehicle in the lane) and adaptive cruise control (ACC, cruise control that adjusts your speed so you don't hit a car in front). The ADAS system achieves it's goals by communitacing with the engine, gearbox and power steering system via CAN (controller area network) which is a standardized way of connecting different control units in the car, so they can communicate. When lane keep assist and adaptive cruise control are active ADAS will take the images from the road, process them and output the commands to keep the car at the correct speed and direction by talking to the engine control unit to potentially accelerate, braking system to brake or power steering system to steer the wheel.

## Comma 2 architecture
### Replace ADAS with Comma 2
In order to use Comma 2 to control the vehicle's steering and acceleration, we unplug the ADAS system and plug in a Comma 2 device. Comma 2 has its own camera so it is capable of controlling the car without the help of the ADAS system. We therefore connect the Comma 2 to the CAN network so that it can send out simmilar packages as the ones the car expects from the ADAS system. 

![Google draw images have dissapeared from google drive](https://docs.google.com/drawings/d/e/2PACX-1vS4Frd-M-_aoWRS8e6puBxHpKmfkUDSn5bbYmGqcLqIeqEqxL__deSa_07j68AS3C7JjLbsoZfOw524/pub?w=1440&h=1080)

### Combining Comma 2 and ADAS
Since ADAS systems in modern cars have many safety features other than lane keep assist and adaptive cruise control, we'd like to give back some ability to control the car back to the ADAS system. We do that with the comma harness. Comma harness will allow the Comma 2 to control the LKA(lane keep assist) and ACC(adaptive cruise control) systems, while the ADAS can still keep operating all of the other important safety features, for example pedestrian protection, automatic emergency braking and so on. 

![Google draw images have dissapeared from google drive](https://docs.google.com/drawings/d/e/2PACX-1vSGxZv4ar2tKiM4mSH-FXteSBHIQJayAc4LD5ag3Trt30VkCgSLDmho0qu8t0_cbhxxS6FIGlZW-_QM/pub?w=1440&h=10800)

### Looking at the whole setup
The Comma 2 device is composed of two main components: the phone ([LeEco Le Pro3](https://www.gsmarena.com/leeco_le_pro3-8344.php)) and the Comma Panda. The phone is responsible for running the whole openpilot code and sending out the signals the car needs to accelerate, brake and steer. The signals get transmitted from a phone to the Panda which has a task of sending them to the Comma harness so they can be sent to the rest of the car. The Panda also has an important role of deciding which signals from the ADAS should not be let through to the rest of the car. Panda has to filter the signals associated with LKA and ACC, so that the Comma 2 device can perform those actions without interference. 

![Google draw images have dissapeared from google drive](https://docs.google.com/drawings/d/e/2PACX-1vQtREgh4GEliSrNfforQ9ts1vdtpmsmXxi3iSo79L8McjANwqjpvi2J6cy__N7AWgG06DPkandecPts/pub?w=1440&h=1080)

