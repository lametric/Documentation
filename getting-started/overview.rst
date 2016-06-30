.. _getting-started-overview:

Overview
========

LaMetric is the open Internet of Things platform.

With LaMetric developers can:

- Create indicator apps that run on LaMetric and display key metrics or KPIs.
- Create button apps that run on LaMetric and can trigger HTTP requests.
- Deliver notifications right to the LaMetric Time in the local network.
- Integrate LaMetric Time into existing smart home or IoT systems.

----

Developer Highlights
--------------------

LaMetric aims to be developer friendly platform. Key developer features:

- Simple REST API to send notifications to device in local network (no need to install apps on LaMetric) and get its state.
- Easy LaMetric app creation that does not require development (IDE can be fount at https://developer.lametric.com)
- Web based simulator is available to help you test your app.
- Growing LaMetric Time `community <https://lametric.freshdesk.com/discussions>`_

-----

How it Works
------------

There are multiple ways of getting information onto LaMetric Time screen. Notification can be pushed in local network using Notification APP in combination with device REST API or to native LaMetric apps.

LaMetric Notification APP + Local REST API
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
This way of sending notifications to device is preferrable if:

- Fast response time is required.
- You are sending sensitive data and you don't want it to leave your local network.
- Data from notification should not stay on the display for too long.

Native LaMetric Apps
^^^^^^^^^^^^^^^^^^^^
It is possible to create indicator or button apps.
Create indicator app when:

- It is important to display numbers, charts or text messages that stay on LaMetric until new data has come and optionally notify the user about change.
- LaMetric Time must get fresh data by itself (via polling) or you want to push fresh data in local network or via LaMetric Cloud.
- Trigger action right from LaMetric Time in response to the data that is displayed.
- You are willing to distribute app to other LaMetric users.

Create button app when:

- It is required to trigger some action from LaMetric Time.
- User must be able to customize text and icon that is displayed on LaMetric when button app is active.
- You are willing to distribute app to other LaMetric users.

.. tip::
    All public native LaMetric apps are available in our `Appstore <http://apps.lametric.com>`_


What's Next?
------------
To start developing for LaMetric, login as a developer to `DevZone <https://developer.lametric.com>`_ and create new app. Also check out `LaMetric User Guide <http://lametric.com/user_guide.pdf>`_. In section 7 you will find answers to some frequent questions.



