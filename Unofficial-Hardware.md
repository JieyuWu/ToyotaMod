![Unofficial Hardware](https://user-images.githubusercontent.com/37757984/83460050-63e0c000-a41a-11ea-8041-ffe0fe9a6077.png)

[◄ Home](https://github.com/commaai/openpilot/wiki)

Community developed hardware based on EON style form factor. For webcam and pc based development click [here](../wiki/Webcam/).

Typically used for customizing an EON case or creating an EON device from scratch

# Cases

* Unibody LePro3 @CloudJ
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
The Lithium batteries in Eons cannot handle the heat of being left in an un-cooled windshield. They can expand and even explode if left in the summer heat. They also, of course, wear out.
### Problems:
1. The EON needs to know it has a battery to even try to boot.\
  The internal software of the phone needs to see that a battery exists. In the case of a OnePlus3T, it just needs to see a voltage between 4.35 and 2.9V from the battery wire. 
1. The Eon requires large spikes of power that most USB chargers (including the white/grey panda) can't provide.\
  Power is made up of Current (Amps) and Voltage. We measure power in watts usually. Watts are calculated by multiplying the current times the voltage.\
  In the case of USB, the voltage is 5 Volts. The default USB specification sets the default current to only 500ma (500 miliamps, or 1/2 of an amp.)That is not nearly enough to run an Eon. Measurements show that the eon requires a pretty constant power of over 3 Watts, and it occasionally spikes to over 10 watts. So basic usb chargers that only output 2.5W won't be able to power the Eon. Even more advanced chargers that can output more current (amps) require the device to send them a special signal to ensure it's okay to use so much.\
  On top of that constant 3 Watts, the Eon occasionally requires large spikes of power that can't be provided by most all chargers (including the white/grey Panda.) The lithium batteries in cell phones solve this because they can provide a large amount of current for small periods of time. So any time there is a big spike that USB can't handle, it's easily provided by the battery.\
When the Eon doesn't get the amount of current it needs, it simply reboots.
## 2 Solutions:
The community has come up with two ways to deal with these issues.
1. Use a DC-to-DC converter (a.k.a. a "buck converter") to take the 5V USB provides and convert it to 4.3V at the battery terminal to fool the phone into thinking it has a battery. This solves the booting issue, but can still have problems with the power spikes, since most dc-dc converters can't handle the additional current.
1. Supercapacitors. They can store and release huge amounts of current even quicker than a battery, but they have much smaller total storage. So you can connect supercapacitors to the battery leads, and as long as you get enough current from the USB to run the EON, the supercapacitors will have enough extra charge to handle the spikes. Conveniently, the OnePlus3T automatically charges the supercapacitors as if they were just batteries. They also provide a voltage that tells the Eon that it has a battery, so it allows it to boot.

Supercapacitors and DC-to-DC converters can also handle the extreme heat of a car dashboard.


<details>
<summary>Replace battery with DC-to-DC converter</summary>

#### Buck Converter Installation

_**Make sure to wrap the DC-to-DC converter in electric tape to prevent shorting**_

* Step one: Carefully remove the battery.
* Step two: Solder connections to the DC-to-DC converter.
* Step three: Solder 5V connection to the USB flex cable by stripping the middle section of the USB flex cable.
* Step four: Solder "battery" connection to battery PCB or logic board.
* Step five: Solder ground connection to the gold connector on USB flex cable or use logic board ground. 

![OnePlus3TNoBatteryWiring](https://user-images.githubusercontent.com/3239886/86073059-45cda600-ba40-11ea-906b-593ece92bd39.jpg)
</details>

<details>
<summary>Replace battery with Supercapacitors</summary>


#### This method is for the OnePlus 3T EON - not tested on LeEco
#### Note: Supercapacitors require charging. But unlike with batteries, they will try to pull as much current as possible from the charging source. The more charged they are, the less current they will try to draw. This means that completely uncharged supercapacitors will look like a short-circuit to any monitoring electronics. However, once they're partially full, they'll be kinder to the charger. The OnePlus3T seems to handle this situation well without modification.  

1. Purchase 2 supercapacitors at least 6 Farad and 2.7V. Here's a [link](https://www.amazon.com/gp/product/B082B2NZLL/ref=ppx_yo_dt_b_asin_title_o05_s00?ie=UTF8&psc=1) I used.
    1. Part number: HV0830-2R7605-R
    1. You want a low ESR Value (Max initial of 0.040ohms in this setup). Thus, the small flat low farad (less than 1F) supercaps will not work!
1. Carefully remove the battery [(iFixit how-to link)](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwi0_bfVsajqAhXSqp4KHRp_DRYQFjATegQIBBAB&url=https%3A%2F%2Fwww.ifixit.com%2FGuide%2FOnePlus%2B3%2BBattery%2BReplacement%2F119676&usg=AOvVaw0USUqLRFEuYnONLSLj3VzY)
1. Remove the tiny circuit board from the old battery (shown below). Cut the big metal from the batteries so the board comes out like below. *Take note of which direction the connector for the battery plugs into the phone's socket*, since its possible to insert upside-down. **DON'T PUT IT IN UPSIDE DOWN LATER!**
1. Cut that circuit board at the point shown in the picture.(Can just use wire-cutters)
1. Peel the blue stuff off of the [B- SDA SCL B+] section.
1. Connect 2 of the supercapacitors in series by twisting one's (+) lead and the other's (-) lead. Solder them together if you want to and **be sure to insulate them** (wrap electrical tape, captan tape or heat-shrink.)
1. Connect the free (+) in your capacitor array to the (+) on your battery board, and the (-) in your capacitor array to the (-) on your battery board. Depending on how you physically mount all of this, you may need to use wires to connect the capacitors to the board.
1. **INSULATE all bare wires and connections**. That includes the leads to the capacitors. They can't touch any other metal.
1. Test if it all works.
    1. Plug your battery board back into it's socket [**DON'T PLUG IN UPSIDE-DOWN!**]
    1. Then plug your USB in and see if it boots.
    1. It may take a few times to boot fully while it tries to charge the capacitors. It may also show the "batteries too low" screen.  But it should eventually (and from now on) boot just fine. 
1. Mount capacitors and alter case as needed to close up the phone
1. Somehow arrange inside your case or alter your case so the capacitors fit and are mounted well.

![BatteryBoard](https://user-images.githubusercontent.com/3239886/86186825-4d9c5180-baf7-11ea-9f64-7b79b6039a53.jpg)
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

#### Le Eco LePro 3

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
  4. Run `./flash.sh`

Success! With NEOS OS installed, you are ready to install OpenPilot.

## Other / Old guides

* Image Flashing
  * https://medium.com/@kirk_40929/getting-comma-openpilot-running-on-a-used-phone-c72d609cb4d3
  * https://drive.google.com/file/d/1HCqYRi2cavgelM00v4bv-S8CnI0neyaI/view

<details>
  <summary>Flashing Steps and Troubleshooting</summary>


Flashing Notes from @Erich
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

# Installation schematics

![](http://justine-haupt.com/bolt/images/openpilot_BoltConfigurations.png)

# Hardware Modifications/Additions

* [Smart DSU/SDSU](https://github.com/commaai/openpilot/wiki/Smart-DSU)
* [Zorro Steering Sensor](https://github.com/commaai/openpilot/wiki/Zorro-Steering-Sensor)