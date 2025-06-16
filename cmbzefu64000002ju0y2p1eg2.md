---
title: "Unveiling the Power of Sherlock: A Key OSINT Tool"
datePublished: Fri Jan 24 2025 18:30:00 GMT+0000 (Coordinated Universal Time)
cuid: cmbzefu64000002ju0y2p1eg2
slug: sherlock
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1750093042714/e5757236-d0ef-49e3-adaf-ded8e8ae6f0d.png
tags: tools, security, cybersecurity, cyber, cybersecurity-1, osint, cybersec, blueteam, redteaming, sherlock, redteam, cybersecuritytools, cyber-2

---

Have you ever wondered how much of your personal information has been circulating the web? If it ever made you go “Oh, I wonder what people will do with just my username. They wouldn’t really be able to do much with it anyway”, then this article is just for you. Today we’ll explore the tool “Sherlock” and see just how much information it can gather in a matter of seconds.

---

## So what actually is Sherlock?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1750093038737/a051e4cd-bfac-4d7f-8cc0-3480ab574ffc.png align="left")

This might be the first question on your mind and rightfully so. Sherlock is an open source tool written in python with the objective of scraping the web to find usernames across social networks. As of today, Sherlock can be used to find usernames in around 300 websites and provides the link of that username on the social media platform which is absolutely WILD to even imagine and it does all of this in a matter of seconds. You could literally get all the social media links of a particular person with just a simple linux command.

---

## How does Sherlock work?

After downloading and installing [Sherlock](https://github.com/sherlock-project/sherlock) on your vm and configuring the requirements file, just run the following command:

python3 sherlock &lt;username&gt;

The python script will run and scrape the entire web to find social media presence on that particular user. Here’s an example of how it works:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1750093040682/7d1af5fe-7241-4cb4-8d32-909b05f776c2.png align="left")

In the example above, the tool is looking for usernames on all 300 social media platforms. Here, I kept the username as, “hackerman1337” just as an example and it returned 26 results with the link of the person’s online presence.

`solvenite@solvenite:~# sherlock -h   usage: sherlock [-h] [--version] [--verbose] [--folderoutput FOLDEROUTPUT]   [--output OUTPUT] [--tor] [--unique-tor] [--csv] [--xlsx]   [--site SITE_NAME] [--proxy PROXY_URL] [--json JSON_FILE]   [--timeout TIMEOUT] [--print-all] [--print-found] [--no-color]   [--browse] [--local] [--nsfw]   USERNAMES [USERNAMES ...]`

## Sherlock: Find Usernames Across Social Networks (Version 0.14.3)

positional arguments:  
USERNAMES One or more usernames to check with social networks.  
Check similar usernames using {%} (replace to '\_',  
'-', '.').

options:  
\-h, --help show this help message and exit  
\--version Display version information and dependencies.  
\--verbose, -v, -d, --debug  
Display extra debugging information and metrics.  
\--folderoutput FOLDEROUTPUT, -fo FOLDEROUTPUT  
If using multiple usernames, the output of the results  
will be saved to this folder.  
\--output OUTPUT, -o OUTPUT  
If using single username, the output of the result  
will be saved to this file.  
\--tor, -t Make requests over Tor; increases runtime; requires  
Tor to be installed and in system path.  
\--unique-tor, -u Make requests over Tor with new Tor circuit after each  
request; increases runtime; requires Tor to be  
installed and in system path.  
\--csv Create Comma-Separated Values (CSV) File.  
\--xlsx Create the standard file for the modern Microsoft  
Excel spreadsheet (xslx).  
\--site SITE\_NAME Limit analysis to just the listed sites. Add multiple  
options to specify more than one site.  
\--proxy PROXY\_URL, -p PROXY\_URL  
Make requests over a proxy. e.g.  
socks5://127.0.0.1:1080  
\--json JSON\_FILE, -j JSON\_FILE  
Load data from a JSON file or an online, valid, JSON  
file.  
\--timeout TIMEOUT Time (in seconds) to wait for response to requests  
(Default: 60)  
\--print-all Output sites where the username was not found.  
\--print-found Output sites where the username was found (also if  
exported as file).  
\--no-color Don't color terminal output  
\--browse, -b Browse to all results on default browser.  
\--local, -l Force the use of the local data.json file.  
\--nsfw Include checking of NSFW sites from default list.

---

## Disclaimer:

I do not encourage gathering information using illegitimate methods and using it against someone. Although Sherlock is legal as we’re only collecting information that is already publicly available (kinda like stalking your crush, lol), it is advised to be careful with the tool and not exploit it. It is just that using Sherlock helps you structure your search, get faster and further, and also give you various perspective you’d never know you needed. Things start getting illegal only when we start to Doxing or enter the dark side of OSINT.

Thank you for reading so far! This was my first article on a tool so do let me know how it was! Don’t hesitate to reach out for any further queries! Until next time!!