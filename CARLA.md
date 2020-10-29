Run openpilot with driving simulator [CARLA](http://carla.org/), which uses docker.

openpilot sim

https://carla.readthedocs.io/en/latest/core_concepts/

https://carla.readthedocs.io/en/latest/start_quickstart/

Download Page

https://github.com/carla-simulator/carla/blob/master/Docs/download.md

https://ubuntu.com/download/desktop

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

`$ curl https://get.docker.com | sh \`  
`&& sudo systemctl start docker \`  
`&& sudo systemctl enable docker`  

`$ sudo docker run hello-world`  

`git clone https://github.com/commaai/openpilot.git`  

`cd tools`  

`cd sim`  

`INSTALL=1 ./start_carla.sh`  
