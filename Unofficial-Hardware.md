![Unofficial Hardware](https://user-images.githubusercontent.com/37757984/83460050-63e0c000-a41a-11ea-8041-ffe0fe9a6077.png)

[◄ Home](https://github.com/commaai/openpilot/wiki)

Community developed hardware based on EON style form factor. For webcam and pc based development click [here](../wiki/Webcam/).

Typically used for customizing an EON case or creating an EON device from scratch

# Cases

* Unibody Lepro3 @CloudJ
  * https://www.thingiverse.com/thing:4069425
* FrEON @ch4se
  * https://github.com/ch4se/OpenFrEON

# Mounts
* variety of mounts from @Tunder
  * https://github.com/Tundergit/openpilot-mounts
* Magnectic Mount @CloudJ 
  * https://www.thingiverse.com/thing:3497526
  * https://docs.google.com/spreadsheets/d/1UxvMszwfw6LFYjCilk6hNuoX6cheE6PvcsdKKO9ggU8/edit#gid=0
* comma2 style mount, magnet mount for EON case @Daehyuk
  * https://github.com/daehahn/comma1.5
  * https://github.com/daehahn/comma1.6

# Fan Replacement

* Noctua - Quiet
  * https://www.amazon.com/gp/product/B00NEMGCIA

# Large Format Fans

* CloudJ 60mm Fan Mount
  * https://www.thingiverse.com/thing:3570209

# Car AV Vent Redirectors

* Ramp @ch4se
  * https://www.thingiverse.com/thing:3014002

# Replacement Batteries

* https://www.ifixit.com/Store/Android/OnePlus-3-Replacement-Battery/IF330-017?o=2

# Batteryless

* Use a DC-DC converter to power the EON without a battery
* Make sure to wrap the DC-DC converter in electric tape to prevent shorting

<details>
<summary>Buck Converter Installation</summary>

* Step one: Carefully remove the battery.
* Step two: Solder connections to the DC-DC converter.
* Step three: Solder 5V connection to the USB flex cable by stripping the middle section of the USB flex cable.
* Step four: Solder "battery" connection to battery PCB or logic board.
* Step five: Solder ground connection to the gold connector on USB flex cable or use logic board ground. 
</details>

---

# Software

## How to install NEOS OS

### Pre-requisites

You will need **ADB and fastboot** to unlock your bootloader and flash the OS.

- Windows: <https://dl.google.com/android/repository/platform-tools-latest-windows.zip> . Extract to folder where you will use these programs in CMD.
- Linux: `sudo apt-get install android-sdk-tools-platform -y` or your distro equivalent.

If your Oneplus 3T is running Oxygen OS 9.0.x, you will have to rollback to OOS 5.0.x or earlier to avoid issues. You can do this by:

- Using MSM Tool on windows. You have will need proper device drivers (QDLoader) to recognize phone's Qualcomm download mode. I recommend this because you can't go wrong.
  - Install device driver's with this guide: <https://forum.xda-developers.com/oneplus-3t/how-to/unbrick-unbrick-tutorial-oneplus-3t-t3515306>
    - **DO NOT PERFORM STEP 1b, 2, 7, 8, AND 9**. We are using firmware in next bullet to rollback.
    - Recent windows appears to recognize this mode and installs QDLoader driver automatically. You can check by booting phone into this Qualcomm Download mode (further down / someone do hyperlink shortcut) and see if device manager has QDLoader driver. If it's unrecognized, go ahead with instructions.
  - Download this: <https://www.androidfilehost.com/?fid=11410963190603910547> (OOS 5.0.8) and extract.
- Flashing package with older firmware via TWRP. Fill this in.

You will need **eon-neos repo** and **python 3**, this should do the majority of your work!

- python3
  - Windows: <https://www.python.org/ftp/python/3.8.2/python-3.8.2.exe>
  - Linux: `sudo apt install python3` or distro equivalent.
- eon-neos: <https://github.com/commaai/eon-neos/archive/master.zip> and extract it.

### Device-specific

#### Oneplus 3T

MSM Tool Method (This will relock bootloader):

  1. Hold your power button for 40 seconds.
  2. Once it is off, hold volume up for 10 seconds and plug phone in.
    - You should see it recognize it as 'QDLoader' or 'Qualcomm 9008' and not 'Unknown devices' plus 'QHUSB_BULK'. Otherwise, you installed drivers wrong or havent.
  3. Launch MSMTool executable in extracted folder and press start.
  4. Once it finishes (goes green), it should restart. Otherwise, disconnect and boot into system.

TWRP Method:

  1. Fill me in.

### Unlocking phone

Unlocking allows you to flash custom firmware. Necessary for NEOS. You can lock bootloader after installing NEOS to save your precious bootloader warning seconds.

#### Oneplus 3T

  1. Enter settings app.
  2. Press 'About phone'.
  3. Tap 'Build Number' like a mad lad till you see results.
  4. Go back, click 'Developer Options'.
  5. Enable 'OEM unlocking' and 'Advanced Reboots'.
  6. Hold power button. Press restart then bootloader.
  7. Plug your phone in and use fastboot.
    - On windows, go to folder you extracted and open CMD. use 'fastboot.exe'
    - On linux, fastboot is avaliable in terminal.
  8. Check if phone is properly connected by typing 'fastboot devices'. It should appear and show connection as 'fastboot'.
  9. (Warning: will clear data.) Type 'fastboot oem unlock' and say yes to prompts. Your phone will clear data and reboot.

#### Leeco Pro 3

- Fill me in.

### Installation
You will use eon-neos repo to download and install NEOS OS. **DO NOT DISCONNECT THE DEVICE!**

Windows:

  1. Open powershell and run `python download.py`.
  2. Put your Eon into fastboot mode by turning off your Eon, then holding volume down + power (comma two, eon gold), or volume up + power (eon).
  3. Run flash.ps1 (right click, run with powershell).
  
Linux/OS X:
  1. Open a terminal.
  2. Run `./download.py`
  3. Put your Eon into fastboot mode by turning off your Eon, then holding volume down + power (comma two, eon gold), or volume up + power (eon).
  4. Run `./flash.py`

Success! With NEOS OS installed, you are ready to install OpenPilot.

## Other / Old guides

* Image Flashing
  * https://medium.com/@kirk_40929/getting-comma-openpilot-running-on-a-used-phone-c72d609cb4d3
  * https://drive.google.com/file/d/1HCqYRi2cavgelM00v4bv-S8CnI0neyaI/view

<details>
  <summary>Flashing Steps and Troubleshooting</summary>


Flashing Notes from @erich
> Images that'll work with 0.6...
> system.simg https://drive.google.com/file/d/1ySz1zLiy9bP6c8lDRgCo7k2kcCReGF__/view?usp=drivesdk
> boot.img https://drive.google.com/file/d/1c1ovbvBP8TqOEiNbh-KAPyI5hxlW1_a1/view?usp=drivesdk
> recovery.img https://drive.google.com/open?id=1mbXjhU2qlfz0jCNdDxHFnFj1YM5CeAQn
> logo.bin https://drive.google.com/file/d/1UEFVnuMp3wlfN9P9pdys33-sNlVfDkLj/view?usp=sharing

Flashing Notes from @Ari
> Just for everyone stuck, I took my working eon and flashed the latest Android 9 then flashed neos and got mac 02:00:00
> Then I flashed this unbrick image
> https://androidfilehost.com/?fid=11410963190603910547
> Booted into android 8, enabled oem unlock and unlocked the bootloader again. After it finished booting into android, > I went back to the bootloader and flashed the system and boot images extracted from this OTA zip
> https://commadist.azureedge.net/neosupdate/ota-signed-> c992abb59cbaf6588f51055db52db619061107851773fc8480acb8bb5d77a28f.zip
> Then I ran fastboot format userdata (because neos doesn't support encrypted data partition from Oxygen OS) and then I rebooted into neos and wifi was working again

</details>
