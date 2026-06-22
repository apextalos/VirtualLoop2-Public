# Apex Talos VirtualLoop2<br>User Guide

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

* Supply voltage: 12-24VDC or PoE
* Power consumption: 3.2W operating (7.5W peak startup)
* Temperature: -34C to +74C
* Humidity:	95% non-condensing
* Dimensions: 125 x 125 x 88 mm (4.9 x 4.9 x 3.5 in)
* Weight: 719g (25oz)

### Technical Specification

* CPU: Quad-core 64-bit ARM Cortex-A76 @ 2.4GHz
* RAM: 2Gb DDR4
* OS: Debian 13
* Flash: 128Gb Removable microSDHC
* USB: 2× 3.0 supporting simultaneous 5Gbps operation
* Ethernet: Gigabit with PoE 802.3af
* IPv4: DHCP and Static

## Models<a name="Models"></a>

### VIRTUALLOOP-2-RACK (COMING SOON)

**Form:** BIU Rack card mounted

**Power:** supplied by the BIU rack backplane at 12 VDC

**Mounting:**  BIU rack card

**Relay Control:**  None

### VIRTUALLOOP-2-DIN

**Form:** DIN rail or shelf mounted

**Power:** supplied either by nominal 12-24VDC on the front (2 pos green connector), or Ethernet (RJ45) PoE 802.3af

**Mounting:** Din or shelf 125 x 125 x 88 mm (4.9 x 4.9 x 3.5 in)

**Relay Control (COMING SOON):** 8 ea of SPDT solid state relays (1 Form C)

<img width="400" alt="front" src="https://github.com/user-attachments/assets/d2948e91-a878-47a2-b3ba-2eb85a1d9fc0" />
<img width="400" alt="back" src="https://github.com/user-attachments/assets/cc36b4e8-087b-44c8-83a2-e580cfff8e0b" />

## Interfaces<a name="Interfaces"></a>

### LEDs

**(Green) Power:** Solid on when the unit is powered

**(Green) Online:** Solid on when the unit is turned on

**(Orange) Active:** Blinks when the flash storage is in use

**(Orange) Status:** Blinks at 1Hz when the system is operating normally.  Fast blinking indicates an error

**(Yellow) SDLC:** Blinks during SDLC bus communication

### OLED Screen

Tapping the Display button rotates the screen:

1. --Network-- addressing (Static or DHCP)

<kbd><img width="400" alt="oled_network" src="https://github.com/user-attachments/assets/5b5eb45f-0594-4993-9e25-b51eb9783722" /></kbd>

1. --About-- versions
 
<kbd><img width="400" alt="oled_about" src="https://github.com/user-attachments/assets/42ae0aca-b986-45c3-86d8-e6d6f468fbbb" /></kbd>

1. --BIU #1-- Detectors 1-16
1. --BIU #2-- Detectors 17-32
1. --BIU #3-- Detectors 33-48
1. --BIU #4-- Detectors 49-64

<kbd><img width="400" alt="oled_biu" src="https://github.com/user-attachments/assets/6d593c7b-7390-48f8-a712-f02995a43a64" /></kbd>

1. --Load Switches-- 1-16

<kbd><img width="400" alt="oled_loadswitches" src="https://github.com/user-attachments/assets/23aaa649-0bc3-4715-ba38-e968a2cf3273" /></kbd>

1. --Failsafe-- Sensor monitor

<kbd><img width="400" alt="oled_failsafe" src="https://github.com/user-attachments/assets/e8020ba3-ccdf-477a-8998-03faab77eed4" /></kbd>

1. --Relays-- 1-8

IMAGE COMING SOON

### SDLC

TS2 Port 1 Serves as BIU 1-4, each with 16 detectors.  The BIU assignments and Detector calls can be operated through both the Web Server "Detector" page and REST API.

### Relays (DIN Rail Model COMING SOON)

8 relays (C/NO/NC contacts) each can switch a max of 1A @ 125VAC or 60VDC

Relays are numbered 1 through 8 with 1 closest to the front of the unit.  Each relay includes Common, Normally Open, and Normally Closed contacts.

IMAGE COMING SOON

## Factory reset<a name="FactoryReset"></a>

Holding the reset button for 5 seconds (or longer) and releasing will factory reset the device.

## Web Server<a name="WebServer"></a>

**Login page** - Requires username and password to access the unit.  Login with "user" and "V1rtualL00p!"

<kbd><img height="480" alt="login" style="border: 5px solid black;" src="https://github.com/user-attachments/assets/b605a9b7-e69b-4d07-9e78-8215b050b332" /></kbd>

