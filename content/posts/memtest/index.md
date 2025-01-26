+++
author = "Collin"
title = "Replacing RAM"
description = "Using memtest to test new RAM"
date = 2025-01-26
+++


One of the memory sticks in my computer died this week. I found out while trying to play Marvel Rivals with my friends. Each time I would launch the game, my computer would freeze up and crash. I've been using linux for 6 years now and I've never had my computer crash on me. 

Upon closer inspection, the RAM light on my motherboard was on

![ram](images/ram.jpeg)

After looking online, the best way to test the health of memory is the tool called [memtest](https://wiki.archlinux.org/title/Stress_testing#MemTest86+). It runs before boot and has a bunch of different stress tests. You can install it with [pacman](https://wiki.archlinux.org/title/Pacman), but I would say to not do that. you'll need to change your grub config and because my drive is encrypted that would take a lot of effort to do it correctly. 

The way I used memtest is by making an Arch bootable drive as it comes included. Just change your boot options in the BIOS to select the arch bootable drive and then select memtest.

After running all the tests (you need to go into the settings to turn all of them on). Memtest would crash. This is actually because of how messed up the RAM is. Testing one memory stick at a time showed that one stick is totally good and the other can't even get to the BIOS.

I bought a new pair of memory sticks (exact same as the old pair just made this year) and running memtest shows that everything works.

[memtest](images/memtest.jpeg)
