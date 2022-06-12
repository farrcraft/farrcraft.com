---
title: Deep Cuts
author: Josh
type: post
url: /deep-cuts/
socialShare: false
---

Welcome to the deep cuts. Over 2+ decades, you develop some portfolio cruft. These are all of the bits and bobs that I've toiled and tinkered with over the years. There are some outdated and ocasionally cringeworthy technology choices, but also some bits that I'm really proud of for what they were at the time.

## Personal Projects

These are all of the projects I have worked on in my spare time for myself (such as this website), friends, or as learning experiences.

![rpi-ferment](/uploads/2015/07/rpiferment.jpg)

### rpi-ferment

This is a beer fermentation temperature monitoring, logging, and control application suite built on the Raspberry Pi platform.  There are a series of [blog posts](/blog/2013/04/20/raspberry-pi-pt-1/) detailing the entire project. The software aspect comprises two Node.js applications written in CoffeeScript. The <a href="https://github.com/farrcraft/rpi-ferment">backend</a> server interacts with the Pi’s GPIO, capturing temperature data from any number of configured DS18B20 temperature sensors and logging them into graphite via statsd. It also exposes a RESTful API built using Express and Mongoose for managing fermentation profiles. A Socket.io server is also integrated for managing the controller. The <a href="https://github.com/farrcraft/rpi-ferment-frontend">frontend application</a> provides a UI for displaying graphs of logged temperature data, managing profiles, and interacting with the backend. It is built using <a href="https://github.com/SimbCo/brunch-with-marionette">Brunch with Marionette</a> and served with a thin static Node.js server.

![qfish2k9](/uploads/2015/07/qfish2k9.jpg)


### quantumfish.com

The original http://www.quantumfish.com website ran a lightweight custom-built MVC framework written in PHP. It originally used ADOdb for database connectivity. The final version provided database access using QCubed’s ORM system implemented as a framework plugin. The next iteration of this website was built using the Octopress blogging framework.

![basilv2](/uploads/2015/07/basilv2.jpg)


### Mystery Basket Generator

The original basil project was a grand vision that never existed beyond the initial prototype phase. This reincarnation is a stripped down weekend project version is a simple randomized ingredient mystery basket generator inspired by shows such as the Food Network’s Chopped series. It is a Node.js application built using the Express framework and MongoDB data store.

### bottletheory.com
This project extends on concepts explored in the original tQF website and Basil application frameworks along with ideas based on various other project research. The genesis began as a conversation among friends in September 2009 about a hypothetical application that could be used as a tool to track and log information about the various beers a person had tried. This original concept has slowly developed into the basis for a social game platform with a feature set including lists, check ins, and achievements. It represents the culmination of my current ideas and best practices in building a modern social web platform &#8211; It is truly for the love of beer and web technology. Among the components it leverages, LAMP, Amazon Web Services, Lucene/Solr, ActiveMQ, Doctrine ORM, Zend Framework, jQuery AJAX, REST JSON services.

![dccom](/uploads/2015/07/dccom.jpg)


### darkclown.com

For darkclown.com I provided the layout and design for the PHP-Nuke based CMS. I also managed the hosting and applied updates as they became available.

![clanversus](/uploads/2015/07/clanversus.jpg)

### clanversus.com

Over the years I have provided several site layouts for the ClanVersus gaming group website, built a complete modular portal/CMS from scratch, managed site hosting, and provided software upgrades to the highly customized phpbb based forums and mediawiki installation.

![sermon](/uploads/2015/07/sermon_qfish.jpg)


### sermons.quantumfish.com
This was my first blog site. It ran on PyBlosxom with content mostly related to Gentoo GNU/Linux topics.

## CTA Work

My work at CTA had me building websites that were for the most part targeted at freight transportation needs. A few, such as lhptransport.com and ctatechs.com were primarily static design jobs. Most, however, were complex web applications powered by a LAMP (Linux+Apache+MySQL+PHP) stack.

![lhp](/uploads/2015/07/lhptransport.jpg)


### lhptransport.com

This was a simple static corporate website. I provided all of the site layout and design. The HTML and CSS were hand coded with a small amount of PHP on the backend utilized for the common header, footer, and navigation elements. The original content was largely MS Office generated and required a good deal of hand reformatting to be standards comformant.

![loadmover](/uploads/2015/07/loadmover.jpg)


### loadmover.com

This site was a complex web application designed to be used in the transportation logistics industry. Its initial purpose was to help match LTL truck carriers with available loads from shippers. Over the course of the development a number of other useful tools were added. The project also became the base code for several sister sites including Prime, Inc.’s customized version and the commercial version available through LoadMax.com.

