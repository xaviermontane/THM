TryHackMe is **an online platform that teaches cyber security through short, gamified real-world labs**.  This platform operates through various rooms that can be acces through an OpenVPN connection, by connecting to the server students are able to deploy hacking machines by 1 click of a button, which allows them to put their knowledge into practice.

### Offensive Security
The first large area within Cyber Security is the offensive side. This area involves attacking different applications and technologies to discover vulnerabilities.

**This career benefits greatly from the following skills:**
-  Understanding how things work
-  Analytical thinking
- Thinking out of the box

The most common offensive security job role is a penetration tester. A pentester is an individual that is legally employed by an organisation to find vulnerabilities in their products, this usually requires a broad range of knowledge including, but not limited to:
- Web application security
- Network security
- Use of programming languages to write various scripts

>More recently, cloud security has also been gaining popularity as various organisations are now shifting their infrastructure to cloud providers such as AWS and Azure.

### Defensive Security
This is the second major area within Security. While Offensive Security involves actively finding vulnerabilities and misconfigurations within technologies, Defensive Security involves detecting and stopping these attacks.

**This career benefits greatly from the following skills:**
- Analytical thinking
- Problem-solving

One of the careers under this track is a Security Analyst. This is an individual in an organisation who's job is to monitor various systems and detect whether any of them are being attacked. To do this, you need to understand how underlying technologies work and then understand what attacks against these technologies look like.

While this is a very specialist role, malware analysis is quite common when detecting and responding to attacks. Malicious actors would use malicious pieces of software in any stage of their attack cycle from gaining access to a system to maintaining persistence. If you can understand what exactly this malware is doing, you can prevent further abuse and also identify the malicious action.

### Introductory Research

Without a doubt, the ability to research effectively is _the_ most important quality for a hacker to have. By its very nature, hacking requires a _vast_ knowledge base. Everyone (professional or amateur, experienced or totally new to the subject) will encounter problems which they don't automatically know how to solve. This is where research comes in, as in the real world, you can't ever expect to simply be handed the answers to your questions.

As your experience level increases, you will find that the things you're researching scale in their difficulty accordingly; however, in the field of information security, there will never come a point where you don't need to look things up.

**Let's try it out!**
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

#### Vulnerability Searching

Often in hacking you'll come across software that might be open to exploitation. For example, Content Management Systems (such as Wordpress, FuelCMS, Ghost, etc...) are frequently used to make setting up a website easier, and many of these are vulnerable to various attacks. So where would we look if we wanted to exploit specific software?

The answer to that question lies in websites such as:

- [ExploitDB](https://www.exploit-db.com/)
- [NVD](https://nvd.nist.gov/vuln/search)
- [CVE Mitre](https://cve.mitre.org/)

[NVD](https://nvd.nist.gov/vuln/search) keeps track of CVEs (**C**ommon **V**ulnerabilities and **E**xposures) — whether or not there is an exploit publicly available — so it's a really good place to look if you're researching vulnerabilities in a specific piece of software. CVEs take the form: **CVE-YEAR-IDNUMBER **

[ExploitDB](https://www.exploit-db.com/) tends to be very useful for hackers, as it often actually contains exploits that can be downloaded and used straight out of the box. — *It tends to be one of the first stops when you encounter software in a CTF or pentest*. 

Kali also comes pre-installed with a tool called "searchsploit" which allows you to search ExploitDB from your own machine. This is offline, and works using a downloaded version of the database, meaning that you already have all of the exploits already on your Kali Linux!

*CVEs* numbers are assigned when the vulnerability are discovered, not when they are publicised. Bear in mind that if a vulnerability is discovered at the end of a year, or if the process of confirming and rectifying the vulnerability takes a long time, then the release date might be the year after the year in the CVEdate.

### Google Dorking

Researching as a whole - especially in the context of Cybersecurity encapsulates almost everything you do as a pentester. "Search Engines" such as Google are huge indexers – specifically, indexers of content spread across the World Wide Web. These essentials in surfing the internet use “Crawlers” or “Spiders” to search for this content across the internet.

#### Crawlers

These crawlers discover content through various means. One being by pure discovery, where a URL is visited by the crawler and information regarding the content type of the website is returned to the search engine. In fact, there are lots of information modern crawlers scrape – but we will discuss how this is used later. Another method crawlers use to discover content is by following any and all URLs found from previously crawled websites. Much like a virus in the sense that it will want to traverse/spread to everything it can.

The diagram below is a high-level abstraction of how these web crawlers work. Once a web crawler discovers a domain such as **mywebsite.com**, it will index the entire contents of the domain, looking for keywords and other miscellaneous information - but I will discuss this miscellaneous information later.

![[Pasted image 20230912222244.png]]

In the diagram above, "**mywebsite.com**" has been scraped as having the keywords as “Apple” “Banana" and “Pear”. These keywords are stored in a dictionary by the crawler, who then returns these to the search engine i.e. Google. Because of this persistence, Google now knows that the domain “**mywebsite.com**” has the keywords “Apple", “Banana” and “Pear”. As only one website has been crawled, if a user was to search for “Apple”...“**mywebsite.com**” would appear. This would result in the same behaviour if the user was to search for “Banana”. As the indexed contents from the crawler report the domain as having “Banana”, it will be displayed to the user.

As illustrated below, a user submits a query to the search engine of “Pears". Because the search engine only has the contents of one website that has been crawled with the keyword of “Pears” it will be the only domain that is presented to the user.

![[Pasted image 20230912222351.png]]

However, as we previously mentioned, **crawlers attempt to traverse, termed as crawling, every URL and file that they can find!** Say if “**mywebsite.com**” had the same keywords as before (“Apple", “Banana” and “Pear”), but also had a URL to another website “**anotherwebsite.com**”, the crawler will then attempt to traverse everything on that URL (**anotherwebsite.com**) and retrieve the contents of everything within that domain respectively.

This is illustrated in the diagram below. The crawler initially finds “**mywebsite.com**”, where it crawls the contents of the website - finding the same keywords (“Apple", “Banana” and “Pear”) as before, but it has additionally found an external URL. Once the crawler is complete on “**mywebsite.com**”, it'll proceed to crawl the contents of the website “**anotherwebsite.com**”, where the keywords ("Tomatoes", “Strawberries” and “Pineapples”) are found on it. The crawler's dictionary now contains the contents of both “**mywebsite.com**” and “**anotherwebsite.com**”, which is then stored and saved within the search engine.

![[Pasted image 20230912222506.png]]

**So to recap, the search engine now has knowledge of two domains that have been crawled:  **
1. mywebsite.com  
2. anotherwebsite.com

Although note that “**anotherwebsite.com**” was only crawled because it was referenced by the first domain “**mywebsite.com**”. Or as illustrated below:

![[Pasted image 20230912222556.png]]

Imagine if a website had multiple external URL's (as they often do!) That'll require a lot of crawling to take place. There's always the chance that another website might have similar information as of that another website crawled - right? So how does the "Search Engine" decide on the hierarchy of the domains that are displayed to the user?

In the diagram below in this instance, if the user was to search for a keyword such as "Tomatoes" (which websites 1-3 contain) who decides what website gets displayed in what order?

![[Pasted image 20230912222652.png]]

**Review Questions**
- Name the key term of what a "Crawler" is used to do:
	- Index
- What is the name of the technique that "Search Engines" use to retrieve this information about websites?
	- Crawling
- What is an example of the type of contents that could be gathered from a website?
	- Keywords
