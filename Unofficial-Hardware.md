Community developed hardware

Typically used for changing an EON or creating a EON device from scratch

# Cases

* Unibody Lepro3 @CloudJ
  * https://www.thingiverse.com/thing:4069425

# Mounts

* FrEON @ch4se
  * https://github.com/ch4se/OpenFrEON
* variety of mounts from @Tunder
  * https://github.com/Tundergit/openpilot-mounts
* Magnectic Mount @CloudJ 
  * https://www.thingiverse.com/thing:3497526
  * https://docs.google.com/spreadsheets/d/1UxvMszwfw6LFYjCilk6hNuoX6cheE6PvcsdKKO9ggU8/edit#gid=0
* comma2 style mount for EON case @Daehyuk
  * https://github.com/daehahn/comma1.5

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

---

# Software

* Image Flashing
  * https://drive.google.com/file/d/1HCqYRi2cavgelM00v4bv-S8CnI0neyaI/view

<details>
  <summary>Flashing Steps and Trouble Shooting</summary>


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
