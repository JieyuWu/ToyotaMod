![FAQ](https://user-images.githubusercontent.com/37757984/82256992-20f7f600-990c-11ea-86b2-48c3c8746197.jpg)

[◄ Home](https://github.com/commaai/openpilot/wiki)

The official comma FAQ is found here [comma.ai/faq](https://comma.ai/faq)

Table of Contents
=================

   * [openpilot](#openpilot)
     * [How do I report a bug?](#how-do-i-report-a-bug)
     * [What is lateral control?](#what-is-lateral-control)
     * [What is longitudinal control?](#what-is-longitudinal-control)
     * [How does Lane Change Assist Work?](#how-does-lane-change-assist-work)
     * [How to a Change a Specific Release?](#how-to-a-change-a-specific-release)
     * [Where are my videos stored? How can I stitch the segments together?](#where-are-my-videos-stored-how-can-i-stitch-the-segments-together)
     * [When are my videos uploaded to the cloud?](#when-are-my-videos-uploaded-to-the-cloud)
   * [comma two](#comma-two)
     * [Why won't my comma two turn on?](#why-wont-my-comma-two-turn-on)
     * [What is a Dongle ID?](#what-is-a-dongle-id)
     * [Where can I find my Dongle ID?](#where-can-i-find-my-dongle-id)
     * [How do I delete my drives?](#how-do-i-delete-my-drives)
     * [How can I reset the device?](#how-can-i-reset-the-device)
     * [What is the comma two hardware?](#what-is-the-comma-two-hardware)
     * [I can't see my screen while wearing polarized sunglasses](#i-cant-see-my-screen-while-wearing-polarized-sunglasses)
     * [Will the comma two kill my car battery?](#will-the-comma-two-kill-my-car-battery)
     * [Can I adjust the brightness calibration?](#can-i-adjust-the-brightness-calibration)
     * [My storage space is filling up, How long are drive segments kept on my device?](#my-storage-space-is-filling-up-how-long-are-drive-segments-kept-on-my-device)
   * [Development](#development)
     * [What is the openpilot development workflow? / What are the branches master, devel, and release?](#what-is-the-openpilot-development-workflow--what-are-the-branches-master-devel-and-release)
     * [What do the LED colors mean?](#what-do-the-led-colors-mean)
   * [Discord Help](#discord-help)
     * [Before Asking a Question](#before-asking-a-question)
     * [How do I search on discord?](#how-do-i-search-on-discord)
     * [How do I read discord channel pins?](#how-do-i-read-discord-channel-pins)
     * [How do I read the channel description?](#how-do-i-read-the-channel-description)

# openpilot

### How do I report a bug?
> Search Discord and this wiki to confirm anomalous behavior. Find the [segment](https://api.comma.ai/#definitions) of interest in [explorer](https://my.comma.ai), then click the lower right `Copy Current Segment`. Go to [#bug-reports](http://discord.comma.ai) and share the segment with a description of the issue.

### What is lateral control?
> In openpilot, lateral control means that openpilot can control your steering wheel.

### What is longitudinal control?
> In openpilot, longitudinal control means that openpilot can control gas and brake. If a car uses stock longitudinal control, that means the stock system that came with you car is in control.

### How does Lane Change Assist Work?
> Lane Change Assist only works at or above 45 Mph. Activate the turn signal and, when it is safe to change lanes, gently nudge the wheel in the direction of the turn signal. This must occur within 10 seconds of initiating the turn signal. **Always paying attention when changing lanes, Openpilot has limited or no ability to check if changing lanes is safe.**

### How to a Change a Specific Release?

> See the instructions for how to [checkout a specific release](https://github.com/commaai/openpilot/wiki/Update-Modify-openpilot#how-to-checkout-a-specific-release).

### When are my videos uploaded to the cloud?
> With comma prime, low quality videos and condensed logs are uploaded constantly, but at a maximum rate of 512kbps.  When your device connects to wifi and the vehicle is stopped, it will upload the full logs and high quality videos.

### Where is my dashcam video footage stored? How can I stitch the segments together?

> Videos are stored on the device in `/sdcard/realdata` as 1 minute segment directories.  Each directory contains the log data and video in `hevc` form.  You can stitch these videos together using this linx command:

```
cat fcamera1.hevc fcamera2.hevc fcamera3.hevc > output.hevc 
```

> The Windows equivalent for binary file concatenation would be 
```
copy /b fcamera1.hevc+fcamera2.hevc+fcamera3.hevc output.hevc
```

> If you rename the videos in sequence, you can use the shorter command:

```
cat fcamera* > output.hevc
```

> Yet another option that doesn't require any renaming, simply change the date and time to match the start of your drive:
```
cd /sdcard/realdata
find . -type f -wholename "*2020-08-01--09-01-14--*/*.hevc" -exec cat {} + > drive.hevc
```

> The output.hevc file can be uploaded to YouTube straight away, or played in VLC. But many others won’t know what to do with a .hevc file. So if sending, then [download ffmpeg](https://ffmpeg.org/download.html) and convert it first. To make a .mpg copy for emailing etc., put the output.hevc file in the same folder as the ffmpeg program, then run a command like 
ffmpeg -I output.hevc -qscale:v 1 output.mpg

Step by step guide for accessing video files [here](../wiki/Video-Files).

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
> LeEco LePro 3, Snapdragon 821. Battery and driver camera infrared filter are removed.

### I can't see my screen while wearing polarized sunglasses
> Try a matte screen protector film which can be trimmed with scissors to fix the screen, that will stop glare and enable you to see the screen with polarized lenses.  This [one from amazon](https://smile.amazon.com/gp/product/B01BZFRC0Y) has been used and recommended.

### Will the comma two kill my car battery?
> It shouldn't.  The comma two is designed to turn off after 30 hours of inactivity, or after a shorter amount of time if it senses the car battery is running low.

### Can I adjust the brightness calibration?
> Yes.  Adjust the light sensor calibration in /persist/comma/params/d/BRIGHTNESS_M & BRIGHTNESS_B.  M is multiplicative, whereas B is an offset.  If it's good at night, but dim during the day, increase M.  If it's too dim all the time, adjust B.

### My storage space is filling up, How long are drive segments kept on my device?
> Videos are saved on your device until additional room is needed.  When less than 5GB or 10% of the drive space remains, the oldest segments will be deleted to clear up room.  On the Comma 2, this results storage for  around 12 hours of segments.  The oldest segments will be deleted to make room for new segments even if the old segments have not been uploaded.

# Development

### What is the openpilot development workflow? / What are the branches `master`, `devel`, and `release`?
> Read [this Medium post on Externalization](https://medium.com/@comma_ai/a-2020-theme-externalization-13b33326d8b3).

### What do the LED colors mean?
> The LED indicates the status of the inbuilt Panda (UNO).

```
* White: CAN send enabled
* Red: This is your panda's heartbeat(power). It fades in and out
* Green: Bad firmware or firmware flashing (only green, fast)
* Blue (static): CAN detected
* Blue (fades in and out): power saving
```

# Discord Help

comma.ai is a very open company.  Their developers spend a lot of time on the Discord Server working with users and collaborating with other community developers.  This is awesome.  <u>But please don't abuse this.</u>  Asking questions that have already be answered is a waste of everyone's time.  Wasting developer time, means slower improvements for us all.  

### Before Asking a Question
> Please follow the instructions on the #Guidelines channel, specifically:

```
• Is it answered on https://comma.ai/faq ?
• Is it answered on https://wiki.comma.ai/ ?
• Is the answer found in the pins of a related channel? (Discord Pins)
• Has the question been asked before? (Discord Search)
• Have you read the channel description to confirm this is the correct place for your question?
```

### How do I search on discord?
> Basic word searching is simple, but you may have better luck if you use search modifiers:

![image](https://user-images.githubusercontent.com/3046315/88340440-afb03700-ccf0-11ea-8572-0fa203cf927d.png)

> So if you have a question about a Toyota Camry you should search in the #Toyota-Lexus channel such as: `in:#toyota-lexus <search term>`

### How do I read discord channel pins?
> On the web app, it is as simple as clicking on the pin icon in the top right of the channel:

![image](https://user-images.githubusercontent.com/3046315/88341372-55b07100-ccf2-11ea-8dbd-446492805946.png)

> On the mobile app pins can be found by dragging from the right edge of the screen to the left.

### How do I read the channel description?
> On the mobile app, the channel description is located at the top of the page.  If the description is truncated, you can click on it to read the entire contents:

![image](https://user-images.githubusercontent.com/3046315/88342237-e63b8100-ccf3-11ea-823a-660dfd1e3b99.png)

> On the mobile app the channel description can be found by dragging from the right edge of the screen to the left.
