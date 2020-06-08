![General Terms](https://user-images.githubusercontent.com/37757984/82586637-bd104000-9b4c-11ea-92bf-6affc4f03835.jpg)

[◄ Home](https://github.com/commaai/openpilot/wiki)

# comma.ai terms

Term | Abbreviation | Definition
--- | --- | ---
comma.ai | | The company behind openpilot
comma API | | [link to docs](https://api.comma.ai/#comma-api-spec)
comma connect | | An [open source](https://github.com/commaai/connect) mobile app for [Android](https://play.google.com/store/apps/details?id=ai.comma.connect&hl=en_US) and [iOS](https://apps.apple.com/us/app/comma-connect/id1456551889) used to view drives and interact with the device remotely
car harness | | A universal interface to your car. A unique harness exists for each of the supported makes and models of cars. This replaces the older giraffe Connector
comma pedal | | A device that provides stop-and-go capability on cars that don't currently support it. This device is not sold by Comma.ai (not officially supported by them), but supported in OpenPilot.
comma points | | Awarded for various activities you perform on the platform. Good for bragging rights.
comma power | CPv1, CPv2 | Use your car's OBD-II port to power your Toyota, Bosch, or FCA Giraffe. CPv1 was the initial version, for use w/ Giraffes. CPv2 came out later, used with Comma Harness, and has an RJ45 jack.
comma prime | | A subscription service from comma.ai offering a [specific list of benefits](https://comma.ai/shop/products/comma-prime-sim-card)
comma two devkit | C2, comma two | The latest generation devkit. A smartphone running a customized version of Android and a custom case with additional cooling. This device runs the openpilot software and has an integrated panda
EON devkit | EON, EON Gold, EON SE | The previous generation of the comma two devkit. It did not have an integrated panda
fingerprint | FPv1, FPv2 | A list of CAN bus signals unique to a particular vehicle. Allows OpenPilot to recognize which car it is connected to. CAN-based FPv1 is now deprecated; emphasis is now on firmware-based FPv2.
FrEON | | "Free EON"... an open source variant of the EON case. The repository contains files that can be used for 3D printing a case. Developed by @Chase#7213
giraffe connector | | An adapter board that lets you read buses that aren't exposed on the main OBD-II connector, with variants for different vehicle makes/models.
Lane Change Assist | LCA | Activate the turn signal and gently nudge the wheel in the direction you wish to travel to when it's safe. Change lanes while always paying attention.
LeEco Le Pro 3 | LeEco, Lepro | The phone used in comma two and EON Gold devkits
LiveParameters | | 	A continually updated file (ie. "Live") that stores learned calibration data for the vehicle.
OnePlus 3T | OP3T | One of the phones used in the previous generation EON devkits. It was discontinued due to a lack of supply. Known model numbers: A3000(US version) A3010(Asian version)
openpilot | OP | An open source driver assistance system developed by comma.ai
panda OBD-II Interface | | A CAN-Bus to USB adapter. Available in 3 variants: white (support dropped in op version 0.6.7+) / grey (incl. high precision GPS) / black (newest variant)
panda paw | | A device to help you unbrick a panda.

# openpilot terms
Term | Abbreviation | Definition
--- | --- | ---
longitudinal | long | Refers to gas and brake control
lateral | lat | Refers to steering control
Model predictive control | MPC | An advanced method of process control that is used to control a process while satisfying a set of constraints. Used for longitudinal control.

# driver-assistance terms

Make-specific terms should be added to [their perspective wiki page](https://github.com/commaai/openpilot/wiki#vehicle-information).

Term | Abbreviation | Definition
--- | --- | ---
Adaptive Cruise Control | ACC | A cruise control system that automatically adjusts the vehicle speed to maintain a safe distance from vehicles ahead.
Advanced Driver-Assistance Systems | ADAS | Electronic systems that aid the driver.
(Automatic) Lane Centering | (A)LC | A system designed to keep a car centered in the lane, relieving the driver of the task of steering.
Collision Avoidance System | AEB, CMS, FCW(S), PCS | A system designed to prevent or reduce the severity of a collision.
Driver Monitoring (System) | DM(S), DAM | A system that uses infrared sensors and/or cameras to monitor driver attentiveness
hugging | | An undesired behavior where the vehicle drives too closely to one side of the lane.
Lane Keep Assist (System) | LKA(S) | Lane keep assist is what comes with most cars sold today. It will assist the driver if they go over a lane line, but will not keep the car centered in the lane.
Lane Departure Warning (System) | LDW(S), LDA | Lane departure warning will beep when a car goes over a lane line.
Pedestrian Crash Avoidance Mitigation | PCAM | A system that uses computer and artificial intelligence technology to recognize pedestrians and bicycles in an automobile's path to take action for safety.
ping pong | | 	An undesired behavior where the vehicle sways from one side of the lane to the other repeatedly. The desired behavior is to stay in the center of the lane.
wobble | | Similar to ping pong, but where the vehicle drives mostly centered in the lane but sways slightly from side to side. Primarily due to improper tuning of the steering control system, influence from wind, or poor lane/path perception due to rain, dirt, and/or debris on the vehicles windshield.
Traffic-sign recognition | TSR | A system by which a vehicle is able to recognize the traffic signs put on the road e.g. "speed limit" or "children" or "turn ahead".

# automotive terms

Make-specific terms should be added to [their perspective wiki page](https://github.com/commaai/openpilot/wiki#vehicle-information).

Term | Abbreviation | Definition
--- | --- | ---
Controller Area Network | CAN, CAN bus | A message-based protocol that provides a standardized way for ECUs to communicate with each other.
Electronic Control Unit | ECU | Any embedded system in automotive electronics that controls one or more of the electrical systems or subsystems in a vehicle.
Electric Power Steering | EPS | Uses an electric motor to assist the driver of a vehicle. Sensors detect the position and torque of the steering column, and a computer module applies assistive torque via the motor, which connects to either the steering gear or steering column.
On-Board Diagnostics Connector | OBD-II, OBD-II port | OBD systems give the vehicle owner or repair technician access to the status of the various vehicle sub-systems. The comma power v2 uses this port to provide constant power to the comma two as well as access the diagnostic bus for FW query.

# discord terms
Term | Abbreviation | Definition
--- | --- | ---
Direct Message | DM (PM preferred to avoid confusion with driver monitoring) | Private message to an individual on Discord
Private Message | PM | Private message to an individual on Discord
Want To Buy | WTB | You want to buy an item (on For-Sale channel)
For Sale | FS | People sale an item (on For-Sale channel)