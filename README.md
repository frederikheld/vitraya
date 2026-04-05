# Vitraya

> Named after the Tree of Souls on Pandora, that connects the Na'vi to Eywa and to each other through its root system.

My own [Home Assistant](https://www.home-assistant.io/) setup.

## Goals

* [ ] runs on a Raspberry Pi 4 Model B or later
* [ ] a docker setup that is defined in a single Docker compose file
* [ ] minimal additional setup required
* [ ] runs Home Assistant
* [ ] separates my smart devices from my home WiFi and from the internet
    * [ ] RasPi connects to my home WiFi
    * [ ] RasPi opens a hot spot for the smart devices to connect to
    * [ ] optional: a web interface to control which device is allowed to access the internet directly
* [ ] SD Card is protected from excessive wear
    * [ ] ramfs or simiar (I don't know what's the best approach in 2026)
    * [ ] SD card is readonly in user space. Only the system should be allowed to write
    * [ ] logging to separate USB stick or to my cloud

## Implementation

> This is a collection of ideas. Not all of them are necessarily what I'm going to choose.

* use vanilla [Rapsberry Pi OS Lite](https://www.raspberrypi.com/software/operating-systems/)
* [How to install Home Assistant via docker compose](https://www.home-assistant.io/installation/alternative/#docker-compose)
* [RaspAP](https://raspap.com/) as wireless router / network manager. Runs in Docker, but needs extended access (which makes sense, because it needs access to the network level of the OS). RaspAP can be [deployed in a Docker container](https://docs.raspap.com/get-started/docker/?h=docker#prerequisites).

## Caveats

The RasPi 4's internal WiFi does not support 5 GHz. If your router uses the same SSID for 2.4 GHz and 5 GHz networks, the RasPi 4 will fail to connect. There's a workaround:

1. configure WiFi credentials in RasPi Imager
2. before first boot, create the file `/etc/wpa_supplicant/wpa_supplicant.conf` on the "rootfs" partition of the SD card an add the following:

    ```
    ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
    update_config=1
    conuntry=DE

    network={
        ssid="<your-wifi-ssid>"
        psk="<your-wifi-secret>"
        bssid="<your-wifi-bssid>"
        key_mgmt=WPA-PSK
    }
    ```

    The important part is the BSSID, which is the MAC address of your router's 2.4-GHz-WiFi-adapter. You can find it in your router's settings.
