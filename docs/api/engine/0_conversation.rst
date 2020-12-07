.. role:: underline
    :class: underline

Conversations
^^^^^^^^^^^^^

Get Conversation
****************

Get Conversation object using conversation identifier.

**GET** */api/v1/conversations/{conversationId}*

**Headers**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Header     
     - Description
   * - Authorization
     - Bearer ``your engine access token``
   * - Content-Type
     - ``application/json``

**Url Segments**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Segment     
     - Description
   * - conversationId
     - The conversation id to get.

**Response** : 200 (OK)

.. code-block:: JSON

    {
        "conversationId": "a9cff9d8-0cb2-40f9-b787-01756ca7b92f",
        "integrationId": "...000000000023",
        "tokenId": "9jP61d8EfmVgSnUtBZsMNw==",
        "integration": {
            "integrationId": "...000000000023",
            "hubId": "...0000000000a2",
            "hub": {
                "hubId": "...0000000000a2",
                "tenantId": "...000000000001",               
                "name": "Dev Hub (Websocket)",
                "description": "Dev Hub 2 (Websocket)",
                "statusId": 2000,
                "created": "2019-01-01T00:00:00",
                "modified": "2019-01-01T00:00:00"
            },
            "integrationTypeId": "Customer",
            "channelId": "Direct",
            "name": "Direct Customer Webhook",            
            "statusId": 3000,
            "created": "2018-01-01T00:00:00",
            "modified": "2018-01-01T00:00:00"
        },
        "properties": {
            "profile": {
                "device": "Direct",
                "full name": "Any name"                
            },
             "additional": {}
        },
        "openedDateTime": "2019-10-28T00:42:12.6452901"
    }

.. list-table::
    :widths: 10 50
    :header-rows: 1   

    * - HTTP Status
      - Description
    * - 200
      - OK response. The body of the response will include the data requested.
    * - 401
      - Unauthorized. Token is invalid.
    * - 403
      - Forbidden. Access to the requested resource is forbidden.
    * - 404
      - Not found. Resource not found.
    * - 408
      - Timed out. The request timed out.
    * - 429
      - Too many requests. API usage limit has been reached.
    * - 500
      - Internal server error. There was an internal issue with the service.
    * - 503
      - Service unavailable. The service is unavailable.

Establish Conversation
**********************

Establish (create) new Conversation object.

**POST** */api/v1/conversations/establish*

**Headers**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Header     
     - Description
   * - Authorization
     - Bearer ``your engine access token``
   * - Content-Type
     - ``application/json``

**Request Properties**

.. list-table::
   :widths: 15 10 60
   :header-rows: 1

   * - Property     
     - Mandatory
     - Description
   * - integrationId
     - Yes
     - Integration identifier.
   * - binding       
     - Yes
     - Binding key used to get conversation.
   * - channelType
     - Yes
     - Type of channel to filter by.
     
       Valid options is:

       -- *Direct* = 2000       
   * - properties
     - No
     - See :ref:`properties<ref_engine_properties_establish_conversation>` object for more info.

.. _ref_engine_properties_establish_conversation:

.. note:: 
    **Properties** can be though of as **metadata** bound to a conversation during establishment. 
    When working for Direct interaction types, the developer can assigned any number properties as 
    necessary. Properties can have one or more collections each containing key/value pairs.
    In the example below, two such collections have been defined.

    By default, Hubster will generate a **profile** collection if not defined. This collection 
    will contain at most, a **device** and **full name** key/value pair. 
    The developer can override anyone of the following values but can also add their own 
    custom key/value pair:

    * **profile.device**
    * **profile.full name**
    * **profile.first name**
    * **profile.last name**
    * **profile.user name**
    * **profile.gender**  
    * **profile.local**
    * **profile.time zone**
    * **profile.imageUrl**
    * **profile.phone**
    * **profile.address**
    * **profile.email**

    | If **profile.device** is not provided, Hubster will default to **Direct**.    
    | If **profile.full name** is not provided, Hubster will default to a random **fun-name**.

    

**Properties**

.. code-block:: JSON

    {        
        "profile": { 
            "device": "Direct",		
            "full name":"User name here",
            "phone": "416-555-0001",
            "some_custom1": "value1",
            "some_custom2": "value2"
        },
        "additional": {
            "some_custom1": "value1",
            "some_custom2": "value2"
        }        
    }


**Response** 200 (OK)

.. code-block:: JSON

    {
        "tenantId": "...000000000001",
        "hubId": "...0000000000a2",
        "integrationId": "...000000000023",
        "conversationId": "a9cff9d8-0cb2-40f9-b787-01756ca7b92f",
        "tokenId": "9jP61d8EfmVgSnUtBZsMNw==",
        "openedDateTime": "2020-10-28T00:42:12.6452901Z",
        "isNew": true,
        "properties": {
            "profile": {
                "device": "Direct",
                "full name": "User name here"                
            },
        "additional": {}
        }
    }