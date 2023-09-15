### Introductory Research

Without a doubt, the ability to research effectively is _the_ most important quality for a hacker to have. By its very nature, hacking requires a _vast_ knowledge base. Everyone (professional or amateur, experienced or totally new to the subject) will encounter problems which they don't automatically know how to solve. This is where research comes in, as in the real world, you can't ever expect to simply be handed the answers to your questions.

As your experience level increases, you will find that the things you're researching scale in their difficulty accordingly; however, in the field of information security, there will never come a point where you don't need to look things up.

<details open>
<summary>Spoilers ahead, open at your own risk!</summary>
<br>
  
  - In the Burp Suite Program that ships with Kali Linux, what mode would you use to manually send a request (often repeating a captured request numerous times)?
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

#### Vulnerability Searching

Often in hacking you'll come across software that might be open to exploitation. For example, Content Management Systems (such as Wordpress, FuelCMS, Ghost, etc...) are frequently used to make setting up a website easier, and many of these are vulnerable to various attacks. So where would we look if we wanted to exploit specific software?

The answer to that question lies in websites such as:

- [ExploitDB](https://www.exploit-db.com/)
- [NVD](https://nvd.nist.gov/vuln/search)
- [CVE Mitre](https://cve.mitre.org/)

[NVD](https://nvd.nist.gov/vuln/search) keeps track of CVEs (**C**ommon **V**ulnerabilities and **E**xposures) — whether or not there is an exploit publicly available — so it's a really good place to look if you're researching vulnerabilities in a specific piece of software. CVEs take the form: **CVE-YEAR-IDNUMBER **

[ExploitDB](https://www.exploit-db.com/) tends to be very useful for hackers, as it often actually contains exploits that can be downloaded and used straight out of the box. — *It tends to be one of the first stops when you encounter software in a CTF or pentest*. 

Kali also comes pre-installed with a tool called "searchsploit" which allows you to search ExploitDB from your own machine. This is offline, and works using a downloaded version of the database, meaning that you already have all of the exploits already on your Kali Linux!

*CVEs* numbers are assigned when the vulnerability are discovered, not when they are publicised. Bear in mind that if a vulnerability is discovered at the end of a year, or if the process of confirming and rectifying the vulnerability takes a long time, then the release date might be the year after the year in the CVEdate.

### Google Dorking

Researching as a whole - especially in the context of Cybersecurity encapsulates almost everything you do as a pentester. "Search Engines" such as Google are huge indexers – specifically, indexers of content spread across the World Wide Web. These essentials in surfing the internet use “Crawlers” or “Spiders” to search for this content across the internet.
