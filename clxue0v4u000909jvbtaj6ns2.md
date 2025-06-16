---
title: "Pyramid Of Pain | SOC Level 1 - TryHackMe"
datePublished: Tue Jun 25 2024 12:33:23 GMT+0000 (Coordinated Universal Time)
cuid: clxue0v4u000909jvbtaj6ns2
slug: pyramid-of-pain-writeup
tags: security, soc, cybersecurity, cyber, cybersecurity-1, tryhackme, cybersec, blueteam, blue-teaming, cyber-2

---

Hey guys! This is my first-ever article! This is the [Pyramid Of Pain](https://tryhackme.com/room/pyramidofpainax) room from the SOC Level 1 Path in TryHackMe. Please always remember to only refer to walkthroughs when you’re stuck for 30 minutes or more on the same step. More often than not, a little bit of brainstorming will give you a clear path towards the answer. Now, let’s get into the intricacies of this room.

### Introduction {Task 1}

> Read the above.

Answer: No Answer Needed

### Hash Values (Trivial) {Task 2}

> Analyse the report associated with the hash “b8ef959a9176aef07fdca8705254a163b50b49a17217a4ff0107487f59d4a35d” [here.](https://assets.tryhackme.com/additional/pyramidofpain/t3-virustotal.pdf) What is the filename of the sample?

Answer: Sales\_Receipt 5606.xls

### **IP Addresses (Easy) {Task 3}**

> Read the following [report](https://assets.tryhackme.com/additional/pyramidofpain/task3-anyrun.pdf) to answer this question. What is the **first IP address** the malicious process (**PID 1632**) attempts to communicate with?

Answer: 50.87.136.52

> Read the following [report](https://assets.tryhackme.com/additional/pyramidofpain/task3-anyrun.pdf) to answer this question. What is the **first domain name** the malicious process ((**PID 1632**) attempts to communicate with?

Answer: craftingalegacy.com

### Domain Names (Simple) {Task 4}

> Go to [this report on app.any.run](https://app.any.run/tasks/a66178de-7596-4a05-945d-704dbf6b3b90) and provide the first **suspicious** URL request you are seeing, you will be using this report to answer the remaining questions of this task.

Answer: craftingalegacy.com

> What term refers to an address used to access websites?

Answer: Domain Name

> What type of attack uses Unicode characters in the domain name to imitate the a known domain?

Answer: Punycode attack

> Provide the redirected website for the shortened URL using a preview: [https://tinyurl.com/bw7t8p4u](https://tinyurl.com/bw7t8p4u)

Answer: https://tryhackme.com/

### Host Artifacts (Annoying) {Task 5}

> A security vendor has analysed the malicious sample for us. Review the report [here](https://assets.tryhackme.com/additional/pyramidofpain/task5-report.pdf) to answer the following questions.

No Answer Required

> A process named **regidle.exe** makes a POST request to an IP address based in the United States (US) on **port 8080**. What is the IP address?

Answer: 96.126.101.6

> The actor drops a malicious executable (EXE). What is the name of this executable?

Answer: G\_jugk.exe

> Look at this [report](https://assets.tryhackme.com/additional/pyramidofpain/vtotal2.png) by Virustotal. How many vendors determine this host to be malicious?

Answer: 9

### Network Artifacts (Annoying) {Task 6}

> What browser uses the User-Agent string shown in the screenshot above?

Answer: Internet Explorer

> How many POST requests are in the screenshot from the pcap file?

Answer: 6

### **Tools (Challenging) {Task 7}**

> Provide the method used to determine similarity between the files

Answer: Fuzzy Hashing

> Provide the alternative name for fuzzy hashes without the abbreviation

Answer: Context Triggered Piecewise Hashes

### TTPs (Tough) {Task 8}

> Navigate to ATT&CK Matrix webpage. How many techniques fall under the Exfiltration category?

Answer: 9

> Chimera is a China-based hacking group that has been active since 2018. What is the name of the commercial, remote access tool they use for C2 beacons and data exfiltration?

Answer: Cobalt Strike

### Practical: The Pyramid of Pain {Task 9}

> Complete the static site.

No Answer Needed

### Conclusion

> Read the above.

No Answer Needed