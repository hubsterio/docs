.. _ref_activities:

Activities
==========

When integrating with disparate systems, data coming in or data going out, mostly like will come in 
various shapes and formats. When dealing with a lot of integrations with similar functional 
characteristics, but each having their own proprietary data specifics, it's important generalize these 
differences in an agnostic common format. At Hubster, we call this common format an **Activity**. 

This section will explain what an activity is, it's constituents and how it’s consumed by Hubster’s conversation pipeline. 
See the depiction below for annotated description on how Hubster transforms both in and outbound data models.

.. image:: images/transformation.png
           :align: center

**How Hubster’s UX Multi-rendering/Response Framework (RRF) works:**

#. When data is sent by a specific integration type, the **inbound** RRF will transform this data into a Hubster activity for further consumption. 
#. The conversation pipeline can now freely work and amend the activity without any knowledge of its original source format.
#. Once the conversation pipeline completes its workflow, it will send the response to the **outbound** RRF which transforms the activity to the appropriate integration type’s proprietary format.


Activity
^^^^^^^^

An activity is fairly simple structure that either contains an :ref:`Message Type<ref_activities_message_types>`  
or an :ref:`Action Type<ref_activities_action_types>`, but not both.

.. note:: 
    For sake of sample, both the **message** and **action** nodes are shown. 
    However, these nodes are mutually exclusive and will never be presented together 
    in actuality.

.. code-block:: JSON

    {
        "type": "message|action",
        "eventTrigger": "message:customer",
        "eventId": 1603933721542,
        "externalId": "my-external-id",
        "isEcho": false,
        "interactionId": "00000000-0000-0000-0000-000000000005",
        "flowProcess": "Default",
        "sender": {
            "integrationId": "00000000-0000-0000-0000-000000000001",
            "integrationType": "Customer",
            "channelType": "Direct",
            "tokenId": "t+8qymYD1jp7wDSHG+3eUA=="
        },
        "recipient": {
            "integrationId": "00000000-0000-0000-0000-000000000006",
            "integrationType": "Agent",
            "channelType": "Direct",
            "tokenId": "971480cb-938c-4dfd-be4e-01756c833490.00000000-0000-0000-0000-000000000003"
        },
        "message": {
            "type": "text",
            "text": "Hi there!"			
        },
        "action": {
            "type": "payload",
            "payloadType": "hubster.transfer",
            "payload": {
                "url": "http://localhost:4200",
                "label": "Click here to be transferred",
                "mount": 1000,
                "force": false
            }
        }        
    }  


.. list-table::
    :widths: 5 50
    :header-rows: 1   
  
    * - Property
      - Description
    * - type
      - The is the type of activity being described. Can only be **message** or **action** at this time. 
    * - eventTrigger
      - The source of the trigger. Typically this is the **sender** of of the activity. See :ref:`Integration Types<ref_api_integration_types>` 
    * - eventId
      - The epoch UNIX time in milliseconds when this event was initiated.
    * - externalId
      - A custom external id that can be sent by custom integrations. Typically, this will is null.
    * - isEcho
      - | A boolean state indicating wither the activity is an echo. Some custom integrations when sending an 
        | activity may wish to receive a feedback activity. This is because when sending an activity, the sender
        | tends to send minimal data. Having echo enabled, the sender will receive a more enriched payload 
        | with additional data that can be important to the sender. For example, if the sender sends a 
        | youtube link in the message text, Hubster will convert the activity to youtube :ref:`message type<ref_activities_message_types>` instead.
    * - interactionId
      - The interaction id for this activity. This only applicable to **message** types.
    * - flowProcess
      - The pipeline flow that was taken. The current values are **Default** or **AutoReplay**.
    * - sender
      - The sender :ref:`source<ref_activities_sources>` of this activity.
    * - recipient
      - The recipient (receiver) :ref:`source<ref_activities_sources>` of this activity.
    * - message
      - If the activity.type is **message** then this value will be set. See :ref:`message type<ref_activities_message_types>` for more details
    * - action
      - If the activity.type is **action** then tis value will be set. See :ref:`action type<ref_activities_action_types>` for more details


.. _ref_activities_sources:

Activity Source
^^^^^^^^^^^^^^^

An activity will always contain a **sender** node who sent the activity and a **recipient** node who will receive the activity. 
The properties are identical but the values and the node name, indicates details of the sending and receiving parties.

.. list-table::
    :widths: 5 50
    :header-rows: 1   
  
    * - Property
      - Description
    * - integrationId
      - The integration id of the source.
    * - integrationType
      - The :ref:`integration type<ref_api_integration_types>` of the source.
    * - channelType
      - The :ref:`channel type<ref_api_channel_types>` of the source.
    * - tokenId
      - Reserved for Hubster.


.. _ref_activities_message_types:

Message Types
^^^^^^^^^^^^^


.. public const string Text = "text";
.. public const string Contact = "contact";
.. public const string Card = "card";
.. public const string Location = "location";
.. public const string Attachment = "attachment";
.. public const string Video = "video";
.. public const string Audio = "audio";
.. public const string Youtube = "youtube";
.. public const string Vimeo = "vimeo";
.. public const string Image = "image";
.. public const string List = "list";
.. public const string Carousel = "carousel";
.. public const string Command = "command";

.. public const string Link = "link";
.. public const string Postback = "postback";
.. public const string Reply = "reply";


.. _ref_activities_action_types:

Action Types
^^^^^^^^^^^^

TODO

.. public const string Seen = "seen";
.. public const string TypingOn = "typing_on";
.. public const string TypingOff = "typing_off";
.. public const string Payload = "payload";
