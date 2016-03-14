# save-mp3Streaming
A simple Python script to save streaming MP3 data.

Latest News
===========

Experimental -f to enable framing out the ID3 v2 tags at 
the beginning of files (don't use this if your mp3 player
can handle ID3 v2 tags).  


Introduction
============

This is a simple Python script to save streaming mp3's so you can 
use them on your portable mp3 player.  This script should actually 
work with any streaming mp3 (see below re: Infinite Streams).




Setup with Netscape in GNU/Linux 
================================

Select Edit->Preferences->Navigator->Applications
Select New (Edit if you already have a handler for m3u playlists)
Enter Description: m3u Playlists
Enter MIMEType: audio/x-mpegurl
Enter Suffixes: m3u
Enter Application: xterm -e save-mp3Streaming.py %s
Select OK->OK

Do the same for suffix pls with mime type audio/x-scpls

Setup with Explorer in Windows
==============================
First download and install python for windows from www.python.org.
Save the save-mp3Streaming.py file to d:\music.  If you are using winamp 
or sonique right now, start the program and under preferences or 
options de-select the m3u file association.

Double click on "My Computer" on the desktop.
View->Folder Options->File Types.
Scroll thru the window and find the application that is handling
the suffixes "m3u", "pls" or both.  Remove it.
Select New Type.
Enter Description: m3u Playlists
Enter Extension: m3u
Enter MIMEType: audio/x-mpegurl
Select OK.
Under Actions click New 
Enter Action: open
Enter Application ...: 
  "C:\Program Files\Python\python.exe" C:\music\save-mp3Streaming.py -v -d c:\music "%1"
Ok

Do the same for pls with mime type audio/x-scpls



Setup with Netscape in Windows
==============================
First download and install python for windows from www.python.org.
Save the save-mp3Streaming.py file to d:\music.  If you are using winamp 
or sonique right now, start the program and under preferences or 
options de-select the m3u file association.

Select Edit->Preferences->Navigator->Applications
Scroll thru the window and find the application that is handling
the mime type: audio/x-mpegurl (probably winamp).  Remove it.
Select New.
Enter Description: m3u Playlists
Enter MIMEType: audio/x-mpegurl
Enter Suffixes: m3u
Enter Application: 
  "C:\Program Files\Python\python.exe" C:\music\save-mp3Streaming.py -v -d c:\music "%1"
Select OK->OK

Do the same for pls with mime type audio/x-scpls


Infinite Streams
================
If you want to make an mp3 for an infinite stream m3u url,
start save-mp3Streaming with the option -v:
xterm -e save-mp3Streaming.py -v %s

Verbose mode will tell you how much data has been read on a 
particular stream.  Hitting ctrl-c in the xterm will cause 
save-mp3Streaming to stop downloading and save the stream to a file.
The default name is "unfinished-stream.mp3" which can be changed
with the -u option.

If you find the stream is dropping out and losing link unexpectedly,
try the -p option.

Many internet radio sites use the .pls file format but the servers
do not treat the mime type correctly :( You can save these streams 
in the following manner:
1) save the .pls file locally
2) from a linux prompt execute: ./save-mp3Streaming.py -v pls_filename

Or you can set both the two mime types:
    audio/x-scpls
    application/octet-stream
with suffix pls to "xterm -e save-mp3Streaming.py -v %s"

Finally, if you want to setup cron jobs, you can stop and save
a save-mp3Streaming transfer by doing a kill -INT to the job.


Options
=======

save-mp3Streaming v1.0 linux

Usage: save-mp3Streaming.py [options] m3u_file

       -c       clobber files instead of appending -# 
       -d dir   top directory to create files/subdirs in 
       -i       use ICY title data from a shoutcast stream 
                (this option is much improved) 
       -l       log output to save-mp3Streaming.log file 
       -m       create a local .m3u playlist (in top dir) 
       -n 1     name as "artist - title.mp3" (default) 
       -n 2     name as "title.mp3" 
       -n 3     name as "title.mp3" in subdir "artist" 
       -n 4     name as "artist - title.mp3" in subdir "artist" 
       -n #u    same as -n 1 to 4 except sub underscores for spaces 
       -p       persistent re-open pls until keyboard interrupt
       -t msec  trim msec milliseconds off the end of ICY files 
       -u file  name for unfinished streams (unfinished-stream.mp3)
       -v       verbose mode 
       -z size  download size limit in megabytes

Set your netscape application for m3u suffixes to something like:
xterm -e save-mp3Streaming.py -v -n 3 %s


Motivation
==========

I apologize in advance to mp3.com for any troubles this software
may cause them.  My motivation for making this available is to
make streaming mp3 usable on portable mp3 players and for people
with transfer limits.  

In the long run, this program will also reduce internet traffic.
In fact, I suggest you consider some sort of "local cache" feature
for my.mp3.com where the user can enter the location of an album
on their local drive.  Then a my.mp3.com playlist can have both
local and remote entries.
