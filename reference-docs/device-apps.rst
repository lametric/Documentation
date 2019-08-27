.. device-display

Apps
=====

Apps API allows you to control some aspects of your LaMetric Time device that is related to apps that are running on it. For example, you will be able to switch between apps as well as configure alarm, control timers, radio and more.

Endpoints
---------

========= ==================================================== ============================================
Method    Path                                                 Description
========= ==================================================== ============================================
GET       `/api/v2/device/apps`_                               Returns the list of installed apps
PUT       `/api/v2/device/apps/next`_                          Switches to next app
PUT       `/api/v2/device/apps/prev`_                          Switches to previous app
GET       `/api/v2/device/apps/:package`_                      Returns info about installed app identified by package name
POST      `/api/v2/device/apps/:package/widgets/:id/actions`_  Sends application specific action to a widget
PUT       `/api/v2/device/apps/:package/widgets/:id/activate`_ Activates specific widget (app instance)
========= ==================================================== ============================================


-----

.. _/api/v2/device/apps:

Get List of Apps
----------------

================  ===========================================
URL               /api/v2/device/apps                                    
Method            GET                                        
Authorization     basic
API Version       2.1.0                                         
================  ===========================================

Description
^^^^^^^^^^^
Returns apps currently installed on LaMetric Time. Each app is identified by package name. Device can run multiple instances of an app. These instances are called widgets. There are at least one widget (instance) running for each app. 

Response
^^^^^^^^
::

    {
        "<package1>" : {
          "package": "<package1>",
          "vendor" : "<vendor>",
          "version" : "<version>",
          "version_code" : "<version_code>",
          "widgets" : {
            "<widget_uuid>" : {
              "index":<position>,
              "package": "<package1>"
            }
          },
          "actions" : {
            "<action1>" : {
              "<action_name1>" : {
                   "<param1>" : {
                      "data_type" : "<bool|int|string">,
                      "name" : "<param name">,
                      "format": "<regexp">,
                      "required": <bool>
                   }
              }
            }
          }
        },
        ...
        "<package_n>" : <app_object_n>
    }

Please refer to `/api/v2/device/apps/:package`_ for more details on Application object.

Example
^^^^^^^
**Request**

REST::

    GET https://<device ip address>:4343/api/v2/device/apps

    Accept: application/json

cURL::

    $ curl -X GET -u "dev" -k -H "Accept: application/json" \ 
      https://<device ip address>:4343/api/v2/device/apps
    $ Enter host password for user 'dev': <device api key>

**Response**
::
    
        {
            "com.lametric.clock": {
                "package": "com.lametric.clock",
                "vendor": "LaMetric",
                "version": "1.0.19",
                "version_code": "31",
                "actions": {
                    "clock.alarm": {
                        "enabled": {
                          "data_type": "bool",
                          "name": "enabled",
                          "required": false
                        },
                        "time": {
                          "data_type": "string",
                          "format": "[0-9]{2}:[0-9]{2}(?::[0-9]{2})?",
                          "name": "time",
                          "required": false
                        },
                        "wake_with_radio": {
                          "data_type": "bool",
                          "name": "wake_with_radio",
                          "required": false
                        }
                    }
                },
                "widgets": {
                      "08b8eac21074f8f7e5a29f2855ba8060": {
                          "index": 0,
                          "package": "com.lametric.clock"
                      }
                }
            },
            "com.lametric.countdown": {
                ...
            },
            "com.lametric.radio": {
                ...
            },
            "com.lametric.stopwatch": {
                ...
            },
            "com.lametric.weather": {
                ...
            }
        }

------

.. _/api/v2/device/apps/next:

Switch to Next App
------------------

================  ===========================================
URL               /api/v2/device/apps/next                                  
Method            PUT                                        
Authorization     basic
API Version       2.1.0                                         
================  ===========================================

Description
^^^^^^^^^^^
Allows to switch to the next app on LaMetric Time. App order is controlled by the user via LaMetric Time app.

