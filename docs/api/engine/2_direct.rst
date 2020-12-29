.. role:: underline
    :class: underline

.. _ref_engine_direct:

Direct
^^^^^^

The **Direct** API is used primarily by :ref:`Direct Channel Types <ref_api_channel_types>` when submitting
:ref:`Message <ref_activities_message_types>` or 
:ref:`Event <ref_activities_event_types>` 
:ref:`Activity <ref_activities>` types.

**POST** */inbound/customer/v1/direct/activity/{conversationId}*

**Headers**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Header     
     - Description
   * - Authorization
     - Bearer ``your portal access token``
   * - Content-Type
     - ``application/json``

**Url Segments**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Segment     
     - Description
   * - conversationId
     - The conversation id to send this activity.

**Request Properties**

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
        This can only be :ref:`message type<ref_activities_message_types>` or 
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
    * - message
      - See **Description**
      - When **type** is set to :ref:`message <ref_activities_message_types>` 
        then this node is required.
    * - event
      - See **Description**
      - When **type** is set to :ref:`event <ref_activities_event_types>` 
        then this node is required.
        
**Example Request Body**

.. code-block:: JSON

    {
        "externalId": "some-external-id",
        "type": "message | event",
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


**Response** : 200 (OK)

.. code-block:: JSON

    {
        "status": 200,
        "eventId": 1609281295385,
        "externalId": "some-external-id",
        "hubId": "00000000-0000-0000-0000-0000000000a1",
        "conversationId": "290e83ff-0ae1-4a62-ae8e-01759ad73ffd",
        "integrationId": "00000000-0000-0000-0000-000000000001",
        "interactionId": "d645f70e-30e2-4649-938c-0176b0a3d41b"
    }

.. note:: 
    If the activity type was **event**, then the **interactionId** will not be part of 
    the response.
    

.. list-table::
    :widths: 10 50
    :header-rows: 1   

    * - HTTP Status
      - Description
    * - 200
      - OK response. The body of the response will include the data requested.
    * - 400
      - Bad request. The body of the response will have :ref:`more info<ref_api_portal_error_codes>`.
    * - 401
      - Unauthorized. Token is invalid.
    * - 403
      - Forbidden. Access to the requested resource is forbidden.
    * - 408
      - Timed out. The request timed out.
    * - 429
      - Too many requests. API usage limit has been reached.
    * - 500
      - Internal server error. There was an internal issue with the service.
    * - 503
      - Service unavailable. The service is unavailable.
