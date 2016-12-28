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
You must send a Notification object.

**Notification object**

====================  ===============  ===========================================================
Property              Type             Description
====================  ===============  ===========================================================
model                 Object           Message structure and data.
priority              Enum             *Optional.* Valid values are "info", "warning", "critical"
icon_type             Enum             *Optional.* Valid values: "none", "info", "alert"
lifetime              Integer          *Optional.* Lifetime of the message in milliseconds.
====================  ===============  ===========================================================

**Detailed Properties Description**

- model 
   Object that represents message structure and data. It consists of "frames", "sound" and "cycles" properties.

   - *frames* – array, that describes the notification structure. Single frame can be *simple*, *goal* or *spike chart*.
      
      - *simple* frame consists of icon and text. Example::
       
         {
            "icon":"<icon_id or binary>",
            "text":"Message"
         }

      - *goal* frame consists of icon and goal data. Example::

         { 
           "icon":"i120",
           "goalData":{
             "start": 0,
             "current": 50,
             "end": 100,
             "unit": "%"
            }
         }

      - *spike chart* consists of array of numbers and is displayed as graph. Example:: 

         {
            "chartData": [ 1, 2, 3, 4, 5, 6, 7 ]
         }



   - *sound* – object that describes the notification sound to play when notification pops on the LaMetric Time's screen. Example::

      {
    	"category":"notifications",
        "id":"cat",
        "repeat":1
      }

     - *category* – sound category. Can be *notifications* or *alarms*.
     - *id* – sound ID. Full list of notification ids::
			
		bicycle         
		car            
		cash           
		cat             
		dog             
		dog2           
		energy         
		knock-knock
		letter_email
		lose1
		lose2
		negative1
		negative2
		negative3
		negative4
		negative5
		notification
		notification2
		notification3
		notification4
		open_door
		positive1
		positive2
		positive3
		positive4
		positive5
		positive6
		statistic
		thunder
		water1
		water2
		win
		win2
		wind
		wind_short

       Full list of alarm ids::

		alarm1
		alarm2
		alarm3
		alarm4
		alarm5
		alarm6
		alarm7
		alarm8
		alarm9
		alarm10
		alarm11
		alarm12
		alarm13       

     - *repeat* – defines the number of times sound must be played. If set to 0 sound will be played until notification is dismissed. By default the value is set to 1.

   - *cycles* – the number of times message should be displayed. If *cycles* is set to 0, notification will stay on the screen until user dismisses it manually or you can dismiss it via the API (DELETE /api/v2/device/notifications/:id). By default it is set to 1.

- priority
   Priority of the message
   
   - *info* – this priority means that notification will be displayed on the same "level" as all other notifications on the device that come from apps (for example facebook app). This notification will not be shown when screensaver is active. By default message is sent with "info" priority. This level of notification should be used for notifications like news, weather, temperature, etc.

   - *warning* – notifications with this priority will interrupt ones sent with lower priority ("info"). Should be used to notify the user about something important but not critical. For example, events like "someone is coming home" should use this priority when sending notifications from smart home.

   - *critical* – the most important notifications. Interrupts notification with priority *info* or *warning* and is displayed even if screensaver is active. Use with care as these notifications can pop in the middle of the night. Must be used only for really important notifications like notifications from smoke detectors, water leak sensors, etc. Use it for events that require human interaction immediately.

- icon_type
    Represents the nature of notification.

    - *none* – no notification icon will be shown.
    - *info* – "i" icon will be displayed prior to the notification. Means that notification contains information, no need to take actions on it.
    - *alert* – "!!!" icon will be displayed prior to the notification. Use it when you want the user to pay attention to that notification as it indicates that something bad happened and user must take immediate action.

- lifetime
    The time notification lives in queue to be displayed in milliseconds. Default lifetime is 2 minutes. If notification stayed in queue for longer than *lifetime* milliseconds – it will not be displayed.




**Example**::

	{
	    "priority": "critical",
	    "model": {
	    	"cycles": 1,
	        "frames": [ 
	        {
	            "icon": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAgAAAAICAYAAADED76LAAAAUklEQVQYlWNUVFBgYGBgYBC98uE/AxJ4rSPAyMDAwMCETRJZjAnGgOlAZote+fCfCV0nOmA0+yKAYTwygJuAzQoGBgYGRkUFBQZ0dyDzGQl5EwCTESNpFb6zEwAAAABJRU5ErkJggg==",
	            "text": "HELLO!"
	        }],
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

==============  ===============================================
URL             /api/v2/device/notifications
Method          GET
Authorization   basic
==============  ===============================================

Description
^^^^^^^^^^^
Returns the list of all notifications in the queue. Notifications with higher priority will be first in the list.


Response
^^^^^^^^
Returns array of *Notification* objects with additional fields like *created*, *exporation_date* and *type*.


Response Example
^^^^^^^^^^^^^^^^

200 OK
::

	[
	  {
	    "id": "50",
	    "type": "external",
	    "priority": "info",
	    "created": "2016-06-28T14:52:55",
	    "expiration_date": "2016-06-28T14:54:55",
	    "model": {
	      "frames": [
	        {
	          "text": "HI!"
	        }
	      ]
	    }
	  }
	]


----


Cancel or Dismiss Notification
------------------------------

==============  ===============================================
URL             /api/v2/device/notifications/:id
Method          DELETE
Authorization   basic
==============  ===============================================

Description
^^^^^^^^^^^
Removes notification from the queue or in case if it is already visible - dismisses it.


Response
^^^^^^^^
Returns object with result.


Response Example
^^^^^^^^^^^^^^^^

200 OK
::
	{
	  "success": true
	}
