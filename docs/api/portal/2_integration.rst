.. role:: underline
    :class: underline

Integrations
^^^^^^^^^^^^

Create
******

Creates an Integration.

**POST** */api/v1/integrations/hubs/{hubId}*

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
   * - hubId
     - The hub id affected.

**Request Properties**

.. list-table::
   :widths: 15 10 60
   :header-rows: 1

   * - Property     
     - Mandatory
     - Description
   * - channelId
     - Yes
     - Has to be one of the following :ref:`Channel Types<ref_api_channel_types>`.
   * - name
     - Yes
     - Unique name for integration per Hub.
   * - statusId
     - No
     - | Integration status. 

       | Valid options are:        
       | -- *Active* = 3000
       | -- *Paused* = 3002
       
       Default is *Active* = 3000, if no value supplied.
   * - configuration
     - Yes
     - See :ref:`configuration<ref_portal_integration_create_config>` properties for each individual **channelId**.

**Example Request Body** 

.. note:: 
    The request body below uses **TwilioSMS** as an example. It should be noted that  
    :ref:`configuration<ref_portal_integration_create_config>` properties for each channel type differs. 
    Please use the correct configuration specific to the **channelId** value defined. 

.. code-block:: JSON

  {                        	
    "channelId": "TwilioSMS",
    "name": "My cool integration name.",
    "statusId": 3000,    
    "configuration": {  
      "authToken": "cb8c5367c3c4586ecb589e25570...",
      "accountSid": "AC1fc1c1722444b0c6313d3ae988b...",
      "numberSid": "PN667435536f4d1cefdf054abf99..."    
    }	
  }	


.. list-table::
    :widths: 5 50
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

.. _ref_portal_integration_create_config:

**Configurations**

:underline:`TwilioSMS`

.. code-block:: JSON

  {
    "authToken": "cb8c5367c3c4586ecb589e25570...",
    "accountSid": "AC1fc1c1722444b0c6313d3ae988b...",
    "numberSid": "PN667435536f4d1cefdf054abf99..."    
  }	

.. list-table::
  :widths: 15 10 60
  :header-rows: 1

  * - Property     
    - Mandatory
    - Description
  * - authToken
    - Yes
    - Twilio authorization token.
  * - accountSid
    - Yes
    - Twilio account SID.
  * - numberSid
    - Yes
    - Twilio phone number SID.

**Response** 200 (OK)

.. code-block:: JSON

  {                        	
    "integrationId": "00000000-0000-0000-0000-000000000000",
    "hubId": "00000000-0000-0000-0000-000000000000",      
    "integrationTypeId": "Customer",      
    "channelId": "TwilioSMS",
    "name": "My cool integration name.",
    "statusId": 3000,    
    "configuration": {        
      "accountSid": "AC1fc1c1722444b0c6313d3da98...",
      "authToken": "cb8c5367c3c4586ecb589e25570....",
      "numberSid": "PN667435536f4d1cefdf054ecf9....",
      "phoneNumber": "+16476960000",
      "capabilities": {
        "mms": true,
        "sms": true,
        "voice": true
      }
    }	
  }

:underline:`Messenger`

.. code-block:: JSON

  {
    "pageAccessToken": "EAAFBmgAdBToBADCvmo5w10tmlh97uxhtorpi5Adrdo0wtwFfXfkNxxLAY29AxwBHJNfXH5rR..."
  }	

.. list-table::
  :widths: 15 10 60
  :header-rows: 1

  * - Property     
    - Mandatory
    - Description
  * - pageAccessToken
    - Yes
    - Facebook page access token.


**Response** 200 (OK)

.. code-block:: JSON

  {                        	
    "integrationId": "00000000-0000-0000-0000-000000000000",
    "hubId": "00000000-0000-0000-0000-000000000000",      
    "integrationTypeId": "Customer",      
    "channelId": "Messenger",
    "name": "My cool integration name.",
    "statusId": 3000,    
    "configuration": {        
      "appId": "35360465938...",
      "pageId": "1013889883...",
      "pageAccessToken": "EAAFBm..."
    }	
  }

:underline:`WebChat`

.. code-block:: JSON

  {        
    "allowedOrigins": [
      "localhost",
      "hubster.io"        
    ],        
    "start": [
      {
        "type": "text",
        "text": "Welcome to Hubster! How can we help you?"
      }
    ]
  }

.. list-table::
  :widths: 15 10 60
  :header-rows: 1

  * - Property     
    - Mandatory
    - Description
  * - allowedOrigins
    - Yes
    - One or more domains hosting the WebChat component.
  * - start
    - No
    - An array of Hubster :ref:`messages types<ref_activities_message_types>`.

