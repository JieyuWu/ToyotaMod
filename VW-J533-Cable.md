[◄ Home](https://github.com/commaai/openpilot/wiki) / [◄ Volkswagen](https://github.com/commaai/openpilot/wiki/Volkswagen)

[REF link; some info may be outdated, links may go dead](https://community.comma.ai/wiki/index.php/J533_Sniffing_Cable)

**note, there is often confusion between whether connectors are referred to by the housing gender or the pin gender. Throughout this document connectors are referred to by pin gender, thus the red J533 connector, despite being a 'plug' is a female connector because the individual contacts are female sockets**

The role of the Gateway (also known J533) is the exchange of data between the CAN data bus systems ('powertrain CAN data bus,' 'convenience CAN data bus' and 'infotainment CAN data bus') and the conversion of diagnostic data from CAN data bus systems. This is a central point where openpilot can intercept data to understand the car's state, and manipulate and insert data to impersonate the lane departure warning system to provide lateral control.

![j533_vw](https://user-images.githubusercontent.com/61742003/87466641-a0d8ce80-c5e4-11ea-8030-c28e031b9d5e.png)

## OBD j533 (White or Gray Panda)
![J533_Ver3 1_2019 11 20](https://user-images.githubusercontent.com/61742003/87466638-a0d8ce80-c5e4-11ea-9a8d-9346a46cb4f4.png)

1. [Gateway Extension Adapter](https://www.aliexpress.com/item/4000334862080.html)
2. [OBD Female Connector w/ Wires | check eBay/Aliexpress](https://www.ebay.com/itm/16-Pin-J1962-OBD2-OBDII-OBD-Female-Connector-Diagnostic-Cable-VEHICLE-SIDE-B155/183783394862)
3. 60 ohm Resistor (5w or less)
4. Cloth electrical harness tape


## panda relay J533 (Black Panda for Comma Two)
![j533 black panda](https://raw.githubusercontent.com/actuallylemoncurd/photo/main/BP%20diagram%20final.png)

A source of some confusion is which direction data flows. In summary, the critical connection is for openpilot to intercept pins 7/17 of the J533 connector. The comma relay 'man-in-the-middles' the flow of data down the VW "extended can bus" (7/17 on the J533 connector). It's easy to wire it the wrong way around. 

Data from pins 7/17 comes into CAN2 of the blackpanda from the socket end of the Aliexpress harness, gets manipulated by openpilot to add steering commands, and then is sent out CAN0 of the black panda to the J533 gateway via the red plug of the Aliexpress harness. CAN0 and CAN2 are electrically connected together when the relay is operating in passthrough mode. So CAN0 should be connected to the red plug and CAN2 should be connected to the black socket. 

1. [Gateway Extension Adapter](https://www.aliexpress.com/item/4000334862080.html)
2. [MQB Development Harness](https://comma.ai/shop/products/comma-car-harness)
3. Cloth electrical harness tape
4. Electrical connectors (butt splices if you're brave or DSUB pins/sockets if you are non-committal) 

## wp/gp/bp J533 harness diagrams together
![j533 harness diagrams together](https://raw.githubusercontent.com/actuallylemoncurd/photo/main/BPWPGPdiagram.png)

![j533 cable location](https://cdn.discordapp.com/attachments/534359517836607488/667975270749306890/image0.jpg)
Lay on your back in the driver's footwell with a torch. Get as close to the firewall as possible. Look up. You will see a red connector. This is the J533 connector. It is plugged into the J533 CAN gateway