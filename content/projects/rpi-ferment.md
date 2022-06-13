---
title: rpi-ferment
author: Josh
type: projects
image: /uploads/2015/07/rpiferment.jpg
socialShare: false
---

## v1

This is a beer fermentation temperature monitoring, logging, and control application suite built on the Raspberry Pi platform.  There are a series of [blog posts](/blog/2013/04/20/raspberry-pi-fermentation-controller-part-1/) detailing the entire project. The software aspect comprises two Node.js applications written in CoffeeScript. The [backend](https://github.com/farrcraft/rpi-ferment) server interacts with the Pi’s GPIO, capturing temperature data from any number of configured DS18B20 temperature sensors and logging them into graphite via statsd. It also exposes a RESTful API built using Express and Mongoose for managing fermentation profiles. A Socket.io server is also integrated for managing the controller. The [frontend application](https://github.com/farrcraft/rpi-ferment-frontend) provides a UI for displaying graphs of logged temperature data, managing profiles, and interacting with the backend. It is built using <a href="https://github.com/SimbCo/brunch-with-marionette">Brunch with Marionette</a> and served with a thin static Node.js server.
