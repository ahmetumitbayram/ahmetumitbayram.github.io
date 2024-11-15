---
layout: post
title: CMSimple 5.15 - Remote Command Execution
date: 2024-04-28
category: exploit
---

# Exploit Title: CMSimple 5.15 - Remote Command Execution
# Exploit Author: Ahmet Ümit BAYRAM
# Date: 04/28/2024
# Vendor Homepage: https://www.cmsimple.org
# Software Link: https://www.cmsimple.org/downloads_cmsimple50/CMSimple_5-15.zip
# Version: latest
# Tested on: MacOS

### Exploit Steps

1. Log in to CMSimple.
2. Go to **Settings** > **CMS**.
3. Append `,php` to the end of the `Extensions_userfiles` field and save the changes.
4. Navigate to **Files** > **Media**.
5. Select and upload `shell.php`.
6. Your shell is now available at:
   
