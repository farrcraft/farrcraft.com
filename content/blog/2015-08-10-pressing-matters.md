---
title: Pressing Matters
author: Josh
type: post
date: 2015-08-10T06:50:58+00:00
url: /blog/2015/08/10/pressing-matters/
socialShare: false
categories:
  - Code

---
## WordPress to Octopress and Back Again

This site is once again running on WordPress.  It&#8217;s been through many changes since its earliest incarnation as handwritten static HTML.  There have been versions based on custom PHP frameworks, a [pyblosxom][1]-based variant, and most recently, the [Octopress][2] installation. Directly prior to Octopress, the site had already been using WordPress.  So why did I leave and why did I come back?


## What I don&#8217;t like about WordPress

Its relative ease of installation and use for newcomers belies the big cumbersome application that WordPress really is underneath.  It can require a server with a decent amount of resources just to run.  You at least need a web server with PHP and a database server to run it. Depending on the size of the site, the server hosting it will need to be powerful enough to run it.  Even if you&#8217;re working with a small personal site, you&#8217;ll need at least enough resources just to support the application itself.

I also don&#8217;t like writing my content in a web browser.  Browser-based WYSIWYG editors have a history of being filled with odd quirks and behaviors that can make them difficult to work with.  The formatting options available in these editors can often be limiting too.  Then there&#8217;s the issue of the inherent danger of losing content in the browser&#8217;s text fields.  I can&#8217;t count the number of times I&#8217;ve lost some text in a web page form due to a closed window, errant link click, back button press, or wrongly focused backspace key.

Lastly, as a PHP developer, I&#8217;ve never been a big fan of the code-base itself.  The majority of it is written in a procedural style that was a more common standard in older PHP versions.  Most of the rest of the PHP world has advanced to other programming styles and design patterns for developing application code.  WordPress has just not kept up with the best practices of modern-day PHP development.


## What I like about Octopress

In the last few years, static site generators have become all the rage &#8211; the concept definitely drew me in.  The pitch is straightforward &#8211; since content authorship is a singular task and content is rarely ever changed after it has been initially published, why not shift the application demands from the server hosting the content to the author&#8217;s computer instead?  In this model, the author creates the content locally and runs the application to build the static HTML pages that comprise the site.  The server hosts the generated files, requiring no web scripting language like PHP or any databases to store any data.  As a result, the server resource requirements are greatly diminished.

Since content is written locally, you have much more flexibility in the tools you use to write in.  Native OS text editors are much more robust than the browser-based equivalents.  The native language for writing content in Octopress is markdown.  If you&#8217;re familiar with markdown &#8211; and it&#8217;s pretty easy to pick up &#8211; it makes writing and formatting posts a breeze.  Plus, there&#8217;s no magic to embed raw HTML if you need to &#8211; it just works.


## What I end up hating about Octopress

If you plan to publish content from multiple devices, be prepared to setup your publishing environment on each device.  That won&#8217;t even be possible from every device.  Want to blog from your iPhone?  Don&#8217;t count on it.  Want to publish posts from your Windows PC? That might not work either &#8211; at least not without a lot of additional effort.  At its heart, Octopress is a ruby application built on top of a number of ruby gem dependencies.  Just to get started writing content, you&#8217;ll need a functional ruby environment.  This can be a monumental challenge on some platforms like Windows.  Some dependencies can be difficult to install or just be entirely broken.

There is also the overhead of managing the data itself.  Octopress sites are typically managed using the git distributed version control system.  If not for the publishing flow itself, it is often the best solution for keeping the content between your multiple publishing devices in sync.  It is also the common approach to updating the application code.  The downside is that working with git can sometimes be cumbersome in itself.  There&#8217;s a lot to know about how git works and how to deal with remotes, merging branches, and dealing with the inevitable file conflicts that come along.


## Final Thoughts

So how do I feel about WordPress now that I&#8217;m back to using it again?  I&#8217;m coming back around to it.  I&#8217;m no longer fighting getting my publishing environment working or updated and just spending time writing content again.

WordPress has a robust ecosystem of plugins and themes to customize the experience.  As a result, I rarely have to roll up my sleeves and dig into the code beyond very minor tweaks.  I&#8217;m still not thrilled about in-browser WYSIWYG editors, but they have come a significant distance in quality since the earlier days.  There are also plugins like [WPBakery&#8217;s Visual Composer](vc.wpbakery.com) that provide advanced tools for laying out your content.

As a developer, I like to have as much control over my environment and the tools I work with.  I also have a tendency to want to tinker.  Of course many of my gripes with WordPress are rooted in those facts.  There are many providers who specialize in hosting and managing nothing but WordPress.  My technical complaints would become largely moot to begin with when the responsibilities were shifted to another party like this.  Unfortunately, relying on a hosted application service provider runs counter to my natural urge to just do it myself.  These are also the desires that draw me into the promise of a tool such as Octopress.

For now, the technical bar is still just a little too high to make it a comfortable solution for content creation.  I&#8217;ll just have to accept what might be the less technically superior solution for the tried and true legacy &#8211; if only until the next shiny new promising platform comes along to try and disrupt things.

 [1]: https://pyblosxom.github.io/
 [2]: http://octopress.org/