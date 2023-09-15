### Introductory Research

Without a doubt, the ability to conduct effective research is _the_ most critical skill for a hacker to possess. Hacking, by definition, requires a _vast_ knowledge base. Everyone (professional or amateur, seasoned or completely new to the subject) will face challenges that they do not know how to handle. This is where research comes in, because you can never expect to be handed the answers to your problems in the real world.

As your experience level grows, the things you're researching will become more complex; yet, in the subject of information security, there will never be a moment where you don't need to search things up.

<details>
<summary>Spoilers ahead; open at your own risk!</summary>
<br>
  
In the Burp Suite Program that ships with Kali Linux, what mode would you use to manually send a request (often repeating a captured request numerous times)?
	- Repeater mode
- What hash format are modern Windows login passwords stored in?
	- NTML Hash
- What are automated tasks called in Linux?
	- Cron jobs
- What number base could you use as a shorthand for base 2 (binary)?
	- Base 16
- If a password hash starts with `$6$`, what format is it (Unix variant)? 
	- SHA512crypt
</details>

### Vulnerability Searching

While hacking, you'll frequently come across software which could be exploited. Content Management Systems (such as Wordpress, FuelCMS, Ghost, etc...), for example, are widely used to facilitate website development, yet many of them are vulnerable to different exploits. So, if we wanted to hack certain software, where might we look?

The answer to that question lies in websites such as:

- [ExploitDB](https://www.exploit-db.com/)
- [NVD](https://nvd.nist.gov/vuln/search)
- [CVE Mitre](https://cve.mitre.org/)

[NVD](https://nvd.nist.gov/vuln/search) keeps track of CVEs (**C**ommon **V**ulnerabilities and **E**xposures) — whether or not there is an exploit publicly available — so it's a really good place to look if you're researching vulnerabilities in a specific piece of software. CVEs take the form: **CVE-YEAR-IDNUMBER**

[ExploitDB](https://www.exploit-db.com/) tends to be very useful for hackers, as it often actually contains exploits that can be downloaded and used straight out of the box. — *It tends to be one of the first stops when you encounter software in a CTF or pentest*. 

Kali Linux also comes pre-installed with a tool called "searchsploit" which allows you to search ExploitDB from your own machine. This offline tool works by using a downloaded version of the database, meaning that you already have all of the exploits already on your Kali machine!

*CVEs* numbers are assigned when vulnerabilities are discovered, not when they are publicised. Therefore, if a vulnerability is discovered at the end of a year, or if the process of confirming and rectifying the vulnerability takes a long time, then the release date might be the year after the year in the CVEdate.

### Manual Pages

_If you haven't already worked in Linux, take a look at the [Linux Fundamentals](https://tryhackme.com/module/linux-fundamentals) module._

Researching can also go beyond search engines, as most cybersecurity specialists know, being well versed in Linux is one of the most important skills a hacker can have. However, we don't always have to fall back in to the arms of our good ol' friend Google. The integrated command `man` allows users to access a manual page for most tools directly inside your terminal. It is possible to come across a tool that does not have a `man` command; thankfully, this is uncommon. In general, when you don't know how to utilize a tool, you should go to its manual first.
