# pi-video-photo-slideshow

You can run VLC from the command line and use the framebuffer instead of X11 to display videos and pictures. I wanted to make a slideshow that will go through photos and videos


1. Install Raspberry Pi OS Lite
2. apt-get install vlc-bin and vlc-plugin-base
3. install sync-thing so you can place photos + videos on your main computer and have it auto-load onto the pi
4. setup turning the monitor off and on @ specified intervals
     https://gist.github.com/bobburgers7/31d98bcb43157b8cb73d456b066e7751
     
     place in root's crontab
          
          # Turn HDMI Off (22:00/10:00pm)
          0 22 * * * /home/pi/rpi-hdmi.sh off

          # Turn HDMI On (9:00/9:00am)
          0 9 * * * /home/pi/rpi-hdmi.sh on

6. create a playlist (default.xspf) that is pointed at the folder shared with remote location
7. cannot run VLC as root, so run it as a user in crontab
        
          @reboot cvlc --image-duration=30 --no-osd --no-repeat -fLZ /home/pi/default.xspf vlc://quit
          
          #--image-duration - change how long each photo displays without having to go into the graphical interface to change settings

- TODO
     how to update the playlist automatically with any new files added via sync-thing?  feh used to be able to refresh the list.  consider just rebooting the pi after it goes through all the files?
     
- Used to use feh but had to compile HEIC support for iphone photos and didn't have video support so swapped to VLC
https://www.splitbrain.org/blog/2018-05/12-diy_digital_picture_frame

Similar Projects:
https://www.instructables.com/Easy-Raspberry-Pi-Based-ScreensaverSlideshow-for-E/
https://www.binaryemotions.com


References:
* https://www.vlchelp.com/image-slideshow-photo-view/
* https://raspberrypi.stackexchange.com/questions/127252/problem-using-vlc-without-x
* https://raspberrypi.stackexchange.com/questions/44169/run-something-after-login
* http://www.wumpus-cave.net/2013/11/06/running-vlc-automatically-on-a-headless-raspberry-pi/
* https://www.matthewhollander.com/play-video-on-startup-of-raspbian-on-raspberry-pi/
* https://raspberrypi.stackexchange.com/questions/105450/display-a-video-at-boot
* https://raspberrypi.stackexchange.com/questions/59898/how-can-i-blank-the-screen-from-the-command-line-over-ssh
