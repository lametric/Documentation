.. device-notifications
    
Notifications
=============

Endpoints
---------

=========  ======================================  =========================================================
Method     Path                                    Description
=========  ======================================  =========================================================
POST       /api/v2/device/notifications            Sends new notification to device
GET        /api/v2/device/notifications            Returns the list of notifications in queue
GET        /api/v2/device/notifications/:id        Returns specific notification
DELETE     /api/v2/device/notifications/:id        Removes notification from queue or dismiss if it is visible
GET        /api/v2/device/notifications/current    Returns current notification (notification that is visible)
=========  ======================================  =========================================================

----

Display Notification
--------------------

==============  ===============================================
URL             /api/v2/device/notifications
Method          POST
Authorization   basic
==============  ===============================================

Description
^^^^^^^^^^^
Sends notification to the device.

Body
^^^^
::

	{
	    "priority": "critical",
	    "model": {
	    	"cycles": 1,
	        "frames": [ 
	        {
	            "icon": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAgAAAAICAYAAADED76LAAAAUklEQVQYlWNUVFBgYGBgYBC98uE/AxJ4rSPAyMDAwMCETRJZjAnGgOlAZote+fCfCV0nOmA0+yKAYTwygJuAzQoGBgYGRkUFBQZ0dyDzGQl5EwCTESNpFb6zEwAAAABJRU5ErkJggg==",
	            "text": "HELLO!"
	        },
	        "sound": {
	    	    "category": "notifications",
	            "id": "cat"
	        }
	    }
	}


Response
^^^^^^^^
Returns success object with notification id.


Response Example
^^^^^^^^^^^^^^^^

200 OK
::

	{
	  "success": {
	    "id": "1"
	  }
	}




----

Get Notification Queue
----------------------

TBD: Work is in progress

----

Modify Notification
-------------------

TBD: Work is in progress


----

Cancel or Dismiss Notification
------------------------------

TBD: Work is in progress

