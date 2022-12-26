---
title: Raspberry Pi Fermentation Controller – Part 2
author: Josh
type: post
date: 2013-04-24T00:00:00+00:00
url: /blog/2013/04/24/raspberry-pi-fermentation-controller-part-2/
image: /uploads/2013/04/pi_console.jpg
socialShare: false
categories:
  - Brewing
  - Code

---

In [part 1][1] I walked through getting the Raspberry Pi initially up and running. Once you’re logged in, you can immediately start hooking up sensors and start polling them directly from the command line. However, you’re likely going to want some more software installed for additional tasks. For my fermentation controller, I’ve decided on the following software stack.

<!-- more -->

## Software Stack

  * [Graphite][2]
  * [StatsD][3]
  * [Node.js][4]
  * [MongoDB][5]

All of the data read from sensors along with GPIO state changes will all be recorded in Graphite. Graphite stores the data and provides tools for generating graphs from it. The StatsD server will be responsible for sending data to the graphite server. I’ll be using Node.js for communicating with the sensors and providing a web-based interface to interact with the entire system. The web UI will also use MongoDB for storing additional fermentation data.

![][6] 

## Screen

Before starting to install all of the necessary software, it’s a good idea to install the screen program and start it up. Some of the steps can take a long time to complete and if your SSH session gets disconnected, screen will keep the session active. In that case all you need to do is reconnect and run the screen command to reattach to your previous running session.<figure class="code"><figcaption>Using screen </figcaption>


```bash
sudo apt-get install screen
# start screen
screen
# list active sessions after reconnecting
screen -ls
# reattach the screen listed in the output from the last command, e.g.:
screen -r 11592.pts-0.raspberrypi
```

## Node.js

There are to ways to install Node.js. You can choose to either install a package via apt-get or to compile it directly from source. While the first option is quick and simple, you’ll get a much older version (currently 0.6.19) than if you build it yourself.<figure class="code"><figcaption>Installing Node.js from a package </figcaption>

```bash
# this will install version 0.6.19 of node
sudo apt-get install nodejs
# if you decide you don't want this version then you can uninstall it
sudo apt-get purge nodejs
```

Fortunately, the most recent versions of Node.js have support for the Pi’s architecture. So Building from source is a fairly straightforward series of steps and doesn’t require any complex patching steps as it did for older versions. The downside is that it’ll take at least several hours to compile. The following steps should result in a fresh installation of the most recent release version of Node.js.<figure class="code"><figcaption>Compiling Node.js </figcaption>

```bash
# install dependencies needed for compiling software
sudo apt-get install git-core build-essential
# download the Node.js source repository
git clone https://github.com/joyent/node.git

cd node

# list remote branches
git branch -r

# change the repository to the source tagged as version 0.10.4
git checkout -t origin/v0.10.4-release
# configure & compile
./configure
make
# install
make install

# verify the node application is installed in /usr/local/bin/node
which node
# check that the version matches what you just installed
node -v
```

## Graphite

Getting Graphite installed isn’t much more work. Since it is a python application it also takes quite a bit less time than compiling Node.js. However, there is some additional configuration work that has to be done. Graphite is composed of several different components. The backend component is called Carbon. The Carbon server is what StatsD will send its data to. The web accessible interface portion responsible for generating the graphs is known as Graphite. Since this is a web interface, we also need a web server. So, the Apache web server will also be installed during the process. If you’d rather have a more automated procedure itt’s also possible to script most of these steps as in this [example][7].<figure class="code"><figcaption>Installing Graphite </figcaption>

```bash
# switch to root user
sudo -i

# install python dependencies
apt-get install python-pip python-cairo python-django python-django-tagging python-twisted

# install apache
apt-get install apache2 libapache2-mod-wsgi libapache2-mod-python

# install graphite
pip install whisper
pip install carbon
pip install graphite-web
```

Graphite comes with a good collection of example configuration files that provide a good set of defaults to get started with. Only a few edits in a few spots are necessary to get going. It’s a good idea to take a look through each configuration file anyway to get an idea of the options that are available.<figure class="code"><figcaption>Configuring Graphite </figcaption>

```bash
# switch to graphite config directory and copy the example configs
cd /opt/graphite/conf
cp carbon.conf.example carbon.conf
cp aggregation-rules.conf.example aggregation-rules.conf
cp storage-aggregation.conf.example storage-aggregation.conf
cp relay-rules.conf.example relay-rules.conf
cp storage-schemas.conf.example storage-schemas.conf
cp dashboard.conf.example dashboard.conf
cp graphTemplates.conf.example graphTemplates.conf
cp graphite.wsgi.example graphite.wsgi

cd /opt/graphite/webapp/graphite
cp local_settings.py.example local_settings.py
# uncomment timezone setting (default is CST, but we're in PST)
sed -i 's/\#TIME_ZONE/TIME_ZONE/g' local_settings.py

nano -w local_settings.py
# find and uncomment DATABASES = … block
python manage.py syncdb
# answer prompts - yes, blank for default username (root), enter email address, enter password (e.g. raspberry)
chown -R www-data:www-data /opt/graphite/storage/

# configure Apache
wget https://raw.github.com/tmm1/graphite/master/examples/example-graphite-vhost.conf -O /etc/apache2/sites-available/graphite
# change default socket path from /etc/httpd/wsgi which doesn't exist to /var/run/apache2
sed -i 's/\/etc\/httpd\/wsgi\//\/var\/run\/apache2\//g' /etc/apache2/sites-available/graphite
# set django root path
sed -i's/@DJANGO_ROOT@/\/usr\/lib\/python2.7\/dist-packages\/django/g' /etc/apache2/sites-available/graphite

# enable graphite website
a2ensite graphite
# restart apache to apply changes
service apache2 reload
```

