.. device-display

Display
=======

Endpoints
---------

========= ====================================================== ============================================
Method    Path                                                   Description
========= ====================================================== ============================================
GET       `/api/v2/device/display <#get-display-state>`_         Returns display state  
PUT       `/api/v2/device/display <#update-display-state>`_      Changes display state
========= ====================================================== ============================================


.. _/api/v2/device/display:

Get Display State
------------------
================  ===========================================
URL               /api/v2/device/display                                     
Method            GET                                        
Authentication    basic
Version           2.0.0                                         
================  ===========================================

Description
^^^^^^^^^^^
Returns information about the display like brightness, mode and size in pixels. Since version 2.1.0 returns information about screen saver settings.


Response
^^^^^^^^
::

	{
	  "brightness": <0-100>,
	  "brightness_mode": "[auto|manual]",
	  "height": 8,
	  "width": 37,
	  "type": "mixed"
	}


Since version 2.1.0 ``screensaver`` node has been added::
	
	{
	  "brightness": <0-100>,
	  "brightness_mode": "[auto|manual]",
	  "brightess_limit": {
	    "max": 75,
	    "min": 2
	  }
	  "brightness_range": {
	   "max": 100
	   "min": 0
	  }
	  "height": 8,
	  "width": 37,
	  "type": "mixed",
	  "screensaver": {
	    "enabled": [true|false],
	    "modes": {
	      "time_based": {
	        "enabled": [true|false]
	        "start_time": "<time in GMT>"
	        "end_time": "<time in GMT>",
	        "local_start_time": "<local time>",
	        "local_end_time": "<local time>"
	      },
	      "when_dark": {
	        "enabled": [true|false]
	      }
	    },
	    "widget": "<widget_uuid>"
	  }
	}


+----------------------+----------------+----------------------------------------------------------------------------+
| Property             | Type           |  Description                                                               |
+======================+================+============================================================================+
| ``brightness``       | Integer        |  Brightness of the display. Valid values [0..100]                          |
+----------------------+----------------+----------------------------------------------------------------------------+
| ``brighrness_mode``  | Enum           | ["auto", "manual"]                                                         |
|                      |                |  - *auto* – automatically adjust brightness                                | 
|                      |                |  - *manual* – brightness is configured by the user                         |
+----------------------+----------------+----------------------------------------------------------------------------+
| ``width``            | Integer        |  Width of the display in pixels                                            |
+----------------------+----------------+----------------------------------------------------------------------------+
| ``height``           | Integer        |  Height of the display in pixels                                           |
+----------------------+----------------+----------------------------------------------------------------------------+
| ``type``             | Enum           |  Display type. Valid values are : ["monochrome", "grayscale", "color",     | 
|                      |                |  "mixed"]                                                                  |
+----------------------+----------------+----------------------------------------------------------------------------+



**Since API version 2.1.0**

+----------------------+----------------+----------------------------------------------------------------------------+
| ``screensaver``      | Object	        | Object for screensaver configuration (off, when dark, timebased).          |
+----------------------+----------------+----------------------------------------------------------------------------+
| ``brightness_range`` | Object         | *Optional*.                                                                |
|                      |                |                                                                            |
|                      |                | | The minimum and the maximum values of a brightness.                      |
|                      |                | | When setting new brightness, the new value must be in this range.        |
|                      |                | | Usually valid values fall between 0 and 100.                             |
+----------------------+----------------+----------------------------------------------------------------------------+
| ``brightness_limit`` | Object         | *Optional*.                                                                |
|                      |                |                                                                            |
|                      |                | | Brightnesss limitations for current conditions.                          | 
|                      |                | | When a device is powered from a computer, we can limit the maximum       |
|                      |                | | brightness value in order to not exceed the maximum power consumption of |  
|                      |                | | a device to avoid unexpected power-offs. In this case the new value of   | 
|                      |                | | brightness can not exceed the *max* value of this limit.                 |
+----------------------+----------------+----------------------------------------------------------------------------+



**Screensaver**

=======================  =============  ============================================================================
Property                 Type           Description 
=======================  =============  ============================================================================
``enabled``              Boolean        Enables or disables the screensaver. 
``modes``                Map            Map of modes supported by the device. Currently "time_based" and "when_dark"
                                        are supported

                                        - *time_based* – activates if time is between start_time and end_time 
                                        - *when_dark* – activates when light sensor senses darkness.
