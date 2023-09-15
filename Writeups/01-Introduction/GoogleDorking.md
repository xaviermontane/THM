### Google Dorking

Google... Regardless of your expertise you're knowledgable of the name, this search engine has stood the test of time. As a matter of fact, Google has 4.3 billion users worldwide, making it the most dominant search engine on the internet.
Researching as a whole, especially in the context of cybersecurity, encapsulates almost everything you do as a pentester. "Search Engines" such as Google are huge indexers, more specifically indexers of content spread across the World Wide Web. These essentials for surfing the internet use “Crawlers” or “Spiders” to search for this content across the web.

#### Crawlers

Crawlers discover content through various means. One being pure discovery, where a URL is visited by the crawler and information regarding the content type of the website is returned to the search engine. In fact, there is lots of information modern crawlers scrape, but we will discuss how this is used later. Another method crawlers use to discover content is by following any and all URLs found on previously crawled websites. Much like a virus in the sense that it will want to traverse or spread to everything it can.



The diagram below is a high-level abstraction of how these web crawlers work. Once a web crawler discovers a domain such as **mywebsite.com**, it will index the entire contents of the domain, looking for keywords and other miscellaneous information - but I will discuss this miscellaneous information later.

![[Pasted image 20230912222244.png]]

In the diagram above, "**mywebsite.com**" has been scraped as having the keywords as “Apple” “Banana" and “Pear”. These keywords are stored in a dictionary by the crawler, who then returns these to the search engine i.e. Google. Because of this persistence, Google now knows that the domain “**mywebsite.com**” has the keywords “Apple", “Banana” and “Pear”. As only one website has been crawled, if a user was to search for “Apple”...“**mywebsite.com**” would appear. This would result in the same behaviour if the user was to search for “Banana”. As the indexed contents from the crawler report the domain as having “Banana”, it will be displayed to the user.

As illustrated below, a user submits a query to the search engine of “Pears". Because the search engine only has the contents of one website that has been crawled with the keyword of “Pears” it will be the only domain that is presented to the user.

![[Pasted image 20230912222351.png]]

However, as we previously mentioned, **crawlers attempt to traverse, termed as crawling, every URL and file that they can find!** Say if “**mywebsite.com**” had the same keywords as before (“Apple", “Banana” and “Pear”), but also had a URL to another website “**anotherwebsite.com**”, the crawler will then attempt to traverse everything on that URL (**anotherwebsite.com**) and retrieve the contents of everything within that domain respectively.

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
- Name the key term of what a "Crawler" is used to do:
	- Index
- What is the name of the technique that "Search Engines" use to retrieve this information about websites?
	- Crawling
- What is an example of the type of contents that could be gathered from a website?
	- Keywords
