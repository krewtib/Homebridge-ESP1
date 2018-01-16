# modified homebridge-http for use with esp8266 server

# homebridge-esp1

Supports https devices on the HomeBridge Platform and provides a readable callback for getting the "On" and brightness level characteristics to Homekit.

# Installation

1. Install homebridge using: npm install -g homebridge
2. Install homebridge-esp1 using: npm install -g homebridge-esp1
3. Update your config.json file. 
   See sample-config.json in this repository for a sample. 

# Configuration

This module has recently been updated to support an additional method to read the power state of the device and the brightness level. Specify the `status_url` in your config.json that returns the status of the device as an integer (0 = off, 1 = on). 

In the latest version you can use custom status responses beyond 0 and 1

For example include these in config.json, these work with motion, exchange for what you get from your status url.
"status_on": "ACTIVE",
"status_off": "PAUSE",

On and off statuses also support JSON responses. If you need a more complex way to tell if your accessory is in an on state have it send a JSON object back that matches what you specify in the config file.
Example:
```
"status_on": {
    "speaker": "ON",
    "playlist": "Top Hits",
    "playmode": "PLAY"
}
```
Note that the response can contain more properties than what is specified, if all of the properties in the config object have matching properties in the response than it will be considered a match.

Specify the `brightnesslvl_url` to return the current brightness level as an integer.

Switch Handling and brightness Handling support 3 methods, yes for polling on app load, realtime for constant polling or no polling

Configuration sample:

 ```
"accessories": [
       {"accessory": "esp1",
        "name": "kerze",
        "on_url": "http://192.168.0.158/servo?value=190",
        "off_url": "http://192.168.0.158/servo?value=195", 
        "http_method": "GET"
        },
        {"accessory": "esp1",
         "name": "zeit",
         "on_url": "http://192.168.0.158/servo?value=191",
         "off_url": "http://192.168.0.158/servo?value=195",         
         "http_method": "GET"
        }      
]
```

# ToDo

Complete documentation
