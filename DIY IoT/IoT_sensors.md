## DIY IoT Sensors - Tips and Tricks    


##### Nova PM SDS011 Air Quality Sensor
A few tips and tricks in case you can't get the sensor working, note: these are all specific to Linux distributions, I haven't tried to use these on OSX or Windows.

* Using the Nova PM SDS011 air quality sensor is fairly simple, plug it into a USB port, run the appropriate python script(s) and away you go.
    * You can find sample code to run the sensor in one of my [other repos:](https://github.com/MarkhamLee/productivity-music-stocks-weather-IoT-dashboard/blob/main/IoT/troubleshooting_sensors.md)
* If you run into issues where the ttyUSB0 can't be found:
    * If you're running a desktop Linux distribution, run sudo apt remove brltty, there is a package that's for the sight impaired that can cause issues with the sensors
    * Check that /dev/ttyUSB0 exists and what permissions are set on it with 'ls -l /dev/ttyUSB0'. You should get something back that includes something like: (/dev/ttyS{0..31}), which belongs to the group dialout. 
        * You may have to join that group via this command: ('sudo usermod -a -G dialout your_username_here'). 
        * Then login and log back out for it to take effect. 
    * Note: I haven't run into any of these issues while attempting to use the sensors on a headless Linux distribution.
* The above steps can be used on must sensor or hub devices you'd plug into USB, like a Zigbee USB hub. Also, if you already have something plugged into one of your USB ports, than the address for the USB port becomes ttyUSB1, if you have two things ttyUSB2, and so on and so forth. 

##### Troubleshooting GPIO based sensors

Using the GPIO pins of a single board computer can be frustrating at first, but in my experience it's one of those things that can be quite trivial once you figure it out, mostly because the source of the problems are far more often than not, not code related:

* Until you're very comfortable with building applications using GPIO pins, only, use, Raspberry Pi Devices. Period. Because while there are some very capable pieces of competing single board computer (SBC) hardwarwe out there, they often lack the same level of software support, drivers and the like for GPIO pins. 
* TL/DR: to save yourself a lot of time and frustration, just get everything working on a Raspberry Pi and THEN figure it out on a different piece of hardware. Also: a lot of software/drivers for many of the IoT sensors out there are for Raspberry Pis.
* Buy a GPIO breakout board with LEDs that indicate that when things are working properly. The LEDs can help you to see if you've got a good connection, and a great way to see if you're connecting to the right pins is to run your code and see which pins light up, if you don't have wires connected to that pin, well... that's probably your problem. I've had good luck with these ones [I bought on Amazon](https://www.amazon.com/GeeekPi-Terminal-Raspberry-Expansion-Connector/dp/B0C2P943ZJ/) <-- NOT an affiliate link. 
* Use the 5v terminals if possible, I've found it helpful with sensor performance as some are slower or struggle to work off of the 3V terminals, even if the documentation for that sensor says it will work with 3v. 



### Helpful Technical References


Air Quality sensor issues:
* https://askubuntu.com/questions/1403705/dev-ttyusb0-not-present-in-ubuntu-22-04
* https://ubuntuforums.org/showthread.php?t=2475878
