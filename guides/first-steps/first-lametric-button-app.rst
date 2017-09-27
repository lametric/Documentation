.. _first-lametric-button-app.rst:

First Button App
================

Button app is a native LaMetric Time app that allows to do things when you press an action button. We will use `zapier.com <http://zapier.com>`_ to demonstrate how it works. Zapier is a service that can do something (like send email) in response to some event. We will use LaMetric Time button app to trigger such an event.

Let's create an app that will notify wife when you are going home.

To do that, we will need to:

#. Create "Button App" at `developer.lametric.com <https://developer.lametric.com>`_
#. Create new Zapp (a.k. rule) at `zapier.com <http://zapier.com>`_
#. Publish you "Button App" and test how it works.

So, let's get started!

Create Button App
^^^^^^^^^^^^^^^^^
Start by logging in to your `developer account <https://developer.lametric.com>`_ and create new button app.

.. image:: ../../images/app-button/devzone-step1.png

Now add "message" parameter that will allow us to change the text that will be sent. Choose icon and enter text that will be displayed on the LaMetric Time when app is active.

.. image:: ../../images/app-button/devzone-step21.png

As you noticed, now we need URL to put into "URL to be triggerd" field. This is when Zapier comes into play.

Let's open `zapier.com <http://zapier.com>`_ in separate tab and proceed with creating new zap.

.. image:: ../../images/app-button/zap-step1.png

Let's search for "webhooks" triggers. Webhook is an API that we can call from our app to do some action.

.. image:: ../../images/app-button/zap-step3.png

Now choose "Catch Hook" and press "Save + Continue" button. This will tell Zapier to create an API endpoint for us that we will be able to call.

.. image:: ../../images/app-button/zap-step4.png

At this step enter parameter name we added to our button app - "message".

.. image:: ../../images/app-button/zap-step5.png

After this step you have the hook URL we can use in our button app. Copy it by pressing on "Copy to clipboard button".

.. image:: ../../images/app-button/zap-step6.png

Lets switch to the tab where we have LaMetric Developer open and continue from step 5. Just paste the URL into "URL to be triggered" field and press "Next".

.. image:: ../../images/app-button/devzone-step22.png

Now enter your app name and short description. As an example we will use "Wife Notifier" name.

.. image:: ../../images/app-button/devzone-step3.png

Ok, now publish app privately by clicking on "Publish" button and install it to your LaMetric Time device.

.. image:: ../../images/app-button/devzone-step4.png

Open LaMetric Time app, go to your device settings and press on "+" button. Choose "Private" category, find your app and press "Add".

.. image:: ../../images/app-button/app-step1.png
.. image:: ../../images/app-button/app-step2.png
.. image:: ../../images/app-button/app-step3.png
.. image:: ../../images/app-button/app-step5.png

Now check your device - you should see "Leve" text (the one we added during app creation). Let's press "Action" button for a few times. This will cause hook URL to be triggered and zapier will know it works.

.. image:: ../../images/app-button/device.jpg

Let's get back to Zapier and continue with our zap. If you see "Test Successful" message - press "Continue". If not - try to press "Action" button on the device few more times.

.. image:: ../../images/app-button/zap-step7.png

Now, when we are done creating trigger let's continue with action. Because we want to send an e-mail, let's find Gmail action by typing "Gmail" into action search field. Choose "Send Email" action and press "Save + Continue" button.

.. image:: ../../images/app-button/zap-step8.png

Login to you Gmail account and select it when asked, followed by "Save + Continue" button.

.. image:: ../../images/app-button/zap-step9.png

Lets fill out the e-mail form:

:To: wife@home.com
  (this may be your wives e-mail address)
:Reply to: me@work.com
  (this is your e-mail addres)
:From name: John
  (your name)
:Subject: I'm on my way!
  (subject of email)
:Body: here choose Querystring Message parameter. It will get replaced by the message from our app.

.. image:: ../../images/app-button/zap-step10.png
.. image:: ../../images/app-button/zap-step11.png

Now it is ok to click "Continue" button to proceed to the next step

.. image:: ../../images/app-button/zap-step13.png

Check your e-mail and click on "Create & Continue" button.

.. image:: ../../images/app-button/zap-step14.png

And finally here is our "Finish" button! Let's click it!

.. image:: ../../images/app-button/zap-step15.png

Final touch, lets choose the name for our zap - "Wife Notifier" would be good.

.. image:: ../../images/app-button/zap-step16.png

That's it! You have created your first zap - rule that sends e-mail to your wife when you click button on your LaMetric Time!

.. image:: ../../images/app-button/zap-step17.png

Let's press the action button.....

.. image:: ../../images/app-button/device.jpg

Ding! It works!

.. image:: ../../images/app-button/app-step6.png

Hope you enjoyed the tutorial. Let us know if you find any issues, typos or other issues. Thanks!
