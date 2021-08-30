## Please note that I have decided to replace SmartThings in favor of a Zigbee/Zwave USB stick connected directly my Home Assistant server. This device handler's code is available for anyone to review/modify, but I will no longer participate in its development. Thank you ##

# WLED-SmartThings
SmartThings Device handler for WLED

 - In the SmarThings IDE, go to “My device handlers”
 - Create new device handler
 - From Code
 - Paste the code of the device handler file
 - Click Create, then save and Publish for me


Then, click on “My devices”, and

 - +New device
 - Give it a name (Desk lamp or whatever)
 - Copy name to Device Network ID
 - Type: go all the way to the bottom to find WLED
 - Version: Published
 - Select your location
 - Select your hub
 - Click “Create”


Now open the ST app. That device should now be available, open it. Go to the setting gear, enter the IP address of the ESP, port (80 by default), save.

Please note that this was custom made for my needs, and that on/off, color and brightness are working. None of the effects etc were implemented. Also confirmed to work with Google Home when linked to ST.
