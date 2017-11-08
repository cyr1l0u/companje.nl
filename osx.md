---
title: Mac OSX
---

=====my updated .bash_profile=====
```bash
export PATH=~/bin:$PATH
alias d="ls -lGa"
alias ls="ls -G"
alias untar="tar xvzf "
alias lsr="ls -ltr"  #recent files ordered ascending

export CLICOLOR=1
export LSCOLORS=ExFxCxDxBxegedabagacad

. /usr/local/etc/profile.d/z.sh
  
git_branch () { git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/\1/'; }
LOCATION='[01;34m\]`pwd | sed "s#\(/[^/]\{1,\}/[^/]\{1,\}/[^/]\{1,\}/\).*\(/[^/]\{1,\}/[^/]\{1,\}\)/\{0,1\}#\1...\2#g"`'
BRANCH=' [00;33m\]$(git_branch)\[[00m\]
\$ '
PS1=$LOCATION$BRANCH
PS2='\[[01;36m\]>'
```

=====z as alternative for cd=====
```bash
brew install z
# add this to ~/.bash_profile: . /usr/local/etc/profile.d/z.sh
```
https://github.com/rupa/z


=====Make automatic screenshots=====

```xml
<!--
~/Library/LaunchAgents/RicksAutoScreenshots.plist
-->
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.example.ricksscreenshots</string>
    <key>ProgramArguments</key>
    <array>
        <string>/Users/rick/screenshot.sh</string>
    </array>
    <key>StartInterval</key>
    <integer>10</integer>
</dict>
</plist>
```


```bash
vardate=$(date +%Y\-%m\-%d); 
vartime=$(date +%H.%M.%S);
folder=~/screenshots/$vardate
mkdir -p $folder
screencapture -t png -x $folder/$vartime.png;
```

=====Launchd=====
* https://developer.apple.com/library/content/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/CreatingLaunchdJobs.html#//apple_ref/doc/uid/10000172i-SW7-BCIEDDBJ

=====Use Automator for making Symbolic Links=====
1 Create an Application
2 add task `Run Shell Script` with 'pass input as arguments'
```
ln -s "$1" /Users/rick/Documents/Websites/
```
(::screen_shot_2017-04-13_at_16.55.11.png?450|)

=====iTerm2 keyboard shortcuts and tips======
https://www.iterm2.com/documentation-one-page.html

=====convert multiple PNG's to JPG=====
You can do it with the Preview App as described here: http://osxdaily.com/2013/01/16/batch-image-conversion-mac-os-x-preview/

=====Kill Google Photo Uploader=====
(or anything containing the word 'Photos')
  kill -9 $(pgrep Photos)

=====SiteSucker=====
recursive download van een website. http://www.sitesucker.us

=====mv command=====
by default it seems to replace a file.
  mv -n src dst  # Do not overwrite an existing file.
[[https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/mv.1.html|man]]

=====to enter unicode character on osx=====
  # System preferences-> input menu
  # check the box next to "Unicode hex".
  # add Unicode hex as a language
  # Switch to unicode input in the menu bar.
  # Hold Alt followed by a 4 digit hexadecimal unicode value to get the character.
  
=====chmod in Sites folder=====
  chmod -R 755 folder_with_wrong_permissions
  
=====.bash_profile=====
<code bash>
export PATH=/opt/local/bin:/opt/local/sbin:~/bin:$PATH

export ANDROID_HOME=~/Documents/android-sdk-macosx
export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools:$ANDROID_HOME/build-tools/20.0.0

export LUA_CPATH=/opt/local/share/luarocks/lib/lua/5.2/?.so
export LUA_PATH=/opt/local/share/luarocks/share/lua/5.2/?.lua

alias d="ls -lGa"
alias ls="ls -G"
alias um="cd ~/Sites/Ultimaker"
alias untar="tar xvzf "

if [ -f /opt/local/etc/profile.d/bash_completion.sh ]; then
   . /opt/local/etc/profile.d/bash_completion.sh
fi
</code>

=====list open ports=====
  lsof -i -P | grep -i "listen"

=====my .bash_profile=====
<code>
export PATH=/opt/local/bin:/opt/local/sbin:~/bin:$PATH
alias d="ls -lGa"
alias ls="ls -G"
alias um="cd ~/Sites/Ultimaker"
alias untar="tar xvzf "
</code>

=====SDL on OSX=====
* http://www.libsdl.org/download-1.2.php

=====own /usr/local=====
  chown -R rick /usr/local

