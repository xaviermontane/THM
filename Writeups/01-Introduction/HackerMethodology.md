### The Hacker Methodology

Congratulations on making it this far! If you're enjoying the course so far, I'd appreciate it if you stared the repo in order to stay tuned for new writeups.
<br><br>
This writeup focuses on the idea of hacker methodology. Like any good craftsman, we ought to have a structure to our process. This is absolutely true in the cybersecurity field. With all of the information publicly available online, we tend to experience analysis paralysis, yet hacking is a long and extensive process.
Therefore, to better optimize our operations, we must seek some sort of structure.

**What process does a Hacker follow?**

Before we answer this question, I would first like to provide some clarifying statements. Hackers are not malicious actors; they're actually IT professionals that leverage their knowledge of systems to break limitations in non-conventional ways.
<br>
With this said, there are different levels of ethics within the field, and we often label these levels of ethicality with the color of our hat.
<br><br>
Take a look at the table below to better understand the different hats:

| Color | Focus |
| ------ | ----- |
| White Hat | Ethical hackers (Pentesters, Security analysts, etc...) |
| Grey Hat | Not malicious, but not always ethical |
| Black Hat | Malicious hacker |
| Green Hat | Beginner — Although they lack the skills, they're eager to learn |
| Blue Hat | Vengeful Hacker — They can be outsource white hats for a company |
| Red Hat | Vigilante hacker — A hacker who takes aggressive steps to stop black hats |
<br>
At first glance, this may seem confusing but in reality we only look at the top three (White, Grey, Black) to label a hacker, as we progress through the course you will be able to better grasp this concept, in the meantime you can try deciding which hat you might want to become.
<br><br>
While we might assume that hackers do anything they want, experienced hackers and penetration testers often follow a set process to research and exploit their targets. In the case of pentesters, this ensures that assessments are performed consistently across the industry.
<br><br>

**This process is summarized in the following steps:**
1. Reconnaissance
2. Enumeration/Scanning
3. Gaining Access
4. Privilege Escalation
5. Covering Tracks
6. Reporting

---

### Reconnaissance

The first phase of the _Hacker Methodology_ is reconnaissance. Reconnaissance is all about collecting information about your target; this makes it the easiest step, as its more akin to conducting qualitative research. Generally speaking, during reconnaissance, we never interact with the target(s) or system(s).
<br><br>
For the sake of learning, we'll act as if we're trying to hack into Tesla, which was actually hacked in March 2023, winning the hackers $100,000 and the Model 3 that they managed to compromise.

