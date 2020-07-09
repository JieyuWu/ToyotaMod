![FAQ](https://user-images.githubusercontent.com/37757984/82256992-20f7f600-990c-11ea-86b2-48c3c8746197.jpg)

[◄ Home](https://github.com/commaai/openpilot/wiki)

The official comma FAQ is found here [comma.ai/faq](https://comma.ai/faq)

# openpilot

### How do I report a bug?
> Search Discord and this wiki to confirm anomalous behavior. Find the [segment](https://api.comma.ai/#definitions) of interest in [explorer](https://my.comma.ai), then click the lower right `Copy Current Segment`. Go to [#bug-reports](http://discord.comma.ai) and share the segment with a description of the issue.

### What is lateral control?
> In openpilot, lateral control means that openpilot can control your steering wheel.

### What is longitudinal control?
> In openpilot, longitudinal control means that openpilot can control gas and brake. If a car uses stock longitudinal control, that means the stock system that came with you car is in control.

# comma two

### Why won't my comma two turn on?
> The comma two is designed to be setup in the car. The USB-C to USB-C cable will only work when attached to the car harness in the vehicle. If you wish to power on the device inside, you must use a USB-A to USB-C cable and a wall charger.

### What is a Dongle ID?
> The Dongle ID is what identifies your device. It can be used to look up drives, and troubleshoot.

### Where can I find my Dongle ID?
> The device Dongle ID is found in `Settings -> Device -> Dongle ID`. If your device is paired with comma connect, you can also log into [my.comma.ai/useradmin](https://my.comma.ai/useradmin) and grab your Dongle ID from the main page under `Devices`.

### How do I delete my drives?
> Perform a factory reset to delete your drives fully (answer below this one). An uninstall / reinstall of openpilot will still keep the drives preserved on the device.

### How can I reset the device?
> Reset the comma two by pressing and holding Power and Volume Up -> Factory Reset -> Full Factory Reset

### What is the comma two hardware?
> LeEco LePro 3, Snapdragon 821. Battery and driver camera infrared cut filter are removed. GPS is u-blox NEO-M8N.

# development

### What is the openpilot development workflow? / What are the branches `master`, `devel`, and `release`?
> Read [this Medium post on Externalization](https://medium.com/@comma_ai/a-2020-theme-externalization-13b33326d8b3).