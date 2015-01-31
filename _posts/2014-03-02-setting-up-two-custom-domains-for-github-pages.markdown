---
layout: post
title: "Setting Up Two Custom Domains for Github Pages"
date: 2014-03-02 20:20:01 -0500
comments: true
categories: [Web_Development]
---

According to [offical tutorial](https://help.github.com/articles/setting-up-a-custom-domain-with-pages), "You can only have one custom domain for any given set of Pages. If you want multiple domains to point to the same Pages, you will need to use a service that can redirect the other domains to your Pages domain."

This post gives an example about how to do the redirection with two domain names from [namecheap](https://www.namecheap.com/) and [name.com](https://www.name.com/) respectively.

<!-- more -->

My personal feeling is that namecheap provides better user experience in managing your domains. You can get what you want very easily and their [help page](https://www.namecheap.com/support/knowledgebase/article/settingup_hostrecords) is indeed very helpful and can save you some time searching on the Internet. Name.com also has a nice-looking management interface, but it seems they don't provide as many functionalities as namecheap does. I can get the redirection working without any pain but I failed to do the same thing on name.com. (I'm not a person who is familiar with web development nor network. If you are one, maybe you could ignore this comment.)

In this example, I use domainA("rdu.im" from name.com) as the main method to access my github pages and use domainB("rxdu.me" from namecheap) to do the redirection.

* Add a CNAME file, which includes your primary domain name, to your github page repository 

* On namecheap:
From the "Host Management" section on the left side, go to "All Host Records". Add just one record:

	- HOST NAME: @; 
	- IP ADDRESS/URL:http://rxdu.github.io; 
	- RECORD TYPE:redirect; TTL:1800

<img src="/img/posts/namecheap_config.png" width="850" />

* On name.com:
Go to DNS Record and add two records:

	- Type:A; Host:rdu.im; Answer:192.30.252.153; TTL:1800
	-Type:A; Host:rdu.im; Answer:192.30.252.154; TTL:1800

<img src="/img/posts/namecom_config.png" width="850" />

After finishing the above 3 three steps, you should be all set. Wait for some time and check if both of the domains work properly.


