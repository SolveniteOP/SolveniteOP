---
title: "WebStrike | CyberDefenders Lab Walkthrough"
seoTitle: "WebStrike Walkthrough"
seoDescription: "A short walkthrough on the WebStrike Lab on CyberDefenders."
datePublished: Mon Jun 16 2025 17:01:50 GMT+0000 (Coordinated Universal Time)
cuid: cmbzcdcqz000i02jl20nn141s
slug: webstrike-walkthrough
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1750092973040/97de45bb-618f-4063-8d6e-bbd0affdbb98.png
tags: security, cybersecurity, network-security, cyber-security, cyber, cybersecurity-1, cybersec, blue-team, wireshark, blueteam, cyberdefenders, writeups, cyber-2

---

### Introduction:

Hey everyone! Been a while since I posted a writeup on here. I was super busy with university and stuff but now i’m going to go back to writing CTF write ups!

Here’s the link to the lab: [https://cyberdefenders.org/blueteam-ctf-challenges/webstrike/](https://cyberdefenders.org/blueteam-ctf-challenges/webstrike/)

---

## Q1- Understanding the geographical origin of the attack aids in geo-blocking measures and threat intelligence analysis. What city did the attack originate from?

Start off by opening the Pcap file. We find that that the Source IP that sends the most requests is **117.11.88.124**, which is a pretty good indicator of malicious behaviour.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1750092959444/12c8e029-7666-4af7-b0bd-515ef377a0fb.png align="left")

Searching this address on [WhatIsMyIPAddress](https://whatismyipaddress.com/) gives us the answer to our first question.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1750092961615/6ef20886-427c-4b5e-bcca-bfcd96cb13ee.png align="left")

> Answer: Tianjin
> 
> ---

## Q2-Knowing the attacker’s user-agent assists in creating robust filtering rules. What’s the attacker’s user agent?

We use the filter **http.request.method == “GET”** to get the User Agent. Then just inspect the Packet Details Pane to find the header.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1750092964364/2261919c-fc15-4822-b616-8f21875469a8.png align="left")

> Answer: Mozilla/5.0 (X11; Linux x86\_64; rv:109.0) Gecko/20100101 Firefox/115.0
> 
> ---

## Q3-We need to identify if there were potential vulnerabilities exploited. What’s the name of the malicious web shell uploaded?

To find a malicious web shell upload, search for packets that have source **IP =117.11.88.124** using **HTTP** with **POST** method.

This is because uploads use the POST method to actually paste the file with the exploit it. Filtering with the post method streamlines our packets, so we can search for the upload easily.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1750092966272/94bcf3a2-cb91-4b25-ab17-c715a8fe99ff.png align="left")

> Answer: image.jpg.php
> 
> ---

## Q4-Knowing the directory where files uploaded are stored is important for reinforcing defences against unauthorized access. Which directory is used by the website to store the uploaded files?

Since we already have the name of the malicious script , searching for it helps us follow it’s execution.

It’s also quite obvious that the /uploads/ subdomain is where the attacker would try to upload the script first ’cause it’s the uploads section.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1750092967843/dbf199ea-0444-45d8-81e3-73695064aa2d.png align="left")

> Answer: /reviews/uploads/
> 
> ---

## Q5-Identifying the port utilized by the web shell helps improve firewall configurations for blocking unauthorized outbound traffic. What port was used by the malicious web shell?

To find this, go back to the POST method that has the upload in it. The script is visible along with the nc listening IP and port used by the attacker.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1750092969585/87170219-a914-4fa2-aba0-fa80bf30a93c.png align="left")

> Answer: 8080
> 
> ---

## Q6-Understanding the value of compromised data assists in prioritizing incident response actions. What file was the attacker trying to exfiltrate?

To see this response, find the packet that has the **source IP 24.49.63.79 and destination IP 117.11.88.124 using the POST method**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1750092970871/13b0a531-9197-4b94-9656-d01ec78c0523.png align="left")

> Answer: passwd
> 
> ---