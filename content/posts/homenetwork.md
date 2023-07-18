+++
author = "Collin"
title = "My Home Network"
description = "Details on my network and how I made it"
date = 2023-07-18
+++

The goal for my home network was to make it compartmentalized, easy to use, and easy to upgrade. I wanted the subnets of the network to be compartmentalized so that untrusted devices, like IOT devices,  could be on their own and monitored. This also made it easy to track down who is who when setting up rules. It needed to be easy to use so my family members could use it without trouble. It needed to be easy to upgrade so I could tinker without messing up anyone elses connections.

## The Network
5 subnets with their own VLANs

1. Main LAN 192.168.10.1/24 VLAN 1
2. Work LAN 192.168.20.1/24 VLAN 2
3. Videogames LAN 192.168.40.1/24 VLAN 4
4. IOT LAN 192.168.30.1/24 VLAN 3
5. Guest network

Each network is isolated from one another but can be changed to talk between some devices. For example, the printer on the IOT network can recieve instructions from the work network to print but cannot send information back to the work network. Printing still works but there is no threat of the printer trying to infect the other networks if it becomes compromised. 

The Guest network is totally isolated with no way of talking to the other networks. This is used just for guests and has a time limit before disconnecting devices.

## The Hardware

I went with TP-Link products as I have had good experiences in the past with them.

- TL-R605 (router)
- TL-SG1024DE (switch)
- EAP225 (WIFI)
- Raspberry Pi (software controller)

The thing that makes everything work here is the Raspberry Pi. It is running a docker container for the Omada software controller. TP-Link makes a hardware controller but I went with the Pi because it was cheaper. The software controller connects all the Tp link hardware on the network so that they can be managed and work together. This is important as we have multiple wifi points on the network and I wanted the connection to be automatically switched to a point with a stronger connection. The software controller lets me do this. It also allows me to easily update the firmware of the devices.

I am currently setting up a read only admin account so I can log into the controller on my phone to monitor the network. If I want to make changes then I would need to log into the main admin account on my computer.

## Drawbacks

Having multiple wifi networks can make it confusing to figure out where you should connect your device to. I tried to set up one wifi network and have the mac address of the device decide which VLAN you would be on but I didn't get it to work.

While I like using TP-Link, it feels like some advanced functions are missing. 95% of the config needs to be done in a gui instead of a shell so there are limitations to what you can do.

## Overall

I like the network I have built and believe I have made it as secure as I can while making it accessible for other users on the network.
