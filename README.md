# P4wnp1-ALOA-Menu-Reworked

## Info

This project was born from: https://github.com/beboxos/P4wnP1_ALOA_OLED_MENU_V2, since python2.7 is deprecated and therefore no longer compatible with the libraries in use, I opened a Fork, updated the code to Python3.7 and made a PullRequest.

Since the original repo seems to be no longer maintained, I decided to open a new one with the updates made, so that everyone can take advantage of this fantastic project of https://github.com/beboxos again.

If BeboXos returns to his repo this will be closed, and i hope so.

All rights to the original code are owned by BeboXos.

## What's New
* I updated the code to work with python3.7, fixed some bugs and added new features.
* new functions to make easier improving the code,see MANUAL.md
* update the gui-code via gui-option
* hosts discovery
* nmap on a specific host and save the report
* vulnerability scan (experimental...help me)
* Deauther(Jammer-like) on Wifi AP (60s, for continuous mode delete "timeout 60s" in the gui.py/deauther() function"
* Deauther(Jammer-like) on a specific client
* ArpPoisoning, saving HttpUrls, HttpUserPass,HttpsUrls, Mails. Output in the current directory (working on)
* TODO others

## Known Bugs
* using DEauther breaks WIFI and BLT connections, so you need to restart your Rasp
* some templates need to be executed 2 times, due to a P4wnp1 bug


## Installation:

### Enabling spi and i2c on the pi zero
On boot partition edit config.txt to set I2C and SPI to active (in terminal you can type nano /boot/config.txt)

edit:

         dtparam=i2c_arm=on

and find and set spi section:

         dtparam=spi=on

if you have a i2c screen or are using a UPS lite you will need to check the i2c has enabled properly after a reboot using the below command

        sudo i2cdetect -y 1

if this displays a table like below of connected i2c devices all is good

        root@172.16.0.1:~ $ sudo i2cdetect -y 1
             0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
        00:          -- -- -- -- -- -- -- -- -- -- -- -- --
        10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
        20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
        30: -- -- -- -- -- -- 36 -- -- -- -- -- -- -- -- --
        40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
        50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
        60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
        70: -- -- -- -- -- -- -- --

but if you dont have i2c-tools or it returns an error like this i2c hasn't been enabled correctly

        Error: Could not open file `/dev/i2c-1' or `/dev/i2c/1': No such file or directory

to enable i2c properly can be a bit fiddly as kali doesn't have rpiconfig. you will need to do the following

edit etc/modules to include the following lines

        i2c_bcm2835
        12c_dev

also will need to install i2c-tools with

        sudo apt-get install i2c-tools

now reboot and try i2cdetect again

### Edit gui.py to suit your setup

###### Note for i2c screen: (on gui.py)

     set USER_I2C=1
     (if you have a ups) set UPS=1

###### Note for SPI: (on gui.py) (currently set like this)

    set USER_I2C=0
    (if you have a ups) set UPS=1

##### GPIO 8 keys are default waveshare hat
    you can edit to set to your hat if different
    * GPIO
    * KEY_UP_PIN     : 6,
    * KEY_DOWN_PIN   : 19,
    * KEY_LEFT_PIN   : 5,
    * KEY_RIGHT_PIN  : 26,
    * KEY_PRESS_PIN  : 13,
    * KEY1_PIN       : 21,
    * KEY2_PIN       : 20,
    * KEY3_PIN       : 16

### Final installation and dependencies

Make the install script executable

        chmod +x install.sh update.sh

Run the install script using bash

        bash install.sh

the script will automatically install all the files needed

## Start at boot
in P4wnP1 web interface , create a trigger action that runs the script runmenu.sh in you default template (by default startup)
select the script runmenu.sh.
* open the web interface
* select Tigger action
* add one
* select runmenu.sh
* select store and type startup

## Improve the code
* see MANUAL.md

enjoy
# i'm not responsible on usage you do with this repo, it's for educational purpose only

###### usefull links
* guide: https://gideonwolfe.com/posts/security/p4wnp1/
* video guide: https://www.youtube.com/watch?v=s0K-YIL_G5c
* rasp that I use : https://www.amazon.it/Melopero-Raspberry-Zero-Starter-Kit/dp/B072LWBL37/ref=sr_1_1?__mk_it_IT=%C3%85M%C3%85%C5%BD%C3%95%C3%91&dchild=1&keywords=melopero+raspberry+pi+zero+w+starter+kit&qid=1594075917&s=electronics&sr=1-1
* oled that I use : https://www.amazon.it/gp/product/B078D6NXFM/ref=ppx_yo_dt_b_asin_title_o01_s00?ie=UTF8&psc=1
* usb addon that I use : https://www.amazon.it/gp/product/B07BPTPDM5/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1

###### credits
* P4wnp1 ALOA repo: https://github.com/RoganDawes/P4wnP1_aloa
* beboxos/P4wnP1_ALOA_OLED_MENU_V2 repo: https://github.com/beboxos/P4wnP1_ALOA_OLED_MENU_V2
