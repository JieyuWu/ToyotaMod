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

## Creating Fingerprint 1.0 (deprecated)

1. Turn off car, connect Panda to car (normally via Giraffe or car harness) and connect Panda to EON running OpenPilot.

2. If you have the car harness, disable openpilot in EON UI settings so that your car is using the stock system. If you have a giraffe, set the switches so that the stock system is enabled. For this procedure you want to collect the messages sent by the stock system, not openpilot.

3. Run these commands in 2 separate sessions (SSH into EON, run "tmux a" and press "\` + c" to create new sessions)...  
in first session run:  
    `/data/openpilot/selfdrive/boardd/boardd`  
in second session run:  
    `PYTHONPATH=/data/openpilot PREPAREONLY=1 /data/openpilot/selfdrive/debug/get_fingerprint.py`

4. Turn on the car's ignition, and wait up to ~20 seconds to ensure all the appropriate DBC messages are seen, like this...

    `number of messages 53:`  
    `fingerprint 2: 8, 64: 8, 65: 8, 72: 8, 73: 8, 280: 8, 281: 8, 290: 8, 312: 8, 313: 8, 314: 8, 315: 8, 316: 8, 326: 8, 544: 8, 545: 8, 546: 8, 552: 8, 554: 8, 557: 8, 576: 8, 577: 8, 722: 8, 801: 8, 802: 8, 805: 8, 808: 8, 816: 8, 826: 8, 837: 8, 838: 8, 839: 8, 842: 8, 912: 8, 915: 8, 940: 8, 1614: 8, 1617: 8, 1632: 8, 1650: 8, 1657: 8, 1658: 8, 1677: 8, 1697: 8, 1743: 8, 1759: 8, 1785: 5, 1786: 5, 1787: 5, 1788: 8, 2015: 8, 2016: 8, 2024: 8`

5. Turn on and off the car few times (some messages are only sent on start) and run the car for at least a minute to make sure all messages are received.

6. \<CTRL\> + C to break out of the process.

7. Copy the DBC messages obtained in step 4 into the "FINGERPRINTS" section of  
    `/data/openpilot/selfdrive/car/<car make>/values.py`  
Create new sub-section for car or overwrite pre-existing fingerprint of similar car.

8. Turn off car's ignition, then reboot EON.