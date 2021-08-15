# raspberry-pi-zero-first-start

1. Download latest Raspbian (https://www.raspberrypi.org/software/operating-systems/)
2. Install OS using Etcher (https://www.balena.io/etcher/)
3. Open terminal with sd-cart/boot
```touch ssh```
```sudo nano config.txt```
and add `dtoverlay=dwc2` at the bottom and save
```sudo nano cmdline.txt```
after the word `rootwait` add `modules-load=dwc2,g_ether` with spaces
4. In internet connection setting (IPv4 card) change to `Link-Local only`
5. Try to connect with `pi@raspberrypi.local` or lunch `ping raspberrypi.local` and use `ssh pi@<ip>` (default password is `raspberry`)
6. For WiFi connection (when you are in SSH)
```sudo nano /etc/wpa_supplicant/wpa_supplicant.conf```
add at the bottom and save
```
network={
  ssid="NETWORK"
  psk="PASSWORD"
}
```
7. Type `sudo wpa_cli reconfigure` to apply changes
