+++
date = ""
draft = true
title = "Useful SEO Javascript Bookmarks"

+++
My list of Chrome extensions is getting very long, too long for my taste. While I deleted some that I barely use, I would still like to get rid of more.

While some extensions are more complex, others can be replaced by a few lines of Javascript. This post is just a place where I'll be listing useful Javascript bookmarks to replace some of these extensions.

Why add Chrome extensions when some lightweight code can do the work just fine, right?

## H-Tag Highlighter

When doing an SEO audit, one of the first things to do is to check the headline structure of a page. 

Hierarchy matters and it's a good indicator of the SEO level of a client. 

A homepage with several H1, for example, is a red flag. It doesn't especially mean that the client doesn't know anything about SEO, but the least we can assume is that he's not giving it enough care. 

There is a simple Chrome plugin for that, called... H-Tag, but here is a short piece of Javascript that gives exactly the same result.

    javascript:void((function()%7Bvar a,b,c,d,e,f%3Bf%3Dnew Array(%27pink%27,%27orange%27,%27yellow%27,%27aquamarine%27,%27lightskyblue%27,%27plum%27)%3Bfor(a%3D1%3Ba<%3D6%3Ba%2B%2B)%7Bb%3Ddocument.getElementsByTagName(%27h%27%2Ba)%3Bfor(c%3D0%3Bc<b.length%3Bc%2B%2B)%7Bd%3Db%5Bc%5D%3Be%3Dd.style%3Be.backgroundColor%3Df%5Ba-1%5D%3Be.border%3D%27solid%27%3Be.padding%3D%272px%27%3Be.color%3D%27black%27%3Bd.innerHTML%3D%27H%27%2Ba%2B%27 - %27%2Bd.innerHTML%3B%7D%7D%7D)())

## Google SERPs Extractor

Actually, this one doesn't replace a Chrome extension that I was using, but it comes (very) handy in addition to an extension that I want to keep.

I don't like Link Building, it's a frustrating sport... it can get very time consuming and results don't always reflect the work you're putting into it. 

The least we can do is find ways to save some time... 

This Javascript allows you to copy all the URLs from the SERPs at once, instead of doing it manually for each result. 