
Hassle free 3D printing using ESP8266 : This LUA code and Adapter for ESP8266 provides wireless networking for RepRap 3D printers. No wired connection is required during the print job - just stream your Gcode up to the ESP module’s IP address. 

From the day of its launch, the ‘ESP8266’ is under the spotlight of many makers, electronic enthusiasts and hackers. The Creatorbot team was quite impressed with the ESP module and we were curious to see if we could interface this module with our 3D printer. When we decided to do it, I started researching on the tool chain for developing on the ESP module and found that LUA API from NodeMcu would be a good start. The code quality if definitely not perfect but it works fine.
To make it easy to use I have develeopped ESP8266 adapter for RAMPS 3D printer shield using Eagle CAD.
 
Features:
1) WiFi enabled G-Code streaming.
2) Remote control and monitor your printer.
3) Automatically displays the IP address of ESP module on your printer LCD.
4) Same adapter can also be used to connect HC-05 / HC0-06  Bluetooth module to RAMPS 3D printer shield.
 
LUA code:

There are 2 LUA code files in this project, namely init.lua & WIFI_Reset.lua ;  When the ESP module powers up it looks for init.lua and starts executing it. The init.lua first try to connect to wifi network and returns the connection status. There are 5 possible connection statuses and for each status init.lua performs different tasks.
 
< Status Number> Meaning-Task performed

< 0 > STATION_IDLE - Get connection status again.

< 1 > STATION_CONNECTING - Do nothing.

< 2 > STATION_WRONdirtG_PASSWORD -  Executes ‘WIFI_Reset.lua’ file.

< 3 > STATION_NO_AP_FOUND - Executes ‘WIFI_Reset.lua’ file.

< 4 > STATION_CONNECT_FAIL - Executes ‘init.lua’ file once again.

< 5 > STATION_GOT_IP - Displays IP address on LCD / Serial. Monitor and calls the function written for TCP- UART data communication.
 
 
  
The other file is WIFI_Reset.lua, It is executed only when the wifi connection is failed. It first configures the serial connection then asks user to enter WIFI credentials. The user have to open the serial monitor at 9600 baud rate and needs to provide SSID and password in specific format. i.e if your wifi SSID is ‘CreatorBot’ and password is ‘1234’ then enter this data in this format- 
ID:CreatorBot
PW:1234
After receiving new wifi credentials init.lua is loaded for execution. If new wifi credentials are correct then it returns Ip address on your serial monitor.
  

ESP8266 adapter for RAMPS: 

To make it easy to use, i have designed ESP8266 adapter for RAMPS 3D printer shield using Eagle CAD. 
 
Features: 
The adapter has got 3 connectors; one to connect the it on RAMS AUX-1, Second one to plug ESP8266 module-1 on top of adapter and third one for bluetooth HC-05/ HC-06. The user have to connect either ESP module or Bluetooth module, we can't connect and use both at a time.
1) Inbuilt 3.3V regulator for both ESP and Bluetooth.
2) Jumper to flash the node mcu api.
3) On/Off switch.
4) Power indication LED.
 
 
Here are a few steps below to get started:

1) Follow the simple steps explained by Peter Jennings about how to start with ESP8266 using LUA code. It gets you from scratch to loading LUA code onto ESP module.
2) Format the ESP8266 module to load fresh code.
3) Download the LUA code from github repository  and load the files onto ESP8266 module.
4) Make the connections between ESP8266 and 3D printer as shown in the image below or simply use the ESP8266-RAMPS adapter  
 

 
There are 2 ways to get the IP address of your ESP module
1) Turn on your 3D printer, then connect ESP module to your 3D- printer (If you are using adapter just plug it on AUX-1). The IP address will appears on the status line of attached LCD.
2) If your printer doesn’t have the LCD, then connect ESP to PC using USB to Serial adapter and open serial terminal at 9600 baud rate.On restart module displays the IP address on the serial monitor.


Note: Connect the ESP8266 module only after the 3D printer is turned on. Otherwise your printer may freeze due to garbage data communication.

Repetier Host settings:
1) Open the repetier host,
2) Go to ‘printer settings’ 
3) Select Connector as ‘TCP/IP connection’
4) Copy the IP address you got from LCD/ serial terminal.
5) Change port number to 9999
6) Apply the changes and connect.
    
 
Thats it, Now you can control/ print/ monitor your 3D printer on air.. Happy and hassle free printing .. :)
 
 
NOTE: in LUA code default baud rate set is 115200 means set your marlin/Printer firmware accordingly.
