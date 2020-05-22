![SSH into comma two](https://user-images.githubusercontent.com/37757984/82586797-0496cc00-9b4d-11ea-9e98-48d193cf38ff.jpg)

[◄ Home](https://github.com/commaai/openpilot/wiki)

You can download the id_rsa key [from the openpilot repo.](https://github.com/commaai/openpilot/blob/master/tools/ssh/key/id_rsa) With that key you can SSH in as root on port 8022. If you're using PuTTY, you'll need to convert that id_rsa (private key) into a .ppk (PuTTY Private Key)... no passwords needed.

Just save the above key as a text file, name it "key.pem" or anything you like;

1) Under Unix/Linux environment, or Mac terminal, please run: $ chmod 600 key.pem (otherwise the system will think the text file is not safe).

2) To connect to your comma two using this key, save the text above to a blank text file and name the file key.pem. (Just make save it into the same working directory, to check using commands "pwd" and "ls".

Then get the IP address of your comma two in settings under settings > wifi > advanced (please make sure your comma two and your computer connect to the same WiFi).

3) To check your connection: $ ping the comma two IP address, like "ping 192.168.1.100"; please try a couple times until you see the data exchanging. like: "PING 192.168.2.1 (192.168.2.1): 56 data bytes 64 bytes from 192.168.2.1: icmp_seq=0 ttl=64 time=1.710 ms 64 bytes from 192.168.2.1: icmp_seq=1 ttl=64 time=13.899 ms"

4) Under a linux, MAC machine or PuTTY environment, use the command:

ssh root@(IP address of comma two) -p 8022 -i key.pem

like "$ ssh root@192.168.1.100 -p 8022 -i key.pem"