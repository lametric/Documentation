.. device-display

Display
=======

Get Display State
------------------
================  ===========================================
URL               /api/v2/device/display                                     
Method            GET                                        
Authentication    basic                                         
================  ===========================================

Description
^^^^^^^^^^^
Returns information about the display like brightness, mode and size in pixels.


Response
^^^^^^^^

=======================  =============  ============================================================================
Property                 Type           Description 
=======================  =============  ============================================================================
brightness               Integer        Brightness of the display. Valid values [0..100]
brightness_mode          Enum           ["auto", "manual"]

									    - *auto* – automatically adjust brightness
									    - *manual* – brightness is configured by the user
width                    Integer        Width of the display in pixels
height                   Integer        Height of the display in pixels
type                     Enum           Display type. Valid values are : ["monochrome", "grayscale", "color", "mixed"] 
=======================  =============  ============================================================================


Examples
^^^^^^^^

**Request**::

	GET http://192.168.0.239:8080/api/v2/device/display

**Response**::

	HTTP/1.1 200 OK
	CONTENT-TYPE: application/json;charset=UTF8
	Transfer-Encoding: chunked
	Date: Wed, 29 Jun 2016 13:47:05 GMT
	Server: lighttpd/1.4.35

	{ 
	    "brightness" : 100, 
	    "brightness_mode" : "auto", 
	    "width" : 37,
	    "height" : 8, 
	    "type" : "mixed"
	}

----

Update Display State
--------------------

================  ===========================================
URL               /api/v2/device/display                                     
Method            PUT                                        
Authentication    basic                                         
================  ===========================================

Description
^^^^^^^^^^^
Updates display state. It is possible to change ``brightness`` and ``brightness_mode``.
If ``brightness_mode`` is set to "auto", brightness value still can be changed but this will not affect the actual brightness of the display. Brightness will be changed as soon as ``brightness_mode`` is set to "manual".

Body
^^^^
::

	{
	    "brightness" : 50,
	    "brightness_mode" : "manual"
	}


Response
^^^^^^^^
::

	HTTP/1.1 200 OK
	CONTENT-TYPE: application/json;charset=UTF8
	Transfer-Encoding: chunked
	Date: Wed, 29 Jun 2016 14:25:48 GMT
	Server: lighttpd/1.4.35

	{ 
	    "success" : { 
	        "data" : { 
	            "brightness" : 50, 
	            "brightness_mode" : "manual", 
	            "height" : 8, 
	            "type" : "mixed", 
	            "width" : 37 
	        }, 
	        "path" : "/api/v2/device/display" 
	    } 
	}
