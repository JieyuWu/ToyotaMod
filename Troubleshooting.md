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