---
title:  " Automating Best Matching LinkedIn Profile URL Search using Python and Selenium"
date:   2016-12-07 05:58:00
description: Web Scrapping 
---

Websites, may it be developed using any framework, the end product is always a bunch of HTML tags.  Not all websites provide APIs to comfortably access the data they contain in formats such as CSV or JSON. So manually searching for the required data in the website is the only option left with us in such a case? What about cases when we are to fetch huge chunks of data from a website? 
**Web Scrapping** is there to save you. It is the practice of using a computer program to sift through a web page and extract the data you want by parsing the HTML.

In this article, we will learn how to automate scrapping of LinkedIn profile URL. We hope that you know basics of web scrapping 
and can write a simple program to scrap data from a web page. If not, you can read this article covering the basics 
of web scrapping <a href="https://automatetheboringstuff.com/chapter11/" target="_blank">here</a>.

Suppose you have an input file in csv/json format which contain information about some executive’s name, title, firm and we need to get his / her best matching linked profile URL. Since the LinkedIn people search API is closed now (more details <a href="https://developer.linkedin.com/support/developer-program-transition" target="_blank">here</a>) searching for best matching profile is a little tricky.

An example **input file**(.xlsx) may look like this:

![Example Input file](../../assets/images/input.png)

It is achieved here in the simplest and best possible way and is based upon the following assumptions based upon empirical evaluation:

<ul>
	<li>Google is the best for LinkedIn X-Ray Search.</li>
	<li>After using relevant search operators and putting in the right queries the first link is the most relevant link to the required user's profile.</li>
	<li>In the worst case, it may be the 5th ranked link and if not, the required person is possibly not on LinkedIn or we may be searching with the wrong details.</li>
	<li>We should at-least have the person's (name, position and the company) he works in or some other information to form a well-formed query which can isolate the required profile with tons of other similar profiles.</li>
</ul>

Let’s see how to construct a query using Google search operators to search for the best matching profile on LinkedIn. First, we’ll start by telling Google that we only want to look at <strong>linkedin.com</strong>. This is accomplished via the site search operator.

<pre>site: www.linkedin.com/in // LinkedIn uses the 'in' directory for public profiles</pre>

Combining it with the input information we have, the search query will look something like this: 

<pre>site: www.linkedin.com/in  + person’s name + person’s position + person’s company</pre>

The search results for **LinkedIn CEO Jeff Weiner's LinkedIn profile** using the form of querying mentioned above may look like this:

![Search Results](../../assets/images/searchop.png)

Since LinkedIn allows user to control what information is viewed by the general public and search engines, some profiles might not be indexed by search engines and this technique might not always work.

If you have already done some web scrapping you might be familiar with libraries like <strong>urllib</strong>, <strong>httplib</strong> and <strong>requests</strong>. These are good traditional tools for web scrapping but some sites don’t like to be scrapped and would put you behind a CAPTCHA check if you overdo it. In such a case your web scrapping bot should disguise itself as a human being. Selenium does exactly the same. <strong>Selenium</strong> is a webdriver and its Python binding allows your script to take control of your browser (Firefox/Chrome/PhantomJS) and makes it difficult for a website to recognize whether it’s a bot or a human being.

You need to install Selenium first and also the Firefox webdriver. Set the path to the Firefox webdriver in your system’s path variable. Install Selenium’s Python bindings. You can simply do a pip install.

<pre>
pip install Selenium
</pre>

Now’s let’s try to open Google using selenium and the Firefox web driver.

```python
from selenium import webdriver

browser  = webdriver.Firefox()
url = ‘https://www.google.com’
browser.get(url)
```

After you run this code you’ll see a Firefox instance launch automatically and the google home page landing up. Now let’s do a google search for the LinkedIn profile of LinkedIn CEO Jeff Weiner using the way of querying proposed earlier.

