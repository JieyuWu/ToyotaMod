![installing openpilot](https://user-images.githubusercontent.com/37757984/82701893-d3d69580-9c25-11ea-8910-3b65c5bc84f6.png)

[◄ Home](https://github.com/commaai/openpilot/wiki)

# On comma two
## Prerequisite
Your comma two must be setup in your car prior to installing openpilot. Please follow the official setup procedures [here](https://comma.ai/setup/two) or the [device installation guide](https://github.com/commaai/openpilot/wiki/Installation-Guides).

Upon first boot of comma two, do _not_ click "Dashcam software" and instead proceed to the installation paragraph below. If you already have, read the paragraph on removing the Dashcam software.

Note: The comma two is intended to be setup in your car. If you attempt to power up the comma two outside of your vehicle, you need to use a usb-A to usb-C adapter with a high output wall charger (min 2A output suggested).

## Install openpilot
Note: only follow this if you have _not_ selected "Dashcam software" on the first boot of the comma two system.

[Video walkthrough](https://www.youtube.com/watch?v=RbD1X6luc0Q).

1. When comma two boots up for the first time, you'll have the choice of either installing "Dashcam software" or "Custom Software (Advanced)." Let's go through this process to install OpenPilot instead of the Dashcam software (which does not pilot the car).
2. Ensure you're connected either to a Wifi hotspot, or that you can "Skip" the wifi hotspot selection (that means the SIM card is connected to a network).
3. Select "Custom Software (Advanced)."
4. Enter `https://openpilot.comma.ai` and click "Install Software."
5. comma two will then download the software, and install it. Note that when using the SIM card for this, you may need to retry once or twice depending on the quality of the connection. When using a wallcharger at your desk, make sure it can output 2-3A (installation draws just a little above 1.0A)
6. Closely follow the training guide.
7. Train (calibrate) the system on your car by manually driving faster than 15 mph (~ 25 km/h) for a few minutes. The screen will show what the camera sees after the training is complete.
8. You may now enable cruise control as per usual, and OpenPilot will take control after emitting a sound.

### Remove Dashcam software
If you selected the "Dashcam" software during setup you can uninstall with the following steps

1. Click on the settings icon (the gear in the top left of the homescreen)
2. Click "Developer" on the right (will say "Dashcam vX.X.X)
3. Scroll down to "Uninstall Dashcam" 
4. When prompted with a confirmation of uninstalling click, "Uninstall"
5. The device will reboot and uninstall the dashcam software. 
6. Once finished it will return to the device's initial state. You can now install other software through the setup. 