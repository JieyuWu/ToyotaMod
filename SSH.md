![SSH into comma two](https://user-images.githubusercontent.com/37757984/82586797-0496cc00-9b4d-11ea-9e98-48d193cf38ff.jpg)

[◄ Home](https://github.com/commaai/openpilot/wiki)

# Before You Start
Ensure SSH is on in the settings of your comma two. Found in `Settings -> Developer -> Enable SSH`

## Beginner
[Workbench for Openpilot](https://github.com/jfrux/workbench#getting-started)
Workbench is a user-friendly desktop application for SSH ([Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell)) into your android device running openpilot.
 

## Advanced
You can download the id_rsa key [from the openpilot repo.](https://github.com/commaai/openpilot/blob/master/tools/ssh/key/id_rsa) With that key, you can SSH in as root on port 8022. If you're using [PuTTY](https://en.m.wikipedia.org/wiki/PuTTY), use [this file.](https://github.com/commaai/openpilot/blob/master/tools/ssh/key/id_rsa.ppk)

Make sure you have **not** added any GitHub usernames to your comma two Authorized SSH Keys, then, under Unix/Linux environment, or macOS terminal:

1) Save the key file above as a text file and name it something like key.pem

2) Run $ chmod 600 key.pem (otherwise the system will think the text file is not safe).

Then get the IP address of your comma two from `Settings > WiFi > Open WiFi Settings > More Options > Options (top right icon) > Advanced` (please make sure your comma two and your computer connect to the same WiFi).

3) To check your connection: $ ping the comma two IP address, like `ping 192.168.1.100`; please try a couple of times until you see the data exchanging. like: 
```
PING 192.168.2.1 (192.168.2.1) 56 data bytes 
64 bytes from 192.168.2.1: icmp_seq=0 ttl=64 time=1.710 ms
64 bytes from 192.168.2.1: icmp_seq=1 ttl=64 time=13.899 ms
```

4) Under a Unix/Linux, macOS terminal or PuTTY environment, use the command:

```
$ssh root@<IP address of comma two> -p 8022 -i key.pem
```

Example:
```
$ ssh root@192.168.1.100 -p 8022 -i key.pem
```

### tmux
Once you are ssh'd into the device, you can monitor openpilot outputs with tmux\
`tmux a` to attach to tmux window\
`` ` + d`` to exit tmux window (this is changed from the default `ctrl-b + d`)

### When SSH is automatically enabled/disabled
**WiFi**\
SSH is automatically enabled with a clean comma 2 factory reset. It is disabled once you start installing dashcam or custom software. You then will need to enable SSH through the phone's UI settings if you want to SSH after install. SSH'ing into the phone before installing software (and typing `tmux a`) is helpful in understanding what is going on if you are having trouble performing your install.\
\
**LTE**\
You can always SSH via the LTE connection. Follow the guide here: [https://ssh.comma.ai](https://ssh.comma.ai)

## Mobile

* Android
  * ConnectBot - https://f-droid.org/en/packages/org.connectbot/
  * Terminus - https://play.google.com/store/apps/details?id=com.server.auditor.ssh.client
  * JuiceSSH - https://play.google.com/store/apps/details?id=com.sonelli.juicessh

* iOS
  * Terminus - https://apps.apple.com/us/app/termius-ssh-shell-console-terminal/id549039908