Body
^^^^
Does not require body.

Response
^^^^^^^^
::
  
    {
        "success": {
            "data" {},
            "path": "<endpoint>"
        }
    }

or ::

    {
        "errors" : [
          {
            "message" : "<Error message>"
          }
        ]
    }

Example
^^^^^^^
**Request**

REST::

    PUT https://<device ip address>:4343/api/v2/device/apps/next

cURL::

    $ curl -X PUT -u "dev" -H "Accept: application/json"-k \
      https://<device ip address>:4343/api/v2/device/apps/next 
    $ Enter host password for user 'dev': <device api key>

**Response**::

        {
            "success": {
                "data": {},
                "path": "/api/v2/device/apps/next"
            }            
        }

------


.. _/api/v2/device/apps/prev:

Switch to Previous App
----------------------

================  ===========================================
URL               /api/v2/device/apps/prev                                  
Method            PUT                                        
Authorization     basic
API Version       2.1.0                                         
================  ===========================================

Description
^^^^^^^^^^^
Allows to switch to the previous app on LaMetric Time. App order is controlled by the user via LaMetric Time app.

Body
^^^^
Does not require body.

Response
^^^^^^^^
::
  
    {
        "success": {
            "data" {},
            "path": "<endpoint>"
        }
    }

or ::

    {
        "errors" : [
          {
            "message" : "<Error message>"
          }
        ]
    }

Example
^^^^^^^
**Request**

REST::

    PUT https://<device ip address>:4343/api/v2/device/apps/prev

cURL::

    $ curl -X PUT -u "dev" -H "Accept: application/json" -k \
      https://<device ip address>:4343/api/v2/device/apps/prev
    $ Enter host password for user 'dev': <device api key>

**Response**
::
  
        {
            "success": {
                "data": {},
                "path": "/api/v2/device/apps/prev"
            }            
        }

----


.. _/api/v2/device/apps/:package: 

Get Specific App Details
-------------------------

================  ===========================================
URL               /api/v2/device/apps/:package                                
Method            GET                                        
Authorization     basic
API Version       2.1.0                                         
================  ===========================================

Description
^^^^^^^^^^^
Returns information about currently installed app identified by the package.

Response
^^^^^^^^
::

    {
        "package": "<string>",
        "vendor": "<string>",
        "version": "<x.x.x>",
        "version_code": "<version code>",
        "actions": {
            "<action_id>": {
                "<parameter_id>": {
                  "data_type": "[bool, int, string]",
                  "name": "<string>",
                  "required": <boolean>,
                  "format": "<regexp>"
                }
            }
        },
        "widgets": {
              "<uuid>": {
                  "index": <order no>,
                  "package": "<string>"
              }
        }
    }


================ =============== ===========================================================
**Application Object**
--------------------------------------------------------------------------------------------
**Field**        **Type**        **Description**
---------------- --------------- -----------------------------------------------------------
``package``      String          Unique identifier of LaMetric Time native app.
``vendor``       String          Name of the app creator
``version``      String          Version in format "<major>.<minor>.<patch>". For example 2.0.0 or 2.0.1
``version_code`` String          Version as number, like 1, 2, 3. Useful for easy comparison
``actions``      Map             Map of actions this app supports. 
                                 For example, clock support action that allows to configure alarm.
``widgets``      Map             Map of Widgets. Widget is an instance of an app.                                 
                                 For example, if you clone Clock app, you'll get two widgets 
                                 representing each clock instance.                                 
================ =============== ===========================================================


================ =============== ===========================================================
**Parameter Object**
--------------------------------------------------------------------------------------------
**Field**        **Type**        **Description**
---------------- --------------- -----------------------------------------------------------
``data_type``    String          One of [bool, int, string]
``name``         String          Name of the parameter
``required``     Boolean         ``true`` if parameter is required or ``false`` otherwise
``format``       String          Optional. Regext that defines the format of string parameter.
================ =============== ===========================================================


