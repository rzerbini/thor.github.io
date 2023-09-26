---
title: "Install Bspwm in Archlinux"
date: 2023-09-26T12:48:42-03:00
draft: true
tags: [bspwm, ocean, install]
categories: [linux, virtual]
---


### Install Bspwm in Debian

![Viking](ocean.png)

```
> sudo apt install bspwm sxhkd polybar compton rofi dunst nitrogen i3lock redshift cmus ranger dmenu
```

Copy the example configuration to your ~/.config folder and make sure bspwmrc is executable :


```
> cd ~/.config/ && mkdir -p bspwm sxhkd
> cp /usr/share/doc/bspwm/examples/bspwmrc ~/.config/bspwm/
> cp /usr/share/doc/bspwm/examples/sxhkdrc ~/.config/sxhkd/
> chmod u+x ~/.config/bspwm/bspwmrc
```

#### Keybindings: sxhkdrc
```
> nano ~/.config/sxhkd/sxhkdrc
```

#### Config file: bspwmrc
Check the config file:
```
> nano ~/.config/bspwm/bspwmrc
```
Declare the apps to autostart when launching a session:
```
make sure sxhkdrc is launched at start: pgrep -x sxhkd > /dev/null || sxhkd &
compositing manager: compton --backend glx --vsync opengl-swc &
usr/lib/xfce-polkit/xfce-polkit &
bar (here polybar, throught a script): ~/bin/polybar.launch.sh &
wallpaper: nitrogen --restore &
```

#### Bar: polybar
We won’t use the default bspwm bar, but Polybar: highy customizable and documented. And fully compatible with bspwm.
```
mkdir ~/.config/polybar
cp /etc/polybar/config.ini ~/.config/polybar/
nano ~/.config/polybar/config
```

We start Polybar through a script referenced in bspwmrc:

```
#!/usr/bin/env sh
# Terminate already running bar instances
killall -q polybar
# Wait until the processes have been shut down
while pgrep -x polybar >/dev/null; do sleep 1; done
# Launch: 'top' is the name of my Polybar
polybar &
```

Done, now it’s time to work on the config file.

#### Install a NerdFont to display icons on your bar:

```
> wget https://github.com/ryanoasis/nerd-fonts/releases/download/v2.1.0/JetBrainsMono.zip
dtrx JetBrainsMono.zip
> sudo cp -avr JetBrainsMono/ /usr/share/fonts/truetype/
> fc-cache -f -v
> rm JetBrainsMono.zip
```

#### Compositor: compton
I’ve tried a few compositor, mostly forks of Picom adding blur, rounded corners and animations. Heavy on CPU, mostly work in progress, sometimes impressive, but in the end an optimized compton.conf is the best solution.

```
# shorter shadows
shadow-radius = 5;
shadow-offset-x = -5;
shadow-offset-y = -5;
shadow-opacity = 0.8;
# faster animations
fade-in-step = 0.07;
fade-out-step = 0.07;
```

#### Launcher: rofi
Rofi is a fantastic customizable launcher for Linux, we use it instead of dmenu and to manage additional menus such as Session menu.

To launch Rofi open a terminal and enter: rofi -show drun

This will launch Rofi in desktop run mode: it allows users to quickly search and launch an application from the freedesktop.org Desktop Entries. These are used by most Desktop Environments to populate launchers and menus. Drun mode features:
favorites list, with frequently used programs sorted on top
auto starting terminal applications in a terminal
Rofi config file is in: ~/.config/rofi/config.rasi. You may compose multiple themes and call them in CLI: rofi -shwo drun -theme path/to/file.rasi I'm using this option for bspwm session menu.

#### ScreenLocker: i3lock
Fantastic screenlocker, to use as it is, and before suspending your machine. It only takes PNG files as background image.

lock: i3lock --image ~/Pictures/Backgrounds/lock.png

lock & suspend: i3lock --image ~/Pictures/Backgrounds/lock.png && sudo pm-suspend

---

ref:
 https://medium.com/tech-notes-and-geek-stuff/installing-bspwm-on-debian-fd6a315f6903  
 https://github.com/thespation/dpux_bspwm/tree/main

see also for ArchLinux https://www.youtube.com/watch?v=PLBm0C5Gv58