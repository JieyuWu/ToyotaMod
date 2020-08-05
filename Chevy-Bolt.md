## System Diagrams ##

|![](http://justine-haupt.com/bolt/images/openpilot_bolt_comma2.png)| ![](http://justine-haupt.com/bolt/images/openpilot_bolt_jshuler.png)|
| ------------- |:-------------:|
|![](http://justine-haupt.com/bolt/images/openpilot_bolt_NVIDIAJetsonNano.png)|

To contribute to the above diagrams, download the [svg file](http://www.justine-haupt.com/bolt/images/openpilot_systemdiagram.svg) and use Inkscape.

## Running on an NVIDIA Jetson Nano instead of a Comma 2 ##
This is an advanced configuration. If you just want reliable L2 autonomy on your Chevy Bolt, use the Comma 2.
### Installation (work in progress 8/5/20) ###
Reference: [tools/webcam wiki](https://github.com/commaai/openpilot/tree/master/tools/webcam)
1. Download the Ubuntu-based OS image (JetPack) from nvidia and flash it to a microSD card
2. Boot the Jetson and go through the configuration process. Connect to a network (a Wifi dongle is needed)
3. SSH is enabled by default. Can log in remotely at this point.
4. In the home directory do $git clone https://github.com/commaai/openpilot.git
5. Add the openpilot directory to your python path (add "export PYTHONPATH=$HOME/openpilot" to the .bashrc file) and source it (or log out/in)
6. The next step *should* be to run ubuntu_setup.sh in ~/openpilot/tools, which just installs all the dependencies needed for openpilot. However, this will fail on the Jetson Nano. Specifically, the pipenv installation tries, but fails, to install the following: h5py, kiwisolver, matplotlib, opencv-python, osmium, pygame, pyproj, scipy, shapely, tensorflow, sympy. The issue is that a few of the dependencies have special installation processes on the Nano, and should be completed before running ubuntu_setup.sh. **THE FIX:**
        1. Use mdegan's nano_build_opencv script to install OpenCV on the Nano: Do $git clone https://github.com/mdegans/nano_build_opencv.git, cd into nano_build_opencv, and run build_opencv.sh.
        2. Reboot Nano (working headless you wouldn't know, but a message pops up on the display at some point asking for a reboot, yikes!)
        3. Install TensorFlow by following [these instructions](https://docs.nvidia.com/deeplearning/frameworks/install-tf-jetson-platform/index.html). This will install some of the other dependencies required by pipenv, like h5py.

        2. $sudo apt install python3-pyosmium python3-pyproj python3-shapely python3-opencv nvidia-cuda
        3. $pip install pygame
        3. Now run ubuntu_setup.sh (in ~/openpilot/tools)

??7. Install nvidia drivers: nvidia-xxx/cuda10.0/cudnn7.6.5
??9. Install OpenCL Driver


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