================ =============== ===========================================================
**Widget Object**
--------------------------------------------------------------------------------------------
**Field**        **Type**        **Description**
---------------- --------------- -----------------------------------------------------------
``index``        Integer         Position of the widget when switching between them with buttons or API. Can be -1.
``package``      String          Id of the LaMetric Time app this widget is an instance of
================ =============== ===========================================================


Example
^^^^^^^

**Request**

REST::
    
    GET https://<device ip address>:4343/api/v2/device/apps/com.lametric.clock

    Accept: application/json


cURL::

    $ curl -X GET -u "dev" -H "Accept: application/json" -k \
      https://<device ip address>:4343/api/v2/device/apps/com.lametric.clock 
    $ Enter host password for user 'dev': <device api key>

**Response**::
    
    {
        "package": "com.lametric.clock",
        "vendor": "LaMetric",
        "version": "1.0.19",
        "version_code": "31",
        "actions": {
            "clock.alarm": {
                "enabled": {
                  "data_type": "bool",
                  "name": "enabled",
                  "required": false
                },
                "time": {
                  "data_type": "string",
                  "format": "[0-9]{2}:[0-9]{2}(?::[0-9]{2})?",
                  "name": "time",
                  "required": false
                },
                "wake_with_radio": {
                  "data_type": "bool",
                  "name": "wake_with_radio",
                  "required": false
                }
            }
        },
        "widgets": {
              "08b8eac21074f8f7e5a29f2855ba8060": {
                  "index": 0,
                  "package": "com.lametric.clock"
              }
        }
    }

----


.. _/api/v2/device/apps/:package/widgets/:id/actions:

Interact With Running Widgets
-----------------------------

================  =======================================================
URL               /api/v2/device/apps/:package/widgets/:id/actions                             
Method            POST                                        
Authorization     basic
API Version       2.1.0                                         
================  =======================================================

Description
^^^^^^^^^^^
Using this endpoint you can control LaMetric Time apps. Each app provides its own set of actions you can use. For example, you can start or stop radio playback, start, pause, reset timers, configure alarm clock etc.
To execute an action just send an Action object in the body of the request to the endpoint like this:
::
  
    {
      "id" : "<action_id>"    
    }


Here are some actions of preinstalled apps:

====================== ========================== ======================================================
**App Name**           **Package**                **Action Id**
---------------------- -------------------------- ------------------------------------------------------
Alarm Clock            ``com.lametric.clock``     | ``clock.alarm`` - configure alarm clock  
                                                  | ``clock.clockface`` - sets or updates a clock face

Radio                  ``com.lametric.radio``     | ``radio.play`` - start playback
                                                  | ``radio.stop`` - stop playback
                                                  | ``radio.next`` - next radio station
                                                  | ``radio.prev`` - previous radio station

Timer                  ``com.lametric.countdown`` | ``countdown.configure`` - set time
                                                  | ``countdown.start`` - starts countdown
                                                  | ``countdown.pause`` - pauses countdown
                                                  | ``countdown.reset`` - resets timer

Stopwatch              ``com.lametric.stopwatch`` | ``stopwatch.start`` - starts stopwatch
                                                  | ``stopwatch.pause`` - pauses stopwatch
                                                  | ``stopwatch.reset`` - resets stopwatch

Weather                ``com.lametric.weather``   | ``weather.forecast`` - displays weather forecast 
====================== ========================== ======================================================

Some actions have parameters, for example ``clock.alarm``, ``clock.clockface`` and ``countdown.configure``.


**Action "clock.alarm"**
::
  
    {
      "id":"clock.alarm",
      "params": {
        "enabled":true,
        "time":"10:00:00",
        "wake_with_radio":false
      }
    }


==================== ================= =======================================================================
**Parameter**        **Format**        **Description**
-------------------- ----------------- -----------------------------------------------------------------------
``enabled``          Boolean           Optional. Activates the alarm if set to ``true``, deactivates otherwise.
``time``             String            Optional. Local time in format "HH:mm:ss".
``wake_with_radio``  Boolean           Optional. If true, radio will be activated when alarm goes off.
==================== ================= =======================================================================

