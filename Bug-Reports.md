# Introduction
Before submitting a bug report to openpilot, please ensure the following.

* You are running stock openpilot (on anything other than stock, report the bug to the fork developer)
* Your issue is not mentioned here (https://github.com/commaai/openpilot/wiki/Troubleshooting)
* There aren't any open issues (https://github.com/commaai/openpilot/issues) about the bug (if there are, please add additional information to them!)

Ready to go? [Create a bug report here!](https://github.com/commaai/openpilot/issues/new?assignees=&labels=bug&template=bug_report.md&title=)

## non-openpilot Issues

These issues aren't with the openpilot software, but are issues with hardware or the operating system that often are thought to be openpilot related.

### Rebooting Device / Stuck on Comma Logo
Very rarely, the comma device can get corrupted during an update or by being unplugged without proper shut down.

This is usually fixed by reflashing the NEOS operating system back onto the device.

A guide on how to do this is here for Windows, Mac, or Linux. https://github.com/commaai/eon-neos#restoring-on-linuxos-x

If that still doesn't work, or if the device continues to reboot while in 'fastboot' mode, email support@comma.ai with your troubleshooting steps.

### 'No Vehicle' on comma two

This is caused by the UNO board failing to communicate with the phone inside the comma device. `Note: this is always expected when the comma device is powered outside the car.`

If the comma device is plugged into the car harness, please proceed.

**1. Reboot the comma device a few times**

> Sometimes the device needs to be rebooted a few times to flash the internal UNO board. Did this fix the issue?

**2. Run SSH commands to reset the UNO board**

> There is a guide on how to SSH here: https://github.com/commaai/openpilot/wiki/SSH If you are still stuck, you can ask for help on discord.comma.ai.

`cd /data/openpilot`

`PYTHONPATH=/data/openpilot python -c 'from selfdrive.thermald.thermald import setup_eon_fan, set_eon_fan; setup_eon_fan(); set_eon_fan(3);'`

> When these commands are run, this error is expected and can be ignored. 'sh: can't create /sys/module/dwc3_msm/parameters/otg_switch: Permission denied'

`PYTHONPATH=/data/openpilot python -c 'from selfdrive.thermald.thermald import setup_eon_fan, set_eon_fan; setup_eon_fan(); set_eon_fan(0);'`

**3. Email support**

If those commands still don't solve the issue after a device reboot, email support@comma.ai with your order # and your troubleshooting steps.