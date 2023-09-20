### The Hacker Methodology

Congratulations on making it this far! If you're enjoying the course so far I'd appreciate if you stared the repo in order to stay tuned on new writeups.
<br><br>
This writeup focuses on the idea of the hacker methodology, like any good craftsman we ought to have a structure to our process, this is absolutely true in the cybersecurity field. With all of the information publicly available online, we tend to experience analysis paralysis, yet hacking is a long and extensive process.
Therefore, to better optimize our operations we must seek some sort of structure.

**What proccess does a Hacker follow?**

Before we answer this question I would first like to provide some clarifying statements, Hackers are not malign actors, they're actually IT proffesionals that leverage their knowledge of systems to break limitations in non-conventional ways.
<br>
Now with this said, there's different levels of ethics within the field, and we often label the different levels of ethicality with the colour of our hat.
<br><br>
Take a look at the table below to better understand the different hats:

| Colour | Focus |
| ------ | ----- |
| White Hat | Ethical hackers (Pentesters, Security analysts, etc...) |
| Grey Hat | Not malicious, but not always ethical |
| Black Hat | Malicious hacker |
| Green Hat | Beginner — Although they lack the skills, they're eager to learn |
| Blue Hat | Vengeful hacker — They can also be outsourced white hats for a compnay |
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

The first phase of the _Hacker Methodology_ is Reconnaissance. Reconnaissance is all about collecting information about your target, this makes it the easiest step as its more akin to conducting qualitative research. Generally speaking, during reconnaissance we never interact with the target(s) or system(s).
<br><br>
For the sake of learning we'll act as if we're trying to hack into Tesla, which was actually hacked in March of 2023 winning the hackers $100,000 and the Model 3 that they managed to compromise.

As discussed previously in our [Google Dorking](THM/Writeups/01-Introduction/GoogleDorking.md) lesson, Google is an incredibly useful tool. With the help of our search engine we can access sites such as [Wikipedia](https://en.wikipedia.org/wiki/Tesla,_Inc.) to understand the companies history, then maybe we can take a look into their socials to discover new releases which may contain unpatched vulnerabilities, or even take a look at their [Linkedin](https://www.linkedin.com/company/tesla-motors/) to understand the company's organizational structure.
