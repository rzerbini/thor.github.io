---
title: "DWM on Debian"
date: 2023-07-04T00:00:00+00:00
categories: [home,dwm,debian]
tags: [debian,linux,etc]             # Tag always lowercase
---

## Debian install dwm

* https://github.com/sgomare/featherOS.git
* https://github.com/ChrisTitusTech/Debian-titus.git
* https://github.com/drewgrif/dwm-debian.git
* https://github.com/PietJanHein/dwm-setup
* https://johnjago.com/dwm/

Base Instructions from https://johnjago.com/dwm/

````
wget https://dl.suckless.org/dwm/dwm-6.4.tar.gz
wget https://dl.suckless.org/tools/dmenu-5.2.tar.gz
wget https://dl.suckless.org/st/st-0.9.tar.gz

tar xf (each_dir)

cd (each_dir)
make
sudo make clean install

sudo apt install make gcc libx11-dev libxft-dev libxinerama-dev xorg kitty thunar
````
Next, create a file called .xinitrc in your home directory. Place this inside of it:
````
while xsetroot -name "`date` `uptime | sed 's/.*,//'`"
do
	sleep 1
done

exec dwm
````
----
other situs soon II