**Response** 200 (OK)

.. code-block:: JSON   

  {
      "integrationId": "00000000-0000-0000-0000-000000000000",
      "hubId": "00000000-0000-0000-0000-000000000000",
      "integrationTypeId": "Customer",
      "channelId": "WebChat",
      "name": "Webchat",
      "statusId": 3000,
      "configuration": {
          "AllowedOrigins": [
              "localhost",
              "hubster.io"
          ],
          "Echo": true,
          "Start": [
              {
                  "type": "text",
                  "text": "Welcome to Hubster! How can we help you?"
              }
          ]
      }
  }


:underline:`Direct`

.. code-block:: JSON

  {        
    "integrationType": "Agent",
    "echo": true,
    "webhookUrl": "https://url_end_point.com"
  }

.. list-table::
  :widths: 15 10 60
  :header-rows: 1

  * - Property     
    - Mandatory
    - Description
  * - integrationType
    - Yes
    - Must be a supported :ref:`integration<ref_api_integration_types>` type.
  * - echo
    - No
    - If yes, when an activity is received from this integration, it will echo it back.
  * - webhookUrl
    - No
    - The endpoint to receive Hubster :ref:`Activities<ref_activities>`.
      If not supplied, activities will be delivered via websockets.        
  * - start
    - No
    - An array of Hubster :ref:`messages types<ref_activities_message_types>`.

**Response** 200 (OK)

