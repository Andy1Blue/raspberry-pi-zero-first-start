# Raspberry Pi Zero - first start

## Install Raspbian and Etcher

Download Raspbian (https://www.raspberrypi.org/software/operating-systems/)

Install OS using Etcher (https://www.balena.io/etcher/)

## First config in sd-cart/boot

```ssh
touch ssh
```

```ssh
sudo nano config.txt
```

and add `dtoverlay=dwc2` at the bottom and save

```ssh
sudo nano cmdline.txt
```

after the word `rootwait` add `modules-load=dwc2,g_ether` with spaces

## USB (SSH) connection

(ONLY FOR LINUX) In internet connection setting (IPv4 card) change to `Link-Local only`

Try to connect with `pi@raspberrypi.local` or lunch `ping raspberrypi.local` and use `ssh pi@<ip>` (default password is `raspberry`)

## WiFi connection

For WiFi connection (when you are in SSH)

```ssh
cd /etc/network
nano interfaces
```

add at the bottom

```ssh
#auto wlan0
allow-hotplug wlan0
iface wlan0 inet manual
wpa-roam /etc/wpa_supplicant/wpa_supplicant.conf

iface default inet dhcp
```

and save

```ssh
cd /etc
nano rc.local
```

add after `exit 0`

```ssh
i‍‍fup wlan0
```

and save

```ssh
sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
```

add at the bottom

```ssh
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=YOUR_COUNTRY

network={
  ssid="NETWORK"
  psk="PASSWORD"
}
```

if you need more netowrks just add next

```ssh
network={
  ssid="NETWORK"
  psk="PASSWORD"
}
```

and save

Type `sudo wpa_cli reconfigure` to apply changes and `sudo reboot`

## Install Docker

```ssh
sudo nano /boot/cmdline.txt
```

Add `cgroup_enable=memory swapaccount=1` at the end

```ssh
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker pi
sudo reboot
```

```ssh
docker version
docker run hello-world
```

## Install Docker-Compose

```ssh
sudo apt-get install libffi-dev libssl-dev
sudo apt install python3-dev
sudo apt-get install -y python3 python3-pip
sudo pip3 install docker-compose
```

```ssh
sudo systemctl enable docker
```

## Run server

```ssh
cd server
docker-compose -f docker-compose.yml up -d
```

## Useful tools

- https://pinout.xyz/pinout/5v_power - pins descriptions
