A few command-line tools that I need from time to time.


dping
-----

ping that also displays the date and time for the requests


hist
-----

history + grep. Just a bit faster.


convert_mkv_to_mpg
------------------

### About
This is my solution to playing mkv files on PS3.

I am using the DS213+ which contains an older version of ffmpeg and PS3 kept claiming that the mp4 files that ffmpeg remuxed where corrupt. Because of that I decided to convert to .mpg instead (while allowing ffmpeg to convert
the audio).

The process is not a quick remux, but all that is converted is audio, so it is quick enough (about 1.5 minutes for 1 hour of movie).

The overal concept and initial script is based on:
http://forum.synology.com/enu/viewtopic.php?f=222&t=81266

The installation steps (i.e. run on download completion) are based on:
http://forum.synology.com/enu/viewtopic.php?f=38&t=75430

The idea for using .mpg rather than .mp4 is based on http://blown-to-bits.blogspot.co.uk/2011/07/synology-dnla-transcoding-alternative.html
and the fix for the missing audio in the mpg is based on http://stackoverflow.com/a/16324025


### Installation

* Copy the script to you NAS e.g. in /volume1/tools

* Login as root
`ssh root@your-nas-ip`

* Make it executable
`chmod +x /volume1/tools/convert_mkv_to_mpg`

* Stop DownloadStation (important to stop before proceeding to the next step)
```
/volume1/@appstore/DownloadStation/scripts/S25download.sh stop
```

* Modify the DownloadStation settings in `/usr/syno/etc/packages/DownloadStation/download/settings.json` by setting:
```
"script-torrent-done-enabled": true,                               
"script-torrent-done-filename": "/volume1/tools/convert_mkv_to_mpg /volume1/video", 
```

* Start the DownloadStation back up again
```
/volume1/@appstore/DownloadStation/scripts/S25download.sh start
```

Once installed this script is executed every time a download is completed. There is nothing that synology passes in, so the script takes any .mkv file and if there is no .mpg version already created then the file is processed.
