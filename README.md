ZnapZend 0.14.1
===============

[![Build Status](https://travis-ci.org/oetiker/znapzend.svg?branch=master)](https://travis-ci.org/oetiker/znapzend)
[![Coverage Status](https://img.shields.io/coveralls/oetiker/znapzend.svg)](https://coveralls.io/r/oetiker/znapzend?branch=master)

ZnapZend is a ZFS centric backup tool. It relies on snapshot, send and
receive todo its work. It has the built-in ability to to manage both local
snapshots as well as remote copies by thining them out as time progresses.

The ZnapZend configuration is stored as properties in the ZFS filesystem
itself.

Zetup Inztructionz
------------------

Follow these zimple inztructionz below to get a custom made copy of
znapzend. Yes you need a compiler and stuff for this to work.

```sh
wget https://github.com/oetiker/znapzend/releases/download/v0.14.1/znapzend-0.14.1.tar.gz
tar zxvf znapzend-0.14.1.tar.gz
cd znapzend-0.14.1
./configure --prefix=/opt/znapzend-0.14.1
```

If configure finds anything noteworthy, it will tell you about it.  If any
perl modules are found to be missing, they get installed locally into the znapzend
installation. Your perl installation will not get modified!

```sh
make
make install
```

Configuration
-------------

Use the [znapzendzetup](doc/znapzendzetup.pod) program to define your backup settings. For remote backup, znapzend uses ssh.
Make sure to configure password free login for ssh to the backup target host.

Running
-------

The [znapzend](doc/znapzend.pod) demon is responsible for doing the actual backups. 

To see if your configuration is any good, run znapzend in noaction mode first.

```sh
/opt/znapzend-0.14.1/bin/znapzend --noaction --debug
```

If you don't want to wait for the scheduler to actually schedule work, you can also force immediate action by calling

```sh
/opt/znapzend-0.14.1/bin/znapzend --noaction --debug --runonce=<src_dataset>
``` 

then when you are happy with what you got, start it in daemon mode.

```sh
/opt/znapzend-0.14.1/bin/znapzend --daemonize
```
 
Best is to integrate znapzend into your system startup sequence, but you can also
run it by hand.

For solaris/illumos OSes you can import make configure install a znapzend
service manifest by calling configure with the option
```--enable-svcinstall=/var/svc/manifest/site```.  Since the manifest
contains the absolute path the the znapzend install directory, it is not
contained in the prebuilt version.  But you can get a copy from github and
roll your own.

```sh
svccfg validate /var/svc/manifest/site/znapzend.xml
svccfg import /var/svc/manifest/site/znapzend.xml
```

and then enable the service 

```sh
svcadm enable oep/znapzend
```

Statistics
----------

If you want to know how much space your backups are using, try the
[znapzendztatz](doc/znapzendztatz.pod) utility.

Support and Contributions
-------------------------
If you find a problem with znapzend, please open an Issue on GitHub.

If you like to get in touch, you can find Dominik and Tobi on the IRC-Channel [#znapzend on irc.freenode.net](irc://irc.freenode.net/#znapzend)

And if you have a contribution, please send a pull request.

Enjoy!

Dominik Hassler & Tobi Oetiker
2015-10-12
