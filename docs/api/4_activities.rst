.. role:: underline
    :class: underline

.. _ref_activities:

Activities
==========

When integrating with disparate systems, data coming in or data going out, most likely come in 
various shapes and formats. In Hubster's case, most integrations may have similar functionalities, 
however, each integration on their own, have proprietary formats that differ from each other. 
Because of these numerous differences, it's important to generalize their formats into a common format that 
is agnostic and most of all consistent. At Hubster, we call this common format an **Activity**. 
This in essence, is the hallmark behind the concept of **unified messaging**.

This section will explain what an activity is, it's constituents and how it’s consumed by Hubster’s conversation pipeline. 
See the depiction below for annotated description on how Hubster transforms both in and outbound data models.

.. image:: images/transformation.png
           :align: center

**How Hubster’s UX Multi-rendering/Response Framework (RRF) works:**

#. When data is sent by a specific integration type, the **inbound** RRF will transform this data into a Hubster activity for further consumption. 
#. The conversation pipeline can now freely work and amend the activity without any knowledge of its original source format.
#. Once the conversation pipeline completes its workflow, it will send the response to the **outbound** RRF which transforms 
   the activity to the appropriate integration type’s proprietary format.


.. _ref_activity:

Activity
^^^^^^^^

An activity is fairly simple structure that contains either a single :ref:`Message <ref_activities_message_types>`  
or a :ref:`Event <ref_activities_event_types>` type, but not both.

.. note:: 
    For sake of sample, both **message** and **event** nodes are shown. 
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
        "event": {
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
      - The is the type of activity being described. Can either be a **message** or **action**. 
    * - eventTrigger
      - The source of the trigger. Typically this is the **sender** of of the activity. See :ref:`Integration Types<ref_api_integration_types>` 
    * - eventId
      - The epoch UNIX time in milliseconds when this event was initiated. 
    * - externalId
      - This can be any string value and will be attached to the lifetime of this activity if provided by the sender. 
        Typically this is used by tenants to maintain a reference or metadata to a given tenant resource. 
        For the most part this value will be null.
    * - isEcho
      - A boolean state indicating wither the activity is an echo. Some custom integrations when sending an 
        activity may wish to receive a feedback activity. This is because when sending an activity, the sender
        tends to send minimal data. Having echo enabled, the sender will receive a more enriched payload 
        with additional data that can be important to the sender. For example, if the sender sends a 
        youtube link in the message text, Hubster will convert the activity to youtube 
        :ref:`message type<ref_activities_message_types>` instead.
    * - interactionId
      - The interaction id for this activity. This only applies to **message** types.
    * - flowProcess
      - The pipeline flow that was taken. The current values are **Default** or **AutoReplay**.
    * - sender
      - The sender :ref:`source<ref_activities_sources>` of this activity.
    * - recipient
      - The recipient (receiver) :ref:`source<ref_activities_sources>` of this activity.
    * - message
      - If the *activity.type* is **message** then this value is required. 
        See :ref:`message type<ref_activities_message_types>` for more details
    * - event
      - If the *activity.type* is **event** then this value is required. 
        See :ref:`event type<ref_activities_event_types>` for more details


.. _ref_activities_sources:

Activity Header 
^^^^^^^^^^^^^^^

When sending activities, there's a minimal amount of header properties that are required. 
See details below:

.. list-table::
    :widths: 5 10 50
    :header-rows: 1   
  
    * - Property     
      - Mandatory
      - Description
    * - type
      - Yes
      - The type of activity to send. 
        This can only :ref:`message type<ref_activities_message_types>` or 
        :ref:`event type<ref_activities_event_types>`
    * - **sender**.integrationId
      - See **Description**
      - | If the source of **integrationId** is bound to a **customer** integration, then this property is **not** required.       
        |
        | However, if the **integrationId** is bound to either an **agent** or **bot** integration, then this property **is** required.
    * - externalId
      - No
      - This can be any string value and will be attached to the lifetime of this activity if provided by the sender. 
        Typically this is used by tenants to maintain a reference or metadata to a given tenant resource.
        For the most part this value will be null.
        

.. code-block:: JSON

    {
        "externalId": "some-external-id",
        "type": "message | event"
        "sender": {
            "integrationId": "00000000-0000-0000-0000-000000000001"
        },
        "message": {
            "type": "text",
            "text": "Hi there!"			
        },
        "event": {
            "type": "payload",
            "payloadType": "my.payload.01",
            "payload": {
                "data1": "value1",
                "data2": "value2",
                "data3": "value3"
            }
        }                
    }  


Activity Source
^^^^^^^^^^^^^^^

An activity will always contain a **sender** and **recipient** nodes. 
The the sender is the source of the activity and 
the recipient is the source that will receive the activity. 

.. code-block:: JSON

    {
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
        }
    }  


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

