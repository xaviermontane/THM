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

Just like its name suggest, _sitemaps_ are the maps used by websites. These _sitemaps_ play a major role in the functioning of crawlers, as they specifiy the adequate routes to find content within the domain. 

Below you can find an illustration of the structure of a website, and how it may look on a _sitemap_.

![image](https://github.com/xaviermontane/THM/assets/101309588/c4fe3902-a603-4d85-af27-2369d1ed0d2b)

However, this is just a simplified representation of _sitemaps_ for the sake of understanding, real sitemaps look like the following:

![image](https://github.com/xaviermontane/THM/assets/101309588/80c654cd-9ab2-458b-acc8-2c8a13777c98)

_Sitemaps_ are Extensible Markup Language (XML) formatted, this is a type of markup language and file format for storing, transmitting, and reconstructing arbitrary data.

The implementation of _sitemaps_ have a significant impact on a website's "optimisation" and favorability. As we discussed earlier in our Search Engine Optimisation (SEO) section, these maps make content traversal significantly easier for crawlers!

**But what makes _sitemaps_ so favourable for search engines?**

Search engines have a lot of data to process. Therefore, the efficiency of how this data is collected is paramount. Crawlers benefit greatly from resources such as _sitemaps_ because the essential routes for content are already supplied! Rather than going through the process of manually locating and scraping, the crawler only needs to scrape certain content. — Consider it similar to utilising a wordlist to find files rather than guessing their names at random.

_**The easier a website is to crawl, the more optimised it is for the Search Engine**_

#### Google's Advanced Searching

As previously discussed, Google has a lot of websites crawled and indexed. Most people utilize Google to browse enterntainment content (YouTube, Reddit, Facebook, Cornhub), and although Google will have this content indexed and ready for its users, this is a rather basic application of the search engine in contrast to what it can really be used for.

For example, we may use operators from programming languages to enhance or decrease our search results - or even perform arithmetic!

If we wanted to for example, narrow down our search query, we could use quotation marks as such: `Really "acurate" search`. Google will interpret everything in between as **exact** and only return the results of the **exact** query provided. This allows us to perform an exact search without the need to filter out useless information.

##### Refining Queries

By using specific terms, we can apply filters when searching within our engine. For example, let's say we want to buy drone components from a certain website, our first instinct is to search for the websites name, but in this case we're actually given the definition of drone racing:

![image](https://github.com/xaviermontane/THM/assets/101309588/af1a20b3-0170-47c8-b981-41f5ddc74be8)

**So how do we find the site we're looking for without mindless scrolling?**

Well, to optimize our search, we can simply apply the keyword "site". By doing so, we're able to retrieve the exact website we were looking for within the first search.

![image](https://github.com/xaviermontane/THM/assets/101309588/576dd566-d47f-4a5a-b7cf-d5261733de02)

##### So What Makes "Google Dorking" so Appealing?

The most important aspect is that it's completely legal, meaning we can perform this type of search at any time. The other reason is that it's all indexed, publicly available information. However, what you do with this information is where the topic of legality comes in to play...

A few common terms we can search for and combine include:
|  Term  | Action |
| --------- | -------- |
| filetype: | Search for a file by its extension (e.g. PDF) |
| cache: | View Google's Cached version of a specified URL |
| intitle: | The specified phrase MUST appear in the title of the page |

For example, let's say we wanted to use Google to search for all PDFs on BBC.co.uk. In this case, we could use the following search query: `site:bbc.co.uk filetype:pdf`.
Through the use of creative search queries such as this, we can refine our search and find files that would've taken a considerably longer amount of time to find. Oftentimes, people publish sensitive information on the web, and through Google Dorking, we can access these valuable files. This is what truly makes Google Dorking so powerful.
