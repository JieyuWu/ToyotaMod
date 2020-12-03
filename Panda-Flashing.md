![panda flashing](https://user-images.githubusercontent.com/37757984/82701897-d5a05900-9c25-11ea-84aa-8439bde81975.png)

[◄ Home](https://github.com/commaai/openpilot/wiki)

### SSH Into Your Device

See [SSH](../wiki/SSH) for more information.

### Navigate to the Panda folder

`cd /data/openpilot/panda/board`

### Run the command

`pkill -f boardd; cd /data/openpilot/panda/board; make; reboot`

Note: For comma two the device must be powered by 12v. 

Doing this a few times may unstick a panda that isn't flashing properly.

### Alternative command

This alternative command can be ran if flashing the Panda via the standard process proves unsuccessful.

`cd /data/openpilot/panda ; pkill -f boardd ; PYTHONPATH=.. python -c "from panda import Panda; Panda().flash()"`

https://github.com/commaai/panda