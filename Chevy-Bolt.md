

![](http://justine-haupt.com/bolt/images/openpilot_BoltConfigurations.png)

## Running on an NVIDIA Jetson Nano instead of a Comma 2 ##
### Installation (work in progress 8/4/20) ###
1. Download the OS image from nvidia and flash it to a microSD card
2. Boot the Jetson and go through the configuration process. Connect to a network (a Wifi dongle is needed)
3. SSH is enabled by default. Can log in remotely at this point.
4. Install Python 3.7
5. In your .bashrc file, add "export PYTHONPATH=$HOME/openpilot"
5. In ~/openpilot/tools run ubuntu_setup.sh
6. Install tensorflow 2.2 
7. Install nvidia drivers: nvidia-xxx/cuda10.0/cudnn7.6.5
8. Install OpenCL Driver
9. Install OpenCV4 (ignore the Python part)
10. In ~/openpilot/selfdrive/camerad/cameras/camera_webcam.cc, edit lines 72 and 146 as needed if any cameras are inverted
11. Build and compile openpilot by running $scons use_webcam=1 (in ~/openpilot directory)
12. Run $touch prebuilt
13. Add /data and /data/params to the root directory.
14. Run #chown $USER /data/params

Notes: The camera indexes are set based on the order in which they're connected. To edit this look at ~/openpilot/selfdrive/camerad/cameras/camera_webcam.cc


These instructions compiled from the [tools/webcam wiki](https://github.com/commaai/openpilot/tree/master/tools/webcam)