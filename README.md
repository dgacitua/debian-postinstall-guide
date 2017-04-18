# Debian Stable Post-install Guide

Created by Daniel Gacitua (<daniel.gacitua@usach.cl>)

This is a simple guide with terminal commands to be executed after a fresh Debian Stable installation to get your computer up and running.

This guide assumes that you have some basic Linux knowledge and that you can use a terminal.

All commands starting with a `$` character must be run as a normal user, and all commands starting with a `#` character must be run as root user. Remember to copy all the line except for these starting characters (they must not be included in the terminal command).

To copy commands from terminal, select the content with your mouse and press `CTRL`+`SHIFT`+`C`.

To paste commands into a terminal, press `CTRL`+`SHIFT`+`V`.

---

## Essential commands

### Create new users

If you need to create more users, go to root with `su -`, run `adduser` and follow the instructions on screen (repeat this command as many times as needed). After your users are set, exit from root.

```
$ su -
# adduser myuser
# exit
```

### Give sudo access to normal users

Go to root with `su -` and run `usermod` replacing `myuser` by the name of the normal user. You can repeat the `usermod` command as many times you need to set multiple sudo users. Once all your sudo users are set, restart the machine with `reboot`.

```
$ su -
# usermod -aG sudo myuser
# reboot
```

### Set apt-get repositories

Open the apt-get repo list with `nano` (a terminal text editor):

```
$ sudo nano /etc/apt/sources.list
```

Once the file has opened, replace all contents with the following:

```
# /etc/apt/sources.list

deb http://ftp.us.debian.org/debian/ jessie main contrib non-free
deb-src http://ftp.us.debian.org/debian/ jessie main contrib non-free

deb http://ftp.us.debian.org/debian/ jessie-updates main contrib non-free
deb-src http://ftp.us.debian.org/debian/ jessie-updates main contrib non-free

deb http://security.debian.org/ jessie/updates main contrib non-free
deb-src http://security.debian.org/ jessie/updates main contrib non-free
```

You can replace the `http://ftp.us.debian.org/debian/` part with any Debian repository mirror of your choice. You can also replace all `jessie` matches in the file to `stable` or `testing` to change your release version (if you change it, you will need to update all your packages).

After you finish to edit the file, use `CTRL`+`O` to save the file and then `CTRL`+`X` to exit. Then, you will need to update the repository settings with the following command:

```
$ sudo apt-get update
```

### Essential packages

This is my own selection of essential packages that are not installed in Debian by default, run this command to install them:

```
$ sudo apt-get install -y build-essential curl zip unzip
```

---

## Optional commands

### Update all packages

With this procedure, you will update all your installed packages. If you have changed you release version, you will need to do this after updated your repository settings.

If you are using a desktop environment, logout all active users on the computer. From your login screen, press `CTRL`+`ALT`+`F2` and login as root in the full screen terminal that just opened. Then run the following commands:

```
# apt-get upgrade
# apt-get dist-upgrade
```

These commands could take some time, since they will search, download and install new versions for all your installed packages. After all packages are updated, you will need to restart your computer:

```
# reboot
```

---

## Legal stuff

### Changelog

2017-04-18: First commit

### License

This guide is released under MIT License.
