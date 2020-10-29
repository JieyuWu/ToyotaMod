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

`sudo docker pull carlasim/carla:latest`  