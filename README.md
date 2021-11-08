# pi-video-photo-slideshow

There are plenty of digital picture frame projects using the raspberry pi but very few support both photos and videos. When they do, they typically use OMXplayer or a custom script. OMXplayer doesn't work for my use case because it doesn't support newer video formats (i.e. recorded using my iphone).  In addition, [OMXplayer has been deprecated in favor of VLC](https://github.com/popcornmix/omxplayer/). Thus, I did some research and put together one using VLC.

You can run VLC from the command line and use the framebuffer instead of X11 to display videos and pictures.

1. Install Raspberry Pi OS Lite
2. apt-get install vlc-bin and vlc-plugin-base
3. create a directory containing your media
4. Create a playlist [default.xspf](default.xspf) that lists your media folder as the only directory
5. Add a line in crontab running VLC.  FYI You cannot run VLC as root.
       
          @reboot cvlc --random --play-and-exit /home/pi/default.xspf
          #--image-duration - change how long each photo displays without having to go into the graphical interface to change settings
          #@reboot cvlc --fbdev /dev/fb0 --image-duration=30 --no-osd --no-repeat -fLZ /home/pi/default.xspf vlc://quit
          #@reboot sleep 15 && clear && cvlc --image-duration=30 --recursive expand --no-osd --no-repeat -fLZ /home/pi/default.xspf vlc://quit

fancy stuff
* Consider using sync-thing so you can auto-upload new photos into your media directory on the pi
* Consider turning the monitor off and on @ specified intervals
     https://gist.github.com/bobburgers7/31d98bcb43157b8cb73d456b066e7751
     
     place in root's crontab
        
          # Turn HDMI Off (22:00/10:00pm)
          0 22 * * * /home/pi/rpi-hdmi.sh off

          # Turn HDMI On (9:00/9:00am)
          0 9 * * * /home/pi/rpi-hdmi.sh on

- TODO
     how to update the playlist automatically with any new files added via sync-thing?  feh used to be able to refresh the list.  consider just rebooting the pi after it goes through all the files?
     
- [Used to use feh for the digital photo frame](feh-pi-picture-frame) but couldn't do video and had to compile HEIC support for iphone photos.

Similar Projects:
* https://www.instructables.com/Easy-Raspberry-Pi-Based-ScreensaverSlideshow-for-E/
* https://www.binaryemotions.com

References:
* https://www.thedigitalpictureframe.com/easiest-way-build-a-raspberry-pi-picture-frame-streaming-framen-photo-app/
* https://www.splitbrain.org/blog/2018-05/12-diy_digital_picture_frame
* https://www.vlchelp.com/image-slideshow-photo-view/
* https://raspberrypi.stackexchange.com/questions/127252/problem-using-vlc-without-x
* https://raspberrypi.stackexchange.com/questions/44169/run-something-after-login
* http://www.wumpus-cave.net/2013/11/06/running-vlc-automatically-on-a-headless-raspberry-pi/
* https://www.matthewhollander.com/play-video-on-startup-of-raspbian-on-raspberry-pi/
* https://raspberrypi.stackexchange.com/questions/105450/display-a-video-at-boot
* https://raspberrypi.stackexchange.com/questions/59898/how-can-i-blank-the-screen-from-the-command-line-over-ssh
