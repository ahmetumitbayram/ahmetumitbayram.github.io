---
layout: post
title: Sublime Text 4 - OS Command Injection
date: 2023-09-17
category: exploit
---

# Exploit Title: Sublime Text 4 - OS Command Injection
# Discovered by: Ahmet Ümit BAYRAM
# Discovered Date: 17.09.2023
# Vendor Homepage: https://www.sublimetext.com
# Software Link: https://www.sublimetext.com/download_thanks?target=win-x64
# Tested Version: 4 (latest)
# Tested on: Windows 2019 Server 64bit

### Steps to Reproduce

1. Open Sublime Text.
2. Navigate to **Tools > Build System > New Build System...**
3. In the newly opened configuration window, paste the following code:

    ```json
    {
        "shell_cmd": "your reverse shell code goes here",
        "shell": true
    }
    ```

4. Use the **File > Save** option to save this configuration. (For example, save it as `ReverseShell.sublime-build`).
5. From the **Tools > Build System** menu, select the `ReverseShell` option that you just saved.
6. Press `Ctrl + B` to run the build system.
7. Your reverse shell should now be active.

Replace `"your reverse shell code goes here"` with your actual reverse shell command to establish a connection.
