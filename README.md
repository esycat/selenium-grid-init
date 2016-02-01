# Selenium Grid Init Scripts

This is forked selenium grid init script for specific configuration

Default configuration defines standard locations for hub and node configs, logs and pid files.
The daemon runs under `ubuntu` user.
The service configuration can be changed in `/etc/default/selenium`.

To run Selenium server a JRE must be installed:
either `openjdk-7-jre`
or [`oracle-java7-jre`](http://webupd8.org/2012/01/install-oracle-java-jdk-7-in-ubuntu-via.html).

This setup was tested on Ubuntu 14.04 JRE7.

## Installation

Create the user and necessary directories:
```bash

sudo mkdir /opt/selenium
sudo mkdir /var/log/selenium
sudo chown ubuntu:ubuntu /var/log/selenium /var/run/selenium
```

Download Selenium Server jar file:
```bash
SELENIUM_VERSION="2.50.1"

cd /opt/selenium/
wget http://selenium-release.storage.googleapis.com/2.50/selenium-server-standalone-$SELENIUM_VERSION.jar
ln -sfn selenium-server-standalone-$SELENIUM_VERSION.jar server-standalone.jar
```

Clone the repository and create necessary symlinks (or copy the files):
```bash
git clone https://github.com/alamsz/selenium-grid-init.git /var/lib/selenium

ln -s /var/lib/selenium/conf.d/   /etc/selenium
ln -s /var/lib/selenium/init.d/*  /etc/init.d/
ln -s /var/lib/selenium/default/* /etc/default/
```

To start and stop Selenium Hub and/or Node daemons:
```bash
service selenium-hub start
service selenium-node-5556 start
service selenium-node-5557 start
```

To setup the service to run automatically on server bootup:
```bash
sudo update-rc.d selenium-node-5556 defaults
```
