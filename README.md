# authtoken 0.3.2
`authtoken` is a small tool that provides an interface to load the PKCS driver for an SSH agent.

This small application helps you to easily add and remove a [Feitian](http://www.ftsafe.com/) authentication token to your
SSH agent on a Ubuntu workstation, like the [Feitian ePass2003](http://www.ftsafe.com/products/PKI/Standard).

It works by defining a hardware device and revision in the configuration and start the
application in your user session. It runs in the background. The application scans the hardware
bus for any changes. When it detects that the configured device is added or removed, it will add
or remove a PKCS11 library from the SSH agent. It presents a nice prompt in the user interface
for your password and it gives you a graphical notification when something happens.

## Support
It has been made for **Ubuntu 18.04 LTS** and **Feitian ePass2003** authentication tokens, but it should
work on other systems as well, maybe with some custom tweaking.

## Installation
Install the provided Debian package, or build it yourself.

```bash
debuild -i -us -uc -b
sudo apt install ../authtoken_0.3.2_amd64.deb
```

It will ask you if you want to disable the Gnome Keyring SSH agent, which you probably should because it
is not compatible with the PKCS11 library. It will also ask you if you want to autodetect the token. Make
sure you have the token inserted in your workstation before you continue.

### Usage
The installation will make a desktop file to auto load the binary at system start up. Just insert your
token and a password prompt will appear. You may also invoke the binary at command line.

```bash
# Initialze the background listener
/usr/bin/authtoken init

# Unlock token with a password on command line
echo 'mypassword' | /usr/bin/authtoken login
```

### Configuration
During the installation of the package it will try to scan the hardware bus for any Feitian tokens. If
multiple tokens are found, you can select the token that you want to use. You may always reconfigure
using `dpkg-reconfigure authtoken` or just change the configuration file `/etc/authtoken/token.conf` manually.

### Changelog

# 0.3.2

* Fix bug where unbind USB events are ignored

# 0.3.1

* Require a legacy version of OpenSC because 0.17.0 has a bug that fails to add the library

# 0.3.0

* Release for Ubuntu 18.04 LTS

# 0.2.2

* Kill previous sessions at startup
* Fix missing Ubuntu icons
* Allow password through stdin
* Fix minor syntax bugs

## Conclusion
Enjoy and let me know if you have some questions or issues.

Thomas Lobker
