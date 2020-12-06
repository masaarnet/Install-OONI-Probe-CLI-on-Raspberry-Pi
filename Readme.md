# Install OONI Probe CLI on Raspberry Pi 4

This instructions explains how to install [OONI Probe CLI](https://github.com/ooni/probe-cli) on Raspberry Pi 4

## Requirements

- Raspberry Pi 4
- Raspberry Pi OS (32-bit) Lite (Minimal image based on Debian Buster)
- SD Card
- Raspberry Pi Imager

## Installation

### Install Raspberry Pi OS

#### Download Raspberry Pi OS

- Use this [link](https://www.raspberrypi.org/software/operating-systems/) to download the last version of `Raspberry Pi OS.`
- Choose the version of OS you want, but `Raspberry Pi OS Lite` will be enough unless you want a desktop environment (You will not need it)

#### Flash Raspberry Pi OS

- Use Raspberry Pi Imager to Flash `Raspbian OS` to your SD card.
- You can download the last version of Raspberry Pi Imager from this [link](https://www.raspberrypi.org/software/).

*See: HOW TO INSTALL RASPBIAN OS to your Raspberry Pi with ease - Raspberry Pi Imager ([Video](https://www.youtube.com/watch?v=J024soVgEeM))*
#### Enable SSH and WiFi

- all instructions will use SSH connection to Raspberry Pi device. You don't need a monitor, keyboard, and mouse to implement this guide.
- To enable SSH, create an empty file called `ssh` in the boot directory
- To enable WiFi, create a file called `wpa_supplicant.conf`. Add the following to this file, in the boot directory:

`ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev`

 

`network={`

 

`ssid="YOUR_NETWORK_NAME"`

 

`psk="YOUR_PASSWORD"`

 

`key_mgmt=WPA-PSK`

 

`}`

You'll need to add your wireless network name and password.

### Boot the Raspberry Pi

- Remove the SD card from your computer, then put it in the Pi and boot
- Find the IP address of the Raspberry Pi, you will find it on your router admin page `(192.168.1.1)` or see this [link](https://howchoo.com/pi/find-your-raspberry-pis-ip-address) to know how to find Your Raspberry Pi's IP address.

#### Connect to Raspberry Pi and update OS

- Use SSH to connect to Raspberry via command: Pi: `ssh pi@192.168.1.7`

*you'll need to change IP (192.168.1.7)  to yours.*

**the default login name and password:**

`Username: pi`

`Password: raspberry`

**Use the following commands to update Raspberry Pi OS:**

`sudo -i`

 
`sudo apt-get update`

 

`sudo apt-get upgrade`

## Download & install Go Programming Language (Golang)

- Make sure that `weget` is installed on the Raspberry Pi, or install it via the following command:

`sudo apt-get install wget`
- Download `Golang` via the following command:

`wget https://golang.org/dl/go1.15.5.linux-armv6l.tar.gz`

Or, get the last version of `Golang` via the [link](https://golang.org/dl/). Make sure to choose the version for ARM Arch.

- Then, extract Golang fils via the following command:

`sudo tar --overwrite -C /usr/local -xzf go1.15.5.linux-armv6l.tar.gz`
- Install Golang via the following command:

`echo 'export PATH=$PATH:/usr/local/go/bin' >> /home/$USER/.bashrc`

 

`source /home/$USER/.bashrc`

 

`export PATH=$PATH:/usr/local/go/bin`
- Test Golang version

`go version`
## clone OONI Probe CLI

- Install git via the following command:

`sudo apt-get install git`
- Start clone ` OONI Probe CLI `via the following commands:

`mkdir -p /home/$USER/opt/ooniprobe`

 

`git clone https://github.com/ooni/probe-cli.git /home/$USER/opt/ooniprobe`

 

`cd /home/pi/opt/ooniprobe`

 

`go build -ldflags='-s -w' -v ./cmd/ooniprobe`

### Run  OONI Probe CLI

You can run `OONI Probe CLI` via the following command:

./ooniprobe

### Usage

Run `./ooniprobe help` command to get usage of `OONI Probe CLI`

**Thanks to the ["MTita"](https://github.com/mdtita) ♡**
