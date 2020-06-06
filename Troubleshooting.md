![Troubleshooting](https://user-images.githubusercontent.com/37757984/83675362-babad680-a58d-11ea-8d3c-3481080eb400.png)

[◄ Home](../wiki)

# Alerts
* [Communication Issue between Processes](../wiki/Troubleshooting#communication-issue-between-processes)

### CAN Errors
* [CAN Error: Check Connections]()
* [Radar Communication Issue](../wiki/Troubleshooting#radar-communication-issue)
* [Harness Box Error](../wiki/Troubleshooting#harness-box-error)

# Communication Issue between Processes
This error can mean a number of things. Essentially, it means not all the right processes are broadcasting to the comma two.

## Common Issues

### frontFrame not broadcasting

Rarely, the driver facing camera connector will become loose. When this happens, frontFrame will stop broadcasting - causing the `Communication Issue between Processes` error. Check if your driver facing camera still works by going to `Settings -> Device -> Driver Camera View`.

### Some process not running

If you are running anything but `release2` on your device, it is likely the fork maintainer missed something - or has an error in their DBC file. A good way to check is to SSH into your device and type tmux 

## CAN Error

There are some message that the device is not recieving properly. Usually this is resolved by fixing a loose connection.

## Radar Communication Issue

This means the CAN bus that the radar sits on is not being received properly, and often means there is a loose cable somewhere.

## Harness Box Error

Simiular to a radar error, this means that a CAN bus is not being recieved by the device.


# Hardware

## Fan

Constant fan running

First start with manually trying to control the fan. Let me dig up the command
The CC line can get in a weird state sometimes and remain on, even if trying to command it off
I think this is what you want 
```cd /data/openpilot && PYTHONPATH=/data/openpilot python -c 'from selfdrive.thermald import setup_eon_fan, set_eon_fan; setup_eon_fan(); set_eon_fan(1);' ```
The value in the set_eon_fan function is the fan speed, anywhere between 0 and 3 (zero being off and 3 being the highest). Start with setting 1 and then set 0. You will get a message about permission denied but the command still runs