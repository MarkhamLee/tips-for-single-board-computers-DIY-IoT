
* Software support isn't great, I'm running a ["bleeding edge" Armbian distro](https://www.armbian.com/orangepi3b/) on it that needs a maintainer, so this is a truly "at your own risk" and YMMV situation. I did try the official Ubuntu image from Orange Pi but the performance was poor, sys bench scores were about 60% of what I get with Armbian: 13,847/1,383 for primes set to 20k. 
* Speed wise it's about 1/2 that of a Raspberry Pi 4B if you go by sysbench (27.6k/2.7k) or about 70-80% if you go by Geekbench 6 205/553 for single vs multi-core on the Opi 3B vs 283 and 653 on a RPI 4B. Still, given that you get 8 GB of RAM in a $45 SBC, in addition to NVME and eMMC slots it would be a price vs performance leader if the OS situation was better. 
* Getting it to boot from NVME and eMMC was fairly simple:
    * Image an SD with Armbian 
    * Boot up the device 
    * sudo armbian-config 
    * Select: system and security --> update boot loader --> select the NVME or eMMC options. 
* Caveats for the above: 
    * The first time I tried to do this with NVME it worked fine, then the device stopped booting after a few weeks 
    * I tried to setup NVME boot again and it didn't work, I then tried eMMC and it cloned my SD onto the eMMC and set it as the boot device. Haven't had a problem since. 

But, as I've said before, YMMV. 

Currently, I have the device running Docker containers managed with Portainer for somoe of my IoT experiments and another project I'm working on. It's basically gathering energy data from smart plugs via the Kasa python library and then writing that data to InfluxDB, as well as turning plugs on and off. Haven't had any issues so far. I also had it running a Nova PM SDS011 USB air quality sensor and had no problems. I've also used it as an ARM dev box via ssh-ing in via VS Code and again, no issues. Capable device if you don't mind the "you're on your own" Armbian OS. 