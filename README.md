![Mini Relay Box](https://github.com/EasySensors/MiniRelayBox/blob/master/pics/miniRelayBox5.jpg?raw=true)
![Mini Relay Box](https://github.com/EasySensors/MiniRelayBox/blob/master/pics/label300.JPG?raw=true)
![Mini Relay Box](https://github.com/EasySensors/MiniRelayBox/blob/master/pics/miniRelayBox2.jpg?raw=true)
![Mini Relay Box](https://github.com/EasySensors/MiniRelayBox/blob/master/pics/miniRelayBox4.jpg?raw=true)


### The Mini Relay Box  is a low cost wireless 220 Volts 10A Relay board. It can switch on-off 220 Volts wirelessly. Arduino IDE compatible (the Atmel ATMega328P) microcontroller with RFM 69 HW radio on board.  Onboard 220 Volts power supply. Secure athentication with ATSHA204A crypto-authentication. Best suitable for Home Automation, IOT. Current sensor can report power consumption. The board dimensions is really small. You may think of it as Arduino Pro Mini plus all the items in the picture below:

![](https://github.com/EasySensors/MiniRelayBox/blob/master/pics/replace.jpg?raw=true)

## Specification: ##
 - Authentication security - Atmel ATSHA204A Crypto Authentication Chip
 - External JDEC EPROM
 - RFM69-HW (high power version) 433 MHz Radio transceiver
 - ACS-712 current sensor. Range from 0,1 A up to 10 amperes.
 - External JDEC EPROM
 - Dualoptiboot bootloader. Implements over the air (OTA) firmware update ability
 - Pixel LED SK6812mini
 - Supply voltage 160-240 Volts AC
 - The Digital and Analog pins are 3.3 volts
 - Uncompromised Protection:<br>
	Overload varistor<br>
	Slow fuse<br>
	Thermal fuse<br>
 - Plastic Enclosure Dimensions 40x45x20mm
 - Board Dimensions 36x38x18mm
 - FTDI  header for programming


**Pin out:** 


Arduino Pins|	Description
------------|--------------
A0, A2 |	Available ARDUINO analog GPIO / DIGITAL GPIO 
A1 |	connected to ACS712 current sensor
A3 |	connected to  ATSHA204A
D5 |	Available ARDUINO digital GPIO
D6 |	connected to Pixel LED SK6812mini
D7 |	connected to the 10A Relay
D8 |	Connected to CS FLASH chip (OTA) M25P40
D9 |	connected to RFM69 reset pin
ANT |	RFM69 antenna


**Arduino IDE Settings**

![Arduino IDE Settings](https://github.com/EasySensors/ButtonSizeNode/blob/master/pics/IDEsettings.jpg?raw=true)



**programming FTDI adapter connection**

![FTDI Power](https://github.com/EasySensors/MiniRelayBox/blob/master/pics/FTDIvcc3.jpg?raw=true)


3.3V power option should be used.



How to use it as home automation (IOT) node Relay
------------------------------------------------------


miniRelayBox.ino is the Arduino example sketch using [MySensors](https://www.mysensors.org/) API. 

Burn the miniRelayBox.ino sketch into it and it will became  one of the MySensors home automation network Relay Node. The Relay could be controlable from a smarthome controller web interface or smarphone App. 
To create Home Automation Network you need smarthome controller and at least two Nodes one as a Sensor, relay or actuator Node and the other one as “Gateway Serial” connected to the smarthome controller. I personally love [Domoticz](https://domoticz.com/) as home automation conroller. Please check this [HowTo](https://github.com/EasySensors/ButtonSizeNode/blob/master/DomoticzInstallMySensors.md) to install Domoticz.

However, for no-controller setup, as example, you can use 3 nodes - first node as “Gateway Serial”, second node as the Mini Relay Box node and the last one as switch for the relay node. No controller needed then, keep the switch and the relay node on the same address and the switch will operate the relay node.

Things worth mentioning about the  [MySensors](https://www.mysensors.org/) Arduino sketch: 


Code |	Description
------------|--------------
#define MY_RADIO_RFM69<br>#define MY_RFM69_FREQUENCY   RF69_433MHZ<br>#define MY_IS_RFM69HW|	Define which radio we use – here is RFM 69<br>with frequency 433 MHZ and it is HW<br>type – one of the most powerful RFM 69 radios.<br>If your radio is RFM69CW - comment out line<br>with // #define MY_IS_RFM69HW 
#define MY_NODE_ID 0xE0 | Define Node address (0xE0 here). I prefer to use static addresses<br> and in Hexadecimal since it is easier to identify the node<br> address in  [Domoticz](https://domoticz.com/) devices list after it<br> will be discovered by controller ( [Domoticz](https://domoticz.com/)).<br> However, you can use AUTO instead of the hardcoded number<br> (like 0xE0) though.  [Domoticz](https://domoticz.com/) will automatically assign node ID then.
#define MY_OTA_FIRMWARE_FEATURE<br>#define MY_OTA_FLASH_JDECID 0x0 | Define OTA feature. OTA stands for “Over The Air firmware updates”.<br> If your node does not utilize Sleep mode you can send new “firmware”<br> (compiled sketch binary) by air. **Here is the link on how to do it.** <br>For OTA we use JDEC Flash chip where the node stores<br> new firmware and once it received and controlsum (CRC) is correct<br>  it reboots and flashes your new code into the node<br> controller. So we define it is "erase type" as 0x2020 here. 
#define MY_SIGNING_ATSHA204 <br>#define  MY_SIGNING_REQUEST_SIGNATURES | Define if you like to use Crypto Authentication to secure your nodes<br> from intruders or interference. After that, you have to “personalize”<br> all the nodes, which have those, defines enabled.<br> [**How to “personalize” nodes with encryption key**](https://github.com/EasySensors/ButtonSizeNode/blob/master/SecurityPersonalizationHowTo.md).<br> You need both defines in the nodes you need to protect.<br> The Gateway Serial could be with only one of those<br> defines enabled - #define MY_SIGNING_ATSHA204
#define AdafruitNeoPixel | Enables onboard Pixel LED SK6812mini

Connect the Relay to FTDI USB adaptor, Select Pro Mini 8MHz board in Arduino IDE and upload the miniRelayBox.ino sketch.

**Done**


The board is created by  [Koresh](https://www.openhardware.io/user/143/projects/Koresh)

![Mini Relay Box](https://github.com/EasySensors/MiniRelayBox/blob/master/pics/r5.jpg?raw=true)
![Mini Relay Box](https://github.com/EasySensors/MiniRelayBox/blob/master/pics/label470.jpg?raw=true)
![Mini Relay Box](https://github.com/EasySensors/MiniRelayBox/blob/master/pics/r1.jpg?raw=true)
![Mini Relay Box](https://github.com/EasySensors/MiniRelayBox/blob/master/pics/r2.jpg?raw=true)
![Mini Relay Box](https://github.com/EasySensors/MiniRelayBox/blob/master/pics/r3.jpg?raw=true)
![Mini Relay Box](https://github.com/EasySensors/MiniRelayBox/blob/master/pics/r4.jpg?raw=true)

>[The board schematics Pdf link](https://github.com/EasySensors/MiniRelayBox/blob/master/pdf/WallInsertableSocket_sch.pdf)
