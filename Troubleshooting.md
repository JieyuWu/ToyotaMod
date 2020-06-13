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

If you are running anything but `release2` on your device, it is likely the fork maintainer missed something - or has an error in their DBC file. A good way to check is to SSH into your device and type `tmux a`

## CAN Error

There are some message that the device is not receiving properly. Usually this is resolved by fixing a loose connection.

See [Fixing a Connection Issue](https://github.com/commaai/openpilot/wiki/Troubleshooting#fixing-a-connection-issue)

## Radar Communication Issue

This means the CAN bus that the radar sits on is not being received properly, which often means there is a loose cable somewhere.

See [Fixing a Connection Issue](https://github.com/commaai/openpilot/wiki/Troubleshooting#fixing-a-connection-issue)

## Harness Box Error

Similar to a radar error, this means that a CAN bus is not being received by the device.

See [Fixing a Connection Issue](https://github.com/commaai/openpilot/wiki/Troubleshooting#fixing-a-connection-issue)

# Hardware

## Fixing a Connection Issue

Disconnect and reconnect every connector from every plug. Ensure each plug is firmly seated in its respective connector. Do this for everything! The comma power v2, the harness box, and the USB-C cable to the comma two.

If the error still persists, try flipping the USB-C connection on the comma two. Sometimes the device will only accept all data lines from a certain direction of USB-C.

If this doesn't fix the issue, it is possible to purchase replacement cables and A-B compare them to the included ones.

### Errors Relating to CAN
* [Anker USB-C Cable - similar length to included cable](https://www.amazon.com/gp/product/B076D76DRQ)
* [Angled USB-C Cable - slightly shorter than included cable](https://www.amazon.com/gp/product/B07VMKRKBR)

### Car Unrecognized (Issues with FW Query)
* [7ft Ethernet Cable](https://www.amazon.com/Monoprice-Cat5e-Ethernet-Patch-Cable/dp/B00ACR5P60)
* [10ft Ethernet Cable](https://www.amazon.com/Monoprice-Cat5e-Ethernet-Patch-Cable/dp/B00ACR5P60)

If none of this resolves the issue, it is most likely a bad harness box. Email support@comma.ai for further assistance, listing the things you tried.

## EON Fan Constantly Running

SSH into your device, and attempt to manually control the fan using this command.

```cd /data/openpilot && PYTHONPATH=/data/openpilot python -c 'from selfdrive.thermald import setup_eon_fan, set_eon_fan; setup_eon_fan(); set_eon_fan(1);' ```

The value in the set_eon_fan function is the fan speed, anywhere between 0 and 3 (zero being off and 3 being the highest). Start with setting 1 and then set 0. (You will get a message about permission denied but the command still runs)

If your fan turns off when setting it to 0, then it is working properly. If it remains on, then you need a replacement fan module.