![prime loadmover](/uploads/2015/07/prime_loadmover.jpg)


### prime.loadmover.com

This was a sister site based on the original with some additional features:
- 3rd party data integration &#8211; retrieving, parsing, and importing EDI formatted data from AS400 mainframes for website display
- 3rd party application integration &#8211; fetching LTL rates from Linux network service utilizing a XML-RPC middleware solution

![loadmax](/uploads/2015/07/loadmax.jpg)


### loadmax.com

This was a commercial version of the original loadmover.com application. Some features included:
- Building custom Bill of Lading forms and generating printable PDF document versions on the fly
- Advanced search capabilities including complex distance and radius location calculations
- Customizable automated search agents providing specific matches via email

![ctatechs](/uploads/2015/07/ctatechs.jpg)


### ctatechs.com

This was a simple static corporate website. I provided all of the site layout and design. The HTML and CSS were hand coded with a small amount of PHP on the backend utilized for the common header, footer, and navigation elements. The original content was largely MS Office generated and required a good deal of hand reformatting to be standards comformant.

![lhp extranet](/uploads/2015/07/lhp_xtranet.jpg)

### LHP Agents Xtranet

The Agents Xtranet project provided a toolset for contracted logistics agents located throughout the country. The tools included data management for trucks, loads, and contacts for each agent. Data could be imported/exported from MS Excel via common CSV type formats. A document storage system for managing images of scanned documents such as Bill of Lading forms was also incorporated into the system. User access was controlled through a detailed ACL framework.

![transbids](/uploads/2015/07/transbids.jpg)


### transbids.com

The Transbids.com project was meant to provide a system for logistics companies to easily complete bid proposals on lanes provided by shippers (e.g. Kodak, Pepsi, Quaker). The system would function similar to a auction or RFP type tool, automating winning bid selections.

![dats](/uploads/2015/07/dats.jpg)


### dats.us

The dats.us website was designed to become a directory of transportation industry service providers with a focus on minority owned businesses.

## F&H Projects

These projects included building and supporting the external customer-facing websites as well as implementing intranet systems for document management, and designing materials for print (logos, brochures, business cards).

![scootinscooters](/uploads/2015/07/scootinscooters.jpg)

### scootinscooters.com

This was a standard business website with a few dynamic features such as a product catalog, product registration forms, and dealer locators. I also did the design and layout for the site.

## Jesscom Work
As the lead web developer at Jesscom.net I was involved with the development of dozens of sites. The projects ranged from simple static brochure type designs to full portals with complex backend systems and multiple integrative components. Most of the backend development was done with ColdFusion and MS SQL.

### e1051.fm + hot1067.com + rockthis.com + kncycountry.com

These were portal websites for several local/regional radio stations owned by the parent company. While layout and design were handled by our in-house web design staff, I provided all of the backend code for dynamic content generation as well as front-end AJAX-style JavaScript programming. These sites also incorporated real-time information about songs currently being played on-air. This required additional network (Windows/Service/C++) application programming in order to extract the data from the studio tracking software and import it into the website backend.

![e1051](/uploads/2015/07/e1051.jpg)

![hot1067](/uploads/2015/07/hot1067.jpg)

![rockthis](/uploads/2015/07/rockthis-new.jpg)

![kncycountry](/uploads/2015/07/kncycountry.jpg)


### dare2care.net + kcdare2care.com
The Dare2Care sites were local charity / volunteer sites supported by our parent company. I implemented the features allowing organizations to post about volunteering opportunities and for volunteers to search that information.

![kcdare2care](/uploads/2015/07/kcdare2care.jpg)

![dare2care](/uploads/2015/07/dare2care.jpg)\

### 417jobline.com + careersinfood.com

These were local job posting boards for which I implemented all of the basic features you would typically find on most employment targetted websites.

![417jobline](/uploads/2015/07/417jobline.jpg)

![careersinfood](/uploads/2015/07/careersinfood.jpg)


## The Others

There are a number of other sites that I also facilitated the development of in some minor capacity. This is a collection of screenshots from a few of those sites.

radio2000.fm<br /> jesscom.net<br /> jesscom.com<br /> coolears.com<br /> intriguemusic.com<br /> walnutrealty.net<br /> titanair.com<br /> theticketfactory.com<br /> 417web.net

![radio 2000](/uploads/2015/07/radio2000.jpg)

![Jesscom.net](/uploads/2015/07/jesscom-net.jpg)

![Jesscom.com](/uploads/2015/07/jesscom-com.jpg)

![Cool Ears](/uploads/2015/07/coolears.jpg)

