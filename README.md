[![AGPL](https://img.shields.io/badge/license-AGPL-blue.svg)](https://raw.githubusercontent.com/ichier/cmus_daemon/master/LICENSE)

# cmus_daemon / cmusd

This is a script to start, stop and access [cmus](https://cmus.github.io/), a powerful console music player, as well as the web-remote-control-server [cmus_app](https://github.com/ichier/cmus_app) detached to a [screen](https://linux.die.net/man/1/screen).  
You can quickly send some commands while cmus is in background or use the webinterface.  
It comes with a systemd.service in order to automatically run as a _daemon_ at machine-startup.

## Dependencies

You need, of course, all the stuff that it's about `cmus`, `screen` and `cmus_app` 

_Note: this is supposed to just work. Paths don't necessarily need to be your home-folder._

Installing dependencies in debian:

    $ sudo apt install cmus cmus-plugin-ffmpeg screen
    $ cd ~
    $ git clone git://github.com/ichier/cmus_app

- Run `cmus` and set a password on options-screen.
- Edit `./cmus_app/config` according to your needs, don't forget the password.

## Installing cmusd

First, navigate to the folder you want the program in, get `cmusd`, put a symlink to /usr/bin and create your config file: 

    $ cd ~
    $ git clone git://github.com/ichier/cmus_daemon
    $ cd ./cmus_daemon
    $ ln -s ./cmusd /usr/bin/cmusd
    $ ln -s ./cmusr /usr/bin/cmusr
    $ cp ./cmusd.service.conf ./cmusd.conf

- Now edit `./cmusd.conf` according to your needs.  
At least do the password and replace all occurences of myusername to your username. That will be the owner of the screens created.

## Installing the cmusd systemd-service

First, create the service-file:

    $ cp ./cmusd.service.example ./cmusd.service

- Now edit `./cmusd.service` by changing all occurences of myusername.
  
Continue with creating a symlink to /etc/systemd/system, enabling and starting it:

    $ ln -s ./cmusd.service /etc/systemd/system/cmusd.service
    $ systemctl enable cmusd
    $ systemctl start cmusd


## Usage

- just type `cmusd` without parameters to get help.

Most useful:

- `cmusd start` to start in background
- `cmusd stop` to stop
- `cmusd p` to start playback
- `cmusd g` to get cmus screen (`ctrl`-`a` + `d` to detach)
- `cmusd rw` to restart webserver (sometimes hangs)
- `cmusd dst` to show systemd-status of cmusd


##
_tested on a ubuntu server 19.10_