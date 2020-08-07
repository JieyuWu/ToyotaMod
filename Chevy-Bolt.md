## System Diagrams ##

|![](http://justine-haupt.com/bolt/images/openpilot_bolt_comma2.png)| ![](http://justine-haupt.com/bolt/images/openpilot_bolt_jshuler.png)|
| ------------- |:-------------:|
|![](http://justine-haupt.com/bolt/images/openpilot_bolt_NVIDIAJetsonNano.png)|

To contribute to the above diagrams, download the [.svg file](http://www.justine-haupt.com/bolt/images/openpilot_systemdiagram.svg) and use Inkscape. The .svg file also includes a bunch of "general case" diagrams for openpilot not specific to the Bolt, but they may contain errors.

## Comma 2 ##
The Comma 2 has an onboard Panda and removes the need for the Giraffe by connecting directly to the car's buses.  To do this, you'll need a harness modified to connect properly to the right buses:

TBD Diagram

To connect the Comma Pedal you can tap into the ethernet run for the Comma Power using an ethernet splitter and extend it to the pedal.  (This configuration is untested on the Bolt).

## Running on an NVIDIA Jetson Nano instead of a Comma 2 ##
This is an advanced configuration. If you just want reliable L2 autonomy on your Chevy Bolt, use the Comma 2.
### Hardware ###
* NVIDIA [Jetson Nano](https://developer.nvidia.com/buy-jetson?product=jetson_nano&location=US) running JetPack (NVIDIA's default OS based on Ubuntu)
* Case and cooling fan for the Nano
* Power cable (TBD -- Will test first w/ USB power in Bolt. Plan Bs: 12V port or OBD-II)
* 64GB MicroSD Card 
* 5.5" OLED HDMI display, namely [this one](https://www.amazon.com/5-5inch-HDMI-AMOLED-Resolution-Capacitive/dp/B07N8WWDRK)
* Two Logitech C920 HD webcams (or one plus something else). The C920 is hard to get (or discontinued?), so I resorted to eBay.
* USB-A to USB-A cable to connect to Panda, or much more common USB-A to Mini-B along with Panda Paw.

*(As tested by J. Haupt)*

### Installation ###
Reference: [tools/webcam wiki](https://github.com/commaai/openpilot/tree/master/tools/webcam)
1. Download the Ubuntu-based OS image (JetPack) from nvidia and flash it to a microSD card
2. Boot the Jetson and go through the configuration process. Connect to a network (a Wifi dongle is needed)
3. SSH is enabled by default. Can log in remotely at this point.
4. In the home directory do `$git clone https://github.com/commaai/openpilot.git`
5. Add the openpilot directory to your python path (add `export PYTHONPATH=$HOME/openpilot` to the .bashrc file) and source it (or log out/in)
6. The next step *should* be to run ubuntu_setup.sh in ~/openpilot/tools, which just installs all the dependencies needed for openpilot. However, this will fail on the Jetson Nano. Specifically, the pipenv installation tries, but fails, to install the following: h5py, kiwisolver, matplotlib, opencv-python, osmium, pygame, pyproj, scipy, shapely, tensorflow, sympy. The issue is that a few of the dependencies have special installation processes on the Nano, and should be completed before running ubuntu_setup.sh. **THE FIX:**
    1. Use mdegan's nano_build_opencv script to install OpenCV on the Nano: Do `$git clone https://github.com/mdegans/nano_build_opencv.git`, then cd into nano_build_opencv, and do `$./build_opencv.sh.` This takes a long time (many hours... 8?) to complete.
    2. Reboot Nano (working headless you wouldn't know, but a message pops up on the display at some point asking for a reboot, yikes!)
    3. Install TensorFlow by following [these instructions](https://docs.nvidia.com/deeplearning/frameworks/install-tf-jetson-platform/index.html). This will install some of the other dependencies required by pipenv, like h5py. NOTE, when issueing the last command in those instructions (the one that actually installs tensorflow with "pip3 install", run with "sudo -H" instead of just sudo.
    4. Now run ubuntu_setup.sh (in ~/openpilot/tools)
7. Do `$sudo apt install scons cython`
8. Do `$pip install jinja2`
9. In /usr/bin/scons, edit the shebang to use python3: `#! /usr/bin/python3`
12. Build and compile openpilot by running `$scons use_webcam=1` (in ~/openpilot directory)

----work in progress (8/6/20)-----

????
    4. $sudo apt install python3-pyosmium python3-pyproj python3-shapely python3-opencv nvidia-cuda
    5. $pip install pygame

????
7. Install nvidia drivers: nvidia-xxx/cuda10.0/cudnn7.6.5
9. Install OpenCL Driver


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

## References ##
Giraffe Info:
[Gerber files](http://www.justine-haupt.com/bolt/giraffefab/)
[Parts list](http://www.justine-haupt.com/bolt/giraffeparts/)
[J. Shuler's design page](https://easyeda.com/jshuler/chevy-bolt-openpilot-giraffe-rev-3)
