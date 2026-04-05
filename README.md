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

## Setup

* configure WiFi, SSH and login in RasPi Image, then flash SD card
* boot for the first time, run apt update and `sudo raspi-config`
* [install Docker](https://docs.docker.com/engine/install/debian/)
* intall git
* clone repo
* run `docker compose up`

## Improve Docker Compose Fil

* [Home Assistant](https://www.home-assistant.io/installation/raspberrypi-other)
