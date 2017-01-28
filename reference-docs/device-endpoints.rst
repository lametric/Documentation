.. device-endpoints

Endpoints
=========

=========  ======================================  =========================================================
Method     Path                                    Description
=========  ======================================  =========================================================
GET        /api/v2                                 Returns API version and endpoint map
GET        /api/v2/device                          Returns full device state
POST       /api/v2/device/notifications            Sends new notification to device
GET        /api/v2/device/notifications            Returns the list of notifications in queue
GET        /api/v2/device/notifications/current    Returns current notification (notification that is visible)
GET        /api/v2/device/notifications/:id        Returns specific notification
DELETE     /api/v2/device/notifications/:id        Removes notification from queue or dismisses if it is visible
GET        /api/v2/device/display                  Returns information about display, like brightness
PUT        /api/v2/device/display                  Allows to modify display state (change brightness)
GET        /api/v2/device/audio                    Returns current volume
PUT        /api/v2/device/audio                    Allows to change volume
GET        /api/v2/device/bluetooth                Returns bluetooth state
PUT        /api/v2/device/bluetooth                Allows to activate/deactivate bluetooth and change name
GET        /api/v2/device/wifi                     Returns wi-fi state
=========  ======================================  =========================================================


Get API Version
---------------
================  ===========================================
URL               /api/v2                                        
Method            GET                                        
Authentication    basic                                         
================  ===========================================

Description
^^^^^^^^^^^^^^^^^^^^^
Gets information about the current API version. Also returns object map with all endpoints
available on the device.

Response
^^^^^^^^

=======================  =============  ====================================================
Property                 Type           Description 
=======================  =============  ====================================================
api_version              String         Current version of the api in format <major>.<minor>.<patch>
endpoints                Object         Map of available API endpoints
=======================  =============  ====================================================

Response Example
^^^^^^^^^^^^^^^^
::

	HTTP/1.1 200 OK
	CONTENT-TYPE: application/json;charset=UTF8
	Transfer-Encoding: chunked
	Date: Thu, 23 Jun 2016 15:56:42 GMT
	Server: lighttpd/1.4.35

	{ 
	    "api_version" : "2.0.0", 
	    "endpoints" : { 
	        "audio_url" : "http://192.168.0.233:8080/api/v2/device/audio", 
	        "bluetooth_url" : "http://192.168.0.233:8080/api/v2/device/bluetooth", 
	        "concrete_notification_url" : "http://192.168.0.233:8080/api/v2/device/notifications{/:id}", 
	        "current_notification_url" : "http://192.168.0.233:8080/api/v2/device/notifications/current", 
	        "device_url" : "http://192.168.0.233:8080/api/v2/device", 
	        "display_url" : "http://192.168.0.233:8080/api/v2/device/display", 
	        "notifications_url" : "http://192.168.0.233:8080/api/v2/device/notifications", 
	        "widget_update_url" : "http://192.168.0.233:8080/api/v2/widget/update{/:id}", 
	        "wifi_url" : "http://192.168.0.233:8080/api/v2/device/wifi" 
	    } 
	}


----