Run openpilot with driving simulator [CARLA](http://carla.org/), which uses docker.

openpilot sim

https://carla.readthedocs.io/en/latest/core_concepts/

https://carla.readthedocs.io/en/latest/start_quickstart/

Download Page

https://github.com/carla-simulator/carla/blob/master/Docs/download.md

https://ubuntu.com/download/desktop

Create an Ubuntu USB stick for install https://ubuntu.com/tutorials/create-a-usb-stick-on-windows#1-overview

https://docs.docker.com/engine/install/ubuntu/


***

Instructions for running openpilot and Carla via docker. 

https://github.com/commaai/openpilot/tree/master/tools/sim#openpilot-in-simulator

***

`$ sudo apt-get update`  

`$ sudo apt-get install \`  
    `apt-transport-https \`  
    `ca-certificates \`  
    `curl \`  
    `gnupg-agent \`  
    `software-properties-common`  

`$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -`  

`$ sudo add-apt-repository \`  
   `"deb [arch=amd64] https://download.docker.com/linux/ubuntu \`  
   `$(lsb_release -cs) \`  
   `stable"`  

` $ sudo apt-get update`  
 `$ sudo apt-get install docker-ce docker-ce-cli containerd.io`  

`$ sudo docker run hello-world`  

`git clone https://github.com/commaai/openpilot.git`  

`cd tools`  

`cd sim`  

`./start_carla.sh`  

`sudo docker pull carlasim/carla:latest`  


***

Open a Terminal window by pressing Ctrl + Alt + T

`sudo apt-get update`  

`ubuntu-drivers devices`  

look for the driver that has "recommended" at the end

for example, the 450 version install command is show below:  

`sudo apt install nvidia-drivers-450`  

`sudo reboot`  

`sudo apt install curl`  

`$ curl https://get.docker.com | sh \`  
`&& sudo systemctl start docker \`  
`&& sudo systemctl enable docker`  

`$ sudo docker run hello-world`  

`git clone https://github.com/commaai/openpilot.git`  

`cd tools`  

`cd sim`  

`./install_carla.sh`

`INSTALL=1 ./start_carla.sh`  

`sudo ./start_openpilot_docker.sh`
