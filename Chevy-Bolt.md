

![](http://justine-haupt.com/bolt/images/openpilot_BoltConfigurations.png)

## Running on an NVIDIA Jetson Nano instead of a Comma 2 ##
### Installation ###
1. Download the OS image from nvidia and flash it to a microSD card
2. Boot the Jetson and go through the configuration process. Connect to a network (a Wifi dongle is needed)
3. SSH is enabled by default. Can log in remotely at this point.
4. Install Python 3.7
5. In your .bashrc file, add "export PYTHONPATH=$HOME/openpilot"
5. In ~/openpilot/tools run ubuntu_setup.sh


These instructions compiled from the [tools/webcam wiki](https://github.com/commaai/openpilot/tree/master/tools/webcam)