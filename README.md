# flir_ax8_simple_driver

### ver0.8 (David Portugal)
Simple drivers for the FLIR AX8 Thermal Camera. We provide three nodes:
 - A Python node that uses web scraping to get the thermal image from the camera webserver (faster, but less customizable): `flir_web_scraping_driver.py`
 - A Python node that uses OpenCV and RTSP streaming to get the camera's image (slower, but more customizable): `flir_ax8_simple_driver_rtsp.py`
 - Same as above but in C++: `flir_ax8_simple_driver_rtsp.cpp`

All nodes publish messages into a raw sensor_msgs/Image topic. 

Launch files are provided to publish their compressed counterpart on ROS.

Tested on Ubuntu 18.04 and ROS Melodic


## Important

Make sure that you have the correct camera IP when running the launch file.

You'll need to ```sudo apt install python-pip```, in case you don't have pip installed.

You will also need to download the Mozilla Geckodriver from [here](https://github.com/mozilla/geckodriver/releases). Place it in `/home/user/mozilla_geckodriver` and add the following line to your `.bashrc` file:

`export PATH=$PATH:/home/user/mozilla_geckodriver `


## Compiling

```
sudo pip install requests selenium
cd your_work_space
catkin_make 
```


## Example Usage

**Parameters**

#### `flir_web_scraping_driver.py` and `flir_ax8_simple_driver_rtsp`:

`flir_camera_ip` (`string`, `default: 172.16.2.10`)

By default, the IP address of the device is 172.16.2.10.

`flir_camera_frame` (`string`, `default: flir_ax8_link`)

The frame ID entry for the messages.

`flir_camera_topic` (`string`, `default: flir_ax8`)

The topic to publish the messages.



#### `flir_ax8_simple_driver_rtsp`:

`flir_encoding` (`string`, `default: mpeg4`)

The encoding type for the streamed images. Possible options are: "avc", "mpeg4" and "mjpg".

`flir_text_overlay` (`string`, `default: off`)

Option to remove the overlaid text from FLIR. Possible options are: "on" and "off".


**Running the launch files**

Web Scraping driver:

```
roslaunch flir_ax8_simple_driver flir_ax8_simple_driver.launch
```
or RTSP driver:

```
roslaunch flir_ax8_simple_driver flir_ax8_simple_driver_rtsp.launch
```

Feel free to play with the parameters in the launch files to suit your setup.
