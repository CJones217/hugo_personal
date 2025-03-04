+++
author = "Collin"
title =  "AirPlay over VLAN"
date =  2025-03-03
description = "Firewall Rules For Using AirPlay Over VLANs"
+++

# Background
I recently upgraded my network from a single TP-Link router to equipment from [Ubiquiti](https://www.ui.com/introduction). This new gear gives me the ability to run managed switches, VLANs, and firewall rules. I haven't worked much with firewall rules, so I want to learn by getting AirPlay working across VLANs and (eventually) printing across VLANs.

# Why AirPlay?

AirPlay is one of those tools that you never think about, but is so cool when you have the chance to use it. Being Apple software will probably mean it is annoying to work with. These two reasons make it a perfect candidate for learning firewall rules and ports.

# Why VLANs?

I want to segment my network into Default, IoT, and guest. I want the Default network to be able to talk with the IoT network, but the IoT network can only talk back to Default when it is an established connection. AirPlay will be running on my Samsung smart TV. I don't trust it so I will be putting the TV on the IoT network. This will also help when I later setup printing from my IoT network.

# Setup

Before the firewall rules, we need to enable mDNS and IGMP Snooping on Default network and IoT network. This is what your devices will use to find other devices to screen share, AirPlay, and print to.

I also made a couple IP groups

### Internal Address - This will be used to block inter VLAN traffic

- 10.0.0.0/8
- 172.16.0.0/12
- 192.168.0.0/16

### mDNS port - This port will be used for mDNS

- 5353

### Apple Ports - These ports are what I think Apple uses with AirPlay (If I should add or remove some, let me know!)

- 192
- 515
- 548
- 554
- 631
- 1900
- 5350
- 5351
- 5353
- 5900
- 9100
- 3689
- 49152-65535
- 7000
- 7100
- 5000-5001

# Firwall Rules (In Order)

1. ALLOW mDNS port from ANY LAN to ANY LAN
2. ALLOW Apple ports from ANY LAN to ANY LAN Apple ports
3. ALLOW ALL Traffic from DEFAULT network to IoT network
4. ALLOW ESTABLISHED Traffic from IoT network to DEFAULT network
5. BLOCK ALL traffic from Internal Address group to Internal Address group


# Conclusion

With my phone on the default network and my TV on my IoT network, I am able to AirPlay directly to my TV. Both video and audio work with no lag! One problem I run into is that the first connection to the TV fails, connecting again right after works no problem. I think this is because the TV can't start up AirPlay fast enough. 

I'd like to redo how I block traffic between networks. The rule was copied from a youtube video but I'm not sure why it works. 

The last 4 lines of the AirPlay port group were found online but I have no idea why they work. Best I can find is that thye are used for fast streaming that I think is new for AirPlay. Without those ports, I could stream audio but no video (it would be a black screen after connecting).

# Sources 
- https://support.apple.com/en-us/101555
- https://service.prowise.com/hc/en-gb/articles/21514668429074-Which-ports-does-Airplay-use
- https://www.reddit.com/r/macsysadmin/comments/a3jy2y/airplay_firewall_port_reqs/
- https://discussions.apple.com/thread/4849637?sortBy=rank
- https://www.reddit.com/r/opnsense/comments/10ajz0e/anyone_have_airplay_working_across_vlans/
- https://support.apple.com/en-us/103229
- https://www.youtube.com/watch?v=seCs6gsBMT4
- https://www.youtube.com/watch?v=v0B2IDEfnjA