``widget``               String         UUID of the widget that should be activated when screensaver is active. 
                                        Currently clock is supported.
=======================  =============  ============================================================================

**brightness_range**

=======================  =============  ============================================================================
Property                 Type           Description 
=======================  =============  ============================================================================
``max``                  Integer        Maximum possible brightness value
``min``                  Integer        Minimum possible brightness value
=======================  =============  ============================================================================


**brightness_limit**

=======================  =============  ============================================================================
Property                 Type           Description 
=======================  =============  ============================================================================
``max``                  Integer        Current maximum brightness value limit. Can be less than *max* value of 
                                        ``brightness_range`` (for example, due to the power comsumption limitation).
``min``                  Integer        Current minimum brightness value limit
=======================  =============  ============================================================================


Example
^^^^^^^

**Request**::

	GET https://<device ip address>:4343/api/v2/device/display

cURL::

	$ curl -X GET -u "dev" -k \
	  -H "Accept: application/json" \
	  https://<device ip address>:4343/api/v2/device/display
	$ Enter host password for user 'dev': <device API key>

**Response**::

	HTTP/1.1 200 OK
	CONTENT-TYPE: application/json;charset=UTF8
	Transfer-Encoding: chunked
	Date: Wed, 29 Jun 2016 13:47:05 GMT
	Server: lighttpd/1.4.35

	{
	  "brightness": 100,
	  "brightness_limit": {
	    "max": 100,
	    "min": 2
	  },
	  "brightness_range": {
	    "max": 100,
	    "min": 0
	  },
	  "brightness_mode": "auto",
	  "height": 8,
	  "width": 37,
	  "type": "mixed",
	  "screensaver": {
	    "enabled": true,
	    "modes": {
	      "time_based": {
	        "enabled": true,
	        "end_time": "18:42:56",
	        "start_time": "18:41:53"
	        "start_local_time": "20:41:53"
	        "end_local_time": "20:42:56"
	      },
	      "when_dark": {
	        "enabled": false
	      }
	    },
	    "widget": "08b8eac21074f8f7e5a29f2855ba8060"
	  }
	}

----


.. _GET/api/v2/device/display:

Update Display State
--------------------

================  ===========================================
URL               /api/v2/device/display                                     
Method            PUT                                        
Authentication    basic      
Version           2.0.0                                   
================  ===========================================

Description
^^^^^^^^^^^
Updates display state. It is possible to change brightness, mode and screen saver settings.
If ``brightness_mode`` is set to "auto", brightness value still can be changed but this will not affect the actual brightness of the display. Brightness will be changed as soon as ``brightness_mode`` is set to "manual".
Since API 2.1.0 it is possible to configure screensaver settings. 

Body
^^^^
::

    {
        "brightness": <0-100>,
        "brightness_mode": "[auto|manual]"
    }

Since API 2.1.0::

    {
        "brightness": <0-100>,
        "brightness_mode": "[auto|manual]",
        "screensaver": {
            "enabled": [true|false],
            "mode": ["when_dark"|"time_based"]
            "mode_params": {
                "enabled": [true|false],
                "start_time": "21:00:00",
                "end_time": "06:00:00"
            }
        }
    }

Examples
^^^^^^^^

Example 1. Let's set auto brightness and enable screensaver in mode "when dark":

**Request**

REST::
	
    PUT https://<device ip address>:4343/api/v2/device/display

    Content-Type: application/json
    Accept: application/json

    {
        "brightness_mode": "auto",
        "screensaver": {
            "enabled" : true,
            "mode": "when_dark",
            "mode_params": {
                "enabled": true
            }
        }
    }

cURL::

    $ curl -X PUT -k -u "dev" \
      -H "Accept: application/json" 
      -H "Content-Type: application/json" \
      -d '{
            "brightness_mode": "auto",
            "screensaver": {
                "enabled" : true,
                "mode": "when_dark",
                "mode_params": {
                    "enabled": true
                }
            }
        }' https://<device ip address>:4343/api/v2/device/display
    $ Enter host password for user 'dev': <device API key>