.. code-block:: JSON

  {                        	
    "integrationId": "00000000-0000-0000-0000-000000000000",
    "hubId": "00000000-0000-0000-0000-000000000000",
    "integrationTypeId": "Agent",      
    "channelId": "Direct",
    "name": "My cool integration name.",
    "statusId": 3000,        
    "configuration": {        
    "integrationType": "Agent",
    "echo": true,
    "webhookUrl": "https://url_end_point.com",
    "publicSigningKey": "6DF60E ...",
    "privateSigningKey": "E0A42 ...",
    "start": [
      {
        "type": "text",
        "text": "Welcome to Hubster! How can we help you?"
      }
    ]      
  }

:underline:`System`

.. code-block:: JSON

  {
    "webhookUrl": "https://url_end_point.com",
    "events": [
      "message:customer",
      "message:agent",
      "message:bot"              
    ]
  }

.. list-table::
  :widths: 15 10 60
  :header-rows: 1

  * - Property     
    - Mandatory
    - Description
  * - webhookUrl
    - Yes
    - The endpoint to receive Hubster :ref:`Activities<ref_activities>`
  * - events
    - Yes
    - The :ref:`activity event filter(s)<ref_webhooks_events>` to be event on.

**Response** 200 (OK)

.. code-block:: JSON

  {
      "integrationId": "00000000-0000-0000-0000-000000000000",
      "hubId": "00000000-0000-0000-0000-000000000000",
      "integrationTypeId": "System",
      "channelId": "System",
      "name": "My cool integration name.",
      "statusId": 3000,
      "configuration": {
          "events": [
              "message:customer",
              "message:agent",
              "message:bot"
          ],
          "webhookUrl": "https://url_end_point.com",
          "publicSigningKey": "6DF60E ...",
          "privateSigningKey": "E0A42 ...",
      }
  }

:underline:`Slack`

.. code-block:: JSON

  {
    "code": "EAAFBmgAdBToBADCvmo5w10tmlh97uxhtorpi5Adrdo0wtwFfXfkNxxLAY29AxwBHJNfXH5rR...",
    "state" : "TODO:"
  }	

.. list-table::
  :widths: 15 10 60
  :header-rows: 1

  * - Property     
    - Mandatory
    - Description
  * - code
    - Yes
    - Slack oauth2 code.
  * - state
    - Yes
    - UNIX timespan plus client secret.

**Response** 200 (OK)

.. code-block:: JSON

  {                        	
    "integrationId": "00000000-0000-0000-0000-000000000000",
    "hubId": "00000000-0000-0000-0000-000000000000",      
    "integrationTypeId": "Agent",            
    "channelId": "Slack",
    "name": "My cool integration name.",
    "statusId": 3000,    
    "configuration": {        
      "botAccessToken": "xoxb-193043142226-...",
      "appAccessToken": "xoxp-193043142226-...",
      "defaultPublicChannel": "general",
      "teamId": "T5P19488N",
      "botName": "Hubster.io"          
    }	
  }


Update
******

Updates an Integration.

**POST** */api/v1/integrations/hubs/{integrationId}*

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
   * - integrationId
     - The integration id affected.

**Request Properties**

.. list-table::
   :widths: 15 10 60
   :header-rows: 1

   * - Property     
     - Mandatory
     - Description
   * - name
     - No
     - Unique name for integration per Hub.
   * - statusId
     - No
     - | Integration status. 
       
       | Valid options are:        
       | -- *Active* = 3000
       | -- *Paused* = 3002
   * - configuration
     - No
     - | See :ref:`configuration<ref_portal_integration_update_config>` properties for each individual **channelId**.       


**Example Request Body** 

.. code-block:: JSON

  {    
    "name": "Direct",
    "statusId": 3002,
    "configuration": {  
       "Echo": true,
       "webhookUrl": "http://hubster.io/v1/api/integration?customer=1"
    }	
  }

.. _ref_portal_integration_update_config:

**Configurations**

.. note:: 
      If you need to update any configuration value, you need to provide **all required** values specific to that channel type. 
      In other words, the complete **configuration** object will replace the old one.

.. warning::
      The following integration types cannot have their **configuration** values updated due to re-authenticating 
      with their respective service providers. Any attempt will be ignored.

        * **TwilioSMS**
        * **Messenger**
        * **Slack** 

      If you need to update their configuration, you must first **delete** the original integration and **recreate** a new one.


:underline:`WebChat`

.. code-block:: JSON

    {        
      "allowedOrigins": [
          "localhost",
          "hubster.io"          
      ],        
      "start": 
          [
            {
              "type": "text",
              "text": "Welcome to Hubster! How can we help you?"
            }
          ]
    }

.. list-table::
  :widths: 15 10 60
  :header-rows: 1

  * - Property     
    - Mandatory
    - Description
  * - allowedOrigins
    - Yes
    - One or more domains hosting the WebChat component.
  * - start
    - No
    - An array of Hubster :ref:`messages types<ref_activities_message_types>`.

**Response** 200 (OK)

.. code-block:: JSON   

  {
      "integrationId": "00000000-0000-0000-0000-000000000000",
      "hubId": "00000000-0000-0000-0000-000000000000",
      "integrationTypeId": "Customer",
      "channelId": "WebChat",
      "name": "Webchat",
      "statusId": 3000,
      "configuration": {
          "AllowedOrigins": [
              "localhost",
              "hubster.io"
          ],
          "Echo": true,
          "Start": [
              {
                  "type": "text",
                  "text": "Welcome to Hubster! How can we help you?"
              }
          ]
      }
  }

.. _ref_integration_update_direct:

:underline:`Direct`

.. code-block:: JSON

  {        
    "integrationType": "Agent",
    "echo": true,    
    "webhookUrl": "https://url_end_point.com",
    "regenerateKeys": true,
    "start": [
      {
        "type": "text",
        "text": "Welcome to Hubster! How can we help you?"
      }              
    ]
  }

.. list-table::
  :widths: 15 10 60
  :header-rows: 1

  * - Property     
    - Mandatory
    - Description
  * - integrationType
    - Yes
    - Must be a supported :ref:`integration<ref_api_integration_types>` type.
  * - echo
    - No
    - If yes, when an activity is received from this integration, it will echo it back.
  * - webhookUrl
    - No
    - The endpoint to receive Hubster :ref:`Activities<ref_activities>`.
      If not supplied, activities will be delivered via websockets.        
  * - regenerateKeys
    - No
    - This forces a new set of public/private keys to be generated.
  * - start
    - No
    - An array of Hubster :ref:`messages types<ref_activities_message_types>`.

**Response** 200 (OK)

.. code-block:: JSON

  {                        	
    "integrationId": "00000000-0000-0000-0000-000000000000",
    "hubId": "00000000-0000-0000-0000-000000000000",
    "integrationTypeId": "Agent",      
    "channelId": "Direct",
    "name": "My cool integration name.",
    "statusId": 3000,        
    "configuration": {        
    "integrationType": "Agent",
    "echo": true,
    "webhookUrl": "https://url_end_point.com",
    "publicSigningKey": "6DF60E ...",
    "privateSigningKey": "E0A42 ...",
    "start": [
      {
        "type": "text",
        "text": "Welcome to Hubster! How can we help you?"
      }
    ]      
  }

:underline:`System`

.. code-block:: JSON

  {    
    "webhookUrl": "https://url_end_point.com",
    "regenerateKeys": true,
    "events": [
      "message:customer",
      "message:agent",
      "message:bot"              
    ]
  }

.. list-table::
  :widths: 15 10 60
  :header-rows: 1

  * - Property     
    - Mandatory
    - Description
  * - webhookUrl
    - Yes
    - The endpoint to receive Hubster :ref:`Activities<ref_activities>`
  * - regenerateKeys
    - No
    - This forces a new set of public/private keys to be generated.
  * - events
    - Yes
    - The :ref:`activity event filter(s)<ref_webhooks_events>` to be event on.

**Response** 200 (OK)

.. code-block:: JSON

  {
      "integrationId": "00000000-0000-0000-0000-000000000000",
      "hubId": "00000000-0000-0000-0000-000000000000",
      "integrationTypeId": "System",
      "channelId": "System",
      "name": "My cool integration name.",
      "statusId": 3000,
      "configuration": {
          "events": [
              "message:customer",
              "message:agent",
              "message:bot"
          ],
          "webhookUrl": "https://url_end_point.com",
          "publicSigningKey": "6DF60E ...",
          "privateSigningKey": "E0A42 ...",
      }
  }


Get
***

Gets an Integration.

**GET** */api/v1/integrations/{integrationId}*

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
   * - integrationId
     - The integration to get.

**Response** 200 (OK)

.. note:: 
    The request body below uses **TwilioSMS** as an example. It should be noted that  
    :ref:`configuration<ref_portal_integration_create_config>` properties for each channel type differs.

.. code-block:: JSON

    {
      "integrationId": "00000000 ...",
      "hubId": "00000000 ...",
      "inboundId": "AC1fc1c1722444b0...",
      "integrationTypeId": 2,
      "channelId": 102,
      "name": "Twilio Test Number: 1647...",
      "statusId": 3000,
      "configuration": {
        "AcccountSid": "AC1fc1c172244...",
        "AuthToken": "cb8c5367c3c458...",
        "NumberSid": "PN667435536f4d...",
        "PhoneNumber": "+1647...",
          "Capabilities": {
          "Mms": true,
          "Sms": true,
          "Voice": true
          }
        }
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

**Response Body Examples**

:underline:`TwilioSMS`

.. code-block:: JSON

   {
      "integrationId": "00000000-0000-0000-0000-000000000000",
      "hubId": "00000000-0000-0000-0000-000000000000",
      "inboundId": "AC1fc1c1722444b0c6313d3....",
      "integrationTypeId": "Customer",
      "channelId": "TwilioSMS",
      "name": "Twilio Test Number: 16476960489",
      "statusId": 3000,
      "configuration": {
          "AccountSid": "AC1fc1c1722444b0c6313d...",
          "AuthToken": "cb8c5367c3c4586ecb589e2...",
          "NumberSid": "PN667435536f4d1cefdf054...",
          "PhoneNumber": "+16476960489",
          "Capabilities": {
              "Mms": true,
              "Sms": true,
              "Voice": true
          }
      }
  }

:underline:`Messenger`

.. code-block:: JSON

    {
        "integrationId": "00000000-0000-0000-0000-000000000000",
        "hubId": "00000000-0000-0000-0000-000000000000",
        "inboundId": "27623838....",
        "integrationTypeId": "Customer",
        "channelId": "Messenger",
        "name": "Messenger: Hubster Biz",
        "statusId": 3000,
        "configuration": {
            "AppId": "218851140...",
            "PageId": "27623838...",
            "PageAccessToken": "EAAfGcISnoh0BAEZBihIAC..."
        }
    }

:underline:`Web Chat`

.. code-block:: JSON

   {
      "integrationId": "00000000-0000-0000-0000-000000000000",
      "hubId": "00000000-0000-0000-0000-000000000000",
      "integrationTypeId": "Customer",
      "channelId": "WebChat",
      "name": "Webchat for Hubster Demo (Blank) ",
      "statusId": 3000,
      "configuration": {
          "allowedOrigins": [
              "localhost",
              "hubster.io"              
          ],
          "echo": true,
          "start": [
              {
                  "type": "text",
                  "text": "Welcome to Hubster! How can we help you?"
              }
          ]
      }
  }

:underline:`Direct`

.. code-block:: JSON

  {
      "integrationId": "00000000-0000-0000-0000-000000000000",
      "hubId": "00000000-0000-0000-0000-000000000000",
      "integrationTypeId": "Customer",
      "channelId": "Direct",
      "name": "Direct Customer (Webhook)",
      "statusId": 3000,
      "configuration": {
          "WebhookUrl": "http://localhost:5100/v1/api/integration?customer=1",
          "publicSigningKey": "6DF60E ...",
          "privateSigningKey": "E0A42 ...",
          "Echo": false,
          "WelcomeMessage": "Welcome to Hubster! How can we help you?"
      }
  }

:underline:`System`

.. code-block:: JSON

  {
      "integrationId": "00000000-0000-0000-0000-000000000000",
      "hubId": "00000000-0000-0000-0000-000000000000",
      "integrationTypeId": "System",
      "channelId": "System",
      "name": "My cool integration name.",
      "statusId": 3000,
      "configuration": {
          "events": [
              "message:customer",
              "message:agent",
              "message:bot"
          ],
          "webhookUrl": "https://url_end_point.com",
          "publicSigningKey": "6DF60E ...",
          "privateSigningKey": "E0A42 ...",
      }
  }

:underline:`Slack`

.. code-block:: JSON

    {
        "integrationId": "00000000-0000-0000-0000-000000000000",
        "hubId": "00000000-0000-0000-0000-000000000000",
        "integrationTypeId": "Agent",
        "channelId": "Slack",
        "name": "Slack for Hubster Demo",
        "statusId": 3000,
        "configuration": {
            "BotAccessToken": "xoxb-...",
            "AppAccessToken": "xoxp-...",
            "DefaultPublicChannel": "general",
            "TeamId": "T017QM...",
            "BotName": "Hubster.io"
        }
    }



Get by Channel Type
*******************

Gets a list of integrations for a given :ref:`Channel Type<ref_api_channel_types>`.

**GET** */api/v1/integrations/hubs/{hubId}/{channelType}*

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
   * - hubId
     - The hub id to obtain all integrations.
   * - channelType
     - The :ref:`Channel Type<ref_api_channel_types>` to filter by.

**Response** : 200 (OK)

.. code-block:: JSON

  [
      {
          "integrationId": "00000000-0000-0000-0000-000000000001",
          "hubId": "00000000-0000-0000-0000-000000000000",
          "integrationTypeId": "Customer",
          "channelId": "Direct",
          "name": "Direct Customer 2 (Webhook)",
          "statusId": 3000,
          "configuration": {
              "WebhookUrl": "http://localhost:5100/v1/api/integration?customer=1",
              "publicSigningKey": "6DF60E ...",
              "privateSigningKey": "E0A42 ...",
              "Echo": false,
              "WelcomeMessage": "Welcome to Hubster! How can we help you?"
          }
      },
      {
          "integrationId": "00000000-0000-0000-0000-000000000002",
          "hubId": "00000000-0000-0000-0000-000000000000",
          "integrationTypeId": "Agent",
          "channelId": "Direct",
          "name": "Direct Agent (Websocket)",
          "statusId": 3000,
          "configuration": {
              "Echo": true
          }
      }
  ]

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
    * - 408
      - Timed out. The request timed out.
    * - 429
      - Too many requests. API usage limit has been reached.
    * - 500
      - Internal server error. There was an internal issue with the service.
    * - 503
      - Service unavailable. The service is unavailable.  


Get Collection
**************

Gets a list of integrations.

**GET** */api/v1/integrations*

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

**Url Arguments**

.. list-table::
   :widths: 15 10 60
   :header-rows: 1

   * - Argument     
     - Mandatory
     - Description
   * - hubId
     - No
     - Filter by hub id.
   * - pageNumber
     - No
     - The requested page number. *Must be >= 0*.
   * - pageSize
     - No
     - The requested page size. *Must be >= 1 and <= 100*.

| **Response** : 200 (OK) 

| :ref:`paginated<ref_api_paginated_results>`

.. code-block:: JSON

  {
        "pageNumber": 0,
        "pageSize": 50,
        "total": 2,
        "results": [
           {
            "hubId": "3bc1e69f-c520-446f-ab2c-01751fd66a31",
            "tenantId": "abc1e69f-c888-875f-ee2c-45789fd66a00",
            "name": "Your New Cool Hub Name",
            "description": "This hub is cool",    
            "closeDormantConversation": 30,
            "statusId": 2000
          },
          {
            "hubId": "3bc1e69f-c520-446f-ab2c-01751fd66a32",
            "tenantId": "abc1e69f-c888-875f-ee2c-45789fd66a01",
            "name": "Your New Cool Hub Name 2",
            "description": "This hub is cool 2",    
            "closeDormantConversation": 30,
            "statusId": 2000
          }
        ]
    }

.. list-table::
    :widths: 5 50
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