At this point you could manually start up the carbon server and connect to the graphite web site. Instead, we’re going to install one more script that will make sure that carbon is started automatically whenever the Pi is booted.<figure class="code"><figcaption>Carbon init script </figcaption>

```bash
wget https://raw.github.com/sigsegv42/rpi-ferment/master/scripts/carbon -O /etc/init.d/carbon
chmod 755 /etc/init.d/carbon
# set default runlevels for carbon service
update-rc.d carbon defaults
# start up carbon
/etc/init.d/carbon start
```

If everything was successful, you should now be able to access graphite in your web browser. The default Apache configuration assigns the name ‘graphite’ to the website. To be able to access it, you’ll need to map that name to the IP of the Raspberry Pi in your hosts file. On OSX or GNU/Linux platforms you would edit the file _/etc/hosts_. The file in MS Windows is usually located at _C:\Windows\System32\drivers\etc\hosts_. The new entry would look similiar to this:

> 192.168.2.189   graphite

modified to reflect the actual IP of the Pi. After the hosts file has been updated, you should be able to open <http://graphite/> in the web browser of your choice. If it worked, you should see the Grahpite graph composer interface. Of course, it’ll be a bit boring still until you start logging some data.

## StatsD

StatsD is a small Node.js application and doesn’t require any special installation steps on its own. You could just download the source repository and start running it. However, we’d like to have it automatically start up when the system boots up just like we setup carbon. Fortunately, the StatsD repository includes everything needed to turn the source into a debian package complete with boot scripts.<figure class="code"><figcaption>Building the statsd debian package </figcaption>

```bash
# install devscripts (pulls in lots of little perl modules) needed to build debian packages
apt-get install devscripts
# download statsd source
git clone git://github.com/etsy/statsd.git
cd statsd
# remove the nodejs package dependency since we installed node from source
sed -i 's/\, .*//g' debian/control
# build a debian package for statsd
debuild -us -uc
# install the statsd package
dpkg -i ../statsd_0.0.3_all.deb
# add statsd to boot
update-rc.d statsd defaults
# copy statsd config
wget https://raw.github.com/sigsegv42/rpi-ferment/master/lib/statsdConfig.js -O /etc/statsd/localConfig.js
# start statsd
/etc/init.d/statsd start
```

## MongoDB

The last piece of software in our stack is MongoDB. Unfortunately, the stock version doesn’t support the Pi’s architecture. Luckily there are several forks which have added this support. I’ve chosen to use one called _mongopi_. This is a slightly older version based on 2.1.1, but it should work for our needs on the Pi. This approach also means that we’re compiling from source again. You’ll want to make sure that you’re running screen before you start because MongoDB takes a really long time to build and install &#8211; on the order of 12 hours long. Once you hit enter on the scons command, you may just want to leave it to run and check back in on it tomorrow.<figure class="code"><figcaption>Installing mongodb </figcaption>

```bash
# install mongodb build dependencies
apt-get install scons libpcre++-dev xulrunner-dev libboost-dev libboost-program-options-dev libboost-thread-dev libboost-filesystem-dev
# checkout a fork of mongodb customized to support the Pi
git clone git://github.com/RickP/mongopi.git
cd mongopi/
# build
scons
# install
```

As we did with the other components, we want to make sure that MongoDB starts up during boot. There are also a few directories to be created before mongo can be started.<figure class="code"><figcaption>Configuring mongodb </figcaption>

```bash
# create a user that the server will run under
useradd mongodb
# create db storage, log, and configuration directories
mkdir /var/lib/mongodb
mkdir /var/log/mongodb
mkdir /etc/mongodb
# configuration file with any additional startup options. empty is fine but it has to exist
touch /etc/mongodb/mongodb.conf
# set ownership
chown mongodb:mongodb /var/lib/mongodb
chown mongodb:mongodb /var/log/mongodb/
# add the mongo path to the global system path
echo "PATH=$PATH:/opt/mongo/bin/" &gt;&gt; /etc/environment
echo "export PATH" &gt;&gt; /etc/environment
# setup the init script
wget https://gist.github.com/ni-c/fd4df404bda6e87fb718/raw/36d45897cd943fbd6d071c096eb4b71b37d0fcbb/mongodb.sh -O /etc/init.d/mongodb
chmod 755 /etc/init.d/mongodb
update-rc.d mongodb defaults
# start the mongodb service
service mongodb start
```

## Conclusion

After going through all of these steps, you’ll have a Raspberry Pi running with Graphite, StatsD, MongoDB, and Node.js. It’s a good idea to try rebooting (_shutdown -r now_ will accomplish this) and make sure that all of the services start up on boot as they’re supposed to. The _ps_ command can be used to show running processes and verify that the services are all running. In [part 3][8] I’ll cover the rest of the hardware components of the project and how to get all of the sensors wired up.

 [1]: /blog/2013/04/20/raspberry-pi-fermentation-controller-part-1/
 [2]: http://graphite.readthedocs.org/en/0.9.10/
 [3]: http://codeascraft.etsy.com/2011/02/15/measure-anything-measure-everything/
 [4]: http://nodejs.org/
 [5]: http://www.mongodb.org/
 [6]: /images/pi/pi_console.jpg
 [7]: https://github.com/ghoulmann/rpi-graphite/blob/master/rpi-graphite.sh
 [8]: /blog/2013/05/14/raspberry-pi-fermentation-controller-part-3/