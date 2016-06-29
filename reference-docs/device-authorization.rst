.. device-authorization
    
Authorization
=============


Overview
--------
LaMetric Time uses basic authorization for simple access to the device via API. Authorization header consists of word "dev" as user name and API key as a password. ::

   Authorization: Basic Base64(dev:api_key)

Steps To Get an API Key
^^^^^^^^^^^^^^^^^^^^^^^
There are 3 steps you should do to get API key.


Step 1. Authenticate on the Cloud
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Please refer to the `Cloud API Documentation / OAuth2 Authorization <cloud-authorization.html>`_ on this subject.


Step 2. Get API key for the device from the Cloud
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Once authenticated please use `GET https://developer.lametric.com/api/v2/users/me/devices <cloud-users.html>`_ API to get list of user's devices.

You should get something like this::

	[
	  {
	    "id": 18,
	    "name": "My LaMetric",
	    "state": "configured",
	    "serial_number": "SA150600000100W00BS9",
	    "api_key": "8adaa0c98278dbb1ecb218d1c3e11f9312317ba474ab3361f80c0bd4f13a6749",
	    "ipv4_internal": "192.168.0.128",
	    "mac": "58:63:56:10:D6:30",
	    "wifi_ssid": "homewifi",
	    "created_at": "2015-03-06T15:15:55+02:00",
	    "updated_at": "2016-06-14T18:27:13+03:00"
	  }
	]

You can find device API key in ``api_key`` property. 


Step 3. Store API key and use it in every API request
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Now store the API key in secure place and use it to authenticate each API call to device.

3.1 Concatenate "dev:" and api_key::

	dev:8adaa0c98278dbb1ecb218d1c3e11f9312317ba474ab3361f80c0bd4f13a6749

3.2 Encode using Base64::

	base64(dev:8adaa0c98278dbb1ecb218d1c3e11f9312317ba474ab3361f80c0bd4f13a6749) = ZGV2OjhhZGFhMGM5ODI3OGRiYjFlY2IyMThkMWMzZTExZjkzMTIzMTdiYTQ3NGFiMzM2MWY4MGMwYmQ0ZjEzYTY3NDk=

3.3 Use in HTTP header::

	Authorization: Basic ZGV2OjhhZGFhMGM5ODI3OGRiYjFlY2IyMThkMWMzZTExZjkzMTIzMTdiYTQ3NGFiMzM2MWY4MGMwYmQ0ZjEzYTY3NDk=

