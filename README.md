# 17CN-Yi-Home-Recovery
This project is the compilation of steps and procedures utilizing the tools, firmware, and hackwork done by others and  available for public use to attempt and downgrade Yi Home Camera 17CN version 1.0 when in a specific state.


# Acknowledgments

I would like to also thank the following projects for their efforts on other Xiaomi cameras and allow me to recovery my camera and downgrade it.

shadow-1: https://github.com/shadow-1/yi-hack-v3  
For developing wonderful firmware with tons of extra features and providing recovery images 

fritz-smh : https://github.com/fritz-smh/yi-hack

Csaba Peter and JonesChi: https://diy.2pmc.net/solved-xiaomi-xiao-yi-ant-home-camera-can-used-china/  
For hacking region blocking limitation with Cloud_API modification

jronemo : https://w3bsit3-dns.com/forum/index.php?showtopic=638230&st=11956  
For providing the backup images for all mtdblock for 1.8.6C version for 17CN camera.

# Recovery When Indicator light is Permanently ON in Yellow

This state happens when someone tries to flash wrong firmware version on 17CN model camera.The simplest and easiest way to recovery from this state witout soldering the serial port and tinkering with the hardware is to use recovery images provided by shadow-1. 

1. Downdload the recovery image from Yi-hack-v3 project --> see link in acknowledgements.
   make sure you download the correct files for 17CN camera home_y18 and rootfs_y18. 
2. copy these files to the root of SD card which should be formated in FAT32 in a windows based system and remove any extension
3. insert the SD card into camera and power up.
4. wait for 30-60 seconds, yellow light should start blinking while camera is restoring the firmware files
5. One restore process is completed camera with start normally and make annoucement in chinese language 

# Downgrading to lower version 1.8.6C to remove region blocking
If above steps has been completed successfully you should be running 1.8.7C firmware which does not allow to run any script for SD card. due to this limiated it is impossible to hack the 17CN camera without soldering the serial port. However if you follow below steps it will allow to you restore and remove region blocking limitation at the same time

Before we proceed I will encourage you too look into yi-hack-v3 custome firmware. It has really good features and easy to use.

1. First of all download all required files 
mtdblock5    --> this is the home partition image for 1.8.6C verion 
yi-hack-v3 for 17CN --> this will allow us to ssh/telnet into the camera
yi-hck-v3 recovery images --> required to restore rootfs partition
Download link:
https://www.dropbox.com/sh/0eerqc43x9strjx/AADM96BjbMDnJfL9tbp8q7Bba?dl=0

2. At this step I assume you already have working 17CN camera with official firmware 
3. copy the files for yi-hack-v3 folder to the root of SD card. 
4. copy mtdblock5 file in to the root of SD card.
5. create a folder named recovery in SD card. then copy rootfs_y18 from "Recovery 17CN" folder to recovery folder in SD card
6. insert SD card into camera and power on. Yellow light should flash at 1Hz and upgrade the firmware to yi-hack-v3 custome firmware
7. at this point open the app in your smartphone and try to pair. Camera will successfully connect to wifi but failed to pair with you phone. that is completely fine. 
8. get the ip address of your camera and ssh in to it with root user. password is blank so just hit enter.
9. Now execute the below commands in sequence
cd /tmp/sd
rm home_y18
rm rootfs_y18
cp ./recovery/rootfs_y18 ./
cat mtdblock5 > /dev/mtdblock5

8. after executing last command wait for the camera to reboot itself and restore original rootfs filesystem.
once camera boot up successfully it will automatically connect to the wifi. now you should be able to telnet into it with root and password is blank. Just hit enter
9.if you are able to login via telnet congratulations you have successfully downgraded to 1.8.6C which is already hack to remove region blocking limitation. 
10. To pair it with your smart phone. Just reset your camera normally by pressing the reset button for few seconds and pair it again
