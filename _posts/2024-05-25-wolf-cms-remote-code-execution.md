---
layout: post
title: Wolf CMS 0.8.3.1 - Remote Code Execution
date: 2024-05-25
category: exploit
---

# Exploit Title: Wolf CMS 0.8.3.1 - Remote Code Execution (RCE)
# Date: 2023-05-02
# Exploit Author: Ahmet Ümit BAYRAM
# Vendor Homepage: https://wolf-cms.readthedocs.io
# Software Link: https://github.com/wolfcms/wolfcms
# Version: 0.8.3.1
# Tested on: Kali Linux

### Steps to Reproduce ###

# Firstly, go to the "Files" tab.
# Click on the "Create new file" button and create a php file (e.g:
shell.php)
# Then, click on the file you created to edit it.
# Now, enter your shell code and save the file.
# Finally, go to https://localhost/wolfcms/public/shell.php

### There's your shell! ###
            