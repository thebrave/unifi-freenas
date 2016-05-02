unifi-freenas
=============

A FreeNAS package that provides the UniFi Controller software.

Purpose
-------

The objective of this project is to develop and maintain a package that provides [Ubiquiti's](http://www.ubnt.com/) UniFi Controller software for the FreeBSD-based [FreeNAS](http://www.freenas.org/) project.

Status
------

The project now provides two working scripts: an rc script to start and stop the UniFi controller, and an installation script to automatically download and install everything, including the rc script.

Licensing
---------

This project itself is licensed according to the two-clause BSD license.

The UniFi Controller software is licensed as-is with no warranty, according to the README included with the software.

[Ubiquiti has indicated via email](https://github.com/gozoinks/unifi-pfsense/wiki/Tacit-Approval) that acceptance of the EULA on the web site is not required before downloading the software.

Upgrading from 3.2
------------------

Be sure to backup your configuration under 3.2 through the web admin UI before upgrading. The upgrade from 3.2 does not appear to go smoothly simply by archiving and restoring the /var/UniFi directory. You will need to use the web admin UI backup tool to create an .unf file, which you can then restore to 4.7.5 when it loads.

Installation
------------

To install the controller software and the rc script:

1. Log in to the FreeNAS command line shell as root.
2. Run this one-line command, which downloads the install script from Github and executes it with sh (points to current 4.6.6 branch):

  ```
    fetch -o - https://git.io/vwyUx | sh -s
  ```

The install script will install dependencies, download the UniFi controller software, make some adjustments, and start the UniFi controller.

Starting and Stopping
---------------------

To start and stop the controller, use the `service` command from the command line.

- To start the controller:

  ```
    service unifi start
  ```
  The UniFi controller takes a few minutes to start. The 'start' command exits immediately while the startup continues in the background.

- To stop the controller:

  ```
    service unifi stop
  ```
  The the stop command takes a while to execute, and then the shutdown continues for several minutes in the background. The rc script will wait until the command received and the shutdown is finished. The idea is to hold up system shutdown until the UniFi controller has a chance to exit cleanly.

References
----------

These sources of information immediately come to mind:

- [UniFi product information page](http://www.ubnt.com/unifi#UnifiSoftware)
- [UniFI download and documentation](http://www.ubnt.com/download#UniFi:AP)
- [UniFi updates blog](http://community.ubnt.com/t5/UniFi-Updates-Blog/bg-p/Blog_UniFi)
