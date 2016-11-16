
Installing OpenCV 3 on Raspbian Jessie running on RPi-3
=======================================================

Following steps from pyimagesearch.com
http://www.pyimagesearch.com/2015/10/26/how-to-install-opencv-3-on-raspbian-jessie/

Update existing packages and Raspberry Pi firmware
--------------------------------------------------
```
sudo apt-get update
sudo apt-get upgrade
sudo rpi-update
sudo reboot
```

Install developper tools
------------------------
```
sudo apt-get install build-essential git cmake pkg-config
```

Install image and video I/O packages
------------------------------------
```
sudo apt-get install libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
sudo apt-get install libxvidcore-dev libx264-dev
```

Install GATK
------------
* GATK development library to compile the highgui sub-module of OpenCV allowing the display images to our screen and build simple GUI interfaces.
```
sudo apt-get install libgtk2.0-dev
```
