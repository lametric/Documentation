.. device-endpoints

Endpoints
=========


=========  =================================================  ==============================================================
Method     Path                                               Description
=========  =================================================  ==============================================================
**Introduced in API 2.0.0**
----------------------------------------------------------------------------------------------------------------------------
GET        /api/v2                                            Returns API version and endpoints available
GET        /api/v2/device                                     Returns full device state
POST       /api/v2/device/notifications                       Sends new notification to device
GET        /api/v2/device/notifications                       Returns the list of notifications in queue
GET        /api/v2/device/notifications/current               Returns current notification (notification that is visible)
GET        /api/v2/device/notifications/:id                   Returns specific notification
DELETE     /api/v2/device/notifications/:id                   Removes notification from queue or dismisses if it is visible
GET        /api/v2/device/display                             Returns information about display, like brightness
PUT        /api/v2/device/display                             Allows to modify display state (change brightness)
GET        /api/v2/device/audio                               Returns current volume
PUT        /api/v2/device/audio                               Allows to change volume
GET        /api/v2/device/bluetooth                           Returns bluetooth state
PUT        /api/v2/device/bluetooth                           Allows to activate/deactivate bluetooth and change name
GET        /api/v2/device/wifi                                Returns wi-fi state
**Added in API 2.1.0**
----------------------------------------------------------------------------------------------------------------------------
GET        /api/v2/device/apps                                Returns the list of installed apps
GET        /api/v2/device/apps/:package                       Returns info about installed app identified by package name
PUT        /api/v2/device/apps/next                           Switches to next app
PUT        /api/v2/device/apps/prev                           Switches to previous app
POST       /api/v2/device/apps/:package/widgets/:id/actions   Sends application specific action to widget
PUT        /api/v2/device/apps/:package/widgets/:id/activate  Activates specific widget (app instance)
**Added in API 2.3.0**
----------------------------------------------------------------------------------------------------------------------------
GET        /api/v2/device/stream                              Returns streaming status
PUT        /api/v2/device/stream/start                        Start streaming
PUT        /api/v2/device/stream/stop                         Stop streaming
=========  =================================================  ==============================================================


Get API Version
---------------
================  ===========================================
URL               /api/v2                                        
Method            GET                                        
Authentication    basic
API Version       2.0.0                                         
================  ===========================================

Description
^^^^^^^^^^^
Gets information about the current API version. Also returns object map with all API endpoints
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
	  "api_version": "2.3.0",
	  "endpoints": {
	      "apps_action_url": "http://192.168.88.153:8080/api/v2/device/apps/{:id}/widgets/{:widget_id}/actions",
	      "apps_get_url": "http://192.168.88.153:8080/api/v2/device/apps/{:id}",
	      "apps_list_url": "http://192.168.88.153:8080/api/v2/device/apps",
	      "apps_switch_next_url": "http://192.168.88.153:8080/api/v2/device/apps/next",
	      "apps_switch_prev_url": "http://192.168.88.153:8080/api/v2/device/apps/prev",
	      "apps_switch_url": "http://192.168.88.153:80803/api/v2/device/apps/{:id}/widgets/{:widget_id}/activate",
	      "audio_url": "http://192.168.88.153:8080/api/v2/device/audio",
	      "bluetooth_url": "http://192.168.88.153:8080/api/v2/device/bluetooth",
	      "concrete_notification_url": "http://192.168.88.153:8080/api/v2/device/notifications/{:id}",
	      "current_notification_url": "http://192.168.88.153:8080/api/v2/device/notifications/current",
	      "device_url": "http://192.168.88.153:8080/api/v2/device",
	      "display_url": "http://192.168.88.153:8080/api/v2/device/display",
	      "notifications_url": "http://192.168.88.153:8080/api/v2/device/notifications",
	      "stream_start_url": "http://192.168.88.153:8080/api/v2/device/stream/start",
	      "stream_stop_url": "http://192.168.88.153:8080/api/v2/device/stream/stop",
	      "stream_url": "http://192.168.88.153:8080/api/v2/device/stream",
	      "wifi_url": "http://192.168.88.153:8080/api/v2/device/wifi"
	  }
	}

----