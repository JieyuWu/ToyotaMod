Run openpilot in the driving simulator world [CARLA](http://carla.org/).

[Simulator Read Me](https://github.com/commaai/openpilot/tree/master/tools/sim#openpilot-in-simulator) - Instructions for running openpilot and Carla. 

## Install Drivers and Software

### Download and Install Ubunutu

https://ubuntu.com/download/desktop

Create an Ubuntu USB stick for install https://ubuntu.com/tutorials/create-a-usb-stick-on-windows#1-overview

https://docs.docker.com/engine/install/ubuntu/

### Update Nvidia Drivers

Open a Terminal window by pressing Ctrl + Alt + T

`sudo apt-get update`  

`ubuntu-drivers devices`  

look for the driver that has "recommended" at the end

for example, the 450 version install command is show below:  

`sudo apt install nvidia-drivers-450`  

`sudo reboot`  

### Install Docker

`sudo apt install curl`  

`$ curl https://get.docker.com | sh \`  
`&& sudo systemctl start docker \`  
`&& sudo systemctl enable docker`  

`$ sudo docker run hello-world`  

### Install openpilot and carla

`sudo apt install git`  

`git clone https://github.com/commaai/openpilot.git`  

`cd openpilot`  

`cd tools`  

`cd sim`  

`./install_carla.sh`

### Install drivers and start carla

`sudo INSTALL=1 ./start_carla.sh`  

### Run openpilot

Open a second terminal window by pressing Ctrl + Alt + T

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

disable the issue in controllerd:212  controlsd.py

everything with ctrl+c in both windows, edit file, run openpilot script in window 0 and bridge in window 1

# See Also

openpilot sim

https://carla.readthedocs.io/en/latest/core_concepts/

https://carla.readthedocs.io/en/latest/start_quickstart/

Download Page

https://github.com/carla-simulator/carla/blob/master/Docs/download.md