**Response**
::
	
    HTTP/1.1 200 OK
    CONTENT-TYPE: application/json;charset=UTF8
    Transfer-Encoding: chunked
    Date: Wed, 29 Jun 2016 14:25:48 GMT
    Server: lighttpd/1.4.35

    {
        "success": {
            "data": {
                "brightness": 40,
                "brightness_mode": "auto",
                "height": 8,               
                "type": "mixed",
                "width": 37                
            },
            "path": "/api/v2/device/display"
        }
    }

Since API 2.1.0::

    HTTP/1.1 200 OK
    CONTENT-TYPE: application/json;charset=UTF8
    Transfer-Encoding: chunked
    Date: Thu, 02 Mar 2017 16:24:18 GMT
    Server: lighttpd/1.4.35

    {
        "success": {
            "data": {
                "type": "mixed",
                "width": 37
                "height": 8,
                "brightness": 40,
                "brightness_mode": "auto",                
                "brightness_range": {
                    "max": 100,
                    "min": 0
                },
                "brightness_limit": {
                    "max": 100,
                    "min": 2
                },
                "screensaver": {
                   "enabled": true,
                    "modes": {
                        "time_based": {
                            "enabled": true,
                            "end_time": "09:21:00",
                            "local_end_time": "12:21:00",
                            "local_start_time": "12:20:00",
                            "start_time": "09:20:00"
                        },
                        "when_dark": {
                            "enabled": false
                        }
                    },
                   "widget": "486f5adeee1511ebab78273c1141c9c8"
                },
            },
            "path": "/api/v2/device/display"
        }
    }

Example 2. Let's set time based screensaver from 9:00 PM to 6:00 AM. First of all, we need to convert our times to GMT.
For example, if we are in GMT+2 timezone, we need to set activation time to 19:00 and deactivation time to 4:00 (subtract 2 hours from
9 pm and 6 am)

**Request**

REST::
    
    PUT https://<device ip address>:4343/api/v2/device/display

    Content-Type: application/json
    Accept: application/json

    {
        "screensaver": {
            "enabled" : true,
            "mode": "time_based",
            "mode_params": {
                "enabled": true,
                "start_time": "19:00:00",
                "end_time": "04:00:00"
            }
        }
    }

cURL::

    $ curl -X PUT -k -u "dev" \
      -H "Accept: application/json" 
      -H "Content-Type: application/json" \
      -d '{
            "screensaver": {
                "enabled" : true,
                "mode": "time_based",
                "mode_params": {
                    "enabled": true,
                    "start_time": "19:00:00",
                    "end_time": "4:00:00"
                }
            }
        }' https://<device ip address>:4343/api/v2/device/display
    $ Enter host password for user 'dev': <device API key>


**Response**
::
    
    HTTP/1.1 200 OK
    CONTENT-TYPE: application/json;charset=UTF8
    Transfer-Encoding: chunked
    Date: Wed, 29 Jun 2016 14:25:48 GMT
    Server: lighttpd/1.4.35

    {
        "success": {
            "data": {
                "brightness": 40,
                "brightness_mode": "auto",
                "height": 8,               
                "type": "mixed",
                "width": 37
            },
            "path": "/api/v2/device/display"
        }
    }

Since API 2.1.0::

    HTTP/1.1 200 OK
    CONTENT-TYPE: application/json;charset=UTF8
    Transfer-Encoding: chunked
    Date: Thu, 02 Mar 2017 16:24:18 GMT
    Server: lighttpd/1.4.35

    {
        "success": {
            "data": {
                "type": "mixed",
                "width": 37
                "height": 8,
                "brightness": 100,
                "brightness_mode": "auto",
                "brightness_range": {
                    "max": 100,
                    "min": 0
                },
                "brightness_limit": {
                    "max": 100,
                    "min": 2
                },                
                "screensaver": {
                    "enabled": true,
                    "modes": {
                        "time_based": {
                            "enabled": true,
                            "start_time": "19:00:00"
                            "end_time": "4:00:00",
                            "local_start_time": "6:00:00",
                            "local_end_time": "21:00:00"                            
                        },
                        "when_dark": {
                            "enabled": false
                        }
                    },
                    "widget": "08b8eac21074f8f7e5a29f2855ba8060"
                },

            },
            "path": "/api/v2/device/display"
        }
    }

Note:
  All timestamps must be given in GMT.
