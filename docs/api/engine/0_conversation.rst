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
                "tenant": {
                    "tenantId": "...000000000001",
                    "name": "Dev Tenant",
                    "tenantTypeId": 105,
                    "servicePackageTypeId": "Internal",
                    "dataRetention": 90,
                    "responseCommands": true,
                    "externalCommands": true,
                    "transferCommands": true,
                    "translations": true,
                    "sentiment": true,
                    "historicalAccess": true,
                    "statusId": 1000,
                    "created": "2017-07-18T03:52:34.53",
                    "modified": "2017-07-18T03:52:34.53"
                },
                "name": "Dev Hub (Websocket)",
                "description": "Dev Hub 2 (Websocket)",
                "statusId": 2000,
                "created": "2019-01-01T00:00:00",
                "modified": "2019-01-01T00:00:00"
            },
            "integrationTypeId": "Customer",
            "channelId": "Direct",
            "name": "Direct Customer Webhook",
            "configuration": "{\"webhook_url\": ... }",
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
    :widths: 5 50
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
    Ross to explain dynamic nature of properties object.

**Properties**

.. code-block:: JSON

    {        
        "profile": { 
            "device": "Direct",		
            "full name":"User name here"            
        },
        "additional": {
        }        
    }

.. list-table::
  :widths: 15 10 60
  :header-rows: 1

  * - Property     
    - Mandatory
    - Description
  * - device
    - No
    - User device.
  * - full name
    - No
    - User name (full name).
  * - additional
    - No
    - Any additional key-value pairs to add.

**Response** 200 (OK)

.. code-block:: JSON

    {
        "tenantId": "...000000000001",
        "hubId": "...0000000000a2",
        "integrationId": "...000000000023",
        "conversationId": "a9cff9d8-0cb2-40f9-b787-01756ca7b92f",
        "tokenId": "9jP61d8EfmVgSnUtBZsMNw==",
        "properties": {
            "profile": {
                "device": "Direct",
                "full name": "User name here"                
            },
        "additional": {}
        },
        "openedDateTime": "2020-10-28T00:42:12.6452901Z",
        "isNew": true
    }