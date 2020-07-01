![Ford](https://user-images.githubusercontent.com/37757984/82703102-25801f80-9c28-11ea-9072-212f93180e14.png)

[◄ Home](https://github.com/commaai/openpilot/wiki)

# Important Information

This brand currently has limited openpilot support on the F150 and Fusion only through community maintained branches. Safety code is not working properly and should **NOT** be used without fully understanding the ramifications of such. 

# Community Branches

The following members currently have Ford code. All code listed here is WIP and not expected to work 100%
 
https://github.com/roxasthenobody98/openpilot

https://github.com/bugsy924/openpilot/tree/ford

# Make-Specific Terms

For general terms, [go here](https://github.com/commaai/openpilot/wiki/General-Terms).

Abbreviation | Term | Definition
--- | --- | ---
AHBC | Automatic High Beam Control |
APA | Active Park Assist |
APIM | Accessory Protocol Interface Module | SYNC Screen
BLIS | Blind Spot Information System |
CCM | Cruise Control Module | ACC Radar Module
CTA | Cross Traffic Alert | 
DAS | Driver Alertness System |
FCIM | Front Controls Interface Module | SYNC Surround (Climate, Hazards, 360 Cam, Hill Descent)
GWM | Gateway Module | Gatekeeper for all CAN networks in the vehicle
HUD | Head Up Display | Used for the Collision Warning and Pre-Collision Assist
IPC | Instrument Panel Cluster | 
IPMA | Image Processing Module A | LKAS Camera
PAM | Park Aid Module | 
PCA | Pre-Collision Assist |
POA | Parallel Park Out Assist | APA Park Out
PPA | Perpendicular Park Assist | APA Perpendicular
SAPP | Semi-Autonomous Parallel Park | APA Parallel
SCCM | Steering Column Control Module | SWC Buttons
SODL | Side Obstacle Detection Left | BLIS Left Module
SODR | Side Obstacle Detection Right | BLIS Right Module
TCU | Telematics Control Unit | SYNC Connect LTE



# openpilot Capabilities

## Lateral Control

Control over the steering wheel.

### Torque

### Minimum Speeds
Lateral Control is tied to the Cruise Control. On non Stop/Go vehicles, Lateral stops at 12mph, and can be manually engaged above 20mph. 
On Stop/Go vehicles, Lateral stops at 10mph. 

## Longitudinal Control

Control over the gas and brakes.

Longitudinal control is provided by the stock system that came with the car.