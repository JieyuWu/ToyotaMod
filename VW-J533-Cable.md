[◄ Home](https://github.com/commaai/openpilot/wiki) / [◄ Volkswagen](https://github.com/commaai/openpilot/wiki/Volkswagen)
# Introduction
If you don't have LKAS (lane keeping assist aka lane departure warning) then you need to interface with your car at the J533 CAN gateway under the steering wheel. The role of the Gateway (also known J533) is the exchange of data between the CAN data bus systems ('powertrain CAN data bus,' 'convenience CAN data bus' and 'infotainment CAN data bus') and the conversion of diagnostic data from CAN data bus systems. This is a central point where openpilot can intercept data to understand the car's state, and manipulate and insert data to impersonate the lane departure warning system to provide lateral control.

A source of some confusion is which direction data flows. In summary, the critical connection is for openpilot to intercept pins 7/17 of the J533 connector. The comma relay 'man-in-the-middles' the flow of data down the VW "extended CAN bus" (7/17 on the J533 connector). It's easy to wire it the wrong way around. 

Data from pins 7/17 comes into CAN2 of the blackpanda from the socket end of the Aliexpress harness, gets manipulated by openpilot to add steering commands, and then is sent out CAN0 of the black panda to the J533 gateway via the red plug of the Aliexpress harness. CAN0 and CAN2 are electrically connected together when the relay is operating in passthrough mode. So CAN0 should be connected to the red plug and CAN2 should be connected to the black socket. 

## Gender convention
There is often confusion between whether connectors are referred to by the housing gender or the pin gender. Throughout this document connectors are referred to by pin gender, thus the red J533 connector, despite being a 'plug' is a female connector because the individual contacts are female sockets

# J533 gateway location
![j533 cable location](https://cdn.discordapp.com/attachments/534359517836607488/667975270749306890/image0.jpg)
Lay on your back in the driver's footwell with a torch. Get as close to the firewall as possible. Look up. You will see a (sometimes) red connector. (It's not red in this picture but it's in the red circle). This is the J533 connector. It is plugged into the J533 CAN gateway

## J533 pinout for MQB cars 
![j533_vw](https://user-images.githubusercontent.com/3917213/98302702-00823c00-2011-11eb-88e8-ea326b25f0ec.png)

## J533 wiring diagram for old white or grey panda
![J533_Ver3 1_2019 11 20](https://user-images.githubusercontent.com/61742003/87466638-a0d8ce80-c5e4-11ea-9a8d-9346a46cb4f4.png)
### Shopping list for white/grey panda harness
1. [Gateway Extension Adapter](https://www.aliexpress.com/item/4000334862080.html)
2. [OBD Female Connector w/ Wires | check eBay/Aliexpress](https://www.ebay.com/itm/16-Pin-J1962-OBD2-OBDII-OBD-Female-Connector-Diagnostic-Cable-VEHICLE-SIDE-B155/183783394862)
3. 60 ohm Resistor (5w or less)
4. Cloth electrical harness tape

## J533 wiring diagram for comma 2 and black panda
![j533 black panda](https://user-images.githubusercontent.com/3917213/98303219-df6e1b00-2011-11eb-9f5c-089564ca8994.png)

### Shopping list for black panda harness
1. [Gateway Extension Adapter](https://www.aliexpress.com/item/4000334862080.html)
2. [MQB Development Harness](https://comma.ai/shop/products/comma-car-harness)
3. Cloth electrical harness tape
4. Electrical connectors (butt splices if you're brave or DSUB pins/sockets if you are non-committal) 

## J533 harness with elimination of comma power
![J533 dream harness](https://user-images.githubusercontent.com/3917213/98303563-6622f800-2012-11eb-9080-46b0c00814b6.png)

## wp/gp/bp J533 harness diagrams together
![j533 harness diagrams together](https://raw.githubusercontent.com/actuallylemoncurd/photo/main/BPWPGPdiagram.png)