![fingerprinting](https://user-images.githubusercontent.com/37757984/82519263-1b4e0c00-9ad6-11ea-9ded-039a72e1d8d7.jpg)

[◄ Home](https://github.com/commaai/openpilot/wiki)

**Getting Car Unrecognized: Dashcam Mode, but have a supported make and model of car? Use the following guides to add support.**

# Fingerprinting 2.0
Used for all officially supported makes such as Honda, Toyota, and is also supported in Hyundai.
## Step 1 : Record a Drive
Ensure your comma power v2 is hooked up to your car harness. Drive around your neighborhood for a bit, then return to upload the drive on WiFi to the comma servers.
## Step 2 : Log into [useradmin](https://my.comma.ai/useradmin)
Click the most recent drive

![Screen Shot 2020-06-02 at 11 20 22 AM](https://user-images.githubusercontent.com/37757984/83562716-e3c86200-a4ce-11ea-9960-91bf334b7a8f.png)

Click the first segment (segment 0)

![Screen Shot 2020-06-02 at 11 20 49 AM](https://user-images.githubusercontent.com/37757984/83562744-f2167e00-a4ce-11ea-952d-c3a9404e0626.png)

## Step 3 : Find the firmware
Search the page for `carFw = [`

<img width="385" alt="Screen Shot 2020-06-02 at 11 21 21 AM" src="https://user-images.githubusercontent.com/37757984/83562767-fb9fe600-a4ce-11ea-9063-c5c0a509e2a2.png">

## Step 4 : Add new firmware versions

In your values.py file, add the firmware in this format. Use a [decimal to hex converter](https://www.rapidtables.com/convert/number/decimal-to-hex.html) to get the correct string to place after 0x.

```CAR.MODEL: {
    (Ecu.type, 0xAddress-converted-to-hex, 0xSub-address-converted-to-hex-'None'-if-0): [
      b'fwVersion',
      b'existingFirmware',
    ],
  },
```
Here is a filled out example for the Honda Civic. Notice the eps firmware from above is already in this list.

```CAR.CIVIC: {
    (Ecu.eps, 0x18da30f1, None): [
      b'39990-TBA,A030\x00\x00',
      b'39990-TBA-A030\x00\x00',
      b'39990-TBG-A030\x00\x00',
      b'39990-TEG-A010\x00\x00',
    ],
  },
```
Ensure that every single ecu has its firmware in this file.

### On Device

1. [SSH](../wiki/SSH/) into the comma two and navigate to /data/openpilot/selfdrive/_make_/values.py
2. Save the file and reboot

### To Your Own Fork

1. Fork openpilot into your own GitHub account
2. Clone the repo on your computer
3. Navigate to /selfdrive/_make_/values.py
4. After changes are made, push to your repo
5. Create a pull request to ensure the car is supported in the next release

# Fingerprinting 1.0
The deprecated version of fingerprinting. Used for most community supported makes.