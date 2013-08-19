# Selenium Grid Init Scripts and Configuration

A pair of simple init scripts to run Selenium Grid as Hub or Node server instances.

You can find [another similar project](https://github.com/feniix/selenium-grid-startup) that predates this one and provides a more complicated init script.
I needed to implement the scripts and arrange the files in a different way, hence this mini-project emerged.

Default configuration defines standard locations for hub and node configs, logs and pid files.
The daemon runs under `selenium` user.
The service configuration can be changed in `/etc/default/selenium`.

To run Selenium server a JRE must be installed:
either `openjdk-7-jre`
or [`oracle-java7-jre`](http://webupd8.org/2012/01/install-oracle-java-jdk-7-in-ubuntu-via.html).

This setup was tested on Ubuntu 12.04 and 13.10 with JRE7.

## Installation

Create the user and necessary directories:
```bash
useradd -r -b /opt -s /usr/sbin/nologin selenium

mkdir /opt/selenium
mkdir /var/log/selenium
mkdir /var/run/selenium
chown selenium:selenium /var/run/selenium /var/run/selenium
```

Download Selenium Server jar file:
```bash
SELENIUM_VERSION="2.35.0"

cd /opt/selenium/
wget https://selenium.googlecode.com/files/selenium-server-standalone-$SELENIUM_VERSION.jar
ln -sfn selenium-server-standalone-$SELENIUM_VERSION.jar server-standalone.jar
```

Clone the repository and create necessary symlinks (or copy the files):
```bash
git clone https://github.com/esycat/selenium-grid-init.git /var/lib/selenium

ln -s /var/lib/selenium/conf.d/   /etc/selenium
ln -s /var/lib/selenium/init.d/*  /etc/init.d/
ln -s /var/lib/selenium/default/* /etc/default/
```

To start and stop Selenium Hub and/or Node daemons:
```bash
service selenium-hub start
service selenium-node start
```

To setup the service to run automatically on server bootup:
```bash
sudo update-rc.d selenium-hub defaults
```