**About page** - Reports location name, status, version, etc.

<kbd><img height="480" alt="about" style="border: 5px solid black;" src="https://github.com/user-attachments/assets/f2229208-ab4c-4959-9951-93211392ec33" /></kbd>

**Network page** - Used to set the device IP through either "auto" (DHCP) or "static" addressing

<kbd><img height="480" alt="network" style="border: 5px solid black;" src="https://github.com/user-attachments/assets/10bc5b5f-8d5c-4255-8b6c-dc676d00d21a" /></kbd>

**Time configuration page** - configure the time server address and check sync status

<kbd><img height="480" alt="time" style="border: 5px solid black;" src="https://github.com/user-attachments/assets/e98ff891-b1ba-40dc-a5f9-4684384a6ef7" /></kbd>

**Detector page** - Allows the user to force a detector on or off through the UI.  Also reports the number of detector activation counts.

<kbd><img height="480" alt="detectors" style="border: 5px solid black;" src="https://github.com/user-attachments/assets/3f199a59-1876-4b64-8c1a-3bcfb813d9f2" /></kbd>

**Load Switches page** - Reports the current phase by identifying the color of the approaches

<kbd><img height="480" alt="loadswitches" style="border: 5px solid black;" src="https://github.com/user-attachments/assets/31ff10bf-8d86-48fd-9db5-60331e23cba6" /></kbd>

**Failsafe page** - The device can monitor upto 4 IP address and ports.  Typically these would be the camera detection devices.  If the connection is not accepted within the specified number of seconds and failure counts, the VirtualLoop will go into FAILSAFE mode and automatically hold calls on all detectors.

<kbd><img height="480" alt="failsafe" style="border: 5px solid black;" src="https://github.com/user-attachments/assets/561cbeab-a28a-4bbf-8412-a7c82e2f694b" /></kbd>

**Logs page** - View logging data

<kbd><img height="480" alt="logs" style="border: 5px solid black;" src="https://github.com/user-attachments/assets/404e2b4d-42c0-4143-86d2-e7ff297f1d6c" /></kbd>

**Firmware page** - Remote upgrades

<kbd><img height="480" alt="firmware" style="border: 5px solid black;" src="https://github.com/user-attachments/assets/21e4c385-f771-4217-9fea-7debd6284b93" /></kbd>

**API page** - Manage API tokens

The REST API supports integration with sensor systems through simple HTTP requests.  See the swagger-ui page of any device for syntax.

<kbd><img height="480" alt="api" style="border: 5px solid black;" src="https://github.com/user-attachments/assets/ee2269cb-0b6c-4e67-9b27-12a38fcb60e6" /></kbd>

**Scripts page** - Generates the Bosch camera alarm task scripts for ease of use.

1. Enter the IP address of the VirtualLoop device, or pull from the Network page
1. Enter the API token of the VirtualLoop device, or pull from the API page
1. Fill out the table with the mappings of cameras and rules to detectors
1. Paste accordingly into your camera's Alarm Task Editors

<kbd><img height="480" alt="scripts" style="border: 5px solid black;" src="https://github.com/user-attachments/assets/7f5e185e-223d-43e1-aab4-1af646486d55" /></kbd>

Mappings coorelate the VCA rule number of the camera to a detector number of the controller.

<kbd><img width="800" style="border: 5px solid black;" alt="mappings" src="https://github.com/user-attachments/assets/24324054-14ae-4cb7-870d-85eb5d194aef" /></kbd>
<kbd><img width="800" style="border: 5px solid black;" alt="scripts_mapping" src="https://github.com/user-attachments/assets/02dd529e-a33e-40df-9daa-959085fbe181" /></kbd>


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
    - [ ] Use the VirtualLoop Web interface to enable the proper BIU #'s
    - [ ] Plugin the SDLC interface cable
    - [ ] Verify communication with the Intersection Control Unit through LEDs and exiting failsafe mode
    - [ ] Use the Scripts page to generate VCA tasks based on the rule and detector mappings
    - [ ] Install scripts onto the cameras as directed by the tool
- [ ] Additional Recommended Items
    - [ ] On the About page, set a unique intersection name or number
    - [ ] Use the Firmware pagel to install the latest firmware onto the device
    - [ ] Add failsafe monitoring configs
    - [ ] Add time synchronization configs
    - [ ] Rotate through the device screens checking for any errors
	- [ ] Check the log page for any errors

## Contact<a name="Contact"></a>

For assistance, please contact your distributor (preferred) or <brandon@apextalos.tech>