An activity **message** supports the following **types**. Messages are an activity's **first-class-citizen** 
as they make up the majority of events being sent and received between integrations.

.. note:: 
    Activities are send via the :ref:`Direct API<ref_engine_direct>` endpoint. 
    Sending an activity is quite simple and requires minimal amount of header details. 
    Once Hubster receives an activity to process, the engine will enrich the activity with 
    more details, such as sources, etc. See :ref:`Activity <ref_activity>` on this page.

Text
~~~~

Sources allowed to send: **customer**, **agent** and **bot**.

.. list-table::
    :widths: 5 10 50
    :header-rows: 1   
  
    * - Property     
      - Mandatory
      - Description
    * - type
      - Yes
      - Must be **text**.
    * - text
      - See **note**
      - | The text message to send.
           
        | Links such as **Image**, **Youtube**, **Vimeo**, **Video**, **Audio** or **location**, may convert this message type to it's property message equivalent 
          if no additional text was provided. If additional text was provided, then Hubster will add a message equivalent, such as **Youtube**, for example
          to the items array.
    * - items
      - See **note**
      - | A list of items containing zero or more of the following **messages types**:
        
        * youtube 
        * vimeo
        * video 
        * audio
        * image
        * attachment
        * location
        * contact
        * card
    * - actions
      - See **note**
      - | A list of actions containing zero or more of the following **action types**:      

        * postback
        * reply
        * link        

.. note:: 
    The **text message** type must provide one or more of the following **mandatory** values:
    
    * text
    * items
    * actions

**Examples**

.. list-table::
    :widths: 10 200
    :header-rows: 1   

    * - Request          
      - View
    * - .. code-block:: JSON

          {
            "type": "text",								
            "text": "Hello there, how can I help you?"
          }  

      - .. image:: images/activity_text_ex_01.png

    * - .. code-block:: JSON

          {
            "type": "text",
            "text": "Here's my contact info",
            "items": [
              {
                "type": "contact",
                "imageUrl": "https://site.com/eva.png",
                "title": "Eva Green",
                "subtitle": "Mighty Health",
                "properties": [
                  { 
                    "key": "Title",
                    "value": "Health Advisor/Coach"
                  },
                  {
                    "key": "Address",
                    "value": "123 Main Street, Maple, ON",
                    "type": "address;work"
                  },
                  {
                    "key": "Cell",
                    "value": "(416) 555-0001",
                    "type": "phone;cell"
                  },
                  {
                    "key": "Email",
                    "value": "eva@mightyhealth.com",
                    "type": "email"
                  }
                ],
                "channels": [
                  {
                    "type": "Webchat",
                    "metadata": [
                      {
                        "key": "caption-show",
                        "value": "true"
                      },
                      {
                        "key": "caption-color",
                        "value": "white"
                      }
                    ]
                  }
                ]
              }
            ]
          }          

      - .. image:: images/activity_text_ex_02.png          

    * - .. code-block:: JSON

          {
            "type": "text",
            "text": "Select one of the following options",
            "actions": [
              {
                "type": "postback",
                "title": "Yes",
                "payload": "Yes",
                "channels": [
                  {
                    "type": "Webchat",
                    "metadata": [
                      {
                        "key": "type",
                        "value": "primary"
                      }
                    ]
                  }
                ]
              },
              {
                "type": "postback",
                "title": "Maybe",
                "payload": "Maybe",
                "channels": [
                  {
                    "type": "Webchat",
                    "metadata": [
                      {
                        "key": "type",
                        "value": "danger"
                      }
                    ]
                  }
                ]
              },
              {
                "type": "reply",
                "title": "No",
                "payload": "No",
                "channels": [
                  {
                    "type": "Webchat",
                    "metadata": [
                      {
                        "key": "type",
                        "value": "success"
                      }
                    ]
                  }
                ]
              },
              {
                "type": "link",
                "title": "hubster",
                "url": "https://hubster.io",
                "channels": [
                  {
                    "type": "Webchat",
                    "metadata": [
                      {
                        "key": "type",
                        "value": "info"
                      }
                    ]
                  }
                ]
              }
            ]
          }


      - .. image:: images/activity_text_ex_03.png          