=====convert DDS file to JPG on Mac OSX=====
*http://www.xnview.com/en/

=====busybox (shell & httpd)=====
http://wiki.openwrt.org/doc/howto/http.httpd

=====dumb AP=====
http://wiki.openwrt.org/doc/recipes/dumbap

=====diskutil on command line=====
<code>
diskutil list</code>
=====file info=====
<code>
file
otool
gobjdump
...
</code>

=====Folder/File sync tools=====
*DeltaWalker
*Singlemizer (not tested yet)

=====keyboard repeat rate / speed=====
<code>
defaults write NSGlobalDomain KeyRepeat -int 0
</code>
try 0, 1 or 2: the lower the faster

=====unpack a .pkg file=====
*https://www.macupdate.com/app/mac/16357/unpkg

=====batch resize images=====
<code bash>
sips -Z 640 *.jpg
</code>

=====serial communication with screen=====
<code>screen /dev/[device name] 115200</code>
To quit screen, press CTRL-a, followed by CTRL-k, followed by y.

=====follow system log=====
<code>tail -f /private/var/log/system.log</code>

=====macports / python=====
To make python 2.7 the default (i.e. the version you get when you run 'python'), please run:
<code>
sudo port select --set python python27
</code>

=====mount ssh folders=====
* http://osxfuse.github.io/

=====PVR QuickLook plugin=====
* http://www.limbic.com/quickpvr.html

=====delete 'bands' files in Time Capsule .sparsebundle folder=====
Removing your Time Capsule .sparsebundle can take multiple days (or weeks) if you use Finder or Terminal.
The fastest way is by connecting to the TimeCapsule through Windows running in Parallels/VMWare etc and delete it using Windows Explorer (\ipadress of time capsule). It took 'only' 80 minutes to remove 1.5TB (1.8 million files of 8MB)

=====thumbsup=====
een handige tool om snel afbeeldingen te bewerken

