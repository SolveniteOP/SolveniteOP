---
title: "SlowLoris: A Tool for Simulated Slow HTTP Attacks"
seoTitle: "SlowLoris: A Tool for Simulated Slow HTTP Attacks"
seoDescription: "SlowLoris: A stealthy and targeted web server attack tool, exploiting HTTP vulnerabilities for minimal bandwidth consumption, causing DDOS attacks."
datePublished: Tue Jun 25 2024 12:46:42 GMT+0000 (Coordinated Universal Time)
cuid: clxuei036000408lab9gf0pyc
slug: slowloris
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1719318398034/dc091e7d-edf9-4c3d-a567-94ff6db70325.png
tags: tools, ddos, cybersecurity, cyber, cybersecurity-1, cybersec, dos-attack, cybersecuritytools, penetration-testing-tools, slowloris, cyber-2

---

What if I tell you that you can DDOS any IP with just a couple of steps? Of course, you wouldn’t believe me, but what if I tell you that it’s very true? Pretty insane right? Of course, I don’t recommend doing that as it is illegal but just knowing that tools like SlowLoris are accessible within our fingertips is interesting to know about. In this article, I’ll walk you guys over how you can test SlowLoris in a **controlled and safe environment** just to learn the tool and understand how it works.

### Disclaimer

Quick heads-up, this article is all about learning and research. If you’re planning to dive into SlowLoris or similar tools, remember: play nice and get permission from the system owners first. Using it without permission for shady stuff is illegal. Stay legal, stay ethical. I’m not liable for any problems you might get into!

### Installation and Setup

If at all you want to test this out, test it by hosting your own Apache server locally. Here are the steps:

1. Create a new Directory on your Desktop named Slowloris using the following command.
    

`mkdir Slowloris`

2\. Move to the directory that you created

`cd Slowloris`

3\. Clone the tool from Github so that you can install it on your machine

`git clone https://github.com/gkbrk/slowloris.git`

4\. Check the IP address of your machine by using

`ifconfig`

5\. Start the Apache server using the following command:

`sudo service apache2 start`

6\. Run the tool using the following command:

`python3 slowloris.py (your IP address) -s 500`

### What is SlowLoris?

SlowLoris is an attack tool designed to allow a single machine to take down an entire server by flooding it with incomplete HTTP requests, using minimal bandwidth. The approach is very similar to a distributed denial of service (DDoS) attack, making it harder for legitimate users to access the server or application. It has demonstrated remarkable effectiveness against popular web server software, including Apache 1.x and 2.x.

### How does SlowLoris work?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318396464/4a3e0dfc-1afa-4c2d-9174-75bcac0e3319.png align="left")

SlowLoris leverages a nuanced exploit within the HTTP protocol to orchestrate its attack. By initiating HTTP requests to a server, SlowLoris prompts the server to allocate resources for each incoming connection, awaiting the completion of the request. However, SlowLoris disrupts this process by perpetually maintaining connections without finalizing them.

The attack starts as SlowLoris establishes multiple connections with the target server and sends HTTP headers intermittently, but crucially, fails to conclude them. This results in a “partial request,” where the connection remains open indefinitely. It carefully regulates the rate of header transmissions to sustain the connection without triggering request completion, effectively consuming server resources.

As SlowLoris persists in maintaining these connections, the web server’s connection limit is slowly exhausted. The server, under the impression of managing substantial traffic, finds its resources strained. Consequently, legitimate users encounter difficulty in establishing new connections, leading to a successful Denial of Service (DoS) attack. It achieves this impact with minimal resource consumption, unlike traditional DoS attacks that demand significant bandwidth.

### Example of a SlowLoris Attack

1. The attacker begins by establishing multiple connections to “TrialWebServer”.
    
2. The attacker starts sending partial HTTP requests to “TrialWebServer”, but keeps the speed slow enough to maintain an open connection.
    
3. “TrialWebServer”, following standard HTTP protocol behaviour, reserves slots for these requests, awaiting their completion.
    
4. The attacker’s SlowLoris script continues to send partial requests at regular intervals, keeping the connections open and preventing “TrialWebServer” from closing the incomplete sessions.
    
5. Eventually, “TrialWebServer” hits its maximum connection pool limit. At this point, legitimate users cannot establish a new connection and any resulting connection will fail.
    
6. The web server, believing it’s under heavy traffic, continues to wait for the requests to be completed, effectively falling victim to a DoS attack.
    

### Why Are SlowLoris Attacks Dangerous?

1\. **Efficiency**: SlowLoris attacks can effectively render a targeted web server inaccessible to legitimate users with minimal resources. Unlike traditional Denial of Service (DoS) attacks that require substantial bandwidth or computational power, SlowLoris can achieve its goal with relatively modest resources, making it accessible to a wider range of attackers.

2\. **Stealth**: SlowLoris attacks are notoriously difficult to detect and mitigate. The attack’s gradual and controlled approach flies under the radar of many intrusion detection systems, as it does not trigger typical threshold-based alerts. Moreover, the attack does not generate unusual traffic patterns, making it challenging to distinguish from legitimate user behaviour.

3. **Persistent Impact**: SlowLoris attacks can have a sustained impact on a targeted web server. By keeping connections open indefinitely, SlowLoris effectively ties up server resources, preventing new connections from being established. Even after the attack ceases, the server may experience lingering effects as it attempts to recover and resume normal operations.
    

4\. **Ease of Execution**: Implementing a SlowLoris attack does not require specialized tools or advanced technical knowledge. Attackers can readily find and deploy readily available scripts to initiate SlowLoris attacks, increasing the likelihood of their occurrence.

5\. **Targeted Exploitation**: SlowLoris attacks specifically exploit vulnerabilities in how web servers handle HTTP connections. As such, they can be used to target a wide range of web servers and applications, regardless of their underlying technology stack. This versatility makes SlowLoris attacks a versatile tool for attackers looking to disrupt online services.

### How Are SlowLoris Attacks Different from Other DoS Attacks?

Unlike conventional Denial of Service (DoS) attacks, SlowLoris employs a distinctive and subtler methodology.

While DoS attacks seek to floor a server with an overwhelming amount of traffic, demanding significant bandwidth and computational resources, SlowLoris takes a different approach. It operates under the principle of “low-and-slow,” aiming to consume minimal bandwidth and often masquerading as legitimate traffic.

In contrast to traditional DoS attacks, which typically affect the entire network, SlowLoris attacks are narrowly targeted at web servers. This focused impact enhances the stealthiness of SlowLoris attacks and complicates their detection and mitigation.

Furthermore, SlowLoris exploits a specific vulnerability in the behaviour of the HTTP protocol, distinguishing it from generic volumetric attacks associated with conventional DoS tactics. Organizations must recognize these nuances and implement measures to protect their web applications and servers from targeted and sophisticated threats like SlowLoris, in addition to mitigating conventional DoS risks.

### Conclusion

Thank you for reading the article! I had a lot of fun learning about the tool and figuring out how it works. Feel free to reach out to me!