Youtube             
~~~~~~~

Sources allowed to send: **customer**, **agent** and **bot**.

.. list-table::
    :widths: 5 10 50
    :header-rows: 1   
  
    * - Property     
      - Mandatory
      - Description
    * - type
      - Yes
      - Must be **youtube**.
    * - url
      - Yes
      - | The youtube url, which can be in anyone of the following formats:
        
        * `https://youtube.com/embed/x1245b` (preferred)
        * `https://youtube.com/watch?v=x1245b`
        * `https://m.youtube.com/watch?v=x1245b`
        * `https://youtu.be/watch?v=x1245b`     
        

**Example**

.. list-table::
    :widths: 10 200
    :header-rows: 1   

    * - Request          
      - View
    * - .. code-block:: JSON

          {
            "type": "youtube",								
            "url": "https://youtube.com/watch?v=x1245b"
          }  

      - .. image:: images/activity_youtube_ex_01.png


Vimeo      
~~~~~

Sources allowed to send: **customer**, **agent** and **bot**.

.. list-table::
    :widths: 5 10 50
    :header-rows: 1   
  
    * - Property     
      - Mandatory
      - Description
    * - type
      - Yes
      - Must be **vimeo**.
    * - url
      - Yes
      - | The Vimeo url, which can be in anyone of the following formats:
        
        * `https://player.vimeo.com/video/12345678` (preferred)
        * `https://vimeo.com/12345678`
        

**Example**

.. list-table::
    :widths: 10 200
    :header-rows: 1   

    * - Request          
      - View
    * - .. code-block:: JSON

          {
            "type": "vimeo",								
            "url": "player.vimeo.com/video/12345678"
          }  

      - .. image:: images/activity_vimeo_ex_01.png


Video         
~~~~~

Sources allowed to send: **customer**, **agent** and **bot**.

.. list-table::
    :widths: 5 10 50
    :header-rows: 1   
  
    * - Property     
      - Mandatory
      - Description
    * - type
      - Yes
      - Must be **video**.
    * - url
      - Yes
      - | The video url, which can be in anyone of the following formats:
        
        * `.mp4` (preferred)
        * `.mov`
    * - label
      - No
      - | The label of this audio. Think of the label as a title to be displayed.
        | **Note**: label is channel specific and may not render on certain channels.
    * - mimeType
      - No
      - The mime type of the video. Hubster will try it's best to determine the mime type 
        based on the **url**.



**Example**

.. list-table::
    :widths: 10 200
    :header-rows: 1   

    * - Request          
      - View
    * - .. code-block:: JSON

          {
            "type": "video",
            "url": "http://site.com/myvideo.mp4"
          }  

      - .. image:: images/activity_video_ex_01.png


Audio      
~~~~~

Sources allowed to send: **customer**, **agent** and **bot**.

.. list-table::
    :widths: 5 10 50
    :header-rows: 1   
  
    * - Property     
      - Mandatory
      - Description
    * - type
      - Yes
      - Must be **audio**.
    * - url
      - Yes
      - | The audio url, which can be in anyone of the following formats:
        
        * `.mp3` (preferred)
        * `.mp4`
        * `.wav`
    * - label
      - No
      - | The label of this audio. Think of the label as a title to be displayed.
        | **Note**: label is channel specific and may not render on certain channels.
    * - mimeType
      - No
      - The mime type of this audio. Hubster will try it's best to determine the mime type 
        based on the **url**.
    
**Example**

