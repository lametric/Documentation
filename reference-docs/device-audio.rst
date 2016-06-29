Audio
=====

Get Audio State
------------------
================  ===========================================
URL               /api/v2/device/audio                                     
Method            GET                                        
Authentication    basic                                         
================  ===========================================

Description
^^^^^^^^^^^
Returns audio state such as volume.


Response
^^^^^^^^
=======================  =============  ============================================================================
Property                 Type           Description 
=======================  =============  ============================================================================
volume                   Integer        Current volume [0..100]
=======================  =============  ============================================================================


Examples
^^^^^^^^

**Request**::

	GET http://192.168.0.239:8080/api/v2/device/audio

**Response**::

	HTTP/1.1 200 OK
	CONTENT-TYPE: application/json;charset=UTF8
	Transfer-Encoding: chunked
	Date: Wed, 29 Jun 2016 14:56:31 GMT
	Server: lighttpd/1.4.35

	{ 
	    "volume" : 100 
	}

----

Update Audio State
--------------------

================  ===========================================
URL               /api/v2/device/audio                                     
Method            PUT                                        
Authentication    basic                                         
================  ===========================================

Description
^^^^^^^^^^^
Updates audio state.

Body
^^^^
::

	{
	    "volume" : 100
	}


Response
^^^^^^^^
::

	HTTP/1.1 200 OK
	CONTENT-TYPE: application/json;charset=UTF8
	Transfer-Encoding: chunked
	Date: Wed, 29 Jun 2016 14:59:15 GMT
	Server: lighttpd/1.4.35

	{ 
	    "success" : { 
	        "data" : { 
	            "volume" : 100
	        }, 
	        "path" : "/api/v2/device/audio" 
	    } 
	}
