# rpi-dietpi-main

For using this project you should own:

- Network connection with public IP.

## Installation

Follow with instructions:

### 1. Download [DietPi](https://dietpi.com) OS.

> DietPi is a extremely lightweight Debian OS. With images starting at 400MB, thats 3x lighter than 'Raspbian Lite'.


### 2. Format SD card and Flash OS image using [balenaEtcher](https://www.balena.io/etcher/)

> The Raspberry Pi's bootloader, built into the GPU and non-updateable, only has support for reading from FAT filesystems (both FAT16 and FAT32), and is unable to boot from an exFAT filesystem.

#### MAC OS:
```
$ diskutil list
$ diskutil unmountDisk disk2
$ diskutil eraseDisk FAT32 RPI /dev/disk2
```
<u>OPTIONAL</u> (if needed):
```
$ diskutil mountDisk /dev/disk2
```

### 3. <u>OPTIONAL</u>: If you want connect rapberry pi using wi-fi

#### Open card fiels using vscode
```
$ code /Volumes/boot/dietpi.txt
```
and change value for ```AUTO_SETUP_NET_WIFI_ENABLED``` from ```0``` to ```1```

#### Add settings for connect with you wi-fi network

```
$ code /Volumes/boot/dietpi-wifi.txt
```
these two configs are the most important for you
```
aWIFI_SSID[0]='WIFI_NAME'
aWIFI_KEY[0]='WIFI_PASSWORD'
```

### 4. Now you can log in to your new system and configure settings

1. Firstly, find an IP address loggin into your router and findind `DietPi` host name

2. Log in into DietPi system

> DietPi has two accounts by default "root" and "dietpi". On first boot, both share the global password "dietpi", respectively the one set in "dietpi.txt".

```
$ ssh root@ip_address_of_dietpi_machine
$ apt-get update
$ apt-get upgrade
```

3. Finish configuration after first loggin

4. Install git.

```
$ apt-get install -y git
```

5. Install project locally and run bash script.

```
$ git clone https://github.com/kubek93/rpi-dietpi-main.git /home/dietpi/rpi-dietpi-main
$ sh /home/dietpi/rpi-dietpi-main/start.sh
```

6. Install docker
```
$ curl -fsSL https://get.docker.com -o get-docker.sh
$ sudo sh get-docker.sh
```

## Good to know (not required)

### Crone process

Path to cron files:

```
/var/spool/cron/crontabs
```

Cron root file:

```
* * * * * sh /home/dietpi/rpi-dietpi-main/cron-scripts/cron.sh
```

Cron scripts for root file:

```
#!/bin/bash

mkdir -p /home/dietpi/rpi-dietpi-main/node-application/logs
cd /home/dietpi/rpi-dietpi-main/node-application
/usr/local/bin/node update_cloudflare.js

```

If you want to view cron process for current user use command: `crontab -e`

### Usefull commands

#### Linux
```
which node      : where node is located
```
#### DietPi

```
dietpi-launcher : All the DietPi programs in one place.
dietpi-config   : Feature rich configuration tool for your device.
dietpi-software : Select optimized software for installation.
htop            : Resource monitor.
cpu             : Shows CPU information and stats.
 ```