**Action "clock.clockface"**
::
  
    {
      "id":"clock.clockface",
      "params": {
        "icon":"data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAgAAAAICAYAAADED76LAAAAOklEQVQYlWNUVFBgwAeYcEncv//gP04FMEmsCmCSiooKjHAFMEF0SRQTsEnCFcAE0SUZGBgYGAl5EwA+6RhuHb9bggAAAABJRU5ErkJggg==",
        "type" : "custom"
      }
    }


==================== ================= =======================================================================
**Parameter**        **Format**        **Description**
-------------------- ----------------- -----------------------------------------------------------------------
``icon``             String            Optional. Icon data in format "data:image/png;base64,<base64 encoded png binary>"
                                       or "data:image/gif;base64,<base64 encoded gif binary>"
``type``             String            Optional. Specifies the clockface type. Possible values are "weather", "page_a_day", "custom" and "none".
==================== ================= =======================================================================



**Action "countdown.configure"**
::
  
    {
      "id":"countdown.configure",
      "params": {
        "duration":1800,
        "start_now":false
      }
    }

==================== ================= =======================================================================
**Parameter**        **Format**        **Description**
-------------------- ----------------- -----------------------------------------------------------------------
``duration``         Integer           Optional. Time in seconds.
``start_now``        Boolean           Optional. If set to ``true`` countdown will start immediately.
==================== ================= =======================================================================

Body
^^^^
::
 
    {
      "id" : "<action_id>",
      "params": {
         "key": "value"
      }
    }


Response
^^^^^^^^
::
    
    {
      "success": {
        "data": {},
        "path": "/api/v2/device/apps/<package>/widgets/<widget_id>/actions"
      }
    }


Example
^^^^^^^
This request starts radio playback.

**Request**

REST::

    POST https://<device ip addess>:4343/api/v2/device/apps/com.lametric.radio/widgets/589ed1b3fcdaa5180bf4848e55ba8061/actions

    Content-Type: application/json

    { "id": "radio.play" }


cURL::
    
    $ curl -X POST -u "dev" -H "Content-Type: application/json" -k \
      -d '{ "id":"radio.play"}' \
      https://<device ip addess>:4343/api/v2/device/apps/com.lametric.radio/widgets/589ed1b3fcdaa5180bf4848e55ba8061/actions
    $ Enter host password for  user 'dev': <device api key>

**Response**
::

    {
      "success": {
        "data": {},
        "path": "/api/v2/device/apps/com.lametric.radio/widgets/589ed1b3fcdaa5180bf4848e55ba8061/actions"
      }
    }


----


.. _/api/v2/device/apps/:package/widgets/:id/activate:

Activate Specific Widget
------------------------

================  =======================================================
URL               /api/v2/device/apps/:package/widgets/:id/activate                             
Method            PUT                                        
Authorization     basic
API Version       2.1.0                                         
================  =======================================================

Description
^^^^^^^^^^^
Allows to make any widget visible using widget id. 

Body
^^^^
Does not require body.

Example
^^^^^^^

**Request**

REST::

    PUT https://<device ip address>:4343/api/v2/device/apps/com.lametric.clock/widgets/08b8eac21074f8f7e5a29f2855ba8060/activate

    Accept: application/json


cURL::

    $ curl -X PUT -u "dev" -H "Accept: application/json" \
      https://<device ip address>:4343/api/v2/device/apps/com.lametric.clock/widgets/08b8eac21074f8f7e5a29f2855ba8060/activate
    $ Enter host password for  user 'dev': <device api key>

**Response**
::

    { 
      "success" : { 
        "data" : {}, 
        "path" : "/api/v2/device/apps/com.lametric.clock/widgets/08b8eac21074f8f7e5a29f2855ba8060/activate" 
      } 
    }
