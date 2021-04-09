# shrink

**Linux bash script to resize Raspberry SD card images**  
consider further [remarks](#remarks)

### new version
\- automated size retrieving from GParted  
\- progress bars with ETA for all time consuming actions  
\- environment variable support

**not widely tested yet, be sure to have backups of your data**  
or use [previous version](readme_071.md)

### download  
download repository from GitHub,  
unzip and copy for example to: ~/shrink

**or**

copy script to current directory  
`wget https://raw.github.com/qrti/shrink/master/script/shrink.sh`

**or**

check if git is installed  
`$ git --version`

if git is not installed  
`$ sudo apt-get install git-all`

clone shrink repository to current directory  
`$ git clone https://github.com/qrti/shrink.git`

- - -

### necessary installs  
`$ sudo apt-get install gparted`  
`$ sudo apt-get install pv`

- - -

### configure  
before executing the script the first time, insert your SD card

enter the following at the command line and find the name of your SD device and partitions  
`$ df -h`

edit the script and enter your data between the quotation marks  
`$ nano shrink.sh`

example for /dev/sdb1 + 2 (omit digit)
```
DEVICE=${DEVICE:-/dev/sdb}
```

example for /dev/mmcblk0p1 + 2 (omit p and digit)
```
DEVICE=${DEVICE:-/dev/mmcblk0}
```

your username is filled in automatically, to override edit USER
```
USER=${USER:-`whoami`}
```

**using environment  variables**  
default values can be overridden by passing them as env vars

for example to set DEVICE and READ enter at the command line  
`$ sudo DEVICE=/dev/sdb READ=false ./shrink.sh`

explore the top of the script to configure some more things

- - -

### execute  
change directory  
`$ cd ~/shrink`

make script executable once  
`$ chmod 755 shrink.sh`  
**or**  
`$ chmod a+x shrink.sh`

execute script  
`$ sudo ./shrink.sh`

- - -

### remarks  
\- use this script completely at your own risk

\- runs on physical or virtual Linux desktop systems

\- cannot handle NOOBS images

\- do not shrink images to minimum, otherwise they won't start on your Raspberry, especially Raspbian Full *Desktop* images need some extra space, about >= 250 MB are advised, Raspbian *Lite* images might be more moderate

\- when starting from a shrinked SD card for the first time, expand the filesystem to fill its space

by raspi-config  
`sudo raspi-config` -> *Expand Filesystem*  
`sudo reboot`  
**or**  
from command line  
`sudo raspi-config --expand-rootfs`  
`sudo reboot`  

\- the script is 'half automatic', meaning at one point it will start GParted on desktop and guide you what to do

\- progress display of 'fill empty space' may not end at 100 % exactly because of difficult file system overhead calculation, nevertheless space will be filled correctly

\- the script was developed and tested on a VirtualBox Windows host with Linux Mint guest

\- inspired by  
[http://www.aoakley.com/articles/2015-10-09-resizing-sd-images.php](http://www.aoakley.com/articles/2015-10-09-resizing-sd-images.php)

Donations are welcome!

[![https://www.paypal.com](https://www.paypalobjects.com/webstatic/en_US/btn/btn_donate_pp_142x27.png)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=E7JNEDMHAJ3TJ)

- - -

### history  
V0.5  
initial version, script keel fix by Barleyman  

V0.6  
mmcblk naming support

V0.7  
simplifications

V0.71  
adaption for parted 3.2, p -> print

V0.8  
automated size retrieving from GParted  
progress bars with ETA for all time consuming actions

V0.81  
default value override by environment variables  
thanks to Leon Miller-Out

- - -

### copyright  
shrink is published under the terms of ISC license

Copyright (c) 2018 [qrt@qland.de](mailto:qrt@qland.de)

Permission to use, copy, modify, and/or distribute this software for any purpose with or without fee is hereby granted, provided that the above copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED 'AS IS' AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
