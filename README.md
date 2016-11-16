
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

Dependencies allowing optimized OpenCV operation (eg: matrix operations)
------------------------------------------------------------------------

```
sudo apt-get install libatlas-base-dev gfortran
```

Install header files for Python 2.7 and Python 3 to compile OpenCV Python bindings
----------------------------------------------------------------------------------

```
sudo apt-get install python2.7-dev python3-dev
```

Download OpenCV and opencv_contrib source codes
-----------------------------------------------
* OpenCV repository: https://github.com/Itseez/opencv
```
cd ~
wget -O opencv.zip https://github.com/Itseez/opencv/archive/3.0.0.zip
unzip opencv.zip
wget -O opencv_contrib.zip https://github.com/Itseez/opencv_contrib/archive/3.0.0.zip
unzip opencv_contrib.zip
```

Install PIP, virtualenv and virtualenvwrapper
---------------------------------------------
```
wget https://bootstrap.pypa.io/get-pip.py
sudo python get-pip.py
sudo pip install virtualenv virtualenvwrapper
sudo rm -rf ~/.cache/pip
```
Also add these lines to ~/.profile

```
export WORKON_HOME=$HOME/.virtualenvs
source /usr/local/bin/virtualenvwrapper.sh
```
Then source the .profile
```
source ~/.profile
```
To install opencv in Python2 or Python3
----------------------------
```
mkvirtualenv cv
# or 
mkvirtualenv cv3 -p python3
```
Choose Python2 virtual environment (virtualenv: Python2)
----------------------------------
```
source ~/.profile; workon cv
```
Install numpy (virtualenv: Python2)
-------------
```
pip install numpy
```
Compile and install OpenCV (virtualenv: Python2)
--------------------------
```
cd ~/opencv-3.0.0/
mkdir build
cd build
cmake -D CMAKE_BUILD_TYPE=RELEASE \
	-D CMAKE_INSTALL_PREFIX=/usr/local \
	-D INSTALL_C_EXAMPLES=ON \
	-D INSTALL_PYTHON_EXAMPLES=ON \
	-D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib-3.0.0/modules \
	-D BUILD_EXAMPLES=ON ..
```
Make sure Interpreter and numpy variables point to the cv virtual environment in the output.
```
sudo make
sudo make install
sudo ldconfig
```
sym-link the OpenCV bindings into the cv virtual environment
```
cd ~/.virtualenvs/cv/lib/python2.7/site-packages/
ln -s /usr/local/lib/python2.7/dist-packages/cv2.so cv2.so
```
Note the .so is in /usr/local/lib/python2.7/dist-packages not /usr/local/lib/python2.7/site-packages

Test python and exit virtual environment (virtualenv: Python2)
------------------------
```
python -c "import cv2; print cv2.__version__"
deactivate
```

Choose Python3 virtual environment (virtualenv: Python3)
----------------------------------
```
source ~/.profile; workon cv3
```
Install numpy (virtualenv: Python3)
-------------
```
pip install numpy
```
Compile and install OpenCV (virtualenv: Python3)
--------------------------
```
cd ~/opencv-3.0.0/
mkdir build
cd build
cmake -D CMAKE_BUILD_TYPE=RELEASE \
	-D CMAKE_INSTALL_PREFIX=/usr/local \
	-D INSTALL_C_EXAMPLES=ON \
	-D INSTALL_PYTHON_EXAMPLES=ON \
	-D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib-3.0.0/modules \
	-D BUILD_EXAMPLES=ON ..
```
Make sure Interpreter and numpy variables point to the cv3 virtual environment in the output.
```
sudo make
sudo make install
sudo ldconfig
```
sym-link the OpenCV bindings into the cv3 virtual environment
```
cd /usr/local/lib/python3.4/site-packages/
sudo mv cv2.cpython-34m.so cv2.so
cd ~/.virtualenvs/cv/lib/python3.4/site-packages/
ln -s /usr/local/lib/python3.4/site-packages/cv2.so cv2.so
```
Note that now the .so is in /usr/local/lib/python3.4/site-packages not /usr/local/lib/python3.4/dist-packages

Test python and exit virtual environment (virtualenv: Python3)
------------------------
```
python -c "import cv2; print(cv2.__version__)"
deactivate
```

Thanks to Adrian Rosebrock (http://www.pyimagesearch.com)


