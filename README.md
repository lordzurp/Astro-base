# Astro-base
 
### Central board to Power and Control telescope stuff

PI Hat compatible, ATmega328 Powered board


##### Power Management
The board power the Rpi directly, and has 2 DC-jack outputs to accessories

IRS-Q12 Modules from Murata provides high-efficiency conversion from wide input voltage range
* 5V 10A
* 12V 4.5A

Linear regulator AMS1117 is used to provide 3.3V for the boards components


#### RTC Unit
Based on DS1307 chip



sudo apt-get update
sudo apt-get -y upgrade

sudo nano /etc/modules
change or add the /etc/modules

snd-bcm2835
i2c-bcm2835
i2c-dev
rtc-ds1307

Next, setup Raspberry's i2c communication

detect your rtc device

sudo i2cdetect -y 1<br>or<br>sudo i2cdetect -y 0

Modify your system line

sudo nano /etc/rc.local
Add the following two lines before the exit 0 line :

echo ds1307 0x68 > /sys/class/i2c-adapter/i2c-1/new_device
hwclock -s


Reboot your pi

sudo reboot
Finally, setup date on RTC

change your Raspberry Pi system time

sudo date -s "20 NOV 2015 18:49:00"
write the rtc module

sudo hwclock -w
match your system and rtc module

sudo date; sudo hwclock -r



#### Dew heater

* 2x 5V 2A dew heaters, MOSFET PWM driver for power dimming
* DHT22 module for ambiant T° and Rh
* DS18B20 for heater T°
* controlled by the µC, can be read and set from the Rpi


#### Rpi shutdown

can send power_off signal to Rpi thru the GPIO4


#### OLED Display

* power ON with short press on switch, auto power-off screen after 30s
* Display misc infos : 
	* Power_IN voltage, current, power and power consumption infos
	* Dew heaters status