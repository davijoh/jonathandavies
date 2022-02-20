+++
date = 2022-02-11T23:00:00Z
tags = ["bookmarklets", "SEO"]
title = "🔖 Useful SEO Bookmarklets"

+++
My list of Chrome extensions is getting very long, too long for my taste. While I deleted some that I barely use, I would still like to get rid of more.

While some extensions are more complex, others can be replaced by a few lines of Javascript. This post is just a place where I'll be listing useful bookmarklets to replace some of these extensions.

Why add Chrome extensions when some lightweight code can do the work just fine, right?

## How to add a Bookmarklet

Adding a Bookmarklet to a Chromium browser is very easy. 

**First, make your bookmarks bar visible if it's not already. To do so:**

1. Open the settings menu of your browser (the 3 dots or lines at the far right of the navigation bar)
2. In the bookmarks menu, click on "Show bookmarks bar"

**Then, once the bookmarks bar is visible, let's add a bookmark:**

1. Right-click on an empty spot (or on a folder) and select "Add Page..."
2. By default, it will fill the name and URL with the data of the current page. Set the Name and replace the URL with the Bookmarklet code.

That's it. When you want to use your Bookmarklet, just click on it from your bookmarks bar.

## Bookmarklets I use the most

The following list is a work in progress. Every time I find a new Bookmarklet that I find useful, I will add it to the list.

### H-Tag Highlighter

When doing an SEO audit, one of the first things to do is to check the headline structure of a page.

Hierarchy matters and it's a good indicator of the SEO level of a client.

A homepage with several H1, for example, is a red flag. It doesn't especially mean that the client doesn't know anything about SEO, but the least we can assume is that he's not giving it enough care.

There is a simple Chrome plugin for that, called... H-Tag, but here is a short piece of Javascript that gives exactly the same result.

    javascript:void((function()%7Bvar a,b,c,d,e,f%3Bf%3Dnew Array(%27pink%27,%27orange%27,%27yellow%27,%27aquamarine%27,%27lightskyblue%27,%27plum%27)%3Bfor(a%3D1%3Ba<%3D6%3Ba%2B%2B)%7Bb%3Ddocument.getElementsByTagName(%27h%27%2Ba)%3Bfor(c%3D0%3Bc<b.length%3Bc%2B%2B)%7Bd%3Db%5Bc%5D%3Be%3Dd.style%3Be.backgroundColor%3Df%5Ba-1%5D%3Be.border%3D%27solid%27%3Be.padding%3D%272px%27%3Be.color%3D%27black%27%3Bd.innerHTML%3D%27H%27%2Ba%2B%27 - %27%2Bd.innerHTML%3B%7D%7D%7D)())

### Google SERP Extractor

Actually, this one doesn't replace a Chrome extension that I was using, but it comes (very) handy in addition to an extension that I want to keep.

I don't like Link Building, it's a frustrating sport... it can get very time consuming and results don't always reflect the work you're putting into it.

The least we can do is find ways to save some time...

This Javascript allows you to copy all the URLs from the SERP at once, instead of doing it manually for each result.

    javascript:(function(){output='<html><head><title>SEO SERP Extraction Tool</title><style type=\'text/css\'>body,table{font-family:Calibri,Verdana,Segoe,sans-serif;font-size:11px;color:#000}h1,h2,th{font-family:Calibri,Verdana,Segoe,sans-serif;color:#4b59ad}th{text-align:left}</style></head><body>'; output+='<table><tbody><tr><td><h1>🌊 Google SERP Extractor</h1></td></tr></tbody></table>'; pageAnchors=document.getElementsByTagName('a'); divClasses=document.getElementsByTagName('div'); var linkcount=0;var linkLocation=''; var linkAnchorText=''; for(i=0;i<pageAnchors.length;i++){ if(pageAnchors[i].parentNode.parentNode.getAttribute('class')!='iUh30'){ var anchorText = pageAnchors[i].textContent; var anchorLink = pageAnchors[i].href; var linkAnchor = anchorLink + '\t'+anchorText; var anchorID = pageAnchors[i].id; if(anchorLink!=''){ if(anchorLink.match(/^((?!google\.|cache|blogger.com|\.yahoo\.|youtube\.com\/\?gl=|youtube\.com\/results|javascript:|api\.technorati\.com|botw\.org\/search|del\.icio\.us\/url\/check|digg\.com\/search|search\.twitter\.com\/search|search\.yahoo\.com\/search|siteanalytics\.compete\.com|tools\.seobook\.com\/general\/keyword\/suggestions|web\.archive\.org\/web\/|whois\.domaintools\.com|www\.alexa\.com\/data\/details\/main|www\.bloglines\.com\/search|www\.majesticseo\.com\/search\.php|www\.semrush\.com\/info\/|www\.semrush\.com\/search\.php|www\.stumbleupon\.com\/url|wikipedia.org\/wiki\/Special:Search).)*$/i)){ if(anchorID.match(/^((?!hdtb_more|hdtb_tls|uh_hl).)*$/i)){ linkLocation+=anchorLink+'<br />'; linkAnchorText+=anchorText+''; linkcount++; if (anchorText === undefined) anchorText = pageAnchors[i].innerText; } } } } } output+='</table><br/><div>'; output+=linkLocation;output+='</div><br/><div>'; with(window.open()){document.write(output);document.close();}})();

**Couple this with a Chrome plugin such as gInfinity and you get yourself a good free tool to extract SERP results for a given KW without having to do it for each page individually.**

### Characters and Words Count

When writing an article, its length will have an impact on SEO. 

An article that is too long will probably be penalized (Eg. You don´t need 3000 words to answer a question such as "Which Country Offers the Best Beers?" We all know that the answer is Belgium...).

But an article that is too short will be penalized in the same way. 

Aside from common sense, there is no perfect way to decide what length an article should be. A simple option is to look at competing articles and make an average of the best 5 articles. 

Here is a Bookmarklet that gives you the character and word count for a selected text. No need to use an extension or a website. 

    javascript:(function(){var a=(document.selection?document.selection.createRange().text:document.getSelection()).toString();alert(a.length?"Characters: "+a.length+"\nWords: "+a.replace(/\s{2,}/g," ").split(" ").length:"No text selected.")})();