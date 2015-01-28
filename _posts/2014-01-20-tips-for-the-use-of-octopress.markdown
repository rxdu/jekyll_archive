---
layout: post
title: "Tips for the Use of Octopress"
date: 2014-01-20 15:36:18 -0500
comments: true
categories: [Web_Development, Octopress]
---

In the past two days, I transferred my blog from several other places to Github Pages with Octopress. Since I'm a stranger to web development, I felt rather lost at the very beginning. But after you finish it, you will find it's not that difficult, at least not so hard to get a less customized Octopress-based blog. There are many good tutorials on the Internet so I see no point to write a new one. In this post, I mainly gather some resources I feel useful to finish the work.

##Setup

####Follow [official tutorial](http://octopress.org/docs/setup/ ) to finish installation

- Install GIt
- Install Ruby
- Clone Octopress repository from Github
- Install Dependencies

 <!-- more -->

####Deploy blog to Github

- Set up github pages: http://pages.github.com/
- Deploy to github repository: http://octopress.org/docs/deploying/github/

####Set up a personal domain
- Register a domain from a domain registrar (for example: [namecheap](https://www.namecheap.com/))
- [Setting the DNS for Github Pages on Namecheap](http://davidensinger.com/2013/03/setting-the-dns-for-github-pages-on-namecheap/)

####Set up Octopress on multiple computers

- [Clone your Octopress to Blog from Two Places](http://blog.zerosharp.com/clone-your-octopress-to-blog-from-two-places/)
- [How to Start Octopress Blog From Multiple Computers](http://yhagio.github.io/blog/2013/04/09/how-to-start-octopress-blog-from-multiple-computers/)
- *Always Remember To Pull From Remote Before Your Start Workong On One Computer To Avoid Push Conflicts*

##Customization

- Official documents are good materials to start: [template](http://octopress.org/docs/theme/template/), [styles](http://octopress.org/docs/theme/styles/)
- Available themes: [Opthemes](opthemes.com), [list by imathis](https://github.com/imathis/octopress/wiki/3rd-Party-Octopress-Themes)
- Third party plugins [list by imathis](https://github.com/imathis/octopress/wiki/3rd-party-plugins)
- Useful blogs/articles:
  - [The OctopressThemes Blog](http://octopressthemes.com/blog/)
  - [Changing Octopress's Header](http://blog.bigdinosaur.org/changing-octopresss-header/)
  - [How to Customize Your Octopress Theme](http://aijazansari.com/2012/08/27/how-to-customize-octopress-theme/)
  - [Octopress Top Categories Plugin](http://time.to.pullthepl.ug/blog/2012/8/20/octopress-top-categories-plugin/)

##Write Blog Posts

####Useful Resources:

- [GitHub Flavored Markdown](https://help.github.com/articles/github-flavored-markdown)
- [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
- Markdown Editor: [Haroopad](http://pad.haroopress.com/user.html)
- Official Document about [blog with plugins](http://octopress.org/docs/blogging/plugins/)

####Basic Commands:
Create a new blog post:
```
rake new_post["title"]
```
Create a new page:
```
rake new_page["title"]
```
Generate blog:
```
rake generate
```
Preview blog:
```
rake preview
```
Deploy blog to remote github repository (_master branch_)
```
rake deploy
```
Push source folder to remote github repository (_source branch_)
```
git add .
git commit -m 'your message'
git push origin source
```
