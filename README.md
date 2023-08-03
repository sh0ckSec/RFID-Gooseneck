# RFID Gooseneck

Traditional RFID badge cloning methods require you to be within 3 feet of your target, so how can you conduct a socially distanced physical penetration test and clone a badge if you must stay at least 6 feet from a person? Since 2020, companies have increasingly adopted a hybrid work environment, allowing employees to partially work remotely, which has decreased the amount of foot traffic in and out of a building at any given time. So after throwing around some ideas, I thought, why not create a mobile long-range reader device that we could deploy early in the morning at a client site and let it do all the work for us.  This project guide contains an entry-level hardware design that you can build in a day and deploy in the field in order to increase your chances of remotely cloning an RFID badge. 

<img src="https://user-images.githubusercontent.com/104524120/183311963-9f5dcf63-abc1-46a2-9d27-cc1c80772709.png" width=50% height=50%> 

This is part of a full paper and talk given during **DEFCON 30** in the Physical Bypass Village and Radio Frequency Village titled: **Keeping Your Distance: Pwning RFID Physical Access Controls From 6FT and Beyond** by myself and Twitter: @_badcharacters (https://www.youtube.com/watch?v=OLLaXOcuYfw). The content has been updated for **DEFCON 31** with cloning your badge loot with a Flipper Zero.

Here's the full build guide for making your own RFID Goosneck Long Range Reader! 

 *Disclaimer:* **This guide is for educational and ethical hacking purposes ONLY. All penetration testing activities must be authorized by all relevant parties.**

# Gooseneck Base Installation Guide 
Ok, let's do this. 

### Wooden Base BOM:
* MDF or Plywood (16"x16"x0.5")
* Non-Slip Furniture Feet: https://a.co/d/8oR8tHj  
* Pedestal Pro 36"H Gooseneck: https://bit.ly/3bCz6go
* 3/8" x 1 1/4" Carriage Bolts and Wing Nuts and Washers (Quantity of 6 each) 
* Black Spray Paint

### Step 1 - Cut Out Wood Base
* If you have access to a laser cutter or a ShopBot, feel free to download the "GooseneckBaseMK2Template_sh0ck" template file(s) or cut out your own 16"x16" piece of MDF or plywood. 

<img src="https://user-images.githubusercontent.com/104524120/183817491-c6211d51-2ad0-4fdc-9640-4c3279d4e3e6.PNG" width=40% height=40%>


### Step 2 - Align Pedestal
* Center the gooseneck pedestal and place the edge of the base approximately 1.25" away from the edge of the base. The 1.25" (3.175cm) distance from the edge will counter-balance the weight of the long-range reader so it will not tip over when installed. 
* Next trace and drill the 3/8" mounting holes.

<img src="https://user-images.githubusercontent.com/104524120/183817731-6e467b8a-858f-40c5-b102-00962ba5c13b.PNG" width=30% height=30%>


### Step 3 - Paint
* Spray the base with a matte black color of your choice.
<img src="https://user-images.githubusercontent.com/104524120/183312993-d70ecfc4-aa1c-4495-b196-3730f4b221fc.jpg" width=30% height=30%>


### Step 4 - Install Feet 
* When the paint is dry, drill the non-slip furniture feet onto the bottom of the base. 
<img src="https://user-images.githubusercontent.com/104524120/183314771-d5d37a13-9c6e-448e-8eae-d29da818cedc.PNG" width=40% height=40%>

![IMG_8114](https://github.com/sh0ckSec/RFID-Gooseneck/assets/104524120/3c917766-4207-4be9-99af-205409b0b5a0)


### Step 5 - Fasten Pedestal to Base 
Last, fasten the pedestal to the wooden base with bolts and wingnuts. Then place the pedestal cover over the top to conceal the screws. 

<img src="https://user-images.githubusercontent.com/104524120/183313071-e98d3297-88a1-43da-954a-7ae55be843b5.jpg" width=30% height=30%>


# Long Range Reader Cloning Guide
Let's build the long-range reader cloning device. 
### Long Range Reader BOM: 
* ESP RFID Tool: https://hackerwarehouse.com/product/esp-rfid-tool/
* Low-Frequency Long Range Reader (e.g. HID MaxiProx 5375) OR High-Frequency Long Range Reader (e.g. HID iCLASS SE R90) 
* Breadboard Jumper Wires - 3.9in (10cm): https://a.co/d/fja090p or 22AWG Wire: https://a.co/d/h7bbBom 
* 18AWG 12V 5A DC Power Pigtail Barrel Plug Connector Cable: https://a.co/d/7l56UFQ
* 12V 6000mAh/5V 12000mAh DC Battery: https://a.co/d/9czvggQ
* 3M Dual Lock Clear Velcro: https://a.co/d/gg4SzBd

### Wiring Guide 
Below is an example of the wiring guide to connect to a long-range reader with screw-in terminals using the ESP RFID Tool. Use the color-coded male-to-male breadboard wires to connect the two terminal interfaces between the Wiegand system and the ESP RFID Tool as seen below.

<img src="https://user-images.githubusercontent.com/104524120/183313184-f8f62a73-4bb1-403b-8c65-bfd9d5edac78.PNG" width=80% height=80%>

* Then connect the 12V 5A DC Power Pigtail Barrel Plug Male Connector cable into the Wiegand system (HID iClass SE R90 pictured) and trail the cable to the outside of the reader so you can plug it into the 12V 6000mAh DC Battery. 

<img src="https://user-images.githubusercontent.com/104524120/183816676-e13ef2d6-b493-4d49-baa1-03c0f9d288a2.jpg" width=40% height=40%>

The same wiring applies to the low-frequency HID MaxiProx 5375 reader. 

**INSERT PIC OF 5375 WIRING**

*WARNING:* Ensure when you are working with the HID MaxiProx 5375 that you change the jumper on the Shunt Pins settings from 2 and 3 +21-2.85 VDC (Default) TO Shunt Pins 1 and 2 +11.6-20.9VDC) because we are using a 12V battery. If you do not switch the jumper, you will fry the unit! YOU'VE BEEN WARNED! Double-check this for any reader you are working with, just in case. 

**INSERT JUMPER SETTINGS PIC HERE**

To remain as stealthy as possible, it is advised to turn off the audible "beep" if the reader allows you to. In this case, we can silence the beep on the HID MaxiProx 5375 reader by pushing down dipswitch #4 of SW1 (the farthest right of the switch sets). 

<img src="(https://github.com/sh0ckSec/RFID-Gooseneck/assets/104524120/a1cb567d-821a-4a09-8444-d661cca4b558)" width=40% height=40%>
*Source: http://exfil.co/2017/01/17/wiegotcha-rfid-thief/*

HID MaxiProx 5375 full manual: https://www.manualsdir.com/manuals/433070/hid-maxiprox-installation-guide.html?page=7 

*Note: For various configurations, check out the official ESP RFID Tool wiring guide here: https://github.com/rfidtool/ESP-RFID-Tool/blob/master/Installation-Schematics/README.md*

### ALTERNATIVE Raspberry Pi Setup: 
If you would like an alternative raspberry pi cloning device setup, I **HIGHLY RECOMMEND** checking out Mike Kelly's (Twitter @lixmk) Wiegotcha – RFID Thief guide: 
http://exfil.co/2017/01/17/wiegotcha-rfid-thief/ 
          
# Mounting Reader to Pedestal
Depending on the reader, you must find the correct mounting hole guide for each. You will have to manually drill holes into the back of the reader in order to center it to the gooseneck pedestal with carriage bolts and nuts. Below is an example mount guide for the HID iCLASS R90.

<img src="https://user-images.githubusercontent.com/104524120/183313721-397f9938-6629-4a41-a248-e4815d4de5c0.PNG" width=40% height=40%>

iCLASS SE Mounting and User Guide: https://fccid.io/JQ6-ICLASSU90/User-Manual/User-Manual-2360366 

HID iClass R90 Gooseneck finished look: 

<img src="https://user-images.githubusercontent.com/104524120/183314105-ac8e840d-e4df-4971-92a6-41a3f69e5eaa.jpg" width=40% height=40%>


# Cloning Low-Frequency Cards - Android Phone + Proxmark3 Easy 
To remain incognito while at the client site, cloning a card via an Android phone will keep the lowest profile rather than fiddling with a laptop when you need to copy the card data. 

<img src="https://user-images.githubusercontent.com/104524120/183313587-635d6993-c76d-49c7-9b92-a2122933511a.PNG" width=40% height=40%>

### Mobile Cloning Gear:
* Android Phone or Tablet of your choice
* AndProx Android App: https://github.com/AndProx/AndProx  
* Proxmark3 Easy (available on eBay or AliExpress)
* USB OTG Cable - Type C To Micro: https://a.co/d/4HGdBqh
* RFID T5557 Rewritable Cards: https://a.co/d/0NF2zJG
* 3D Printed Case (optional): https://www.thingiverse.com/thing:3123482 
                                                                                                                 
![MobileSetup](https://user-images.githubusercontent.com/104524120/183818120-04b57153-fbe9-4b91-b2df-90b1f6a31262.jpg)
                                                                                                          

### Step 1A  - Access RFID Loot
Once the implant is in place and a few employees have walked past the gooseneck reader, hop onto your phone and log into your the RFID ESP Key SSID to look for loot. The default SSID is "ESP-RFID-Tool" but it is recommended to change the name to something that will blend into the target environment. In order to change the SSID and password protect the ESP RFID Tool wifi (and not leak all your client's credentials to the world), jump over to the configuration page to customize the settings. 
* Default SSID: **ESP-RFID-Tool**
* URL: http://192.168.1.1


Default credentials to access the configuration page:
* Username: *admin*
* Password: *rfidtool*

(Full ESP RFID Tool user guide here: https://github.com/rfidtool/ESP-RFID-Tool)

Once you're on the ESP RFID Tool WiFi, access HEX Code Data in the "List Exfiltrated Data" Page:

<img src="https://user-images.githubusercontent.com/104524120/183313563-2b3c480d-2005-4bf0-b2db-7d00d182feda.PNG" width=50% height=50%>

### Step 1B - Copy the HEX Code Payload!

<img src="https://user-images.githubusercontent.com/104524120/183313560-a9b16ced-396f-4657-bc75-e541297411d2.PNG" width=70% height=70%>


### Step 2 - Android Cloning Setup
* Download and install AndProx (Root NOT required!): https://github.com/AndProx/AndProx 
* Plug in your Proxmark3 via OTG cable
* Click Connect Via USB
* Begin sending commands!

### Step 3 - AndProx Commands 
Once your Proxmark3 Easy is connected, copy your Hex Code and enter these commands: 

<img src="https://user-images.githubusercontent.com/104524120/183313638-804a3cc5-ddee-48dc-ab06-ab20b3baef0d.PNG" width=50% height=50%>

> lf hid clone [INSERT HEX CODE]

#Example: 
> lf hid clone 20043C0A73 

Verify your card data:
> lf search

<img src="https://user-images.githubusercontent.com/104524120/183313654-86c90889-5f66-4756-9d9a-b1d1330022e4.PNG" width=40% height=40%>


Boom! Happy Hunting!


![D3FC0N](https://user-images.githubusercontent.com/104524120/183314908-3d3c6d66-29b2-4ba0-84ae-932c3c2ca782.PNG) 

Special Shoutouts to the Bill Graydon of the Physical Security Village and Zero_Chaos of the Radio Frequency Village for hosting this talk during DEFCON 30!

# References
* Dib, Alex. "RFID Thief v2.0." July 2018, https://scund00r.com/all/rfid/tutorial/2018/07/12/rfid-theif-v2.html
* Farrell, Michael and Boris Hajduk. "AndProx." July 2021, GitHub, https://github.com/AndProx/AndProx
* Harding, Cory. "ESP-RFID-Tool." March 2018, GitHub, https://github.com/rfidtool/ESP-RFID-Tool
* Kelly, Mike. “Wiegotcha – RFID Thief” January 2017, https://exfil.co/2017/01/17/wiegotcha-rfid-thief/                     
* Rumble, Rich. "RFID Sniffing Under Your Nose and in Your Face." DerbyCon IX, September 2019, https://www.youtube.com/watch?v=y37j6RDtybQ
* W., Viktor. "Enclosure For Proxmark3 Easy." Thingiverse, September 2018, https://www.thingiverse.com/thing:3123482
* White, Brent and Tim Roberts. "Breaking Into Your Building: A Hacker's Guide to Unauthorized Access." NolaCon 2019, May 2019, https://www.youtube.com/watch?v=eft8PElmQZM 
