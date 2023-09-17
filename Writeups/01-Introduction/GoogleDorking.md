### Google Dorking

Regardless of your technological proficiency chances are you've heard of the name Google. This search engine has stood the test of time and as a matter of fact, Google has 4.3 billion users worldwide, making it the most dominant search engine on the internet.
Research as a whole, especially in the context of cybersecurity, covers pretty much everything you do as a penetration tester. "Search Engines" such as Google are huge indexers, more specifically indexers of content spread across the World Wide Web. These essentials for surfing the internet use “Crawlers” or “Spiders” to search for this content across the web.

#### Crawlers

Crawlers aim at discovering content through various means. One of them being pure discovery, in which the crawler visits a URL and returns information about the website's content type to the search engine. In truth, current crawlers scrape a lot of data, but we'll get into how this is used later. Crawlers can also uncover material by tracking any and all URLs found on previously crawled websites. It will seek to traverse or spread to whatever it can, much like a virus.

The graphic below is a high-level representation of how various web crawlers function. When a web crawler detects a domain like **mywebsite.com**, it will index the full contents of the domain, looking for keywords and other extraneous information.

![image](https://github.com/xaviermontane/THM/assets/101309588/428bc5bf-b67c-45b5-aba7-96d4bd6e14e7)

"**mywebsite.com**" has been scraped as having the keywords "Apple," "Banana," and "Pear". The crawler stores these keywords in a dictionary and subsequently returns them to the search engine, such as Google. The search engine now knows that the domain "**mywebsite.com**" contains the keywords "Apple", "Banana", and "Pear". Since only one website has been crawled, a user searching for "Apple" would get the result "**mywebsite.com**". This would produce the same results if the user searched for "Banana."

As shown below, a user enters a search query for "Pears" into a search engine. Because the search engine only knows the contents of one website that has been crawled with the keyword "Pears," it will present the user with the single domain.

![image](https://github.com/xaviermontane/THM/assets/101309588/ec7a4946-050a-4849-87d1-3bc632e8e03e)

However, as previously stated, **crawlers attempt to crawl, or traverse, every URL and file that they can find!** If "**mywebsite.com**" contained the same keywords as before ("Apple", "Banana", and "Pear"), but also a URL to another website "**anotherwebsite.com**", the crawler will attempt to traverse everything on that URL (**anotherwebsite.com**) and retrieve the contents of everything within that domain.

The graphic below illustrates this. The crawler first finds "**mywebsite.com**," where it explores the website's contents, discovering the same keywords ("Apple," "Banana," and "Pear") as before, but it has now discovered an external URL. Once the crawler has finished on "**mywebsite.com**," it will proceed to crawl the contents of the website "**anotherwebsite.com**," which contains the keywords ("Tomatoes," "Strawberries," and "Pineapples"). The crawler's dictionary now includes the contents of both "**mywebsite.com**" and "**anotherwebsite.com**", which is then stored and kept within the search engine.

![image](https://github.com/xaviermontane/THM/assets/101309588/f0784eae-4947-40b7-9308-aa3e737c7eb4)

So now our search engine has managed to retrieve keywords through the help of crawlers, this is how our search queries operate.  This is fantastic! But what if a website had many external URLs (as they frequently do!)? That will necessitate a lot of crawling. There's always the possibility that another website will have similar information to the one that was crawled, right? So, how does the "Search Engine" determine the hierarchy of domains displayed to the user?

Imagine if a website had multiple external URL's (as they often do!) That'll require a lot of crawling to take place. There's always the chance that another website might have similar information as of that another website crawled - right? So how does the "Search Engine" decide on the hierarchy of the domains that are displayed to the user?

In the diagram below in this instance, if the user was to search for a keyword such as "Tomatoes" (which websites 1-3 contain) who decides what website gets displayed in what order? To understand this we will then have to take a look into _Search Engine Optimisation_.

---

#### Search Engine Optimisation (SEO)

Search Engine Optimisation, or SEO, is a popular and profitable topic among today's search engines. Indeed, enhancing a domain's SEO "ranking" is so important that entire businesses are built around it. In general, search engines will "prioritise" domains that are easier to index. Many factors influence how "optimal" a domain is, culminating in something akin to a point-scoring system.

Some factors that influence this scoring system include the following:
- How responsive your website is to the different browser types I.e. Google Chrome, Firefox and Internet Explorer - this includes Mobile phones too!
- How easy it is to crawl your website (or if crawling is even allowed) through the use of "Sitemaps"
- What kind of keywords your website has (i.e. In our examples if the user was to search for a query like “Colours” no domain will be returned - as the search engine has not (yet) crawled a domain that has any keywords to do with “Colours”

There are various online tools - sometimes provided by the search engine providers themselves that will show you just how optimised your domain is. For example, let's use [Google's Site Analyser]([https://web.dev/](https://pagespeed.web.dev/)) to check the rating of [TryHackMe](tryhackme.com):

<img width="955" alt="Screenshot 2023-09-17 at 12 38 35" src="https://github.com/xaviermontane/THM/assets/101309588/8a6a9441-e3ec-4a52-8bf3-7a32ac8caec9">

#### How Are Crawlers Regulated?

Aside from the search engines who provide these "Crawlers", website/web-server owners themselves ultimately stipulate what content "Crawlers" can scrape. Search engines will want to retrieve everything from a website - but there are a few cases where we wouldn't want all of the contents of our website to be indexed!

#### Robots.txt

When crawling a website, this is the first file that is indexed. This file must be served from the webserver's default root directory. The text file specifies the _Crawler's_ access to the webpage. For example, what kind of _Crawler_ is permitted (You might only want Google's _Crawler_ to index your site, not MSN's). Furthermore, Robots.txt allows us to designate which files and folders we want or don't want the _Crawler_ to index.

**Click [here](www.youtube.com/robots.txt) to view YouTube's own Robots.txt file —** To view a website's Robots.txt file just type in `www.website.com/robots.txt`

A very basic markup of a Robots.txt looks like this:

```
User-agent: *
Allow: /

Sitemap: http://mywebsite.com/sitemap.xml
```

Let's take a look at the syntax:
<br>

|  Keyword  | Function |
| --------- | -------- |
| User-agent | Specify the type of _crawler_ that can index your site (the asterisk being a wildcard, allowing all "User-agents" |
| Allow | Specify the directories/file(s) that the _crawler_ can index |
| Disallow | Specify the directories/file(s) that the _crawler_ cannot index |
| Sitemap  | Provide a reference to where the sitemap is located (improves SEO) |

#### Permissions
Robots.txt works on a "blacklisting" basis, meaning unless told otherwise, the _crawler_ will index whatever it can find. With this knowledge, let's now try to hide directories or files from a _crawler_. 

```
User-agent: *
Disallow: /secret-directory/
Disallow: /not-a-secret/but-this-is/

Sitemap: http://mywebsite.com/sitemap.xml
```

To allow certain crawlers to index the site, we must use the following syntax:

```
User-agent: Googlebot
Allow: /

User-aget: msnbot
Disallow: /
```

Now let's prevent certain files from being indexed:

```
User-agent: *
Disallow: /*.ini$
Sitemap: http://mywebsite.com/sitemap.xml
```

In this example, any _crawler_ can index the site, however, they cannot index any file (*) that has the extension of .ini within any directory/sub-directory using ("$") of the site. But why would you want to hide a .ini file? Well, files like this contain sensitive configuration details. By aplying changes like this we can protect our site against any maling actors.

#### Sitemaps
