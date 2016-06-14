.. cloud_users
    
Users
=====


Endpoints
---------

+--------+------------------------------+-------------------------------------------+
|*Method*|*Path*                        |*Description*                              |
+--------+------------------------------+-------------------------------------------+
|GET     |api/v2/users/me               |Returns information about logged in user   |
+--------+------------------------------+-------------------------------------------+
|GET   	 |api/v2/users/me/devices       |Returns list of user's devices             |
+--------+------------------------------+-------------------------------------------+
|GET   	 |api/v2/users/me/devices/:id   |Returns information about specific device  |
+--------+------------------------------+-------------------------------------------+
|PUT   	 |api/v2/users/me/devices/:id   |Updates device info                        |
+--------+------------------------------+-------------------------------------------+

-----


Get User
--------

+-------+-----------------------------------------------+
|URL    |/api/v2/users/me                               |
+-------+-----------------------------------------------+
|Method | GET                                           |
+-------+-----------------------------------------------+
|Scope  | basic                                         |
+-------+-----------------------------------------------+

Description
^^^^^^^^^^^^^^^^^^^^^
Gets information about the logged in user.

Response
^^^^^^^^
Returns User object.

+---------------------+---------------+---------------------------------------------------+
|*Property*           |*Type*         |*Description*                                      |
+---------------------+---------------+---------------------------------------------------+
|email                |String         |User's login and e-mail address                    |
+---------------------+---------------+---------------------------------------------------+
|name                 |String         |User's name                                        |
+---------------------+---------------+---------------------------------------------------+
|apps_count           |Integer        |Total number of apps created by the user           |
+---------------------+---------------+---------------------------------------------------+
|private_device_count |Integer        |Number of devices connected to the user's account  |
+---------------------+---------------+---------------------------------------------------+
|private_apps_count   |Integer        |Number of private apps created by the user         |
+---------------------+---------------+---------------------------------------------------+

Response Example
^^^^^^^^^^^^^^^^

200 OK
::

    {
        "id":1,
        "email":"user@mail.com",
        "name":"John Smith",
        "apps_count":1,
        "private_device_count":5,
        "private_apps_count":3
    }


----

Get Devices
-----------

+-------+-----------------------------------------------+
|URL    |/api/v2/users/me/devices                       |
+-------+-----------------------------------------------+
|Method | GET                                           |
+-------+-----------------------------------------------+
|Scope  | devices_read                                  |
+-------+-----------------------------------------------+

Description
^^^^^^^^^^^^^^^^^^^^^
Gets the list of all devices connected to the user's account.


Response
^^^^^^^^
Returns array of Device objects.

+---------------------+---------------+----------------------------------------------------+
|*Property*           |*Type*         |*Description*                                       |
+---------------------+---------------+----------------------------------------------------+
|id                   |Integer        |Device id                                           |
+---------------------+---------------+----------------------------------------------------+
|name                 |String         |Device name                                         |
+---------------------+---------------+----------------------------------------------------+
|state                |String         |Device state. Valid values are "new", "configured"  |
|                     |               |or "banned".                                        |
+---------------------+---------------+----------------------------------------------------+
|serial_number        |String         |Device serial number                                |
+---------------------+---------------+----------------------------------------------------+
|api_key              |String         |Key that is used as access token to access          |
|                     |               |device's API in local network                       |
+---------------------+---------------+----------------------------------------------------+
|ipv4_internal        |String         |IP address of the device in local nerwork           |
+---------------------+---------------+----------------------------------------------------+
|mac                  |String         |Mac address of the device                           |
+---------------------+---------------+----------------------------------------------------+
|wifi_ssid            |String         |Name of the wi-fi access point the device is        |
|                     |               |connected to                                        |
+---------------------+---------------+----------------------------------------------------+


Response Example
^^^^^^^^^^^^^^^^

200 OK
::

	[
	  {
	    "id": 18,
	    "name": "My LaMetric",
	    "state": "configured",
	    "serial_number": "SA140100002200W00BS9",
	    "api_key": "8adaa0c98278dbb1ecb218d1c3e11f9312317ba474ab3361f80c0bd4f13a6749",
	    "ipv4_internal": "192.168.0.128",
	    "mac": "58:63:56:10:D6:30",
	    "wifi_ssid": "homewifi",
	    "created_at": "2015-03-06T15:15:55+02:00",
	    "updated_at": "2016-06-14T18:27:13+03:00"
	  }
	]

-----

Get Device By Id
----------------

+-------+-----------------------------------------------+
|URL    |/api/v2/users/me/devices/:id                   |
+-------+-----------------------------------------------+
|Method | GET                                           |
+-------+-----------------------------------------------+
|Scope  | devices_read                                  |
+-------+-----------------------------------------------+

Description
^^^^^^^^^^^^^^^^^^^^^
Gets device by id.


Response
^^^^^^^^
Returns Device object.

+---------------------+---------------+----------------------------------------------------+
|*Property*           |*Type*         |*Description*                                       |
+---------------------+---------------+----------------------------------------------------+
|id                   |Integer        |Device id                                           |
+---------------------+---------------+----------------------------------------------------+
|name                 |String         |Device name                                         |
+---------------------+---------------+----------------------------------------------------+
|state                |String         |Device state. Valid values are "new", "configured"  |
|                     |               |or "banned".                                        |
+---------------------+---------------+----------------------------------------------------+
|serial_number        |String         |Device serial number                                |
+---------------------+---------------+----------------------------------------------------+
|api_key              |String         |Key that is used as access token to access          |
|                     |               |device's API in local network                       |
+---------------------+---------------+----------------------------------------------------+
|ipv4_internal        |String         |IP address of the device in local nerwork           |
+---------------------+---------------+----------------------------------------------------+
|mac                  |String         |Mac address of the device                           |
+---------------------+---------------+----------------------------------------------------+
|wifi_ssid            |String         |Name of the wi-fi access point the device is        |
|                     |               |connected to                                        |
+---------------------+---------------+----------------------------------------------------+


Response Example
^^^^^^^^^^^^^^^^

200 OK
::

  {
    "id": 18,
    "name": "My LaMetric",
    "state": "configured",
    "serial_number": "SA140100002200W00BS9",
    "api_key": "8adaa0c98278dbb1ecb218d1c3e11f9312317ba474ab3361f80c0bd4f13a6749",
    "ipv4_internal": "192.168.0.128",
    "mac": "58:63:56:10:D6:30",
    "wifi_ssid": "homewifi",
    "created_at": "2015-03-06T15:15:55+02:00",
    "updated_at": "2016-06-14T18:27:13+03:00"
  }


----

Update Device
----------------

+-------+-----------------------------------------------+
|URL    |/api/v2/users/me/devices/:id                   |
+-------+-----------------------------------------------+
|Method | PUT                                           |
+-------+-----------------------------------------------+
|Scope  | devices_write                                 |
+-------+-----------------------------------------------+

Description
^^^^^^^^^^^^^^^^^^^^^
Updates specific device by id.

Body
^^^^
::

	{
	    "name": "Device @ Work"
	}


Response
^^^^^^^^
Returns success object with device id and name.


Response Example
^^^^^^^^^^^^^^^^

200 OK
::

	{
	  "success": {
	    "id": 18,
	    "name": "Device @ Work"
	  }
	}

