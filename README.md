# Raspberry Pi Zero - first start

1. Download Raspbian (https://www.raspberrypi.org/software/operating-systems/)

2. Install OS using Etcher (https://www.balena.io/etcher/)

3. Open terminal with sd-cart/boot
```
touch ssh
```
```
sudo nano config.txt
```
and add `dtoverlay=dwc2` at the bottom and save
```
sudo nano cmdline.txt
```
after the word `rootwait` add `modules-load=dwc2,g_ether` with spaces

4. (ONLY FOR LINUX) In internet connection setting (IPv4 card) change to `Link-Local only`

5. Try to connect with `pi@raspberrypi.local` or lunch `ping raspberrypi.local` and use `ssh pi@<ip>` (default password is `raspberry`)

6. For WiFi connection (when you are in SSH)
```
cd /etc/network
nano interfaces
```

add at the bottom

```
#auto wlan0
allow-hotplug wlan0
iface wlan0 inet manual
wpa-roam /etc/wpa_supplicant/wpa_supplicant.conf

iface default inet dhcp
```

and save

```
cd /etc
nano rc.local
```

add after `exit 0`

```
i‍‍fup wlan0
```

and save

```
sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
```

add at the bottom

```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=YOUR_COUNTRY

network={
  ssid="NETWORK"
  psk="PASSWORD"
}
```

if you need more netowrks just add next

```
network={
  ssid="NETWORK"
  psk="PASSWORD"
}
```

and save

7. Type `sudo wpa_cli reconfigure` to apply changes and `sudo reboot`

# Useful tools

* https://pinout.xyz/pinout/5v_power - pins descriptions
