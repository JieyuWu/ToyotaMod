![Ford](https://user-images.githubusercontent.com/37757984/82703102-25801f80-9c28-11ea-9072-212f93180e14.png)

[◄ Home](https://github.com/commaai/openpilot/wiki)

# Important Information

This brand currently has limited openpilot support on the F150 and Fusion only through community maintained branches. Safety code is not working properly and should **NOT** be used without fully understanding the ramifications of such. 

Ford currently has a steering lockout on the PSCM, and after 10 seconds, commands will drop for approximately 200-300ms. A fix has not yet been implemented. 

# Community Branches

The following members currently have Ford code. All code listed here is WIP and not expected to work 100%
 
https://github.com/roxasthenobody98/openpilot

https://github.com/bugsy924/openpilot/tree/ford

# Supported Vehicles

| Make      | Model                         | Supported Package | ACC              | No ACC accel below | No LKA below | No Lateral below |
| ----------| ------------------------------| ------------------| -----------------| -------------------| -------------| -----------------|
| Ford      | F150 2015-Present             | Lariat or Higher  | Stock            | 12mph              | 35mph        | 10mph            |
| Ford      | Fusion 2013-Present           | SE or Higher      | Stock            | 12mph              | 35mph        | 10mph            |

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
PSCM | Power Steering Control Module | 
PPA | Perpendicular Park Assist | APA Perpendicular
SAPP | Semi-Autonomous Parallel Park | APA Parallel
SCCM | Steering Column Control Module | SWC Buttons
SODL | Side Obstacle Detection Left | BLIS Left Module
SODR | Side Obstacle Detection Right | BLIS Right Module
TCU | Telematics Control Unit | SYNC Connect LTE



# openpilot Capabilities

## Lateral Control

Control over the steering wheel.

Vehicles without LKAS can use openpilot, so long as the LKAS Enable bit is changed in the PSCM with Forscan. This will throw a recurring DTC for a missing IPMA, but will not show up on the IPC. 
Ford currently has a steering lockout on the PSCM, and after 10 seconds, commands will drop for approximately 200-300ms. A fix has not yet been implemented. 

### Torque

### Minimum Speeds
Lateral Control is tied to the Cruise Control. On non Stop/Go vehicles, Lateral stops at 12mph, and can be manually engaged above 20mph. 
On Stop/Go vehicles, Lateral stops at 10mph. 

## Longitudinal Control

Control over the gas and brakes.

Most Ford/Lincoln vehicles do not support OP Longitudinal Control. The CCM on these vehicles (Non Stop/Go) interfaces directly with the HS2 CAN bus and cannot be intercepted. These vehicles run in Lateral Only mode. 

Stop/Go Ford's can be intercepted, but this has not been tested. 