.. list-table::
    :widths: 10 200
    :header-rows: 1   

    * - Request          
      - View
    * - .. code-block:: JSON

          {
            "type": "audio",
            "url": "http://site.com/myaudio.mp3"
          }  

      - .. image:: images/activity_audio_ex_01.png


Image      
~~~~~

Sources allowed to send: **customer**, **agent** and **bot**.

.. list-table::
    :widths: 5 10 50
    :header-rows: 1   
  
    * - Property     
      - Mandatory
      - Description
    * - type
      - Yes
      - Must be **image**.
    * - url
      - Yes
      - The image url.
    * - urlAnchor
      - No
      - The url anchor. Used when user clicks on image.
    * - alt
      - No
      - The alternate text for this image.
    * - title
      - No
      - | The text to show on the image.         
        | **Note**: title is channel specific and may not render on certain channels.
    * - channels
      - No
      - Channel specific applied properties. The example below shows how to render 
        the title on a **Webchat** channel.


**Example**

.. list-table::
    :widths: 10 200
    :header-rows: 1   

    * - Request          
      - View
    * - .. code-block:: JSON

          {
            "type": "image",
            "url": "http://site.com/myimage.png",
            "alt": "Some alternate text",
            "title": "Eva Green",
            "channels": [{
                "type": "Webchat",
                "metadata": [
                    { 
                      "key": "caption-show", 
                      "value": "true" 
                    },
                    { 
                      "key": "caption-color", 
                      "value": "white" 
                    }
                ]
            }]
          }  

      - .. image:: images/activity_image_ex_01.png



Attachment      
~~~~~~~~~~

Sources allowed to send: **customer**, **agent** and **bot**.

.. list-table::
    :widths: 5 10 50
    :header-rows: 1   
  
    * - Property     
      - Mandatory
      - Description
    * - type
      - Yes
      - Must be **attachment**.
    * - label
      - Yes
      - The label for this attachment.
    * - mimeType
      - Yes
      - The mime type for this attachment i.e pdf, etc.
    * - url
      - Yes
      - The attachment url.
    
**Example**

.. list-table::
    :widths: 10 200
    :header-rows: 1   

    * - Request          
      - View
    * - .. code-block:: JSON

          {
            "type": "attachment",
            "label": "Year end report",
            "mimeType": "pdf",
            "url": "http://site.com/myfile.pdf"
          }  

      - .. image:: images/activity_attachment_ex_01.png



Location          
~~~~~~~~

Sources allowed to send: **customer**, **agent** and **bot**.

.. list-table::
    :widths: 5 10 50
    :header-rows: 1   
  
    * - Property     
      - Mandatory
      - Description
    * - type
      - Yes
      - Must be **location**.
    * - Address
      - See **note**
      - A fully qualified address.
    * - latitude
      - See **note**
      - A latitude coordinate value. **Note**: The longitude coordinate value must be supplied.
    * - longitude
      - See **note**
      - A longitude coordinate value. **Note**: The latitude coordinate value must be supplied.

    
**Example**

.. list-table::
    :widths: 10 200
    :header-rows: 1   

    * - Request          
      - View
    * - .. code-block:: JSON

          {
            "type": "location",
            "address": "2640 Matheson, Mississauga, ON",
            "latitude": 43.8425254,
            "longitude": -79.5240196
          }  

      - .. image:: images/activity_location_ex_01.png

.. note:: 
    Either a fully qualified **address** or a set of **latitude/longitude** coordinates must be supplied. 
    If both **address** or **latitude/longitude** are supplied, Hubster will resort to using 
    the **latitude/longitude** coordinates as the preferred option. 
    
    Please note, when using **latitude/longitude** coordinates, Hubster will try to yield the appropriate address. 
    However, if the address yielded is not exact, then the **latitude/longitude** coordinates may be off. 
    Alternatively, you can always use the **address** property without the need to provide **latitude/longitude** coordinates.


Contact
~~~~~~~

Sources allowed to send: **customer**, **agent** and **bot**.

