## System Diagrams ##

|![](http://justine-haupt.com/bolt/images/openpilot_bolt_comma2.png)| ![](http://justine-haupt.com/bolt/images/openpilot_bolt_jshuler.png)|
| ------------- |:-------------:|
|![](http://justine-haupt.com/bolt/images/openpilot_bolt_NVIDIAJetsonNano.png)|

To contribute to the above diagrams, download the [.svg file](http://www.justine-haupt.com/bolt/images/openpilot_systemdiagram.svg) and use Inkscape. The .svg file also includes a bunch of "general case" diagrams for openpilot not specific to the Bolt, but they may contain errors.

## Comma 2 ##
The Comma 2 has an onboard Panda and removes the need for the Giraffe by connecting directly to the car's buses.  To do this, you'll need a harness modified to connect properly to the right buses:

TBD Diagram

To connect the Comma Pedal you can tap into the ethernet run for the Comma Power using an ethernet splitter and extend it to the pedal.  (This configuration is untested on the Bolt).

## Pedal Interceptor ##

***coming soon (8/8/20 -jh)***

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

*(configuration tested by J. Haupt)*

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
    4. Now run ubuntu_setup.sh (in ~/openpilot/tools). Everything should run fine until it gets to line 88 (`pipenv install --dev --system --deploy`), at which point will give "An error occured while installing" a few packages, like h5py v2.10.0 and some others. But if you run `$pip freeze` to display the versions of all installed modules, you should find that some are in fact installed, and the ones that aren't can be manually installed using pip.

***work in progress -- (8/7/20 -jh)***

## References ##
Giraffe Info:
[Gerber files](http://www.justine-haupt.com/bolt/giraffefab/)
[Parts list](http://www.justine-haupt.com/bolt/giraffeparts/)
[J. Shuler's design page](https://easyeda.com/jshuler/chevy-bolt-openpilot-giraffe-rev-3)
