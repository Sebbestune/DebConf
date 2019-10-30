# DebConf
## My (Minimal) Debian Configuration
Coming from an extensively cluttered Windows environment, no coherent way to do things and a feeling of distraction instead of productivity, I decided to create a minimal and distraction free environment of my own. I read the book *Exploring the UNIX system* by *Stephen G. Kochan and Patrick H. Wood*, and even though it was mostly for enjoyment I felt like the way they used their system felt relieving somehow. I decided to make a system which would mimic this 80's computer system, but still being able to do everything a modern system can do and modern development require. 

I wanted a configuration that could do several things:

1. Provide me a distraction free environment
    - I got this from ridding myself of enforced GUI and only using it when necessary.
2. I should be able to do modern development (in my case): 
    - Mobile (Android/Vue Native), 
    - Web (+Vue), 
    - Bash-scripts, 
    - C/C++,
    - (and for the future testing out some technologies of course)
3. I should be able to do screen recording
    - Using OBS
4. I should be able to do administrative tasks
    - Using VIM (LibreOffice can be downloaded by you if you wish)
5. I should be able to browse the internet
    - I use Firefox
6. I should be able to play games (old games is a plus)
    - Gaming with Wine+Lutris<3
7. The system should be minimal and feel snappy
    - Mostly a given due to the Linux system without GUI
8. The system should be easily maintained
    - Which is why I developed this DebConf project

### Reminder
This is not a new system, it is simply a configuration of Linux (Debian) as per how I want to use it. Feel free to use this configuration if you wish! But bare in mind that some of the packages I use may not be something you want, if you want to configure the system even more, simply look through the process and do it manually instead, in this way you can tailor it even more. If you're just curious I invite you to test the automatic install and the full system.

## Prerequisites
To use this system you'd need to know a bit about CLI (command line interface) and how to use Linux. But I've tried to include many of the things you need to get up and running. You also need to know a bit about using git in the terminal. If you want to install on a real machine then I trust you know what you're doing and in a virtual machine that you can set that up by yourself too.

## Installation process
I started with installing a netinstall of Debian with no GUI. I chose: https://www.debian.org/distrib/netinst or to be completely precise this: https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-10.1.0-amd64-netinst.iso . Personally I started by intalling it on a virtual machine, for this I can recommend virtualbox. 

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
After these steps are done (make sure you're still in super user mode) and run the file auto_config:
```
./auto_config
```

Press *y* (no need to hit enter), and then let the configuration happen. In my experience this should take just over 15 minutes over a 1MB/s internet connection (which is what I'm sitting on at the moment). 

If everything goes well the system will install, you will have to press the yes-button (different depending on languages but mostly 'y', but in my case 'j').

If there is a hickup this will most possible be due to Android SDK changing version. You'll then have to download it manugally and then do that part of the code manually (or extract that part from the auto installer to its own script):
```
#DO THIS PART ONLY IF TYPING sdkmanager DOESN'T WORK
#Start GUI (learn foundational navigation here: https://youtu.be/j1I63wGcvU4?t=183 )
./xinit-i3

#Start firefox and download Command line tools from: https://developer.android.com/studio
#It should be called something like sdk-tools-linux-*.zip (example: sdk-tools-linux-4333796.zip)
#https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip

#After (do as superuser)
cd 
cd Downloads/
unzip sdk-tools
rm sdk-tools-linux-*.zip
sudo mv tools /opt/android-tools
cd 
printf "\nexport PATH=/opt/android-tools/:/opt/android-tools/bin:$PATH\n" | tee -a .profile
touch .android/repositories.cfg
sdkmanager --no_https --list
```

## That's it!
Hopefully you're now all up and running! To give some pointers of where to go next I invite you to check out this video about how to use i3wm (https://youtu.be/j1I63wGcvU4?t=183). Basically you set your MOD-key and then the most important thing to know is that you can create new terminals with MOD-Enter and move between the terminals either with MOD-<direction key> or by focusing with the mouse. You can also put the windows in their own area by MOD-Shift-<number> and then jump between different areas by MOD-<number>. You can exit windows in i3wm by MOD-Shift-q. To shutdown or reboot the entire system when back in terminal mode use "sudo reboot" or "sudo shutdown -h now". To run any of the tools simply write the name of the tool, e.g. writing *lutris* will start lutris and *obs* will start obs. I also included a cool music player called cmus (http://www.tuxarena.com/static/cmus_guide.php). 
  
Happy Exploring!
> Sebastian Lindgren
