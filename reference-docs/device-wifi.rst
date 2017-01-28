.. device-wifi

Wi-Fi
=====

Get Wi-Fi State
------------------
================  ===========================================
URL               /api/v2/device/wifi                                     
Method            GET                                        
Authentication    basic                                         
================  ===========================================

Description
^^^^^^^^^^^
Returns Wi-Fi state.


Response
^^^^^^^^
=======================  =============  ============================================================================
Property                 Type           Description 
=======================  =============  ============================================================================
available                Boolean        Indicates whether device has Wi-Fi module on board or not.              
active                   Boolean        Indicates whether Wi-Fi is active or not.
encryption               Enum           Wi-Fi encryption – ["OPEN", "WEP", "WPA", "WPA2"]
ipv4                     String         IP address of LaMetric Time in local network
mac                      String         Mac address of Wi-Fi module
mode                     Enum           ["static", "dhcp"]
netmask                  String         Network mask
signal_strength          Integer        Quality of Wi-Fi signal in range between [0..100]
ssid                     String         Name of the Wi-Fi hotspot device is connected to
=======================  =============  ============================================================================


Examples
^^^^^^^^

**Request**::

	GET http://192.168.0.239:8080/api/v2/device/wifi

**Response**::

	HTTP/1.1 200 OK
	CONTENT-TYPE: application/json;charset=UTF8
	Transfer-Encoding: chunked
	Date: Wed, 29 Jun 2016 15:31:24 GMT
	Server: lighttpd/1.4.35

	{ 
	    "available" : true,
	    "active" : true, 
	    "encryption" : "WPA", 
	    "ipv4" : "192.168.0.225", 
	    "mac" : "58:63:56:23:6E:5C", 
	    "mode" : "dhcp", 
	    "netmask" : "255.255.255.0", 
	    "signal_strength" : 100, 
	    "ssid" : "homewifi" 
	}
