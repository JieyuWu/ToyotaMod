## System Diagrams ##

|![](http://justine-haupt.com/bolt/images/openpilot_bolt_comma2.png)| ![](http://justine-haupt.com/bolt/images/openpilot_bolt_jshuler.png)|
| ------------- |:-------------:|
|![](http://justine-haupt.com/bolt/images/openpilot_bolt_NVIDIAJetsonNano.png)|

To contribute to the above diagrams, download the [svg file](http://www.justine-haupt.com/bolt/images/openpilot_systemdiagram.svg) and use Inkscape.

## Running on an NVIDIA Jetson Nano instead of a Comma 2 ##
This is an advanced configuration. If you just want reliable L2 autonomy on your Chevy Bolt, use the Comma 2.
### Installation (work in progress 8/5/20) ###
Reference: [tools/webcam wiki](https://github.com/commaai/openpilot/tree/master/tools/webcam)
1. Download the OS image from nvidia and flash it to a microSD card
2. Boot the Jetson and go through the configuration process. Connect to a network (a Wifi dongle is needed)
3. SSH is enabled by default. Can log in remotely at this point.
4. Install Python 3.8
5. In your .bashrc file, add "export PYTHONPATH=$HOME/openpilot"
6. In ~/openpilot/tools run ubuntu_setup.sh, which just installs all the dependencies needed for openpilot. When it gets to the point where it says "Installing dependencies from Pipfile.lock" it will take a very long time and eventually (probably), fail. This is part of the pipenv install process (line 88 in ubuntu_setup.sh). Specifically, the following installations failed for me: h5py, kiwisolver, matplotlib, opencv-python, osmium, pygame, pyproj, scipy, shapely, tensorflow, sympy. According to [this](https://forums.developer.nvidia.com/t/tensorflow-installation-hang-at-h5py/75717) NVIDIA forum, installing the packages in a different order, such that h5py happens later, may clear the issue. The packages can be installed manually, one by one, with either apt or pip. 
    1. THE FIX: Install TensorFlow first, which is a special case on the Jetson. To install, follow [these instructions](https://docs.nvidia.com/deeplearning/frameworks/install-tf-jetson-platform/index.html). This will install some of the other dependencies required by pipenv, like h5py.

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
