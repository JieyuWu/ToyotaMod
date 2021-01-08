Run openpilot in the driving simulator world [CARLA](http://carla.org/).

[Simulator Read Me](https://github.com/commaai/openpilot/tree/master/tools/sim#openpilot-in-simulator) - Instructions for running openpilot and Carla. 



## Install Drivers and Software

### Download and Install Ubunutu

https://ubuntu.com/download/desktop

Create an Ubuntu USB stick for install https://ubuntu.com/tutorials/create-a-usb-stick-on-windows#1-overview

### Update Nvidia Drivers

Open a Terminal window by pressing Ctrl + Alt + T

`sudo apt-get update`  

`sudo apt-get upgrade -y`  

`ubuntu-drivers devices`  

look for the driver that has "recommended" at the end

for example, the 450 version install command is show below:  

`sudo apt install nvidia-driver-450`  

`sudo reboot`  

### Install Docker

`sudo apt install curl`  

`curl https://get.docker.com | sh \`  
`&& sudo systemctl start docker \`  
`&& sudo systemctl enable docker`  

`sudo docker run hello-world`  

### Install openpilot and carla

`sudo apt install git`  

`git clone https://github.com/commaai/openpilot.git`  

`cd openpilot/tools/sim`  

`./install_carla.sh`

### Install drivers and start carla

`sudo INSTALL=1 ./start_carla.sh`  

### Run openpilot

Open a second terminal window by pressing Ctrl + Alt + T

`cd openpilot/tools/sim`  

`sudo ./start_openpilot_docker.sh`

# Tips and Troubleshooting

`+0

scrolling press ` and [

exit scroll mode press q

As  an aside you can add yourself to the docker group with sudo usermod -aG docker $USER then logout/login to not have to sudo everything

ctrl+d to exit container

ctrl+c to kill process

sudo service docker restart

### "communication issue between processes"

see github issue - https://github.com/commaai/openpilot/issues/2501

disable the issue in controllerd:212  controlsd.py

everything with ctrl+c in both windows, edit file, run openpilot script in window 0 and bridge in window 1

### Carla scene is slow or fails to load in openpilot ui window

Try setting CARLA to the low quality rendering  

Open the file openpilot/tools/sim/start_carla.sh in the ubuntu file explorer  

on the last line, add `./CarlaUE4.sh -quality-level=Low` to the end of the docker command. It should look like the following:  

`docker run -it --net=host --gpus all carlasim/carla:0.9.7 ./CarlaUE4.sh -quality-level=Low`  

# Noted Dependencies

* "think is some dependency conflict between cuda 10.2/11, cudnn 7.5/8 and the pypi shipped onnxrunner binaries" - marsch

* "onnxruntime-gpu 1.5.2 relies on cuda 10.2"

* "OSError: libcublas.so.10: cannot open shared object file: No such file or directory"  
  * "cuda 10.2 instead of 11.1"

# See Also

openpilot sim

https://carla.readthedocs.io/en/latest/core_concepts/

https://carla.readthedocs.io/en/latest/start_quickstart/

Many users and developers hang out in the [comma.ai Discord](https://discord.comma.ai)'s #openpilot-simulation. 

Download Page

https://github.com/carla-simulator/carla/blob/master/Docs/download.md
