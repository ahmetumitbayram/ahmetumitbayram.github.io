---
layout: post
title: Typora v1.7.4 - OS Command Injection
date: 2024-05-25
category: exploit
---

# Exploit Title: Typora v1.7.4 - OS Command Injection
# Discovered by: Ahmet Ümit BAYRAM
# Discovered Date: 13.09.2023
# Vendor Homepage: http://www.typora.io
# Software Link: https://download.typora.io/windows/typora-setup-ia32.exe
# Tested Version: v1.7.4 (latest)
# Tested on: Windows 2019 Server 64bit

# # #  Steps to Reproduce # # #

# Open the application
# Click on Preferences from the File menu
# Select PDF from the Export tab
# Check the “run command” at the bottom right and enter your reverse shell
command into the opened box
# Close the page and go back to the File menu
# Then select PDF from the Export tab and click Save
# Reverse shell is ready!
            