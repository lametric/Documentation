.. device-audio

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
+-----------------------+--------------+-----------------------------------------------------------------------------+
| Property              | Type         | Description                                                                 |
+=======================+==============+=============================================================================+
| ``volume``            | Integer      | Current volume [0..100]                                                     |
+-----------------------+--------------+-----------------------------------------------------------------------------+
| ``volume_range``      | Object       |  *Optional*. Minimum and maximum volume values.                             |
|                       |              |   - ``min`` is the minimum volume value                                     |
|                       |              |   - ``max`` is the maximum volume value                                     |
+-----------------------+--------------+-----------------------------------------------------------------------------+
| ``volume_limit``      | Object       | *Optional*. Volume value limits                                             |
|                       |              |  - ``min`` stands for *lower* volume limit                                  |
|                       |              |  - ``max`` stands for *upper* volume limit                                  |
|                       |              | | Device can limit its volume when it is powered from a computer in order   |
|                       |              | | to limit its power consumption and avoid unexpected power-offs. You will  |
|                       |              | | get error when try to set ``volume`` value that does not fall into        | 
|                       |              | | this range.                                                               |
+-----------------------+--------------+-----------------------------------------------------------------------------+


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
	    "volume" : 69,
	    "volume_range": {
	        "max": 100,
	        "min": 0
	    },	    
	    "volume_limit": {
	        "max": 69,
	        "min": 0
	    }
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
	    "volume" : 69
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
	            "volume" : 69,
	            "volume_range": {
	               "max": 100,
	               "min": 0
	            },	    
	            "volume_limit": {
	               "max": 69,
	               "min": 0
	            }	            
	        }, 
	        "path" : "/api/v2/device/audio" 
	    } 
	}
