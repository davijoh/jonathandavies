+++
date = ""
draft = true
showToc = true
tags = []
title = " 🙌 Useful Code Snippets for Wordpress"

+++
Useful WP code

Most of the websites I work on are built using WordPress (Gutenberg) and Elementor.

Now, this combination isn't perfect and there are some -very frustrating- limitations to the existing functionalities. 

For example, how come Gutenberg blocks don't include a table of contents block? Do I really have to install a plugin or add one manually to each post?! 

Or what do I do if I want to block non-professional email domains on my Elementor forms? Another plugin, really?!

This rapidly adds up, especially since many plugins can easily be replaced by a few lines of code. Plus, I personally try to keep my plugins count to a minimum because they make the website heavier and can be the source of compatibility issues or hacks. 

Unfortunately, my coding skills are very limited, but many website owners/builders are in the same situation and there are always friendly developers to help us out.

Here is some very useful code that I've found over time. 

## Blacklist/block email domains on Elementor forms

This is particularly useful in 2 situations:

1. You want to allow professional email addresses only and block generic domains such as Gmail, Hotmail or Yahoo. 
2. You keep getting spam from the same email domain