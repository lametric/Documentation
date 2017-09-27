.. device-discovery

Device Discovery
================

There are multiple ways to discover LaMetric devices in local network. Discovering works if 3rd party service, device or app is located in the same subnet.

1. Cloud API
-------------

To get the local IP address of the LaMetric Time device do these steps:

1. Login to LaMetric Cloud
2. Get list of user's devices
3. Get IP address and api_key of the device via API request.

For more details check `Authorization <device-authorization.html>`_ section.


2. UPnP
-------
1.1. Send SSDP discovery request (more info can be found `here <https://en.wikipedia.org/wiki/Universal_Plug_and_Play#Discovery>`_ ) and listen for incomming broadcast messages:
::

	HTTP/1.1 200 OK
	CACHE-CONTROL: max-age=1800
	EXT:
	LOCATION: http://192.168.88.153:60669/b2d83c5d-6012-4857-916e-6238ca6cab4e/device_description.xml
	SERVER: Linux/3.4.103 UPnP/1.1 HUPnP/1.0
	ST: upnp:rootdevice
	USN: uuid:b2d83c5d-6012-4857-916e-6238ca6cab4e::upnp:rootdevice
	BOOTID.UPNP.ORG: 0
	CONFIGID.UPNP.ORG: 0


1.2. Take the URL from ``LOCATION`` parameter and get device_description.xml::

	curl -i http://192.168.88.153:60669/b2d83c5d-6012-4857-916e-6238ca6cab4e/device_description.xml

::

	HTTP/1.1 200 OK
	DATE: Tue, 28 Jun 2016 19:59:36
	Connection: close
	HOST: 192.168.88.153:60669
	content-length: 771

	<?xml version="1.0" encoding="UTF-8"?>
	  <root xmlns="urn:schemas-upnp-org:device-1-0">
	    <specVersion>
	      <major>1</major>
	      <minor>0</minor>
	    </specVersion>
	    <URLBase>https://192.168.88.153:443</URLBase>
	    <device>
	      <deviceType>urn:schemas-upnp-org:device:LaMetric:1</deviceType>
	      <friendlyName>LaMetric (LM1419)</friendlyName>
	      <manufacturer>Smart Atoms Inc.</manufacturer>
	      <manufacturerURL>http://www.smartatoms.com</manufacturerURL>
	      <modelDescription>LaMetric - internet connected ticker witn UPnP SSDP support</modelDescription>
	      <modelName>LaMetric Battery Edition</modelName>
	      <modelNumber>SA01</modelNumber>
	      <modelURL>http://www.lametric.com</modelURL>
	      <serialNumber>SA150800000100W00BP9</serialNumber>
	      <serverId>1</serverId>
	      <UDN>uuid:b2d83c5d-6012-4857-916e-6238ca6cab4e</UDN>
	    </device>
	  </root>


LaMetric Time public API is located on ports 8080 and 4343. You should have api_key to access it (see `Authorization <device-authorization.html>`_ section for more details).


1.3. If you have api_key on this stage you can check if LaMetric Time API works. ::

	curl -i -H "Authorization: Basic dXNlcjpiZTBmNTNhYTQ1NzdjMzUxMDE3OGY2Mzc3Yjk3NTEwY2U0ZTA2ZGQ3ZTBjYTlkMDRjNDMyMDRiY2RlZTllMjY2"
	http://192.168.88.153:8080/api/v2

	HTTP/1.1 200 OK
	CONTENT-TYPE: application/json;charset=UTF8
	Transfer-Encoding: chunked
	Date: Tue, 28 Jun 2016 17:36:54 GMT
	Server: lighttpd/1.4.35

	{
	  "api_version" : "2.0.0",
	  "endpoints" : {
	    "audio_url" : "http://192.168.88.153:8080/api/v2/device/audio",
	    "bluetooth_url" : "http://192.168.88.153:8080/api/v2/device/bluetooth",
	    "concrete_notification_url" : "http://192.168.88.153:8080/api/v2/device/notifications{/:id}",
	    "current_notification_url" : "http://192.168.88.153:8080/api/v2/device/notifications/current",
	    "device_url" : "http://192.168.88.153:8080/api/v2/device",
	    "display_url" : "http://192.168.88.153:8080/api/v2/device/display",
	    "notifications_url" : "http://192.168.88.153:8080/api/v2/device/notifications",
	    "widget_update_url" : "http://192.168.88.153:8080/api/v2/widget/update{/:id}",
	    "wifi_url" : "http://192.168.88.153:8080/api/v2/device/wifi"
	  }
	}

We recommend to use secure way of accessing the API via https using port 4343::

	curl -i -H "Authorization: Basic dXNlcjpiZTBmNTNhYTQ1NzdjMzUxMDE3OGY2Mzc3Yjk3NTEwY2U0ZTA2ZGQ3ZTBjYTlkMDRjNDMyMDRiY2RlZTllMjY2"
	https://192.168.88.153:4343/api/v2 --insecure

	HTTP/1.1 200 OK
	CONTENT-TYPE: application/json;charset=UTF8
	Transfer-Encoding: chunked
	Date: Tue, 28 Jun 2016 17:51:25 GMT
	Server: lighttpd/1.4.35

	{
	  "api_version" : "2.0.0",
	  "endpoints" : {
	    "audio_url" : "https://192.168.88.153:4343/api/v2/device/audio",
	    "bluetooth_url" : "https://192.168.88.153:4343/api/v2/device/bluetooth",
	    "concrete_notification_url" : "https://192.168.88.153:4343/api/v2/device/notifications{/:id}",
	    "current_notification_url" : "https://192.168.88.153:4343/api/v2/device/notifications/current",
	    "device_url" : "https://192.168.88.153:4343/api/v2/device",
	    "display_url" : "https://192.168.88.153:4343/api/v2/device/display",
	    "notifications_url" : "https://192.168.88.153:4343/api/v2/device/notifications",
	    "widget_update_url" : "https://192.168.88.153:4343/api/v2/widget/update{/:id}",
	    "wifi_url" : "https://192.168.88.153:4343/api/v2/device/wifi"
	  }
	}

``--insecure`` option must be added because of the random IP address LaMetric may have, and it is not possible to verify  host stored inside the certificate.
