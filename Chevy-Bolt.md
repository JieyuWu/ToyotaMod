

![](http://justine-haupt.com/bolt/images/openpilot_BoltConfigurations.png)

## Running on an NVIDIA Jetson Nano instead of a Comma 2 ##
### Installation (work in progress 8/4/20) ###
1. Download the OS image from nvidia and flash it to a microSD card
2. Boot the Jetson and go through the configuration process. Connect to a network (a Wifi dongle is needed)
3. SSH is enabled by default. Can log in remotely at this point.
4. Install Python 3.8
5. In your .bashrc file, add "export PYTHONPATH=$HOME/openpilot"
6. In ~/openpilot/tools run ubuntu_setup.sh, which just installs all the dependencies needed for openpilot. When it gets to the point where it says "Installing dependencies from Pipfile.lock" it will take a very long time and eventually (probably), fail. This is part of the pipenv install process (line 88 in ubuntu_setup.sh). Specifically, the following installations failed for me: h5py, kiwisolver, matplotlib, opencv-python, osmium, pygame, pyproj, scipy, shapely, tensorflow, sympy
6a. The fix:

7. Install tensorflow 2.2 
8. Install nvidia drivers: nvidia-xxx/cuda10.0/cudnn7.6.5
9. Install OpenCL Driver
10. Install OpenCV4 (ignore the Python part)
11. In ~/openpilot/selfdrive/camerad/cameras/camera_webcam.cc, edit lines 72 and 146 as needed if any cameras are inverted
12. Build and compile openpilot by running $scons use_webcam=1 (in ~/openpilot directory)
13. Run $touch prebuilt
14. Add /data and /data/params to the root directory.
15. Run #chown $USER /data/params

### Connecting to car/hardware and running openpilot ###
Note: The camera indexes are set based on the order in which they're connected. To edit this look at ~/openpilot/selfdrive/camerad/cameras/camera_webcam.cc
1. Connect the road facing camera first, then the driver facing camera
2. Connect computer to panda
3. In ~/openpilot/tools/webcam run $./accept_terms.py 
4. In ~/openpilot/selfdrive run $PASSIVE=0 NOSENSOR=1 WEBCAM=1 ./manager.py
5. Start the car. The UI should show the road webcam's view
6. Engage

These instructions compiled and modified from the [tools/webcam wiki](https://github.com/commaai/openpilot/tree/master/tools/webcam)