=====alternative to spotlight=====
* [[http://www.alfredapp.com/|Alfred]]
=====get ip address=====
<code>
ipconfig getifaddr en1
</code>
or
<code>
ifconfig en1 | grep "inet " | cut -d " " -f2
</code>

=====convert png to ico=====
<code>
convert file.png file.ico
</code>

=====osx keyboard shortcuts=====
* http://support.apple.com/kb/HT1343

=====cls=====
<code>
clear
</code>

=====show contents of clipboard=====
<code>
pbpaste
pbpaste | head -n 5
</code>

=====copy text to clipboard=====
<code>
ls | pbcopy
</code>

=====Convert tabs to spaces for the lines in the Clipboard=====
<code>
pbpaste | expand | pbcopy
</code>

=====sorting etc=====
ls | sort
ls | rev
ls | uniq
ls | uniq -d
ls | uniq -u

=====eject cd=====
<code>
diskutil eject disk1
</code>
or
<code>
drutil tray eject
</code>

=====dig=====
<code>
dig companje.nl A
</code>

=====disable dashboard=====
<code>
defaults write com.apple.dashboard mcx-disabled -boolean YES
killall Dock
</code>

=====get name of current wifi network=====
<code>
/System/Library/PrivateFrameworks/Apple80211.framework/Versions/A/Resources/airport -I|grep " SSID: "|cut -c 18-
</code>
or
<code>
networksetup -getairportnetwork en1
networksetup -getairportnetwork en1 | cut -c 24-
</code>

=====airdrop info=====
* [[http://www.yourdailymac.net/2011/09/how-to-enable-os-x-lion-airdrop-on-every-mac/|enable OS X Lion AirDrop on every Mac]]

=====restart Finder=====
<code>
killall Finder
</code>

=====list all network hardware ports=====
<code>
networksetup -listallhardwareports
</code>

=====get info about current wifi point=====
<code>
/System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport --getinfo
</code>

=====scan for wifi points=====
<code>
/System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport -s
</code>

=====symbolic links=====
<code bash>
ln -s fullpath-source-www /Users/rick/Sites/8
</code>

=====show display settings=====
''alt+F2''

=====QuickLook / Quick Preview / Syntax Highlighting / Color Code=====
Download [[http://qlcolorcode.googlecode.com/files/QLColorCode-2.0.2.tgz|QLColorCode]]. Create folder ''~/Library/QuickLook'' and copy QLColorCode.qlgenerator to that folder.

=====SetFile=====
<code>
SetFile
</code>

=====dmg create command line=====
<code>
hdiutil create ....
</code>
* http://stackoverflow.com/questions/96882/how-do-i-create-a-nice-looking-dmg-for-mac-os-x-using-command-line-tools

=====usb device info=====
<code>
system_profiler SPUSBDataType
</code>

=====network utilities=====
* From the Applications folder, open the Utilities folder, and then open the Network Utility application. 
* In the Network Utility window, click the Ping tab. 

=====broadcast ping=====
<code>
ping -i 5 -c 2 192.168.1.255
</code>

=====using arp to find mac address=====
<code>
ping IPADDRESS
arp -a
</code>

=====fping range=====
<code>
sudo fping -s -g 192.168.0.1 192.168.0.9 -r 1
fping -ag 192.168.1.0/24
</code>

=====websharing is removed from Mountain Lion Preferences but still usable=====
<code>
sudo apachectl start
</code>

=====Repeatable crash of Time Capsule wifi=====
* http://forums.macrumors.com/showthread.php?t=1324678

=====Mac OSX Driver for Sweex Graphics Tablet USB TA006=====
* The UC-Logic driver for Mac OSX works for me: http://www.uc-logic.com/

=====serial terminal app=====
CoolTerm - http://www.macupdate.com/app/mac/31352/coolterm/

=====stop cups=====
<code bash>
sudo launchctl stop org.cups.cupsd
</code>

=====40 lion tips=====
* http://mac.appstorm.net/roundups/utilities-roundups/40-super-secret-os-x-lion-features-and-shortcuts/

=====write disk image to sd card=====
* [[http://www.thelinuxdaily.com/2010/01/writing-images-to-disk-on-mac-osx-with-dd/|read article on the linuxdaily]]
<code bash>
diskutil list
diskutil unmountDisk /dev/disk3
dd if=debian6-19-04-2012.img of=/dev/disk3 bs=1m
</code>
(...additional "bs" parameter to "1m"? This parameter is used to set both the input and output block size for the copy)

=====jhbuild bootstrap --ignore-system=====
geen idee wat het doet maar het doet iets.

=====network dump=====
only loopback traffic: ''tcpdump -i lo0 -vv''  
\
en0 ethernet, en1 wifi

=====tftp=====
- er is standaard een tftp client geinstalleerd
- een prima tftp server is [[http://ww2.unime.it/flr/tftpserver/|TftpServer]]

=====Some dynamic linker tools that will come in handy=====
<code>
otool -L
install_name_tool
libtool
</code>
[[http://qin.laya.com/tech_coding_help/dylib_linking.html]]
otool is an alternative for linux' 'ldd'

=====List files in library=====
<code bash>
ar -t libctest.a
</code>

=====Tijdelijk een header search path toevoegen via CFLAGS=====
<del><code>
export CFLAGS="-i /usr/local/include/libusb-1.0"
</code></del>

=====disable OSX Lion remember open documents=====
see [[http://www.macworld.com/article/1161330/four_lion_terminal_hacks.html|this]] or [[http://reviews.cnet.com/8301-13727_7-20083707-263/managing-mac-os-x-lions-application-resume-feature/|this]]

for Preview, Quicktime and XCode:
<code bash>
defaults write com.apple.Preview NSQuitAlwaysKeepsWindows -bool false
defaults write com.apple.QuickTimePlayerX NSQuitAlwaysKeepsWindows -bool false
defaults write com.apple.dt.Xcode NSQuitAlwaysKeepsWindows -bool false
</code>

=====/etc/paths=====
this file contains the search paths

=====goto home dir=====
instead of ''cd ~'' you can just type ''cd''

=====move mouse with code=====
<code cpp>
CGPoint pt;
pt.x = x;
pt.y = y;
CGEventRef mouseDownEv = CGEventCreateMouseEvent (NULL,kCGEventMouseMoved,pt,kCGMouseButtonLeft);
CGEventPost(kCGHIDEventTap, mouseDownEv);
CFRelease(mouseDownEv);
</code>
=====spoof your MAC address=====
<code>sudo ifconfig en1 ether aa:bb:cc:dd:ee:ff</code>
to check the result type: 
<code>ifconfig en1 | grep ether</code>
for Lion you might need to change ether into Wi-Fi.
When you reboot your computer the original address is restored.

=====escape character in tenet on osx=====
<code>
Escape character is '^]'
</code>
which means Ctrl+]

=====hosts file=====
<code bash>
sudo nano -w /etc/hosts
sudo dscacheutil -cachedump -entries Host
dscacheutil -flushcache
</code>

=====stty=====
http://stackoverflow.com/questions/3918032/bash-serial-i-o-and-arduino
can you run stty -a < /dev/tty.usbserial-A800eIUj while you have the serial port working on the Arduino IDE? That would give you the settings to use.
<code bash>
stty -f /dev/tty.PL2303-00001004 19200
</code>

=====otool=====
otool -L libopenFrameworks.dylib
install_name_tool

=====automatisch opstarten=====
nog uitzoeken: launchd en lingon

=====launch application by keyboard shortcut=====
[[http://hints.macworld.com/article.php?story=20090903085255430|link]]

=====swap alt+windows key on external keyboard=====
* [[http://www.gearhack.com/Forums/DisplayComments.php?file=Computer/Mac%20OS/Swapping_the_Windows_Key_and_the_Alt_Key_on_Mac_OS_X|link]]
* http://www.bohemianalps.com/blog/2008/x11-control2command/

=====searching in files recursively=====
<code bash>
grep -ir "texttofind" *
</code>

=====using the find command on the command line=====
<code bash>
find . | grep -i ".cpp"
</code>

=====use grep to search output of a program=====
<code bash>
git diff | grep 'piano'
</code>

=====compile a simple glut program written in c on mac=====
<code bash>
g++ -Wall -O3 -g -framework OpenGL -framework GLUT bezmesh.c -o bezmesh
</code>

Don't forget to include OpenGL and GLUT like this:
<code cpp>
#ifdef __APPLE__
#include <OpenGL/OpenGL.h>
#include <GLUT/glut.h>
#else
#include <GL/glut.h>
#endif
</code>

=====Enable colors in the terminal's ls command=====
or type ''ls -G'' or put the following in your ''~/.profile'' file for a permanent solution.
<code bash>export CLICOLOR=1</code>

=====Show hidden files/folders=====
<code bash>defaults write com.apple.finder AppleShowAllFiles TRUE</code>
(and reload Finder)

=====Change screenshots folder (and other settings)=====
* http://www.tekrevue.com/tip/how-to-customize-screenshot-options-in-mac-os-x/
<code bash>
defaults write com.apple.screencapture location /Users/rick/Desktop/screenshots
killall SystemUIServer
</code>

=====SizeUp=====
[[http://www.irradiatedsoftware.com|SizeUp]] allows you to quickly position a window to fill exactly half the screen (splitscreen), a quarter of the screen (quadrant), full screen, or centered via the menu bar or configurable system-wide shortcuts (hotkeys).  Similar to "tiled windows" functionality available on other operating systems.

=====Visor=====
Install [[http://visor.binaryage.com/|Visor]] to have a system-wide terminal on a hot-key.

=====Rotate an image=====
<code bash>sips input.jpg -r 90 --out output.jpg</code>

=====convert an image=====
<code bash>
sips -s format jpeg 4.gif --out 4.jpg
</code>

=====chmod recursive write access=====
<code bash>chmod -R 777 data</code>

=====~/.profile=====
on osx 10.9 I had to rename .profile to . bash_profile
<code bash>
alias dir="ls -lGa"
</code>

<code bash>
alias tocaf="afconvert -f caff -d LEI16"
</code>

<code bash>
alias cdd="cd ~/Desktop"
</code>

=====ffmpeg for converting movie to iPad=====
see [[:ffmpeg]]  
\

=====combine pdf's on mac osx (with pdftk) =====
<code bash>
sudo port install pdftk
pdftk 1.pdf 2.pdf 3.pdf cat output 123.pdf
</code>

=====homebrew (brew) =====
An alternative for macports

=====Wireshark=====
Wireshark is a tool to analyze network traffic

=====hexdump=====
installed by default.
<code bash>
hexdump filename
</code>

=====sneltoetsen in nano console editor=====
zie [[nano]]

=====gmail berichten sturen via command line in osx=====
See this page: [[http://www.amirwatad.com/blog/archives/2009/03/21/send-email-from-the-command-line-using-gmail-account/|link]]
I managed to send an email but it's not working completely yet.

=====terminal / iTerm2=====
* Cmd+[ ] move between panels
* Cmd+D new panel
* Cmd+W close panel
* ^A naar begin regel

=====Pleasant3D.app=====
Handige app om GCODES mee te bekijken in 3D

=====Synergy2=====
<code bash>
synergys --config synergy.conf
</code>
synergy.conf:
<code bash>
section: screens
        rick.local:
        User-PC:
end
section: links
rick.local:
        right = User-PC
User-PC:
        left = rick.local
end
</code>