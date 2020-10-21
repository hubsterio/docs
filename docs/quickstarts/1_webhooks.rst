Webhooks
========

This section describes the necessary considerations along with an example, **on-how-to** prepare your webhook endpoint, 
to safely trust incoming messages sent by Hubster. This only applies to integration types that support 
webhooks such as the integration types below:

* System
* Direct
* BYOI (Bring your own Integration)

.. warning:: For **Direct** and **BYOI** integration types, they have the option to either receive 
             activities via **webhooks** vs **websockets**. If an integration has been configured using websockets and 
             its endpoint is unreachable, Hubster will not enforce it's :ref:`retry policy<ref_webhooks_retry>` as websockets 
             adhere to **fire-and-forget** paradigm.


HMAC Signature Validation
*************************

C# Sample
*********

.. https://www.nuget.org/packages/Hubster.Abstractions/1.0.1
.. Install-Package Hubster.Abstractions -Version 1.0.1


System Integration Activity Event Filters
*****************************************

Below are list of of activity events that **system** integrations can register too. 
System integrations must register to at least one event but can register to more as deemed necessary.
Hubster will only send events once one of the following events is triggered.

.. _ref_webhooks_events:

.. list-table::
    :widths: 5 50
    :header-rows: 1

    * - Event
      - Description
    * - message
      - Hubster will notify the webhook on **all message** activities for the given hub.
    * - message:customer
      - Hubster will only notify the webhook on **all customer message** activities for the given hub.
    * - message:agent
      - Hubster will only notify the webhook on all **agent message activities** for the given hub.
    * - message:bot
      - Hubster will only notify the webhook on all **bot message activities** for the given hub.

.. _ref_webhooks_retry:

Webhook Retry Policy
********************

.. list-table::
    :widths: 10 20 20
    :header-rows: 1

    * - Retry Attempt      
      - Next Retry Period
      - Timeout Before Retry
    * - 0 x 2 minutes
      - 0 minutes (immediate)
      - 10 seconds
    * - 1 x 2 minutes
      - 2 minutes
      - 10 seconds
    * - 2 x 2 minutes
      - 4 minutes
      - 10 seconds
    * - 3 x 2 minutes
      - 6 minutes
      - 10 seconds
    * - 4 x 2 minutes
      - 8 minutes
      - 10 seconds
    * - 5 x 2 minutes
      - 10 minutes
      - 10 seconds
      
.. note:: Once all retries attempts have been exhausted, Hubster will send a notification to the tenant account holder
          with details to as to why the endpoint is failing. It is up to the the account holder to rectify 
          their integration issue. 



