# VirtualLoop User Guide

## Table of Contents
1. [Introduction](#Introduction)
1. [Models](#Models)
1. [Interfaces](#Interfaces)
1. [Factory reset](#FactoryReset)
1. [Web Server](#WebServer)
1. [Getting started checklist](#GettingStarted)
1. [Contact](#Contact)

## Introduction<a name="Introduction"></a>

The VirtualLoop is a SDLC-to-Ethernet Bus Interface Unit device.  Tested with a variety of brands of 2070 and ATC controllers, the VirtualLoop is flexible to work in many cabinet environments and a variety of different detection sensors.

### Intended use

The VirtualLoop serves as a translator for various detection technologies to be able to represent themselves to the traffic controller in a manner similar to inductive loops.  The sensor (camera, lidar, etc) places a call to the VirtualLoop REST API which is translated into calls through TS2 SDLC.

### Physical and Environmental Specification

* Temperature: -34C to +74C
* Humidity:	95% non-condensing
* Dimensions: 55 x 153 x 106mm
* Weight: 18oz
* Low power consumption: 1 Watt

### Technical Specification

* Cortex-A76 (Armv8) SoC @ 2.4GHz
* 2Gb RAM
* 128Gb Removable flash (microSD)
* 2 × USB 3.0 ports, supporting simultaneous 5Gbps operation
* Gigabit Ethernet with PoE 802.3af
* IP addressing through DHCP and Static

## Models<a name="Models"></a>

### VIRTUALLOOP-2-RACK (COMING SOON)

BIU Rack card mounted

**Power:** supplied by the BIU rack backplane at 12 VDC

**Mounting:**  BIU rack card

**Relay Control:**  None

### VIRTUALLOOP-2-DIN

DIN rail or shelf mounted

**Power:** supplied either by nominal 12-24VDC on the front (2 pos green connector), or Ethernet (RJ45) PoE 802.3af (consumes only ~1w)

**Mounting:** Din or shelf 122mm (5") wide x 123mm (5") deep x 88mm (3.5") tall

**Relay Control (COMING SOON):** 8 ea of SPDT solid state relays (1 Form C)


## Interfaces<a name="Interfaces"></a>

### LEDs
* **(Green) Power:** Solid on when the unit is powered

* **(Green) Online:** Solid on when the unit is turned on

* **(Orange) Active:** Blinks when the flash storage is in use

* **(Orange) Status:** Blinks at 1Hz when the system is operating normally.  Fast blinking indicates an error

* **(Yellow) SDLC:** Blinks during SDLC bus communication

### OLED Screen

<img height="157" alt="OLED" src="" />

Tapping the button rotates the screen:

1. --Network-- addressing (Static or DHCP)

<img height="320" alt="oled_network" src="https://github.com/user-attachments/assets/8324125f-33c3-404b-b153-0fc0e6ee639e" />

1. --About-- versions

<img height="320" alt="oled_about" src="https://github.com/user-attachments/assets/c4c23240-7b1b-4f38-ba83-f51dd031c5b3" />

1. --BIU #1-- Detectors 1-16
1. --BIU #2-- Detectors 17-32
1. --BIU #3-- Detectors 33-48
1. --BIU #4-- Detectors 49-64

<img height="320" alt="oled_biu" src="https://github.com/user-attachments/assets/9c8a2bb8-8125-4a4a-af18-227a871cea47" />

1. --Load Switches-- 1-16

<img height="320" alt="oled_loadswitches" src="https://github.com/user-attachments/assets/172dc32c-8b23-4bfb-b5d5-54945b044a14" />

1. --Failsafe-- Sensor monitor

<img height="320" alt="oled_failsafe" src="https://github.com/user-attachments/assets/52c74e19-ef57-4053-a3f1-f559614b033b" />

1. --Relays-- 1-8

### SDLC

TS2 Port 1 Serves as BIU 1-4, each with 16 detectors.  The BIU assignments and Detector calls can be operated through both the Web Server "Detector" page and REST API.

### Relays (DIN Rail Model COMING SOON)

8 relays (C/NO/NC contacts) each can switch a max of 1A @ 125VAC or 60VDC

Relays are numbered 1 through 8 with 1 closest to the front of the unit.  Each relay includes Common, Normally Open, and Normally Closed contacts.

<img width="800" alt="Relay contacts" src="" />

## Factory reset<a name="FactoryReset"></a>

Holding the reset button for 5 seconds (or longer) and releasing will factory reset the device.

## Web Server<a name="WebServer"></a>

**Login page** - Requires username and password to access the unit

<img height="480" alt="login" src="https://github.com/user-attachments/assets/b605a9b7-e69b-4d07-9e78-8215b050b332" />

**About page** - Reports version, internal voltage, device name, etc.

<img height="480" alt="about" src="https://github.com/user-attachments/assets/f2229208-ab4c-4959-9951-93211392ec33" />

**Network page** - Used to set the device IP through either DHCP or Static addressing

<img height="480" alt="network" src="https://github.com/user-attachments/assets/10bc5b5f-8d5c-4255-8b6c-dc676d00d21a" />

**Time configuration page** - configure the time server address and check sync status

<img height="480" alt="time" src="https://github.com/user-attachments/assets/e98ff891-b1ba-40dc-a5f9-4684384a6ef7" />

**Detector selection page** - Allows the user to force a detector on or off through the UI.  Also reports the number of detector activation counts and provides the user a droplist of the load switch numbers for mapping in ATSPM data

<img height="480" alt="detectors" src="https://github.com/user-attachments/assets/3f199a59-1876-4b64-8c1a-3bcfb813d9f2" />

**Load switch status page** - Reports the current phase by identifying the color of the approaches

<img height="480" alt="loadswitches" src="https://github.com/user-attachments/assets/31ff10bf-8d86-48fd-9db5-60331e23cba6" />

**Failsafe monitoring page** - The device can monitor upto 4 IP address and ports.  Typically these would be the camera detection devices.  If the connection is not accepted within the specified number of seconds and failure counts, the VirtualLoop will go into FAILSAFE mode and automatically hold calls on all detectors.

<img height="480" alt="failsafe" src="https://github.com/user-attachments/assets/561cbeab-a28a-4bbf-8412-a7c82e2f694b" />

**Log page** - View logging data

<img height="480" alt="logs" src="https://github.com/user-attachments/assets/404e2b4d-42c0-4143-86d2-e7ff297f1d6c" />

**Firmware page** - Remote upgrades

<img height="480" alt="firmware" src="https://github.com/user-attachments/assets/21e4c385-f771-4217-9fea-7debd6284b93" />

**API page** - Manage API tokens

The REST API supports integration with sensor systems through simple HTTP requests.  See the swagger-ui page of any device for syntax.

<img height="480" alt="api" src="https://github.com/user-attachments/assets/ee2269cb-0b6c-4e67-9b27-12a38fcb60e6" />

**Scripts page** - Generates the Bosch camera alarm task scripts for ease of use.

1. Enter the IP address of the VirtualLoop device
1. Fill out the table with the mappings of cameras and rules to BIUs and detectors
1. Hit the "Generate" button and now you have each of the script blocks
1. Paste accordingly into your camera's Alarm Task Editors

<img height="480" alt="scripts" src="https://github.com/user-attachments/assets/7f5e185e-223d-43e1-aab4-1af646486d55" />

<img width="1235" alt="mappings" src="https://github.com/user-attachments/assets/dc0dad7b-f46c-40ca-8c7d-655c6e1b3928" />

## Getting started checklist<a name="GettingStarted"></a>

- [ ] Installation
	- [ ] Physical mounting on DIN, Rack, or Shelf
    - [ ] Power the device either through PoE, 12/24VDC plug, or BIU rack insertion
    - [ ] Verify the unit turns on and the heartbeat light blinks 1 per second
- [ ] Networking
    - [ ] Setup a laptop to communicate on the subnet 192.168.1.XXX and plugin to the front Ethernet port
    - [ ] The device initial IP address is indicated by the OLED screen
    - [ ] Login to the unit's web interface using a browser
    - [ ] Set the proper address, subnet, and gateway IP for the network which allows communication to the sensors
- [ ] Detector integration
    - [ ] Plugin the SDLC interface cable
    - [ ] Use the VirtualLoop Web interface to enable the proper BIU #'s
    - [ ] Verify communication with the Intersection Control Unit through LEDs and exiting failsafe mode
    - [ ] Use the [Script Generator for Bosch Cameras](#Scripts) to generate VCA tasks based on the rule and detector mappings
    - [ ] Install scripts onto the cameras as directed by the tool
- [ ] Additional Recommended Items
    - [ ] On the System tab, set a unique intersection name or number
    - [ ] Use the [Firmware upgrades](#Firmware) tool to install the latest firmware onto the device
    - [ ] Add failsafe monitoring configs
    - [ ] Add time synchronization configs
    - [ ] Rotate through the device screens checking for any errors

## Contact<a name="Contact"></a>

For assistance, please contact your distributor (preferred) or <brandon@apextalos.tech>
