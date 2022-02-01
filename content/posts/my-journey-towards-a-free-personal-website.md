+++
date = ""
draft = true
title = "👨‍💻 My journey towards a free personal website"

+++
Since I started working as a digital marketing consultant, I´ve always wanted to have my own website. After all, I build websites for a living but I don´t have my own?!

The problem is I don't feel like spending money on it monthly. I just want to store my notes.

"Why don't you go for Notion or Wordpress.org?"

Two things, I want my own domain and I want it to be SEO friendly (I can't help it, the SEO in me is addicted to green lighthouse scores...).

And to be honest, where's the challenge in that?!

## My journey

A typical website brings several costs:

* Hosting
* CMS like wordpress.com
* Domain name rental

So what can I do to pay as little as possible?

After some research, I've come to the conclusion that my best option - and the most challenging one - is a **static website**.

Static websites are fast, secure and in most cases... free!

Except for the domain name. There is nothing we can do there.

Actually, this isn't true. More on that later.

**But my point is, my static website + hosting + CMS + domain name cost me a one-time fee of $20.**

Here is the breakdown:

* Static website generator: Hugo (free)
* Hosting: Netlify (free for personal website)
* CMS: Forestry (free)
* Domain name: Unstoppable Domain ($20)
* Lighthouse scores: 100 - 100 - 100 - 100

![Lighthouse results](/uploads/lighthouse-result.jpg "Lighthouse results")

## Static website generator

Pickling a static site generator was actually more difficult than I thought.

I don't want to go too much into the details here, as I am no expert, but my first pick wasn't Hugo.

After reading several articles, I decided to go for 11ty. It's one of the newest players and it has a smaller community, but several articles recommended it as it's growing in popularity and supposedly easier to use.

The thing is, I know nothing about static websites and my coding level is barely enough to write some custom CSS and HTML on Wordpress websites...

This means I can't code a static website from scratch and I need a theme to play with. That was the first limitation of 11ty... I couldn't find a theme that ticked my boxes...

The second limitation came up when creating the website. A smaller community means fewer tutos available and fewer problems resolved online.

After hours of trials and errors, I couldn't get a working website. Git errors, Netlify fails,...

(I know I probably jumped many steps by trying to create a static website without knowing code, but I believe in learning by trying)

I am not saying 11ty is bad. In fact, it's one of the best generators out there. It's just not for complete beginners.

Soooo...

After some more research, I decided to go for Hugo. Its blazing fast reputation comforted my SEO ego and as it's been here for a while, it has a strong community and plenty of themes to pick from.

Other contenders were Jekyll, Gatsby and Next.js. They all have a strong community.

Why Hugo? I repeat: it's fast. Yes, it adds Golang to the coding languages mix, compared to 11ty, but whatever.

## Hosting and CMS

There are a few options for free hosting, including Netlify, Github Pages and Vercel.

I went for **Netlify**.

Github Pages seemed like a less popular option nowadays and Vercel seemed more complicated.

* The connexion between my Github repository and Netlify was seamless!
* The free plan is perfect for personal websites as it includes 1 member, 100GB/month of bandwidth and 300 minutes/month of build time

As for the CMS, there were a few free options as well, starting with Netlify's own product.

Using Netlify for hosting, I naturally tried its CMS, but I didn't like it. For some reason, I had basic formatting issues that made simple things like bullet lists unusable. 

I didn't look more into that issue and finally decided to go for **Forestry**. 

Other top choices were Contentful and Sanity, but I preferred Forestry for the highly technical reason that its name just sounds better to me. 

* No issue to declare so far. But this is my first article using it.
* Connexion with my Github repository was easy and it automatically identified my existing pages and posts
* The free plan is quite complete. Just keep in mind that inactive websites (for 3 months) are archived (but they can be unarchived)

## Domain Name

Renting a domain name really isn't too expensive, but having to rent it has always annoyed me. 

Why can't we just own it?!

Well, my friends, it seems like that question is no longer valid as I found out we actually CAN own our domain (as long as you're ready to give up on classic domain extensions like .com)

Being quite interested in blockchain technology, web 3.0 etc, I found Unstoppable Domains (or rather, an Unstoppable Domain Instagram ad found me...) 

This is basically an NFT domain provider. Meaning you pay only once to acquire (mint) the domain name and that's it, no yearly renewal fees to pay. You own an NFT domain, the same way as you'd own 

How much did I pay?

I purchased jonathandavies.nft on Unstoppable Domains for $20.

I repeat: one time payment! 

And no, no minting and extra gas fees on my side. The mint is on Polygon and the tiny gas fee is covered by Unstoppable Domain.

**But wait, there is a catch...**

Well, most browsers don't support NFT domains natively yet... (Brave, that I use, does, but most people don't use it).

I know, kind of a turn off. I'm hoping this changes fast.