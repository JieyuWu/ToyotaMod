![Troubleshooting常见故障排除](https://user-images.githubusercontent.com/37757984/83675362-babad680-a58d-11ea-8d3c-3481080eb400.png)

[◄ Home](../wiki)

# List of On Screen Messages屏幕消息列表
 * "Harness Malfunction"线束故障, "Please Check Hardware"请检查硬件
   * See[Fixing a Connection Issue]请参阅解决连接问题 (https://github.com/commaai/openpilot/wiki/Troubleshooting#fixing-a-connection-issue)

# Alerts界面弹出警告
* [Communication Issue between Processes过程中出现通讯问题](../wiki/Troubleshooting#communication-issue-between-processes)

### CAN Errors
* [CAN Error  CAN错误: Check Connections检查连接]()
* [Radar Communication Issue雷达通讯问题](../wiki/Troubleshooting#radar-communication-issue)
* [Harness Box Error Harness Box错误](../wiki/Troubleshooting#harness-box-error)

# Communication Issue between Processes过程中的通讯问题
This error can mean a number of things. Essentially, it means not all the right processes are broadcasting to the comma two.
这个错误有很多种可能的原因。
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

Disconnect and reconnect every connector from every plug. Ensure each plug is firmly seated in its respective connector. Do this for everything! The comma power v2, the harness box, and the ODB-C cable to the comma two.

If the error still persists, try flipping the ODB-C connection on the comma two. Sometimes the device will only accept all data lines from a certain direction of ODB-C.

If this doesn't fix the issue, it is possible to purchase replacement cables and A-B compare them to the included ones.

### EON discharges during use, or charges slowly

Get a better USB cable: thicker gauge and shorter length. The Panda outputs 5V, but due to resistance in the cable, there is voltage drop to the point where the EON cannot charge effectively.

### Errors Relating to CAN or Not Detecting Ignition
For a cable to work, it must have all pins present. The only specs that do are **USB-C 3.1 Gen 2** or **USB-C with Thunderbolt**.
Cables below are recommended and confirmed to work. We ship with a 1.5ft cable for most harnesses, or a 3 meter cable on Nissan and OBD-II harnesses.
* [Anker USB-C Cable - similar length to included cable](https://www.amazon.com/gp/product/B076D76DRQ)
* [Angled USB-C Cable - slightly shorter than included cable](https://www.amazon.com/gp/product/B07VMKRKBR)

### Car Unrecognized (Issues with FW Query)
* [7ft Ethernet Cable](https://www.amazon.com/Monoprice-Cat5e-Ethernet-Patch-Cable/dp/B00ACR5P60)
* [10ft Ethernet Cable](https://www.amazon.com/Monoprice-Cat5e-Ethernet-Patch-Cable/dp/B00ACR5P60)

If none of this resolves the issue, it is most likely a bad harness box. Email support@comma.ai for further assistance, listing the things you tried.

## Rebooting Device / Stuck on Comma Logo
Very rarely, the comma device can get corrupted during an update or by being unplugged without proper shut down.

This is usually fixed by reflashing the NEOS operating system back onto the device.

A guide on how to do this is here for Windows, Mac, or Linux. https://github.com/commaai/eon-neos#restoring-on-linuxos-x

If that still doesn't work, or if the device continues to reboot while in 'fastboot' mode, email support@comma.ai with your troubleshooting steps.

## 'No Vehicle' on comma two

This is caused by the UNO board failing to communicate with the phone inside the comma device. `Note: this is always expected when the comma device is powered outside the car.`

If the comma device is plugged into the car harness, please proceed.

**1. Reboot the comma device a few times**

> Sometimes the device needs to be rebooted a few times to flash the internal UNO board. Did this fix the issue?

_If you're running on a fork, you may have to SSH into your comma two and run `make recover` in `cd /data/openpilot/panda/board`_

**2. Run SSH commands to reset the UNO board**

> There is a guide on how to SSH here: https://github.com/commaai/openpilot/wiki/SSH If you are still stuck, you can ask for help on discord.comma.ai.

`cd /data/openpilot`

`PYTHONPATH=/data/openpilot python -c 'from selfdrive.thermald.thermald import setup_eon_fan, set_eon_fan; setup_eon_fan(); set_eon_fan(3);'`

> When these commands are run, this error is expected and can be ignored. 'sh: can't create /sys/module/dwc3_msm/parameters/otg_switch: Permission denied'

`PYTHONPATH=/data/openpilot python -c 'from selfdrive.thermald.thermald import setup_eon_fan, set_eon_fan; setup_eon_fan(); set_eon_fan(0);'`

**3. Email support**

If those commands still don't solve the issue after a device reboot, email support@comma.ai with your order # and your troubleshooting steps.

## EON Fan Constantly Running

SSH into your device, and attempt to manually control the fan using this command.

```cd /data/openpilot && PYTHONPATH=/data/openpilot python -c 'from selfdrive.thermald.thermald import setup_eon_fan, set_eon_fan; setup_eon_fan(); set_eon_fan(1);' ```

The value in the set_eon_fan function is the fan speed, anywhere between 0 and 3 (zero being off and 3 being the highest). Start with setting 1 and then set 0. (You will get a message about permission denied but the command still runs)

If your fan turns off when setting it to 0, then it is working properly. If it remains on, then you need a replacement fan module.

# Advanced Debugging
First [SSH into your device](https://github.com/commaai/openpilot/wiki/SSH).  Once you are ssh'd into the device, you can monitor openpilot outputs with tmux\
`tmux a` to attach to tmux window\
`` ` + d`` to exit tmux window (this is changed from the default `ctrl-b + d`)