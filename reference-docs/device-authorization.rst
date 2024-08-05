.. device-authorization
    
Authorization
=============


Overview
--------
LaMetric devices use basic authorization to simplify access to the device API. Authorization credentials consist of word "dev" as a user name and API key as a password. 

::

   Authorization: Basic Base64(dev:<api_key>)


Get the API key
---------------
There are multiple ways of getting the API key: 

1. :ref:`Manualy via LaMetric mobile app <get-the-API-key-via-mobile>` (only for 2022+ devices)
2. :ref:`Manualy via LaMetric Developer portal <get-the-API-key-via-devportal>`
3. :ref:`Programmatically via the Cloud API <get-the-API-key-programmatically>`.


.. _get-the-API-key-via-mobile:

Get the API key via Mobile app 
------------------------------

If you have LaMetric device produced after 2022+ you may get the API key from the app.

1. Open ``LaMetric`` app for iOS or Android
   
2. Go to Device → Settings → Device API Key.

.. image:: ../images/device-authorization/device-settings-screen.png

3. Long press on the key to copy it, or, if it is not have been generated yet – press on the "Generate API Key" button.

.. image:: ../images/device-authorization/device-api-key-screen.png
   
.. tip:: Key generated via the LaMetric app stays on the LaMetric device and works offline. It is not synced to the Cloud.


.. _get-the-API-key-via-devportal:

Get the API Key via Developer Portal
-------------------------------------

.. |LaMetric Developer Portal| raw:: html

	<a href="https://developer.lametric.com" target="_blank">LaMetric Developer Portal</a>

API key also can be get from the |LaMetric Developer Portal|. In order to do that:

1. Open |LaMetric Developer Portal|
2. Login with your LaMetric Account
3. Go to ``User`` → ``My Devices``

.. image:: ../images/device-authorization/lametric-developer-profile-menu.png

4. Copy API key located on the ``Devices`` tab.

.. image:: ../images/device-authorization/lametric-developer-devices-page.png


.. _get-the-API-key-programmatically:

Get the API Key Programmatically
--------------------------------
There are 3 steps you should do to get API key programmatically via LaMetric Cloud API


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


Use API Key in every API Request to the Device
----------------------------------------------

Once API key is received, store it in a secure place and use it to authenticate each API call to the device.

3.1 Concatenate "dev:" and api_key::

	dev:8adaa0c98278dbb1ecb218d1c3e11f9312317ba474ab3361f80c0bd4f13a6749

3.2 Encode using Base64::

	base64(dev:8adaa0c98278dbb1ecb218d1c3e11f9312317ba474ab3361f80c0bd4f13a6749) = ZGV2OjhhZGFhMGM5ODI3OGRiYjFlY2IyMThkMWMzZTExZjkzMTIzMTdiYTQ3NGFiMzM2MWY4MGMwYmQ0ZjEzYTY3NDk=

3.3 Use in HTTP header::

	Authorization: Basic ZGV2OjhhZGFhMGM5ODI3OGRiYjFlY2IyMThkMWMzZTExZjkzMTIzMTdiYTQ3NGFiMzM2MWY4MGMwYmQ0ZjEzYTY3NDk=

For example:

.. code-block:: python

    #Python

    import requests
    import base64

    DEVICE_IP = '192.168.0.128'
    DEVICE_PORT = 4343
    DEVICE_API_KEY = '8adaa0c98278dbb1ecb218d1c3e11f9312317ba474ab3361f80c0bd4f13a6749'
   
    # Encode API key for authorization
    auth_str = f'dev:{DEVICE_API_KEY}'
    auth_bytes = auth_str.encode('ascii')
    auth_base64 = base64.b64encode(auth_bytes).decode('ascii')

    # Headers for API requests
    HEADERS = {
        'Authorization': f'Basic {auth_base64}',
        'Content-Type': 'application/json',
        'Accept': 'application/json'
    }

    url = f'https://{DEVICE_IP}:{DEVICE_PORT}/api/v2'
    response = requests.get(url, headers=HEADERS, verify=False)
    if response.status_code == 200:
        # Success
    else:
        # Failure