.. list-table::
    :widths: 5 10 50
    :header-rows: 1   
  
    * - Property     
      - Mandatory
      - Description
    * - type
      - Yes
      - Must be **contact**.
    * - imageUrl
      - No
      - The image url to the contact.
    * - title
      - Yes
      - At minimum, the contact message requires a title. i.e. Person's name, company name, job title, etc.
    * - subtitle
      - No
      - A subtitle for the contact. i.e. company name, job title, etc.
    * - properties
      - No
      - | A tuplet made out of key/value/type set that can used to provide more metadata for the contact. See example.
        |

        .. note:: 
            The **type** portion of the tuplet is not required, however, if used, can provide additional 
            metadata for certain property types. For example, if Hubster detects that a 
            recipient device supports **vcards**, such as an SMS device, Hubster will create a 
            contact element, allowing the recipient of the message to store the contact to their device's contact list.
            
            Hubster supports the following **vcard** types and their counterpart:
            
            * address; ``work``, ``home``
            * phone; ``work``, ``home``, ``cell``
            * email
    * - channels
      - No
      - Channel specific applied properties. The example below shows how to render 
        the title on a **Webchat** channel.
    
    
**Example**

.. list-table::
    :widths: 10 200
    :header-rows: 1   

    * - Request          
      - View
    * - .. code-block:: JSON

          {
            "type": "contact",
            "imageUrl": "https://site.com/eva.png",
            "title": "Eva Green",
            "subtitle": "Mighty Health",
            "properties": [
              { 
                "key": "Title",
                "value": "Health Advisor/Coach"
              },
              {
                "key": "Address",
                "value": "123 Main Street, Maple, ON",
                "type": "address;work"
              },
              {
                "key": "Cell",
                "value": "(416) 555-0001",
                "type": "phone;cell"
              },
              {
                "key": "Email",
                "value": "eva@mightyhealth.com",
                "type": "email"
              }
            ],
            "channels": [
              {
                "type": "Webchat",
                "metadata": [
                  {
                    "key": "caption-show",
                    "value": "true"
                  },
                  {
                    "key": "caption-color",
                    "value": "white"
                  }
                ]
              }
            ]
          }           

      - .. image:: images/activity_contact_ex_01.png

Card       
~~~~

Sources allowed to send: **customer**, **agent** and **bot**.

.. list-table::
    :widths: 5 10 50
    :header-rows: 1   
  
    * - Property     
      - Mandatory
      - Description
    * - type
      - Yes
      - Must be **card**.
    * - urlType
      - No
      - | If **url** is supplied, then this property is required. 
        | The possible types are as follows:
        
        * image
        * youtube 
        * vimeo
        * video 
        * audio
    * - url
      - No
      - | The link to the resource to display. The **urlType** property must be provided.
        | The possible types are as follows:

        * image
        * youtube 
        * vimeo
        * video 
        * audio
    
    * - fallbackImageUrl
      - No
      - When supplying a **url** that supports an image placeholder, such as youtube for example, 
        and the link doesn't support an image, Hubster will use the **fallbackImageUrl** link as an alternate.

    * - title
      - No
      - A title to display.
    * - subtitle
      - No
      - A subtitle to display.
    * - content
      - No
      - The content to display.
    * - channels
      - No
      - Channel specific applied properties. The example below shows how to render 
        the title on a **Webchat** channel. Note: only applicable if **urlType=image** 

**Example**

.. list-table::
    :widths: 10 200
    :header-rows: 1   

    * - Request          
      - View
    * - .. code-block:: JSON

          {
            "type": "card",	
            "urlType": "image",
            "imageUrl": "https://site.com/car.png",
            "title": "Victorious",
            "subtitle": "European style",
            "content": "Lorem Ipsum is simply..."
            "channels": [
              {
                "type": "Webchat",
                "metadata": [
                  {
                    "key": "caption-show",
                    "value": "true"
                  },
                  {
                    "key": "caption-color",
                    "value": "white"
                  }
                ]
              }
            ]
          }           

      - .. image:: images/activity_card_ex_01.png

    * - .. code-block:: JSON

          {
            "type": "card",	
            "urlType": "youtube",
            "imageUrl": "https://youtube.com/embed/abc",
            "title": "Cosmic Journeys",
            "subtitle": "Space Odyssey",
            "content": "Lorem Ipsum is simply..."
          }           

      - .. image:: images/activity_card_ex_02.png