```python
from selenium import webdriver

query = ‘site: www.linkedin.com/in  Jeff Weiner CEO LinkedIn’

'''The following url will give us the first 5 (start=0, num=5) 
google search results corresponding to our #query.'''

url = 'https://www.google.com/webhp?#num=5&start=0'+'&q=' + query

browser = webdriver.Firefox()

browser.get(url)
```

Now we need to scrap the title and URL of the search results. For this you can find the required elements (title and link) of all the search results using their <strong>XPath</strong>. XPath contains the path of the element situated at the web page. Standard syntax for creating XPath is:

<pre> Xpath=//tagname[@attribute='value']</pre>
<ul>
	<li><strong>//</strong>: Select current node.</li>
	<li><strong>Tagname</strong>: Tagname of the particular node.</li>
	<li><strong>@:</strong> Select attribute.</li>
	<li><strong>Attribute</strong>: Attribute name of the node.</li>
	<li><strong>Value</strong>: Value of the attribute.</li>
</ul>



You can also right click on an element and click on inspect element and then again right click on the highlighted html content and copy the XPath. So, we need to add the following lines to the code above to get the title and link corresponding to each search result. 
( You can learn more about XPath from <a href="http://www.w3schools.com/xml/xpath_intro.asp" target="_blank">w3Schools</a> article.)

```python
links = browser.find_elements_by_xpath("//h3[@class='r']/a[@href]")

'''XPath will find a subnode of h3, a[@href] specifies that we only want <a> nodes 
with any href attribute that are subnodes of <h3> tags that have a class of ‘r’'''

results = []

for link in links:
        title = link.text.encode('utf8')
        url = link.get_attribute('href')
        title_url = (title, url)
        results.append(title_url)

print (results)
```

This will print the top 5 Google search results for our query. We may want to write our search results to a JSON file. The following code would help us achieve that.

```python
import json

with open('urls.json','wb') as outputfile:
    json.dump(results, outputfile) 
```

The **output** in JSON after running the code would look something like: 

<pre>
[["Jeff Weiner | LinkedIn", "https://www.linkedin.com/in/jeffweiner08"],
 ["Jeff Weiner | LinkedIn", "https://www.linkedin.com/in/jeffreyweiner"], 
 ["Jeff Weiner | LinkedIn", "https://www.linkedin.com/in/jeff-weiner-16a92a41"], 
 ["Jeff Weiner | LinkedIn", "https://www.linkedin.com/in/jeffweiner100"],
 ["Jeff Weiner | LinkedIn", "https://www.linkedin.com/in/jeffweiner"]]
</pre>

Out of these five profiles we need to find the best match. We can write a simple function to do the same.

```python
from difflib import get_close_matches()

def urlMatch(titles_urls, name):

    links = []
    titles= []

    for item in titles_urls:
        if "linkedin.com/in/" in item[1]:
            titles.append(item[0].split('|')[0].strip())
            links.append(item[1])

    if titles == []: return None
    elif len(titles)==1: return links[0]
    else:
        best_match = get_close_matches(name,titles,n=1)
        return links[titles.index(best_match[0])]
```

This function takes the search results as it is along with the executive’s name we searched for as parameters. It then extracts the name from the search results’ title and tries to find the closest match between them and the searched executive’s name by using <a href="https://docs.python.org/2/library/difflib.html#difflib.get_close_matches" target="_blank">difflib.get_close_matches()</a>. 

To install difflib you can simply do a pip install.
<pre>
pip install difflib
</pre>

Finally, it returns the LinkedIn profile URL corresponding to the best matched profile. If all the names scrapped from the search result are exactly the same as the searched executive’s name, the function will return the URL corresponding to the first ranked result.

<ul>
	<li><a href="https://gist.github.com/AkshayAgarwal007/46d2715292165f60f54657849502cccf" target="_blank">GitHub Gist Link</a></li>
	<li><a href="https://github.com/AkshayAgarwal007/LinkedinScrapper" target="_blank">GitHub Repository Link</a></li>
</ul>



In the next article you'll learn how to scrap information from the searched LinkedIn profile.
