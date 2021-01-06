![custom forks](https://user-images.githubusercontent.com/37757984/82701890-d2a56880-9c25-11ea-8ed8-fc287b7ae883.png)

**Comma does not validate custom forks for safety. Install them at your own risk.**

[◄ Home](https://github.com/commaai/openpilot/wiki)

openpilot [forks](https://en.wikipedia.org/wiki/Fork_(software_development)) are used for various purposes, often for use on a certain vehicle or for the development and testing of new features.

See JFrux's guide for installing forks [here](https://medium.com/@jfrux/comma-eon-installing-a-fork-of-openpilot-5c2b5c134b4b).

You can also use the fork manager at [emu-sh/.oh-my-comma](https://github.com/emu-sh/.oh-my-comma) see: [demo](https://emu.sh/demo.gif)

Or, if you just want something to help you SSH into your device, check out [Utilities for Developers](https://github.com/commaai/openpilot/wiki/Utilities-for-developers)


Owner         | Link                                                                | Description
------------- | ------------------------------------------------------------------- | -----------------------
@kegman       | [kegman](https://github.com/kegman/openpilot)                       | Largely supports Honda. Has many various customization options.
@zorrobyte        | [zorrobyte](https://github.com/zorrobyte/openpilot)                 | Close to stock, automatically learns your curvature factor for better curve handling. Also supports the highly-accurate Zorro Steering Sensor (ZSS).
@ErichMoraga      | [ErichMoraga](https://github.com/ErichMoraga/openpilot)             | Toyota / ZSS
@xx979xx          | [xx979xx](https://github.com/xx979xx/openpilot/tree/HKG_community)  | Hyundai / Kia / Genesis
@eFini            | [dragonpilot](https://github.com/dragonpilot-community/dragonpilot) | Heavily modified fork of openpilot with many different customizations accessible via UI.
@jyoung8607       | [jyoung8607](https://github.com/jyoung8607/openpilot)               | Volkswagen
@ShaneSmiskol     | [Stock Additions](https://github.com/ShaneSmiskol/openpilot)        | Close to stock, has an implementation of following distance profiles similar to the stock Toyota cruise control system. Supports Prius w/ ZSS
@bugsy924         | [bugsy924](https://github.com/bugsy924/openpilot)                   | Subaru (Recommended to use use mlp's fork which contains Bugsy's work).
@mlp              | [martinl](https://github.com/martinl/openpilot)                     | Subaru (In progress PR supporting both Global and Pre-Global models).
@afa              | [Afa](https://github.com/Rming/openpilot)                          | Honda fork for Chinese users who like customization
@Ponzu       | [Ponzu07](https://github.com/ponzu07/openpilot)                       | Japanese?


# Development

Helpful tips for creating and maintaining a successful openpilot fork.

- comma.ai suggests familiarizing yourself with [functional safety](https://en.wikipedia.org/wiki/ISO_26262) before starting development on a custom fork.

- Here's where some of the commonly modified openpilot files are:
  - [longcontrol.py](https://github.com/commaai/openpilot/blob/master/selfdrive/controls/lib/longcontrol.py): Controls gas and brakes from an input desired speed, using a PI controller

  - [lane_planner.py](https://github.com/commaai/openpilot/blob/master/selfdrive/controls/lib/lane_planner.py): Calculates `dPoly` (the path openpilot tries to drive) from input lane line and path polys from the model

  - [planner.py](https://github.com/commaai/openpilot/blob/master/selfdrive/controls/lib/planner.py): Has longitudinal acceleration limits. Picks the slowest longitudinal solution to use for cruise control (between set speed and the two longitudinal MPCs)

  - interface.py (path: selfdrive/car/YOUR MAKE/interface.py): Houses the tuning values for each car. Specifies custom alerts/events for that make. Inherits from [interfaces.py](https://github.com/commaai/openpilot/blob/master/selfdrive/car/interfaces.py)

- [From @Torq_boi](https://discordapp.com/channels/469524606043160576/538741329799413760/695014354428362868): `A lot of people seem to be changing the CAMERA_OFFSET parameter. So I just want to make clear that that just modifies the laneline positions, not the predicted path. If you want the car to consistently drive more left or right you should change the path too. Since OP sometimes relies on lanelines sometimes on path, having them mismatched can cause weirdness.`

# Custom Fork Do's and Don'ts

Forks can change many of the fundamental pieces of openpilot software. Because of this, custom forks are expected to maintain certain safety procedures in order to access comma.ai's server infrastructure.

## Do's

- [Overview of the safety of openpilot (SAFETY.MD)](https://github.com/commaai/openpilot/blob/master/SAFETY.md)

## Don'ts

- By in large, comma.ai recommends developers to not touch any of the [panda safety code](https://github.com/commaai/panda) to add new features or modify existing behavior. One exception is `unsafe_mode` defined in [`safety_declarations.h`](https://github.com/commaai/panda/blob/master/board/safety_declarations.h), near the bottom. Some definitions of what each mode does can also be found in that file.

  - If you would like to propose a change in panda safety, consider opening a pull request.

- The integrity of the time variables in the [driver_monitor.py](https://github.com/commaai/openpilot/blob/master/selfdrive/monitoring/driver_monitor.py) file must remain consistent with what's been predefined by comma.

- Don't use the car's Parking Assist parameters to drive at highway speeds unless you know what you're doing. Don't promote to other users. See medium article for more details: https://medium.com/@comma_ai/safer-control-of-steering-362f3526c9ab

*NOTE: To fork maintainers. Disabling or nerfing safety features may get you and your users banned from our servers. comma.ai strongly discourages the use of openpilot forks with safety code either missing or not fully meeting the requirements defined in [SAFETY.md](https://github.com/commaai/openpilot/blob/master/SAFETY.md).*