Carousel         
~~~~~~~~

Sources allowed to send: **agent** and **bot**.

.. list-table::
    :widths: 5 10 50
    :header-rows: 1   
  
    * - Property     
      - Mandatory
      - Description
    * - type
      - Yes
      - Must be **carousel**.
    * - items
      - yes
      - | Must contain one or more of the following message types:
        
        * image
        * youtube 
        * vimeo
        * video 
        * audio
    * - channels
      - No
      - Channel specific applied properties. The example below shows how to render 
        the title on a **Webchat** channel. Note: only applicable to image items.

**Example**

.. list-table::
    :widths: 10 200
    :header-rows: 1   

    * - Request          
      - View
    * - .. code-block:: JSON

          {
            "type": "carousel",	
            "items": [
              {
                "title": "Victorious",
                "content": "Lorem Ipsum is...",
                "urlType": "image",
                "url": "http://site.com/image1.png",
                "actions": [
                  {
                    "type": "reply",
                    "title": "Select",
                    "payload": "Victorious"
                  },
                  {
                    "type": "link",
                    "title": "More Info",
                    "url": "https://hubster.io"
                  }
                ]
              },
              {
                "title": "Green Dragon",
                "content": "Lorem Ipsum is...",
                "urlType": "image",
                "url": "http://site.com/image2.png",
                "actions": [
                  {
                    "type": "reply",
                    "title": "Select",
                    "payload": "Green Dragon"
                  },
                  {
                    "type": "link",
                    "title": "More Info",
                    "url": "https://hubster.io"
                  }
                ]
              },
              {
                "title": "Panther",
                "content": "Lorem Ipsum is...",
                "urlType": "image",                
                "url": "http://site.com/image3.png",
                "actions": [
                  {
                    "type": "reply",
                    "title": "Select",
                    "payload": "Black Panther"
                  },
                  {
                    "type": "link",
                    "title": "More Info",
                    "url": "https://hubster.io"
                  }
                ]
              }
            ],
            "channels": [
              {
                "type": "Webchat",
                "metadata": [
                  {
                    "key": "caption-show",
                    "value": "true"
                  },
                  {
                    "key": "caption-color",
                    "value": "white"
                  }
                ]
              }
            ]
          }           

      - .. image:: images/activity_carousel_ex_01.png


    * - .. code-block:: JSON

          {
            "type": "carousel",	
            "items": [
              {
                "title": "Cosmic Journeys",
                "content": "Lorem Ipsum is...",
                "urlType": "youtube",
                "url": "youtube.com/embed/1234",
                "actions": [
                  {
                    "type": "reply",
                    "title": "Select",
                    "payload": "Cosmic Journeys"
                  },
                  {
                    "type": "link",
                    "title": "Watch",
                    "url": "youtube.com/embed/1234"
                  }  
                ]
              },
              {
                "title": "Space",
                "content": "Lorem Ipsum is...",
                "urlType": "vimeo",
                "url": "player.vimeo.com/video/1234",
                "actions": [
                  {
                    "type": "reply",
                    "title": "Select",
                    "payload": "Space"
                  },
                  {
                    "type": "link",
                    "title": "Watch",
                    "url": "player.vimeo.com/video/1234"
                  }  
                ]
              },
              {
                "title": "Elephants",
                "content": "Lorem Ipsum is...",
                "urlType": "video",
                "url": "http://site.com/v1.mp4",                
                "actions": [
                  {
                    "type": "reply",
                    "title": "Select",
                    "payload": "Elephants"
                  },
                  {
                    "type": "link",
                    "title": "Watch",
                    "url": "https//site.com/v1.mp4"
                  }  
                ]
              }
            ]           
          }           

      - .. image:: images/activity_carousel_ex_02.png


.. note:: 
    Certain devices do not support carousels. If a device is unable to display a carousel,
    Hubster will render the carousel as a list.    


List
~~~~

Sources allowed to send: **agent** and **bot**.

.. note:: 
    Lists are similar to Carousels. The only differences are: 
    how it's displayed and that a list provides the ability to offer a global 
    set of **actions** for the message type.
    