![Intrigue Music](/uploads/2015/07/intriguemusic.jpg)

![Walnut Realty](/uploads/2015/07/walnutrealty.jpg)

![Titan Air](/uploads/2015/07/titanair.jpg)

![The Ticket Factory](/uploads/2015/07/theticketfactory.jpg)

![417 Web](/uploads/2015/07/417web.jpg)

## Game Dev Code

![voxel](/uploads/2015/07/voxel.png)


### Voxel

This is a small application created for the purposes of testing out voxel-based random world generation and manipulation a la [Minecraft](//minecraft.net). It is written in C++ using the <a href="https://github.com/sigsegv42/v3dlibs">v3dlibs</a> components and libnoise for the terrain generation.<br /> <a href="https://github.com/sigsegv42/voxel">GitHub repo</a>


![mos](/uploads/2015/07/mos.jpg)


### Minions of Steel
This is an independent RTS (with some FPS elements mixed in) game project which I contributed some coding work on (porting from Ogre 1.2 to 1.4, level/scene loading, input handling, collision detection, camera controls, etc). It is built on the Ogre3D game engine and uses a number of other components such as OIS for input, CEGUI for UI support, tinyxml for XML parsing, et al.

![pong](/uploads/2015/07/pong.jpg)


### Pong!
A rehash of the classic. Simple 2D graphics using OpenGL and sound effects via OpenAL. Supports 2 player Co-op and single player versus AI game play modes. It began as a simple project to implement a completely finished and working game utilizing modern C++. Since the completion of the working prototype, it has slowly become a test application for a growing set of common framework libraries.

### v3D Libraries

The v3dlibs project is a collection of C++ application libaries used across my various 3D application projects. There are libraries for image reading & writing (PNG, TGA, BMP, JPEG), font rendering (bmfont, FreeType), OpenAL audio, basic 3D data types, an event framework, OpenGL rendering helpers, and backend window drivers for SDL, SDL2, FLTK, and SMFL.

![tetris](/uploads/2015/07/tetris.png)


### Tetris

A rehash of the classic. Simple 2D graphics using OpenGL and sound effects via OpenAL. Supports 2 player Co-op and single player versus AI game play modes. It began as a simple project to implement a completely finished and working game utilizing modern C++. Since the completion of the working prototype, it has slowly become a test application for a growing set of common framework libraries.

![v3d](/uploads/2015/07/v3d-ss2_sm.png)

### Rigel

This is a GNU/Linux 3D Modelling Application. It supports a limited set of polygon objects (cube, cone, cylinder), standard transformation tools (rotate, translate, scale), interactive picking/selection of objects and sub-object components, and subobject component editing (edge/face/vertex transformations, face/edge splitting). It is built using GTK– for the interface and renders 3D scenes using OpenGL.

![code](/uploads/2015/07/code.jpg)



### libhookah
This is the common library used in pong, tetris, et al. It is written in modern C++ and utilizes features from the standard library and boost libraries. While it began as a single engine library, it is currently organized into a collection of small libraries. Each library provides a limited collection of services &#8211; config file parsing, abstract input device and event handling, concrete SDL binding, 3D data types, fonts, sound support. External dependencies include OpenAL for sound, SDL for video and input, and QuantumXML for config files.

### QuantumXML

An XML Parsing library with DOM API support written in C++.

### Particles

A particle system demo.

### Mesh Loaders

A 3D File Format Loader demo.


### libluxa
An OpenGL GUI library.


### SuperMassive

A UT2004 mod consisting of a random assortment of UnrealScript classes for testing out new ideas.<


### Meerkat
A small UT2004 mod. This is an UnrealScript-only modification that adds a new DM gametype with a new starting weapon. The weapon fires targetting beacons and target seeking rockets.

### Caravan of Mastodons
A tiny UT2004 mod. This modification creates a new main menu screen with a custom background image and a map list selection box.

### Linux Shell
A tiny test command shell built on GNU/Linux.<br /> <a href="http://quantumfish.com/files/shell.cxx">download</a>


### Particle Demo 1.4

This is my original OpenGL game engine demo project. This release is based on approximately 15K lines of object-oriented C++ implementing some basic game engine features such as tga texture loading, 2D fonts, a particle system, command console, multitextured skybox, Quake 2 and Milkshape 3D model loading, scene antialiasing, and a command/event binding system.

![screen 1](/uploads/2015/07/screen14_1-1024x796.jpg)
![screen 2](/uploads/2015/07/screen14_2-1024x796.jpg)
![screen 3](/uploads/2015/07/screen14_3-1024x796.jpg)
