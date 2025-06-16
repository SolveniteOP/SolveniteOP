---
title: "Library | TryHackMe WriteUp"
seoTitle: "Library - TryHackMe Lab Writeup"
datePublished: Tue Jun 25 2024 12:50:45 GMT+0000 (Coordinated Universal Time)
cuid: clxuen77v00090ajn9082cewf
slug: library-tryhackme-writeup-7c80fce2651a
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1719319979602/50e12ae6-5cf8-4d71-b835-7eaf1af9a5e2.png
tags: cybersecurity, penetration-testing, cyber, cybersecurity-1, tryhackme, cybersec, write-up, red-team, red-teaming, ctf-writeup, cyber-2

---

This is quite an easy room in TryHackMe which uses brute forcing, enumerating and privilege escalating to find the flags. The objective of this room is to get user.txt and root.txt. This guide will give you context on how to go about the room.

### Enumeration

We use Nmap here to scan for open ports. I’m using the -sV -sC and -Pn commands here to give me detailed info on the target.

`sudo nmap -sC -sV -Pn <target ip>`

After the Nmap scan, we notice,

![](https://miro.medium.com/v2/resize:fit:1400/1*fXPALNLdQag-XWfQ5AJx2w.png align="left")

Here, we can see that ssh is open for login and HTTP is open on port 80, meaning there is a website. Looking under http, we can see that robots.txt is disallowed.

Now we go to the website,

`http://<IP Address>`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318328680/2429e51a-a8af-42a9-8f83-9c3e18d43e17.png align="left")

Http website on port 80

We come to this screen and right away, we can see that the blog was posted by “meliodas”. So we note this down, as it could be a potential ssh login.

I tried looking at the page source but nothing interesting could be found

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318330975/ad4bd279-f6e7-4ac0-9344-32175e8ab662.png align="left")

Page source of the HTTP website

Then, I decided to use ffuf to enumerate the website to find hidden pages

`ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http:///FUZZ -t 200`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318332932/6668746e-5b37-4c02-a9ac-e756acba46e2.png align="left")

Ffuf enumeration scan

Enumerating did not give me anything useful, so I decided to move on to the next possible step, Bruteforcing.

### Bruteforcing

Since we have a potential username “meliodas”, I decided to use Hydra to try brute forcing using rockyou on ssh.

After some time, we can see that Hydra successfully brute forced with rockyou and has given us a password

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318335438/4c712993-915a-40f7-8214-fde46089865b.png align="left")

Bruteforcing using Hydra to get SSH login credentials

Now we can ssh login using the username and password.

`ssh meliodas@IP Address`

Finally, we’ve logged into meliodas and found user.txt. Copy the output and paste it into TryHackMe

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318337158/4560ab23-c14f-46c8-832d-1faec1a094c8.png align="left")

Logging in via ssh and getting user.txt

### Privilege Escalation

The first thing we can do here, is to put in sudo -l to check if we can escalate privileges, and check files that can be run by root.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318338995/76bb2455-1467-4f9f-9b59-578eeda5eb5b.png align="left")

Checking privileges available to the user and root

Here we’re allowed to run the bak.py script.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318340661/627c24f1-8814-44b7-ad38-a4bde63de994.png align="left")

Checking permission of files

However, we can’t really modify the bak.py to put in our own exploit as it’s owned by root and we do not have write permission on it. The best we can do here is to delete the bak.py script and write our own exploit.

`rm -f bak.py`

Now we can create a new script called bak.py using nano.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318342788/0ab7164a-cdb2-4ef8-88b7-a554363bbbbc.png align="left")

We’ve used the pty spawn exploit to generate our own shell to escalate privileges. Next, we save and write this to our machine.

Now we can run the command we found earlier when we used sudo -l to be able to execute the shell and thus escalate our privileges.

`sudo /usr/bin/python3 /home/meliodas/bak.py`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318344065/52ea5566-33dd-416d-87c4-f66a2c5621ee.png align="left")

Escalated to root!

With that, our exploit has successfully worked and we’ve escalated to root.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318345483/08c10d19-5536-4f77-b030-8def552bab51.png align="left")

Opening root.txt file

Now we can go to the root directory and read root.txt to get our root file. Copy and paste the content of root.txt into TryHackMe to complete root.txt and finish the room.

And with that, we finished the room! We started off with Nmap scanning, enumerating the website, brute forcing with the username we found, and finally escalating our privileges using a simple exploit.

### Conclusion

The hardest part I found in the room was actually discovering the username itself, as I wasn’t looking hard enough and took me around 20–25 minutes to even realize using meliodas as a username to log in. This is a very good room to learn about privilege escalation, and I recommend people do it.

Thanks for reading! If you have some queries or suggestions for me, do feel free to reach out to me.