.. list-table::
    :widths: 5 10 50
    :header-rows: 1   
  
    * - Property     
      - Mandatory
      - Description
    * - type
      - Yes
      - Must be **list**.
    * - items
      - yes
      - | Must contain one or more of the following message types:
        
        * image
        * youtube 
        * vimeo
        * video 
        * audio
    * - actions
      - No
      - | A list of actions containing zero or more of the following **action types**:      

        * postback
        * reply
        * link 
    * - channels
      - No
      - Channel specific applied properties. The example below shows how to render 
        the title on a **Webchat** channel. Note: only applicable to image items.

**Example**

.. list-table::
    :widths: 10 200
    :header-rows: 1   

    * - Request          
      - View
    * - .. code-block:: JSON

          {
            "type": "list",	
            "items": [
              {
                "title": "Alien",
                "content": "Lorem Ipsum is...",
                "urlType": "image",                
                "url": "http://site.com/image1.png",
                "actions": [
                  {
                    "type": "reply",
                    "title": "Select",
                    "payload": "Alien"
                  },
                  {
                    "type": "link",
                    "title": "More Info",
                    "url": "https://hubster.io"
                  }
                ]
              },
              {
                "title": "Red Baron",
                "content": "Lorem Ipsum is...",
                "urlType": "image",                
                "url": "http://site.com/image2.png",
                "actions": [
                  {
                    "type": "reply",
                    "title": "Select",
                    "payload": "Red Baron"
                  },
                  {
                    "type": "link",
                    "title": "More Info",
                    "url": "https://hubster.io"
                  }
                ]
              }
            ],
            "actions": [
              {
                "type": "postback",
                "title": "See more options",
                "payload": "More Options"
              },
              {
                "type": "link",
                "title": "Check our catalog",
                "url": "https://hubster.io"
              }
            ],	            
            "channels": [
              {
                "type": "Webchat",
                "metadata": [
                  {
                    "key": "caption-show",
                    "value": "true"
                  },
                  {
                    "key": "caption-color",
                    "value": "white"
                  }
                ]
              }
            ]
          }           

      - .. image:: images/activity_list_ex_01.png

   
.. note:: 
    Certain devices do not support lists. If a device is unable to display a list,
    Hubster will render the list as a carousel.    

Commands
~~~~~~~~

Sources allowed to send: **agent** and **bot**.

Commands are no different then sending a simple one line **text** message type. 
The main difference is when issuing a command it must start with a double (colon) **::** 
to be recognized. For example when issuing this text, **::some_command** *-arg1* *-arg2*, ... 
Hubster will treat this as a command to be processed.

See examples below:

.. list-table::
    :widths: 50
    :header-rows: 1

    * - Request                
    * - .. code-block:: JSON

          {
            "type": "text",								
            "text": "::resp -n contact.eva.green"
          }  

    * - .. code-block:: JSON

          {
            "type": "text",								
            "text": "::trans -force -n shopify"
          }  

.. _ref_activities_event_types:

Event Types
^^^^^^^^^^^

Event types are similar to message types and are must simpler in nature.

.. code-block:: JSON

    {        
        "type": "event"
        "event": {
            "type": "typing_on"
        }                
    }  



.. code-block:: JSON

    {        
        "type": "event"
        "event": {
            "type": "payload",
            "payloadType": "my.payload.01",
            "payload": {
                "data1": "value1",
                "data2": "value2",
                "data3": "value3"
            }
        }                
    }  


.. list-table::
    :widths: 5 10 50
    :header-rows: 1   
  
    * - Property     
      - Mandatory
      - Description
    * - type
      - Yes
      - Must be **list**.
    * - items
      - yes
      - | Must contain one or more of the following message types:
        
        * image
        * youtube 
        * vimeo
        * video 
        * audio






Basic
~~~~~



.. note:: 
    Basic event types are currently not supported by Hubster. This feature is currently on our road-map.
    





.. this will be a future feature and currently not supported
.. note: not all devices support these features
.. public const string Seen = "seen";
.. public const string TypingOn = "typing_on";
.. public const string TypingOff = "typing_off";

Payload
~~~~~~~

