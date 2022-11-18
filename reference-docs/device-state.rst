.. device-state

Device
======

Get Device State
---------------
================  ===========================================
URL               /api/v2/device                                      
Method            GET                                        
Authentication    basic                                         
================  ===========================================

Description
^^^^^^^^^^^
Returns information about the device like name, serial number, version of the firmware, model etc.
Response also contains state of audio, display, bluetooth and wi-fi.


Parameters
^^^^^^^^^^

=======================  ==========================================================================
Property                 Description 
=======================  ==========================================================================
fields                   Comma separated list of field you want to receive in response. 
                         Possible values are:

                         - id
                         - name
                         - serial_number
                         - os_version
                         - mode
                         - model
                         - audio
                         - display
                         - bluetooth
                         - wifi
=======================  ==========================================================================


Response
^^^^^^^^

=======================  =============  ============================================================================
Property                 Type           Description 
=======================  =============  ============================================================================
id                       String         Id of the device on the cloud
name                     String         User specified name of the device
serial_number            String         Device serial number
os_version               String         Software version in format <major>.<minor>.<patch>
update_available         Object         Since API 2.3.0. Optional. If present, means that firmware upgrade is available for the device.
model                    String         Model number. Can be one of "LM 37X8", "sa8", "sa5"

                                        - *"LM 37X8"* stands for LaMetric TIME devices, produced before 2022.
                                        - *"sa8"* stands for LaMetric TIME devices, produced in 2022 and later
                                        - *"sa5"* snands for LaMetric SKY devices.
mode                     String         Current device mode. Can be one of "auto", "manual", "schedule" or "kiosk"

                                        - *auto* - auto scroll mode, when device switch between apps automatically
                                        - *manual* - click to scroll mode, when user can manually switch between apps
                                        - *schedule* - mode when apps get switched according to a schedule
                                        - *kiosk* - kiosk mode when single app is locked on the device.
audio                    Object         Audio state. Allows to get current volume
bluetooth                Object         Bluetooth state
display                  Object         Display state
wifi                     Object         Wi-Fi state
=======================  =============  ============================================================================


Examples
^^^^^^^^

**Request**::

    GET http://192.168.0.239:8080/api/v2/device
    
    Authorization: Basic <Base64("dev:Device API Key")>
    Accept: application/json

**Response**::

	HTTP/1.1 200 OK
	Content-Type: application/json;charset=UTF8

	{
	    "id" : "1",
	    "name" : "LM0001",
	    "serial_number" : "SA150600000100W00BS9",
	    "mode" : "manual",
	    "model" : "LM 37X8",		
	    "os_version" : "2.3.0",
	    "update_available": {
	        "version": "2.3.1"
	    },
	    "audio" : {
	        "volume" : 100
	    },
	    "bluetooth" : {
	        "available" : true,
	        "name" : "LM0001",
	        "active" : false,
	        "discoverable" : false,
	        "pairable" : true,
	        "address" : "58:63:56:10:FD:2F"     
		},
	    "display" : {
	        "brightness" : 67,
	        "brightness_mode" : "auto",
	      	"width" : 37,
	        "height" : 8,
	        "type" : "mixed"
	    },
	    "wifi" : { 
	        "active" : true,
	        "address" : "58:63:56:10:D6:1F",
	        "available" : true,
	        "encryption" : "WPA", 
	        "essid" : "home-wifi",
	        "ip" : "192.168.0.233",
	        "mode" : "dhcp",
	        "netmask" : "255.255.255.0",
	        "strength" : 100
	    }
	}

----

**Request**::

	GET http://192.168.0.233:8080/api/v2/device?fields=name,wifi

**Response**::

	HTTP/1.1 200 OK
	CONTENT-TYPE: application/json;charset=UTF8
	Transfer-Encoding: chunked
	Date: Thu, 23 Jun 2016 17:06:14 GMT
	Server: lighttpd/1.4.35

	{ 
	    "name" : "LM0001", 
	    "wifi" : { 
	        "active" : true, 
	        "address" : "58:63:56:10:D6:1F", 
	        "available" : true, 
	        "encryption" : "WPA", 
	        "essid" : "home-wifi", 
	        "ip" : "192.168.0.233", 
	        "mode" : "dhcp", 
	        "netmask" : "255.255.255.0", 
	        "strength" : 100 
	    } 
	}


----

Change Device Mode
------------------
================  ===========================================
URL               /api/v2/device
Method            PUT
Authentication    basic
API Version       2.3.1
================  ===========================================

Description
^^^^^^^^^^^
Allows changing device mode to one of four supported ones: manual, auto, schedule, kiosk.

Body
^^^^
::

    {
        "mode": "[manual|auto|schedule|kiosk]"
    }


Response
^^^^^^^^
::
	
    {
        "success" : {
            "data" : { "mode": "[manual|auto|schedule|kiosk]" },
            "path" : "/api/v2/device"
        }
    }

Example. Enable automatic app switching mode
^^^^^^^
**Request**

REST
::

    PUT https://<device ip address>:4343/api/v2/device
    
    Authorization: Basic <Base64("dev:Device API Key")>
    Accept: application/json
    Content-Type: application/json
    
    {
        "mode": "auto"
    }

cURL
::
    $ curl --location --request PUT 'https://192.168.170.14:4343/api/v2/device' \
      -u "dev:<device API key>" -k \
      --header 'Accept: application/json' \
      --header 'Content-Type: application/json' \
      --data-raw '{ "mode": "auto" }'

**Response**
::
    HTTP/1.1 200 OK

    {
        "success": {
            "data": { "mode": "auto" },
            "path": "/api/v2/device"
        }
    }