---
title: Encrypt All The Things!
author: Josh
type: post
date: -001-11-30T00:00:00+00:00
draft: true
url: /blog/2017/01/17/encrypt-all-the-things/
socialShare: false
categories:
  - Uncategorized

---
For over a year now I&#8217;ve been using Let&#8217;s Encrypt SSL certificates on my domains. They&#8217;ve had an amazing year of growth and have really proven themselves so far. While I&#8217;m happy with the service now, it was a rocky start. [CUT TO]

[FLASHBACK]

[VOICEOVER]

I started the original draft of this post around a year ago just after initially setting up the original Let&#8217;s Encrypt SSL certificates. I wanted to give the less than positive experience to settle before finishing it, but eventually just forgot about it completely.

[FADE IN]

I&#8217;ve been looking forward to trying this product out since it was first announced. I think it&#8217;s a great idea and I really want it to work. When the beta opened up, I was eager to give it a try and find out how it really worked. Unfortunately, I think it&#8217;s still got a ways to go before I&#8217;d say it&#8217;s really production-ready. At least in the end I was able to finally get certificates generated for my sites. That&#8217;s not to say that I didn&#8217;t run into trouble along the way.

I have really only been following the product closely enough to know that it should be available as something I can download onto my server to start using. Just visiting the main website, I couldn&#8217;t really figure out how it worked as an end user. The site goes into great detail about who is behind it and how things work behind the scenes. However, without a bunch of digging, it&#8217;s not obvious how to start using it. 

Eventually I found the Github repository which represents the official client tool for generating and renewing certificates. This tool is a python application, requiring a basic python environment to run. The installation directions indicate to simply clone the repository and run the CLI tool with the &#8211;help option.

I expect that the help flag will verify that my environment is someone sanely configured and that the tool works in its most basic form, showing me an extensive catalog of available options to control its behavior. To my horror, instead it appears to be running apt updates and installing any additional missing dependencies onto my system. It does this without any further input or consent, invoking commands using sudo without warning. This isn&#8217;t a first-run behavior either. It continues to do apt updates on subsequent invocations.

The tool has a number of options for generating certificates which depend on the web server you&#8217;re running. This is important mostly for the fact that the tool wants to be able to handle all of the web server configuration as well as certificate creation. The best support is currently for apache. My setup uses nginx behind varnish. The support for nginx is experimental and isn&#8217;t even included in the standard tool by default yet. Instead I opted to handle the web server configuration myself and just have the tool handle standalone certificate generation.

Before a certificate can be created for a domain, a process of domain ownership verification needs to happen. While the technical overview on the main website indicates that this validation can happen either via DNS record or by allowing the tool to write a hidden file into the webroot that the CA can query, the tool appears to only support the latter option. This means that if you&#8217;re working with a site that isn&#8217;t publicly accessible, this probably isn&#8217;t going to work for you. Also, if you have a properly hardened web server configuration, you probably have rules to disallow direct access to hidden directories / files. It will be necessary to update your configuration either temporarily or to add a permanent exception for the specific file path that the tool uses.

After clearing those hurdles, I did manage to generate new certificates for my various domains. One of the stated goals is to have a tool that works well in highly automated systems where it isn&#8217;t necessary to remember when certificates expire and to have to manually go through steps to renew them. Toward that end, certificates expire after only 90 days. It should be as simple as running the tool again with the same parameters to renew a certificate. This should be doable from a monthly crontab entry just to be safe.

I think what Let&#8217;s Encrypt is trying to do is great and an important step toward a safer, more secure Internet. I&#8217;m thrilled that I finally have SSL certificates on all of my personal domains. I hope that the Let&#8217;s Encrypt team is able to smooth over the current rough edges as they move from beta to a generally available product. I also hope this helps push other CA&#8217;s to embrace similar ideals and technical approaches.

[ROLL CREDITS]

[POST CREDITS SCENE]

Over a year, every 90 days when I needed to renew my certificates, it was always a manual struggle to get the tools working and the certificates renewed. My automation never seemed to work. I would attribute this to my early adoption and lack of time investment in maintenance as the early release tools matured. There were undoubtedly kinks in the early versions.

When I finally got around to doing a complete refresh of my automation near the beginning of this year, I found much better alternatives to the original tools. This time, an acme chef cookbook had become available, providing the necessary resources for automating SSL certificate creation and renewal.