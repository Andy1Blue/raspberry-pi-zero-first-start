# Raspberry Pi Zero - first start

1. Download Raspbian (https://www.raspberrypi.org/software/operating-systems/)

2. Install OS using Etcher (https://www.balena.io/etcher/)

3. Open terminal with sd-cart/boot

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

4. (ONLY FOR LINUX) In internet connection setting (IPv4 card) change to `Link-Local only`

5. Try to connect with `pi@raspberrypi.local` or lunch `ping raspberrypi.local` and use `ssh pi@<ip>` (default password is `raspberry`)

6. For WiFi connection (when you are in SSH)

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

7. Type `sudo wpa_cli reconfigure` to apply changes and `sudo reboot`

8. Install Docker with docker-comppose (https://docs.docker.com/engine/install/ubuntu/)

Run

```ssh
cd server
docker-compose -f docker-compose.yml up -d
```

## Useful tools

- https://pinout.xyz/pinout/5v_power - pins descriptions
