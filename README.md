# DebConf
## My (Minimal) Debian Configuration
This is the continuation of my minimal debian configuration. Since last time I've been working at some different positions using either Windows or Mac or Linux (usually Ubuntu). I have not really had a problem with any of these but somehow I always feel drawn back to the minimalism and the "beauty" of a downscaled system, which still has the power to do everything I want it to do. I've also started to see how XDG (the base directory specification) can help to make things even more ordered and minimalistic. My previous project can be found here: https://dev.to/sebbestune/a-minimal-and-distraction-free-debian-configuration-386b. This new project will remain its main focus to be minimal, decluttered and functional for modern programming, and add the focus to use XDG and perhaps order my config in such a way that I can finally start reusing it properly.

### What the system should include:

1. Distraction free environment
    - GUI only when necessary (i3 with startx)
    - XDG to clear my home directory
2. Minimal and snappy environment
    - Only have programs I use
    - XDG to clear my home directory
    - Using minimal linux system
3. Easily maintained system
    - This DebConf project
    - Optionally divide config into other git submodules
4. Ability to do everyday tasks
    - Browse internet
    - Screen recording (using OBS)
    - Vim (with decent config)
    - Optinally LibreOffice
    - Some gaming (Wine+Lutris)
5. Ability to do modern development
    - Node, NPM, PNPM
    - Browser: Google-Chrome
    - IDE: Visual Studio Code (when not using VIM)
    - Web with... Frontend (Mostly React), Backend (Mostly Node and Express)
    - Mobile with... Mostly React-Native
    - Possibly other: C/C++, RUST, GOlang
6. Ability to work as teacher 
    - Zoom for holding lectures online
    - Making slides (using latex/overleaf.com)

### Reminder
This is not a new system, it is simply a configuration of Linux (Debian) as per how I want to use it. Feel free to use this configuration if you wish! But bare in mind that some of the packages I use may not be something you want, if you want to configure the system even more, simply look through the "installer"-script and do it manually instead, in this way you can tailor it even more.

## Prerequisites
To use this system you'd need some skills in:
- terminal use in Linux,
- git,
- how to set up a virtual machine or install debian on your own computer.

## Installation process
I started with installing a minimal Debian 11 with no GUI and only system tools (https://www.debian.org/CD/http-ftp/#stable). Personally I started by intalling it on a virtual machine, if you also want to do this I can recommend virtualbox. 

### Installing Debian
To install the OS will probably be very pain free. Just go through the installation process. Make sure that you in the Software Selection part only pick the **standard system utilities** everything else we will download and any desktop environment will ruin the minimal installation. Also make sure to remember the password you set for root (super user).

### Configuring the system
I've made an automatic config to try to make the installation process as easy as possible. If it breaks it will probably be because Android changed it's version and that download doesn't work any more. I will tell what you can do if that would happen in the end of this part.  

When you first get in your system do the following:
```
su 
apt-get install git sudo

#add yourself to sudoers
sudo usermod -a -G sudo <username>

#setup your git 
git config --global user.name "<your name>"
git config --global user.email <your email>
git clone https://github.com/Sebbestune/DebConf.git
cd DebConf
```
Then 

1. Replace your .profile with the .profile in the DebConf (or otherwise add XDG directories) 
2. Add the folders (in home): 
```
mkdir $HOME/.local/bin
mkdir $HOME/.config
mkdir $HOME/.local/share
mkdir $HOME/.cache
mkdir $HOME/.runtimes
```
3. run the installer:

```
./installer
```

##
To start i3 run: startx
To change screen resolution run: 
1. xrandr, to see available resolutions
2. E.g. xrandr -s 1920x1200, to change to that resolution.

## That's it!
Hopefully you're now all up and running! To give some pointers of where to go next I invite you to check out this video about how to use i3wm (https://youtu.be/j1I63wGcvU4?t=183). Basically you set your MOD-key and then the most important thing to know is that you can create new terminals with MOD-Enter and move between the terminals either with MOD-<direction key> or by focusing with the mouse. You can also put the windows in their own area by MOD-Shift-<number> and then jump between different areas by MOD-<number>. You can exit windows in i3wm by MOD-Shift-q. To shutdown or reboot the entire system when back in terminal mode use "sudo reboot" or "sudo shutdown -h now". To run any of the tools simply write the name of the tool, e.g. writing *lutris* will start lutris and *obs* will start obs. I also included a cool music player called cmus (http://www.tuxarena.com/static/cmus_guide.php). 
  
Happy Exploring!
> Sebastian Lindgren
