# Selenium Grid Init Scripts and Configuration

A pair of simple init scripts to run Selenium Grid as Hub or Node server instances.

There's another similar project that was implemented earlier:
https://github.com/feniix/selenium-grid-startup
but I needed to implement the scripts and arrange the files differently.

Default configuration assumes a number of standards directories which have to be created.

The scripts were tested on Ubuntu 12.04 and 13.10.

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

To start and stop Selenium Hub and/or Node server:
```bash
service selenium-hub start
service selenium-node start
```

To setup the service to run automatically on server bootup:
```bash
sudo update-rc.d selenium-hub defaults
```

The service configuration can be found in `/etc/default/selenium`.
