# my-linux-conf
## My Ubuntu SSD tweeks
1. in file /etc/fstab added discard,noatime,nodiratime and tmpfs. Comment out "/swapfile ..." line if exists.
```bash
UUID=SOME-ROOT-UUID / ext4 discard,noatime,nodiratime,errors=remount-ro 0 1

tmpfs /tmp tmpfs defaults,noatime,mode=1777 0 0

```
2. Turn off swapiness for 6GB or more - in file /etc/sysctl.conf set vm.swappiness
```bash
# 2 GB = 30, 4 GB = 10, 6 GB or more = 0
vm.swappiness = 0
```
source: [How to tweak and optimize SSD for Ubuntu, Linux Mint](https://itbeginner.net/tweak-optimize-ssd-ubuntu-linux-mint.html)


## AUDIO MIC PROBLEM

remap example
/etc/pulse/default.pa
```bash
load-module module-remap-source master=alsa_input.usb-046d_0809_B84881A3-02.mono-fallback rate=16000 
```
chane default rate (per user)
```bash
mkdir $HOME/.pulse/
echo "default-sample-rate = 16000" >> $HOME/.pulse/daemon.conf
pulseaudio --kill && pulseaudio --start
```
