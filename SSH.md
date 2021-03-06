![SSH into comma two](https://user-images.githubusercontent.com/37757984/82586797-0496cc00-9b4d-11ea-9e98-48d193cf38ff.jpg)

[◄ Home](https://github.com/commaai/openpilot/wiki)

# Before You Start
1. Ensure SSH is on in the settings of your comma two. Found in `Settings -> Developer -> Enable SSH`
2. If you have entered a GitHub username in `Settings -> Developer -> GitHub Username` you must use the private key of a public key saved in your GitHub settings, see [ssh.comma.ai](https://ssh.comma.ai/) for details.  It is highly recommended that new users **not** enter a GitHub Username.
3. Assuming you are using a GitHub Username to SSH, make sure you follow the steps [here](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/connecting-to-github-with-ssh): to create and test your SSH keys.

Table of Contents
=================

   * [Beginner](#beginner)
      * [Option 1 - Putty SSH Client](#option-1---putty-ssh-client)
      * [Option 2 - Preinstalled OpenSSH Client on Windows 10](#option-2---pre-installed-openssh-client-on-windows-10)
      * [Option 3 - Workbench](#option-3---workbench)
   * [Advanced](#advanced)
      * [OpenSSH or Similar Client](#openssh-or-similar-client)
      * [Connecting to ssh.comma.ai](#connecting-to-sshcommaai)
         * [Using OpenSSH](#using-openssh)
         * [Using Putty to Connect to ssh.comma.ai](#using-putty-to-connect-to-sshcommaai)
   * [Mobile SSH Clients](#mobile-ssh-clients)
   * [Troubleshoot SSH Issues](#troubleshoot-ssh-issues)
      * [I'm hotspotting my comma two/phone. What IP do I use?](#im-hotspotting-my-comma-twophone-what-ip-do-i-use)
      * [When SSH is automatically enabled/disabled](#when-ssh-is-automatically-enableddisabled)
      * [Invalid Format when trying to connect](#invalid-format-when-trying-to-connect)
      * [No route to host](#no-route-to-host)
      * [Permission denied (publickey,keyboard-interactive)](#permission-denied-publickeykeyboard-interactive)

# Beginner

## Option 1 - Putty SSH Client
Putty is a simple beginner friendly way to connect to a comma device via SSH.
1. Download and install Putty.
2. Download and save the [Putty Private Key](https://github.com/commaai/openpilot/blob/master/tools/ssh/key/id_rsa.ppk) `Right click the 'Raw' button and Save As to download`
3. Get the IP address of your EON/C2 in settings under `Settings > WiFi > Open WiFi Settings > More Options > Three Dots in Top Left > Advanced` (Please make sure your EON and your computer connect to the same WiFi)
4. Open Putty, and enter the hostname as `root@<ip_address>` where <ip_address> is your device IP and change the port to `8022`:

![Putty Main Page](https://user-images.githubusercontent.com/3046315/87094708-3561bc00-c1f4-11ea-96c9-0029bda9664e.png)

5. Load the private key file in `Connection > SSH > Auth > Private key for authentication`:

![Putty Private Key](https://user-images.githubusercontent.com/3046315/86837824-54c1e300-c054-11ea-9b61-fdbfefa8e834.png)

6. Finally, click `Open` on the bottom of the program, and if all works correctly, an SSH connection will be created.

## Option 2 - Pre-installed OpenSSH client on Windows 10

Windows 10 already comes with a SSH client and has everything you need to SSH into an EON/C2. No additional software download or installation required.

1. Get the IP address of your EON/C2 in settings under `Settings [⚙️ icon] > WiFi > Open WiFi Settings > More Options > Three Dots in Top Right > Advanced`
   * Please make sure your EON/C2 and your computer connect to the same WiFi or network.
2. Open PowerShell. You can find PowerShell by pressing the Start Menu and typing "PowerShell".
3. Run the command `Invoke-WebRequest "https://raw.githubusercontent.com/commaai/openpilot/master/tools/ssh/id_rsa" -OutFile "id_rsa"`
   * This will save a file called `id_rsa` to the current directory, which is likely `C:\Users\<your username here>\`. 
4. Run the command `ssh -i id_rsa -p 8022 root@555.555.555.555` after replacing `555.555.555.555` with the IP address you discovered in the settings earlier.
   * If you get "permission denied": on the EON/C2 under tap the `Settings [⚙️ icon] > Developer > Authorized SSH Keys [edit] > Remove all` button and try again. While you're here, make sure again that "Enable SSH" option is enabled.

## Option 3 - Workbench
[Workbench for Openpilot](https://github.com/jfrux/workbench#getting-started)
Workbench is a user-friendly desktop application for SSH ([Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell)) into your android device running openpilot.
   * Note - Workbench is no longer maintained by the developer. Things may not always work as expected. It is suggested to learn how to SSH using a method above (which will help you if you want to SSH into other, non-comma, devices in the future.) 

# Advanced
This section assumes that you have used SSH before.  If you want to use Putty, use [the instructions above](https://github.com/commaai/openpilot/wiki/SSH#option-1---putty-ssh-client).  

## OpenSSH or Similar Client
1. Download the private key [from the openpilot repo.](https://github.com/commaai/openpilot/blob/master/tools/ssh/id_rsa). Save the key file as a text file and name it something like key.pem.
2. Open a terminal
3. Run `$ chmod 600 key.pem` (otherwise, the system will think the text file is not safe).
4. Get the IP address of your comma two from `Settings > WiFi > Open WiFi Settings > More Options > Options (top right icon) > Advanced` (please make sure your comma two and your computer connect to the same WiFi).
5. Ping the device address from your computer to make sure it is reachable.
6. Under a Unix/Linux, macOS terminal or Windows 10 with OpenSSH, use the command:

```
$ssh root@<IP address of comma two> -p 8022 -i key.pem
```

Example:
```
$ ssh root@192.168.1.100 -p 8022 -i key.pem
```

## Connecting to ssh.comma.ai
### Using OpenSSH
The instructions on [ssh.comma.ai](https://ssh.comma.ai/) for a saved connection are slightly wrong.  If you want to connect to your comma device by typing `ssh comma-{dongleid}` your `~/.ssh/config` file should read as follows (Note the ${%h} entries in the ProxyCommand):

```
Host comma-*
  Port 22
  IdentityFile ~/.ssh/my_github_key
  ProxyCommand ssh ${%h}@ssh.comma.ai -W ${%h}:%p

Host ssh.comma.ai
  Hostname ssh.comma.ai
  Port 22
  IdentityFile ~/.ssh/my_github_key
```

Better yet, if you just want to connect directly to your vehicle without memorizing your DongleID you can do as follows (replacing <DongleID> with, you know the ID.  You can change the hostname <comma-rav4> to anything) then you can use `ssh comma-rav4`:

```
Host comma-rav4
  Port 22
  IdentityFile ~/.ssh/my_github_key
  ProxyCommand ssh <DongleID>@ssh.comma.ai -W <DongleID>:%p

Host ssh.comma.ai
  Port 22
  IdentityFile ~/.ssh/my_github_key
  Hostname ssh.comma.ai
```

The one time connection listed on [ssh.comma.ai](https://ssh.comma.ai/) works just fine.

### Using Putty to Connect to ssh.comma.ai
Using Putty to connect to ssh.comma.ai is a bit involved.  First, it assumes you have already gotten the direct SSH connection using Putty to work as described [above](#option-1---putty-ssh-client).

1. Start the pageant program (it is found in the same folder as Putty).
2. Pageant will load in your taskbar ![](https://user-images.githubusercontent.com/3046315/87094964-b456f480-c1f4-11ea-971e-57e4ba63e161.png).  Right click the icon and select View Keys

![](https://user-images.githubusercontent.com/3046315/87095063-e7998380-c1f4-11ea-9843-474119b4e6bb.png)

3. Click Add Key

![image](https://user-images.githubusercontent.com/3046315/87095188-24fe1100-c1f5-11ea-8c43-65abfbc20589.png)

4. Locate and select your private key `id_rsa.ppk`
5. After opening the key, you should see it in the key list

![image](https://user-images.githubusercontent.com/3046315/87095343-6ee6f700-c1f5-11ea-8749-6a91d55be424.png)

6. You can click Close (pageant will keep running)
7. Open Putty
8. In the Host Name enter `root@<dongleid>` where <dongleid> is your dongle id and Port `22`

![image](https://user-images.githubusercontent.com/3046315/87095535-c08f8180-c1f5-11ea-9e3d-69707f93d306.png)

9. Under `Connection > Proxy` enter the following:
- Proxy type `Local`
- Proxy hostname `ssh.comma.ai`
- Port `22`
- Telnet command or local proxy command `plink.exe -v %host@%proxyhost -nc %host:%port`

![image](https://user-images.githubusercontent.com/3046315/87095770-31cf3480-c1f6-11ea-9b42-3a37415d50c1.png)

10. Go back to `Session`
11. Type a name in `Saved Session`

![image](https://user-images.githubusercontent.com/3046315/87095535-c08f8180-c1f5-11ea-9e3d-69707f93d306.png)

12. Click `Save`
13. Click `Open`
14. You may get a few prompts to accept the server fingerprints.

You should now be connected to your device.  If you made any mistakes, you can load the saved session and fix the errors, but be sure to click `Save` after making any changes, or they will not be permanent.

Pageant will keep running until you log off your computer.  You can also exit pageant by right-clicking the taskbar icon and selecting `Exit`.

# Mobile SSH Clients

* Android
  * ConnectBot - https://f-droid.org/en/packages/org.connectbot/
  * Terminus - https://play.google.com/store/apps/details?id=com.server.auditor.ssh.client
    - Supports Putty .ppk key.
  * JuiceSSH - https://play.google.com/store/apps/details?id=com.sonelli.juicessh
  
* iOS
  * Terminus - https://apps.apple.com/us/app/termius-ssh-shell-console-terminal/id549039908

# Troubleshoot SSH Issues

## I'm hotspotting my comma two/phone. What IP do I use?
**If your Android phone is connected to comma two:** comma two should be 192.168.43.1

**If your comma two is connected to your Android phone:** comma two should be 192.168.43.2

**If you're connecting your comma two to an iPhone:** comma two should be 172.20.10.2

## When SSH is automatically enabled/disabled
**WiFi**\
SSH is automatically enabled with a clean comma 2 factory reset. It is disabled once you start installing dashcam or custom software. You then will need to enable SSH through the phone's UI settings if you want to SSH after install. SSH'ing into the phone before installing software (and typing `tmux a`) is helpful in understanding what is going on if you are having trouble performing your install.\
\
**LTE**\
You can always SSH via the LTE connection. Follow the guide here: [https://ssh.comma.ai](https://ssh.comma.ai)

## Invalid Format when trying to connect
Something is wrong with your private key.  Again, Putty and OpenSSH private keys are in different formats, make sure you are using the correct one.

## No route to host
The IP address to your device is wrong in some way.  Are both your computer and device on the same network, is the IP address typed correctly?

## Permission denied (publickey,keyboard-interactive)
This is a generic authentication error and could mean many things.  Did you enable SSH on the device?  If you entered a GitHub Username, did you use a private key that matches one in your GitHub account? Did you correctly download and save the private key file?  Does the private key have the correct permissions?