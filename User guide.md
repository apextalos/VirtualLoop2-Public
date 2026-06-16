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

### VIRTUALLOOP-2-RACK

BIU Rack card mounted (COMING SOON)

**Power:** supplied by the BIU rack backplane at 12 VDC

**Mounting:**  BIU rack card

**Relay Control:**  None

### VIRTUALLOOP-2-DIN

DIN rail or shelf mounted

**Power:** supplied either by nominal 12-24VDC on the front (2 pos green connector), or Ethernet (RJ45) PoE 802.3af (consumes only ~1w)

**Mounting:** Din or shelf 122mm (5") wide x 123mm (5") deep x 88mm (3.5") tall

**Relay Control (COMING SOON):** 8 ea of SPDT solid state relays (1 Form C)

<img height="300" alt="DIN" src="" />

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
1. --About-- versions
1. --BIU #1-- Detectors 1-16
1. --BIU #2-- Detectors 17-32
1. --BIU #3-- Detectors 33-48
1. --BIU #4-- Detectors 49-64
1. --Load Switches-- 1-16
1. --Failsafe-- Sensor monitor
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

<img width="400" alt="Login" src="" />

**About page** - Reports version, internal voltage, device name, etc.

<img width="400" alt="About" src="" />

**Network page** - Used to set the device IP through either DHCP or Static addressing

<img width="400" alt="Network" src="" />

**Time configuration page** - configure the time server address and check sync status

<img width="400" alt="Time" src="" />

**Detector selection page** - Allows the user to force a detector on or off through the UI.  Also reports the number of detector activation counts and provides the user a droplist of the load switch numbers for mapping in ATSPM data

<img width="400" alt="Detectors" src="" />

**Load switch status page** - Reports the current phase by identifying the color of the approaches

<img width="400" alt="Load switch" src="" />

**Failsafe monitoring page** - The device can monitor upto 4 IP address and ports.  Typically these would be the camera detection devices.  If the connection is not accepted within the specified number of seconds and failure counts, the VirtualLoop will go into FAILSAFE mode and automatically hold calls on all detectors.

<img width="400" alt="Failsafe" src="" />

**Log page** - View logging data

<img width="400" alt="Log" src="" />

**Firmware page** - Remote upgrades

<img width="400" alt="Firmware" src="" />

**API page** - Manage API tokens

The REST API supports integration with sensor systems through simple HTTP requests.  See the swagger-ui page of any device for syntax.

<img width="400" alt="API" src="" />

**Scripts page** - Generates the Bosch camera alarm task scripts for ease of use.

1. Enter the IP address of the VirtualLoop device
1. Fill out the table with the mappings of cameras and rules to BIUs and detectors
1. Hit the "Generate" button and now you have each of the script blocks
1. Paste accordingly into your camera's Alarm Task Editors

<img width="1235" alt="mappings" src="https://github.com/user-attachments/assets/dc0dad7b-f46c-40ca-8c7d-655c6e1b3928" />

<img width="400" alt="Scripts" src="" />

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
