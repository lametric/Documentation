.. time-info
    
Info
=====

Get Device Info
---------------

=================  ======================================
URL                /api/v2/info                                   
=================  ======================================
Method             GET                                   
Authentication     Basic
=================  ======================================


Description
^^^^^^^^^^^
Gets information about the device like serial number, model, name and version of the API and software.

Response
^^^^^^^^
Returns Info object.

======================  ================  ==================================================
Property                Type              Description 
======================  ================  ==================================================
server_id               String            Id of the device on the cloud
api_version             String            API version number in format of <major>.<minor>.<bugfix>
os_version              String            Version of the LaMetric software in the same format as api_version
name                    String            Device name
mode                    Enum              Device mode. Can be one of "auto", "manual" or "kiosk".
                                            - auto - auto scroll mode
                                            - manual - click to scroll mode
                                            - kiosk - kiosk mode (single app is locked on the screen)
serial_number           String            Device serial number
model                   String            Device model
======================  ================  ==================================================


Response Example
^^^^^^^^^^^^^^^^

200 OK
::

	{
	  "api_version": "2.0.0",
	  "mode": "manual",
	  "model": "LM 37X8",
	  "name": "LM0001",
	  "os_version": "1.6.0",
	  "serial_number": "SA150800000100W00BP9",
	  "server_id": "1111"
	}


----