As discussed previously in our [Google Dorking](THM/Writeups/01-Introduction/GoogleDorking.md) lesson, Google is an incredibly useful tool. With the help of our search engine we can access sites such as [Wikipedia](https://en.wikipedia.org/wiki/Tesla,_Inc.) to understand the companies history, then maybe we can take a look into their socials to discover new releases which may contain unpatched vulnerabilities, or even take a look at their [Linkedin](https://www.linkedin.com/company/tesla-motors/) to understand the company's organizational structure.

> You might think hackers use special tools to conduct research (and in some cases, that is true), but overall, they use simple tools like these to conduct research.

Reconnaissance typically entails conducting research about your target using publicly accessible resources such as Google. Despite its simplicity, reconnaissance is the single most crucial phase of a penetration test.

There are some specialized tools that we can utilize, but for now, it's good to know the following:
- Google (specifically Google Dorking)
- Wikipedia
- PeopleFinder.com
- who.is
- sublist3r
- hunter.io
- builtwith.com
- wappalyzer

---

### Scanning & Enumeration

The second phase of the _Hacker Methodology_ is Scanning and Enumeration. This phase is where the hacker will start interacting with the target to attempt to map the system and find vulnerabilities.
This is the first time we begin using more complex tools, such as:
- Nmap
- Dirb
- Metasploit
- Exploit-db
- Burp Suite
- And other very useful tools...

During this phase, the attacker is interacting with the target to determine its overall **attack surface**. The attack surface determines what the target might be vulnerable to in the Exploitation phase. These vulnerabilities might range from a webpage not being properly locked down, a website leaking information, SQL Injection, Cross Site Scripting or any number of other vulnerabilities.

> The enumeration and scanning phase is where we will try to determine WHAT the target might be vulnerable to.

#### Nmap

This is a very powerful enumeration tool. Personally, I find this tool to be one of my first steps when scanning a network. The great thing about `Nmap` is that it basically maps out the network and exposes all services that might be vulnerable to different types of attacks. Most notably, this tool is capable of:
- Listing open ports (TCP or UDP)
- Detecting the operating system and its version
- Determining what services are running and the version of the services

```
Let's try to use `Nmap` to map out my laptop's network. First off, we'll use an aggressive `Nmap` scan:
$> nmap -Pn -A -n -sT 192.168.1.7

1. Starting Nmap 7.92 ( https://nmap.org ) at 2023-10-05 15:10 CEST
2. Nmap scan report for 192.168.1.7
3. Host is up (0.00013s latency).
4. Not shown: 999 closed tcp ports (conn-refused)
5. PORT   STATE SERVICE VERSION
6. 22/tcp open  ssh     OpenSSH 9.3p2 Debian 1 (protocol 2.0)
7. Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
8. Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
9. Nmap done: 1 IP address (1 host up) scanned in 1.24 seconds
```
At first, you might be overwhelmed by the amount of data displayed on your terminal, but if we read this information line by line, we can actually make sense of what it's telling us. The IP utilized in this case is nothing more than the private IP of my own laptop, and you could also perform this scan by simply inputing the `ifconfig` command and choosing your target. <br><br> `Nmap` works in terms of ports; there's no need to understand it all right now, but ports can be easily explained as entry points for your network clients. For example, in line `6`, we see that port `22/TCP` (Number/Protocol) is open. This means we have an SSH port running, and it's what makes it possible for me to connect to my laptop from any network around the world.<br><br> _Both lines `5` and `6` provide a breakdown of the port function_. Now, this is great for me since I can connect from wherever, but it also puts me at a disadvantage since I'm exposed to everywhere, so anyone looking to exploit me could easily do it.
A lot of what I'm mentioning may sound foreign to you, but this is where the true skills of a hacker shine through. Having the ability to understand networks, systems, and services to exploit them at your will is one of the (if not the most) essential parts of hacking.

#### To -sS or to -sT ?

In the example above, I mentioned that I applied an aggressive scan. As cybersecurity specialists, we want to focus on being as secure as possible; therefore, it's important that our interactions with the system remain hidden or at least well-covered. To be as secure as possible, we will have to understand how the system behaves; in this case, `Nmap` performs what we call a SYN request, which is part of the [TCP 3-way handshake proccess](https://www.geeksforgeeks.org/tcp-3-way-handshake-process/).
<br><br>
With the `-sS` flag, the TCP packet flow is **SYN | SYN/ACK | RST**. The service that is listening on the port won't notice since the handshake never completes. On the other hand, `-sT` performs a proper handshake (**SYN | SYN/ACK | ACK**) which establishes a connection, so the service notices.
<br><br>
We use a SYN request since it's the default and most popular scan option, as it's one of the fastest ones because instead of fully connecting to the service, we basically just ask it if the host is running, as a matter of fact, this is actually one of the most common ways of performing a [Denial of Service Attack (DoS)](https://en.wikipedia.org/wiki/Denial-of-service_attack).

---

### Exploitation
Now that we have identified our vulnerabilities, it's time to hack. Although we might get excited at the thought of exploiting our target, the truth is that the exploitation phase can only be as good as the enumeration phases before it. If you do not enumerate all vulnerabilities, you may miss an opportunity, or **if you do not look hard enough at the target, the exploit you have chosen may fail entirely!**

#### MetaSploit
MetaSploit is a great tool as it has many built-in scripts that help keep things nice and organized. Metasploit scripts are most notable for their capabilities in reconnaissance, scanning, exploitation, privilege escalation, and maintaining access. Metasploit is also frequently updated with new exploits published in the Common Vulnerabilities and Exposures (CVE), so we basically have a tool that updates itself on new vulnerabilities.
<br><br>
Metasploit is a powerful framework for vulnerabilities. Let's take a look at its structure:
- **Exploits**
  - An exploit is a piece of code designed to take advantage of or _exploit_ a system. Based on the level of vulnerability, some exploits might have a stronger effect. Metasploit offers two types of exploits in accordance with the existing system vulnerabilities.
    - **Active Exploits** — Active exploits will run on a target system, exploit the system, give you access or perform a specific task, and then exit.
    - **Passive Exploits** — Passive exploits will wait until the target system connects to the exploit. This approach is often used by hackers on the internet asking you to download files or software. Once you do, you connect yourself to a passive exploit running on the hacker’s computer.
- **Payloads**
  - A payload is the code that runs through the exploit. — You use exploits to get into a system and payloads to perform specific actions. These are a variety of payloads within MS but the most common are:
    - **Singles** — Payloads that work on their own, for example keyloggers.
    - **Stagers** — Payloads that work with others, for example two payloads: one to establish a connection with the target, the other to execute an instruction.
    - **Meterpreter** — An advanced payload that lives on the target’s memory, is hard to trace, and can load/unload plugins at will.
- **Auxiliaries**
  - These are modules that help perform custom functions other than exploiting a system. For example, you can use the CERT auxiliary to check for expired SSL certificates on a network.

This may seem like a lot, but with enough practice and hands-on experience, we can better understand how to leverage these technologies to exploit any system.
<br><br>
There are many other tools that we can utilize during this phase, one of my favourite web-hacking tools is BurpSuite, a full fledged beehemoth of a tool, but really to fully understand it we'd need to make a whole different lesson for it. If you'd like to learn more about this tool check out the following [BurpSuite Guide](https://www.stationx.net/how-to-use-burp-suite/).

---

### Privilege Escalation
Throughout the exploitation phase, the goal was to gain access to the machine. Now the goal is to have higher privileges and more control over the system, preferably root privileges or as close as possible.

> In Windows, the target account is Administrator or System. Whereas in Linux, the target account is usually root.

As you can tell, discovering which Operating System a device is utilizing is quite important once its time to escalate privileges, and we should bear this in mind during our reconnaissance phase. Once we gain access as a low-level user, we will try to run another exploit or find a way to become root/administrator.

Privilege escalation can take many forms; some examples are:

- Cracking password hashes found on the target
- Finding a vulnerable service or version of a service which will allow you to escalate privilege THROUGH the service
- Password spraying of previously discovered credentials (password re-use)
- Using default credentials
- Finding secret keys or SSH keys stored on a device which will allow pivoting to another machine
- Running scripts or commands to enumerate system settings, like `ifconfig` to find network settings or the command `find / -perm
4000 -type f 2>/dev/null` to see if the user has access to any commands that can run as root.
<br><br>
These are just some examples of how privilege escalation could work, and there are many more ways in which privilege escalation could take place. Just think of this section of the methodology as getting to a higher-level user account or pivoting to another machine with the ultimate goal to "own" the machine.

---

### Covering Tracks
Now, as ethical hackers, there's no need for us to _cover our tracks_, yet it's true that as security proffesional, we should be able to understand how others cover their tracks; doing so will ensure we've got a fuller skillset when dealing with a real-life threat.

> You should always have explicit permission from the system owner regarding when the test is happening, how its occurring, and the scope of targets in any penetration test.

Since the rules of engagement for a penetration test should be agreed to before the test occurs, the penetration tester should stop when they have achieved privilege escalation and report the finding to the client.<br><br>
As such, a professional will never cover their tracks because the assessment was planned and agreed to beforehand. However, even though you do not cover your tracks, this does not relieve you of liability for your exploitation. Often, you will need to assist the IT administrator or system owner in cleaning up the exploit code that you utilized and also recommending how to prevent the attack in the future. <br><br>
While ethical hackers rarely have a need to cover their tracks, you still must carefully track and notate all of the tasks that you performed as part of the penetration test to assist in fixing the vulnerabilities and recommending changes to the system owner.

---

### Reporting
This is the final phase of the Hacker's methodology. During the reporting phase you will outline everything that you've found, this phase often includes the following:
- The Finding(s) or Vulnerabilities
- The CRITICALITY of the Finding
- A description or brief overview of how the finding was discovered
- Remediation recommendations to resolve the finding

The amount of reporting necessary during each pentest varies depending on the type of engagement that the pentester is involved in. A findings report generally goes in three formats:
- Vulnerability scan results (a simple listing of vulnerabilities)
- Findings summary (list of the findings as outlined above)
- Full formal report.

**The following is an example of a vulnerability report:**
![image](https://github.com/xaviermontane/THM/assets/101309588/24e5489a-d17b-4571-a47e-ec5c78caefdf)

A findings summary is usually something like this:
- **Finding:** SQL Injection in ID Parameter of Cats Page
- **Criticality:** Critical
- **Description:** Placing a payload of 1' OR '1'='1 into the ID parameter of the website allowed the viewing of all cat names in the cat Table of the database. Furthermore, a UNION SELECT SQL statement allowed the attacker to view all usernames and passwords stored in the Accounts table. 
- **Remediation Recommendation:** Utilize a Prepared SQL statement to prevent SQL injection attacks

Although this may seem like the most tedious phase, it's important to understand that, as security specialists, this phase is as important as many of the other phases. As a matter of fact, this phase would be the one that'd take up most of your time, even more than the enumaration and exploitation phases. Writing a proper report is another essential skill a cybersecurity professional should have under their belt.

---

## Resources

_If you want to improve your hacking capabilities, I'd recommend taking a look into the following resources:_

- [TCP/IP Model Reading List](https://www.geeksforgeeks.org/tcp-ip-model/?ref=lbp)
- [Guide to Metasploit](https://www.freecodecamp.org/news/metasploit-a-walkthrough-of-the-powerful-exploitation-framework/)
- [Mockup Reports](https://github.com/hmaverickadams/TCM-Security-Sample-Pentest-Report/tree/master)
