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

### How does Lane Change Assist Work?
> Lane Change Assist only works at or above 45 Mph. Activate the turn signal and, when it is safe to change lanes, gently nudge the wheel in the direction of the turn signal. This must occur within 10 seconds of initiating the turn signal. **Always paying attention when changing lanes, Openpilot has limited or no ability to check if changing lanes is safe.**

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
> LeEco LePro 3, Snapdragon 821. Battery and driver camera infrared cut filter are removed. GPS is a NEO-M8.

### I can't See My Screen While Wearing Polarized Sunglasses
> Try a matte screen protector film which can be trimmed with scissors to fix the screen, that will stop glare and enable you to see the screen with polarized lenses.  This [one from amazon](https://smile.amazon.com/gp/product/B01BZFRC0Y) has been used and recommended.

### Will the Comma 2 Drain my Car Battery?
> It shouldn't.  The Comma 2 is designed to turn off after 30 hours of inactivity.  That said, some of the 12v batteries used in hybrid vehicles are rather small (they are mainly used to boot up the computers, at which time the large hybrid battery charges the 12v batteries.)

### Can I adjust the brightness calibration?
> Yes. You can adjust your light sensor calibration in /persist!/params/d/BRIGHTNESS_M and P. M is multiplicative, P is an offset. If it's good at night but dim during the day, increase M. If it's too dim for your liking everywhere, then adjust P.


# Development

### What is the openpilot development workflow? / What are the branches `master`, `devel`, and `release`?
> Read [this Medium post on Externalization](https://medium.com/@comma_ai/a-2020-theme-externalization-13b33326d8b3).