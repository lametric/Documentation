Bluetooth
=========

Get Bluetooth State
------------------
================  ===========================================
URL               /api/v2/device/bluetooth                                     
Method            GET                                        
Authentication    basic                                         
================  ===========================================

Description
^^^^^^^^^^^
Returns Bluetooth state.


Response
^^^^^^^^
=======================  =============  ============================================================================
Property                 Type           Description 
=======================  =============  ============================================================================
available                Boolean        Indicates whether device has Bluetooth module on board or not.              
active                   Boolean        Indicates whether Bluetooth module is enabled or not.
discoverable             Boolean        Indicates whether Bluetooth module is visible for other Bluetooth devices 
                                        or not.
pairable                 Boolean        Indicates whether other devices can pair with LaMetric Time.
name                     String         Name of the LaMetric visible via Bluetooth discovery.
mac                      String         LaMetric Time Bluetooth MAC address.
=======================  =============  ============================================================================


Examples
^^^^^^^^

**Request**::

	GET http://192.168.0.239:8080/api/v2/device/bluetooth

**Response**::

	HTTP/1.1 200 OK
	CONTENT-TYPE: application/json;charset=UTF8
	Transfer-Encoding: chunked
	Date: Wed, 29 Jun 2016 15:11:42 GMT
	Server: lighttpd/1.4.35

	{ 
	    "active" : false, 
	    "available" : true, 
	    "discoverable" : false, 
	    "mac" : "58:63:56:23:95:6C", 
	    "name" : "LM0001", 
	    "pairable" : true 
	}

----

Update Bluetooth State
--------------------

================  ===========================================
URL               /api/v2/device/bluetooth                                     
Method            PUT                                        
Authentication    basic                                         
================  ===========================================

Description
^^^^^^^^^^^
Updates Bluetooth state.

Body
^^^^

=======================  =============  ============================================================================
Property                 Type           Description 
=======================  =============  ============================================================================
active                   Boolean        *Optional.*  True – activates Bluetooth module, false – deactivates.
name                     String         *Optional.*  Sets new Bluetooth name
=======================  =============  ============================================================================

**Example**
::

	{
	    "active" : true,
	    "name" : "LaMetric Time"
	}


Response
^^^^^^^^
::

	HTTP/1.1 200 OK
	CONTENT-TYPE: application/json;charset=UTF8
	Transfer-Encoding: chunked
	Date: Wed, 29 Jun 2016 15:23:07 GMT
	Server: lighttpd/1.4.35

	{ 
	    "success" : { 
	        "data" : { 
	            "active" : true, 
	            "available" : true, 
	            "discoverable" : false, 
	            "mac" : "58:63:56:23:95:6C", 
	            "name" : "LaMetric Time", 
	            "pairable" : true 
	        }, 
	        "path" : "/api/v2/device/bluetooth" 
	    } 
	}
