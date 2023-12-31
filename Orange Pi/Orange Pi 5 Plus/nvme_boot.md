### Setting up Orange Pi 5 Plus to boot from NVME. 

**Note:** this is just the process that worked for me with multiple of these devices, I give no guarantees that it will for you, use this guide at your own risk. 

**2nd Note:** for this entire setup process I had the device plugged into a USB C MacBook charger, see the power issues noted in the general tips MD file. 

**3rd Note:** the best advice is to do this when the device is "fresh out the box", if you do this after installing other operating systems, things can get, hairy... more on that later. 

This example presumes you want to install [Joshua Riek's Ubuntu image for Rockchip 3588 devices](https://github.com/Joshua-Riek/ubuntu-rockchip). You can potentially just install the Armbian image directly on the NVME drive and the device will boot up, but my experience there has been inconsistent at best. I've had it work and I've had it not work. The following is my "standard approach", meaning: I know this will consistently enable the device to always boot from NVME and allowed me to eschew the SD card all together. 

1. Go to the Armbian web site and download a copy of the Armbian OS for the Orange Pi 5. 
2. Image the card using something like belenaEtcher 
3. Insert the card into the device and boot it up. 
    * The usual stuff around with it plugged into a monitor or get the IP address and then use it via SSH apply 
4. Once the device has fully booted up and you've gone through the usual setup steps, type "sudo armbian-config". Chances are, neither Wi-Fi or LAN works at this point, so you'll get an error message about the utility not working as well without internet. Open the utility anyway, and you should be presented with a screen that looks like this: 
5. Select System and security settings
6. Select "Install to/update boot loader" 
7. Select "Boot from MTD Flash - system on SATA, USB or NVMe" <-- yes the last e is lower case in the menu and click "Ok" 
    * Picking the second option would be status quo + you could also boot from the eMMC module if you have one, but, that's probably not why you're here. 
8. You'll have to then click through a couple of menus, just select the choice given for the drive, I then selected ext4 in the filesystem format screen, click through a few more screens and you're done. 
9. Image your NVME with your preferred OS and you're good to go... 

...probably. One of the times I did this I had alreayd booted into another OS (Armbian Desktop), before trying Armbian server and then deciding to switch to Joshua Riek's Ubuntu image. While in Armbian server I got an error message saying there wasn't enough space in the SPI. I then tried to use the disk utilities to clear out the bootloader but it didn't work and my device couldn't connect to the internet via Armbian. I then installed the Orange Pi Ubuntu image, I used the utility to clear out the partitions, I tried to install the bootloader, but despite the options being the same it wanted to install it to the NVME. Meaning: it would install the Orange Pi Ubuntu image that was on the SD card to my NVME/erase my NVME that had my preferred Ubuntu image on it. I then went back to Armbian and got the same message as before as as there not being enough space on the SPI. I turned the device off, pulled out the SD card, put in my NVME with Josh's Ubuntu image and it booted up just fine. That was in early September and I use the device semi-regularly and haven't had a single problem since. 



