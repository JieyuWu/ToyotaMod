# Hardware/software requirements
Openpilot cannot run on every device and operating system. If you want to tweak openpilot code or help with by contributing pull requests you will need to have a device you can run it on. The latest version of openpilot can run on a Comma2 device, or on a computer running Ubuntu 20.04 (older versions will probably work, but all of development is currently done on 20.04 so it should probably be used), or MacOS (10.15 is the one we use for testing, other may or may not work) 

If you want to run the actual model on the computer you will also need a GPU with openCL support. Nvidia is used for development and is known to work. 

If you have a Comma 2, you can connect to it from a computer running Windows. 

# Setup
Comma 2 already includes everything you need for development. For Ubuntu you'll need to clone openpilot and install some libraries. We wrote some scripts to make this easier. 
* First clone openpilot to your home directory(~)
* Go into ~/openpilot/tools and run ./ubuntu_setup.sh . If it complains about pyenv follow the steps on the console.
* Go up into ~/openpilot and run ./update_requirements.sh
* If this was all successfull you should now have all of the needed libraries for development. The next 2 steps will check if everything works
* Build openpilot by running scons -j8 in ~/openpilot (-j8 selects 8 compile threads. You can use more if you have more available). 
* The build should pass without issues. Go to ~/openpilot/selfdrive/ui and run ./ui . You should now see openpilot UI running on your computer.