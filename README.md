# DebConf
Recently I got the feeling that I was too often distracted in when using my current system. It felt like I was more prone to happen to watch a clip on youtube or game than happen to start working on some project or code that I have been waiting to do for a while. I started to reason that in fact when coming into my system I am immediately greeted by a lot of graphics and things to do, I have nice little icons everywhere and usually starting up youtube or a game is one or two clicks away. To start working on a project on the other hand usually demands a bit more action from my part. Starting some different programs or finding my way through some folders. Sure shortcuts can be placed on the desktop, but no matter how often I clean it I seem to get so many ideas and want to pick up so many trails when browsing online that my desktop seem to always be full. The icons that draws you attention is usually not the ones looking like a folder but the bright ones that lead towards the joy of procrastination.

I came up with an idea that I'd change this and to try to create a system where I can focus. Where the amount of clicks needed to get to e.g. youtube or a game is at least as long or longer than continuing on a project. I wanted something distraction free and suited for projects and production while still being able to game or browse online when I later really wanted to.

To give the full picture I had simultaneously read a book about the Unix system from back to back and was already fascinated by it. It was not my first time introduced to the world of Unix since I'd previously owned both a Mac and used a computer with Ubuntu, but I had mostly used the GUI features and felt that after the book I was finally ready to face the system through the CLI. I had also been more and more aware that my Windows system had several limitations. Some DevOps tool were not working properly which would've worked in Linux, I felt that I didn't need much of the clutter and I used Vim mostly for writing anyways, and I started to wonder why so much resources where being hogged from my system. (As a small taste of what's to come, my Windows system usually had over 200 processes at all times, my Linux system has under 10 in most scenarios making it run fast even in a severelly limited virtual box). 

## The idea
I wanted the configuration to do some things (the numbers of this list will be referensed later):

1. Provide me a distraction free environment
2. I should be able to do modern development (in my case: Android, Web (+Vue), Bash-script, C/C++)
3. I should be able to do screen recording
4. I should be able to do administrative tasks
5. I should be able to browse the internet
6. I should be able to play games (old games is a plus)
7. The system should be minimal and feel snappy
8. The system should be easily maintained

### Reminder
This is not a new system, it is simply a configuration of Linux (Debian) as I want to use it. Feel free to use this configuration if you wish! But bare in mind that some of the packages I use may not be something you want and by following my process instead of just copying the files you might get an even more minimal or at least more personally configured system.

## Practice
I started with installing a netinstall of Debian with no GUI. I chose: https://www.debian.org/distrib/netinst or to be completely precise this: https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-10.1.0-amd64-netinst.iso . I installed it on a virtual machine for now to be able to see what I felt about it (now I'm starting to seriously consider to try it as my main OS, but more to that later). 

### Getting (1) a distraction free environment which is also (7) minimal and snappy
The bare Debian system without GUI practically gives me 1 and 7 automatically. Since I wanted to be able to also do point 2-6 in an easy way I decided to install the Window Manager i3wm. It's an easy process through an apt download. It's then easily started by executing the file 
```
./xinit-i3
```
or running the code within this file. You could also put this script into your .profile or .bashrc to make it happen automatically at each system start. Interesting to note here that i3wm will only take a few megabytes of space and hardly any computer resources.

### Getting (8) easy maintainability
I want to give this information as early as possible since this is how to basically clone the Debian Configuration quite automatically. The file "installed_packages" include all the apt-packages I've installed in my configuration (for full disclosure I'll personally use the "installed_packages_wjdk", this simply includes java-8 which is not possible to do directly, for more info check out the Android part of this document). At this point you can either just use my file, remove some packages (lines) and then use it or do all apt-get's from scratch. If you'd like to save your own configuration just use: 
```
./dpkgscript
```
and all the packages currently installed via apt-get will be saved into a file called installed_packages.

To put all the packages in the installed_packages file into the system run (as su): 
```
dpkg --add-architecture i386
apt update
apt-get install software-properties-common
apt update

apt-get install $(cat installed_packages)

wget https://download.opensuse.org/repositories/home:/strycore/Debian_9.0/Release.key
apt-key add Release.key

echo 'deb http://download.opensuse.org/repositories/home:/strycore/Debian_9.0/ ./' > /etc/apt/sources.list.d/lutris.list
apt update
apt install lutris
```
Of course if you don't want to use Lutris (which will enable you to play games) you can omit the lines starting with wget. 

### Getting (2) a modern development setup
The tools needed for most development I am doing is enabled by just installing Linux and the packages in "installed_packages". These tools I am using are right now mostly limited to those used in traditional development (such as C/C++) and some web and app development.

#### Android
App development was the hardest to set up as this was less transparent to do automatically. I found that downloading the sdkmanager for linux and installing java8 alongside java11 was the easiest way to set up Android development in a minimal setting. This gives us most of the tools needed without almost any overhead. 

To do this you must first enable downloading java8 from apt by adding the following to your *sources.list* file in */etc/apt/*:
```
deb "http://ftp.debian.org/debian" stretch main
deb-src "http://ftp.de.debian.org/debian" stretch main
```
Then run (as su):
```
apt-get update
apt-get install openjdk-8-jdk openjdk-8-jre
update-alternatives --config java
```
In the alternatives given by *update-alternatives* choose java-8-openjdk while you want to do Android Development. 

Then download go to https://developer.android.com/studio and download the linux package from under "Command line tools only". Extract and then I propose moving it to */opt/android-tools/*. Also add the tools to your path by:
```
export PATH=/opt/android-tools/:/opt/android-tools/bin:$PATH
```

#### Web Development
Since I also want to do modern web development I downloaded some packages via npm e.g.:
```
npm install --global vue-native-cli
npm install -g sass
npm install --global react-native-cli
```
Other or more development packages can of course be downloaded for people with other needs.

### Doing (4) administrative tasks, (5) browse the net, (6) play games and record the screen (3)
While reading my development setup you might've reflected about the IDE and that you didn't see any. That's because I'm mostly using Vim and the terminal for my development needs. I have been working on my vimrc for a while and if you want you can try it or give some suggestions. Keep in mind that I'm trying to keep away from plugins if possible (to keep the system (7) minimal and snappy), but other changes are appreciated. If you're not a Vim person there's also emacs and nano already in the system (although I'd recommend Vim, especially in this i3wm configuration where more terminals are just two buttons away). 

Other administrative tasks can easily be done too. Since I want a minimal system and don't mind doing some things online I have so far created spreadsheets and power point presentations by using the programs in icloud.com through firefox (google drive or windows equivalent could just as well been used too). You could of course simply download the Libre Office Suite if you wish.

For browsing the net I was able to download firefox-esr (which I kind of spoiled previously). This is done automatically in the maintainability part. For playing games I use Lutris and to record the screen I use OBS. Both also downloaded through apt using the steps under maintainability. I tested OBS and it worked flawlessly with sound and picture without any problem and while using i3wm windows. With Lutris I tried installing Empire Earth (through GOG) and Monkey Island (through Windows Steam). They both worked well which was a nice surprise since Empire Earth have a hard time working on Modern Windows. (Also just to notice: To be able to play any steam games after reboot I had to download steam outside of installing the app).

## That's it!
Hopefully this will all work for you without hickups, no matter if you do your own build or borrow some of my files. In the future I've planned to also create an installation script that will setup everything from scratch on a newly installed Debian netinst with no GUI. When this is done the readme will of course be updated accordingly with an added section of how to run the minimal effort installation.

> Sebastian Lindgren
