.. role:: underline
    :class: underline

Portal
======

Hubs
^^^^

Create
******

Create Hub.

**POST** */api/v1/hubs*

**Headers**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Header     
     - Details
   * - Authorization
     - Bearer ``your portal access token``
   * - Content-Type
     - ``application/json``

**Request Properties**

.. list-table::
   :widths: 15 10 60
   :header-rows: 1

   * - Property     
     - Mandatory
     - Details
   * - name
     - Yes
     - Unique Hub name for tenant.
   * - description       
     - Yes
     - Hub description.
   * - closeDormantConversation       
     - No
     - | The number of days to close this conversation if dormant.
       | If no value supplied, the conversation will remain open until
       | a command has been initiated.
   * - statusId
     - No
     - | Hub status. Default is *Active* = 2000, if no value supplied.
       | Valid options are:        
       | -  *Active* = 2000
       | -  *Paused* = 2002

**Example Request Body**

.. code-block:: JSON

    {
        "name": "Your New Cool Hub Name",
        "description": "Provide some brief description for your new Hub",
        "closeDormantConversation": 30,
        "statusId": 2000
    }

**Response** : 200 (OK)

.. code-block:: JSON

    {
        "hubId": "3bc1e69f-c520-446f-ab2c-01751fd66a31",
        "tenantId": "00000000-0000-0000-0000-000000000001",
        "name": "Your New Cool Hub Name",
        "description": "Provide some brief description for your new Hub",        
        "closeDormantConversation": 30,
        "statusId": 2000,
        "created": "2020-10-13T02:42:26.9932101Z",
        "modified": "2020-10-13T02:42:26.9932101Z"
    }

.. list-table::
    :widths: 5 50
    :header-rows: 1   

    * - HTTP Status
      - Meaning
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


Update
******

Update Hub.

**PUT** */api/v1/hubs/{hubId}*

**Headers**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Header     
     - Details
   * - Authorization
     - Bearer ``your portal access token``
   * - Content-Type
     - ``application/json``

**Request Properties**

.. list-table::
   :widths: 15 10 60
   :header-rows: 1

   * - Property     
     - Mandatory
     - Details
   * - name
     - No
     - Unique Hub name for tenant.
   * - description       
     - No
     - Hub description.
   * - closeDormantConversation       
     - No
     - | The number of days to close this conversation if dormant.
       | If no value supplied, the conversation will remain open until
       | a command has been initiated.
   * - statusId
     - No
     - | Hub status. Default is *Active* = 2000, if no value supplied.
       | Valid options are:        
       | -  *Active* = 2000
       | -  *Paused* = 2002

**Example Request Body**

.. code-block:: JSON

    {
        "name": "Your New Cool Hub Name",
        "description": "Provide some brief description for your new Hub",
        "closeDormantConversation": 30,
        "statusId": 2000
    }

**Response** : 200 (OK)

.. code-block:: JSON

    {
        "hubId": "3bc1e69f-c520-446f-ab2c-01751fd66a31",
        "tenantId": "00000000-0000-0000-0000-000000000001",
        "name": "Your New Cool Hub Name",
        "description": "Provide some brief description for your new Hub",        
        "closeDormantConversation": 30,
        "statusId": 2000,
        "created": "2020-10-13T02:42:26.9932101Z",
        "modified": "2020-10-13T02:42:26.9932101Z"
    }

.. list-table::
    :widths: 5 50
    :header-rows: 1   

    * - HTTP Status
      - Meaning
    * - 200
      - OK response. The body of the response will include the data requested.
    * - 400
      - Bad request. The body of the response will have :ref:`more info<ref_api_portal_error_codes>`.
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

Delete
******

Delete Hub.

**DELETE** */api/v1/hubs/{hubId}*

**Headers**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Header     
     - Details
   * - Authorization
     - Bearer ``your portal access token``
   * - Content-Type
     - ``application/json``

**Response** : 200 (OK)

.. list-table::
    :widths: 5 50
    :header-rows: 1   

    * - HTTP Status
      - Meaning
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

Get
***

Get Hub.

**GET** */api/v1/hubs/{hubId}*

**Headers**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Header     
     - Details
   * - Authorization
     - Bearer ``your portal access token``
   * - Content-Type
     - ``application/json``

**Response** : 200 (OK)

.. code-block:: JSON

    {
        "hubId": "3bc1e69f-c520-446f-ab2c-01751fd66a31",
        "tenantId": "00000000-0000-0000-0000-000000000001",
        "name": "Your New Cool Hub Name",
        "description": "Provide some brief description for your new Hub",        
        "closeDormantConversation": 30,
        "statusId": 2000,
        "created": "2020-10-13T02:42:26.9932101Z",
        "modified": "2020-10-13T02:42:26.9932101Z"
    }

.. list-table::
    :widths: 5 50
    :header-rows: 1   

    * - HTTP Status
      - Meaning
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


Get Collection
**************

Get Hub Collection.

**GET** */api/v1/hubs*

**Headers**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Header     
     - Details
   * - Authorization
     - Bearer ``your portal access token``
   * - Content-Type
     - ``application/json``

**Request Arguments**

.. list-table::
   :widths: 15 10 60
   :header-rows: 1

   * - Argument     
     - Mandatory
     - Details
   * - pageNumber
     - No
     - The requested page number. *Must be >= 0*
   * - pageSize
     - No
     - The requested page size. *Must be >= 1 and <= 100*

| **Response** : 200 (OK) 
| :ref:`paginated<ref_api_paginated_results>`

.. code-block:: JSON

  {
        "pageNumber": 0,
        "pageSize": 50,
        "total": 2,
        "results": [
            {
                "hubId": "00000000-0000-0000-0000-0000000000a2",
                "tenantId": "00000000-0000-0000-0000-000000000001",
                "name": "Dev Hub 1",
                "description": "Dev Hub 1 (Websocket)",
                "statusId": 2000
            },
            {
                "hubId": "00000000-0000-0000-0000-0000000000a3",
                "tenantId": "00000000-0000-0000-0000-000000000001",
                "name": "Hubster Demo (blank)",
                "description": "Hubster Demo mainly used for Videos",
                "statusId": 2000
            }
        ]
    }

.. list-table::
    :widths: 5 50
    :header-rows: 1   

    * - HTTP Status
      - Meaning
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


Integrations
^^^^^^^^^^^^

Create
******

**POST** */api/v1/integrations/hubs/{hubId}*

**Headers**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Header     
     - Details
   * - Authorization
     - Bearer ``your portal access token``
   * - Content-Type
     - ``application/json``

**Request Properties**

.. list-table::
   :widths: 15 10 60
   :header-rows: 1

   * - Property     
     - Mandatory
     - Details
   * - channelId
     - Yes
     - Has to be one of the following :ref:`Channel Types<ref_api_channel_types>`.
   * - name
     - Yes
     - Unique name for integration per Hub.
   * - statusId
     - No
     - | Integration status. Default is *Active* = 3000, if no value supplied.
       | Valid options are:        
       | -  *Active* = 3000
       | -  *Paused* = 3002
   * - configuration
     - Yes
     - See :ref:`configuration<ref_portal_integration_create_config>` properties for each individual **channelId**.

**Example Request Body** 

.. note:: The request body below is using **TwilioSMS** as an example. However, The :ref:`configuration<ref_portal_integration_create_config>` 
          properties for each channel type differs. Please use the correct JSON format specific to the **channelId** value defined. 

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
      - Meaning
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
      - Details
    * - authToken
      - Yes
      - Authorization token.
    * - accountSid
      - Yes
      - Account SID.
    * - numberSid
      - Yes
      - Phone number SID.
  
  **Example Response Body**

  .. code-block:: JSON

    {                        	
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
      - Details
    * - pageAccessToken
      - Yes
      - Facebook page access token.
  

  **Example Response Body**

  .. code-block:: JSON

    {                        	
      "channelId": "Messenger",
      "name": "My cool integration name.",
      "statusId": 3000,    
      "configuration": {        
        "appId": "35360465938...",
        "pageId": "1013889883...",
        "pageAccessToken": "EAAFBm..."
      }	
    }

  :underline:`Web Chat`

  .. code-block:: JSON

      {        
        "allowedOrigins": [
            "localhost",
            "hubster.io",
            "demo1.hubster.io"
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
      - Details
    * - allowedOrigins
      - Yes
      - One or more domains hosting the WebChat component.
    * - start
      - No
      - An array of Hubster messages types TODO:Ross.

  :underline:`Direct`

  .. code-block:: JSON

      {        
        "integrationType": "TODO: Ross",
        "echo": true,
        "webhookUrl": "http://url_end_point",
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
      - Details
    * - integrationType
      - Yes
      - Must be a supported :ref:`integration<ref_api_integration_types>` type.
    * - echo
      - No
      - TODO: Ross.
    * - webhookUrl
      - Yes (If echo = false)
      - TODO: Ross.
    * - start
      - No
      - An array of Hubster messages types TODO:Ross.

  **Example Response Body**

  .. code-block:: JSON

    {                        	
      "channelId": "Direct",
      "name": "My cool integration name.",
      "statusId": 3000,    
      "configuration": 
      {        
        "integrationType": "TODO: Ross",
        "echo": true,
        "webhookUrl": "http://url_end_point",
        "publicSigningKey": "6DF60E ...",
        "privateSigningKey": "E0A42 ...",
        "start": 
        [
          {
          "type": "text",
          "text": "Welcome to Hubster! How can we help you?"
          }
        ]
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
      - Details
    * - code
      - Yes
      - Slack oauth2 code.
    * - state
      - Yes
      - UNIX timespan plus client secret.
 
  **Example Response Body**

  .. code-block:: JSON

    {                        	
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

**POST** */api/v1/integrations/hubs/{integrationId}*

**Headers**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Header     
     - Details
   * - Authorization
     - Bearer ``your portal access token``
   * - Content-Type
     - ``application/json``

**Request Properties**

.. list-table::
   :widths: 15 10 60
   :header-rows: 1

   * - Property     
     - Mandatory
     - Details
   * - name
     - No
     - Unique name for integration per Hub.
   * - statusId
     - No
     - | Integration status. Default is *Active* = 3000, if no value supplied.
       | Valid options are:        
       | -  *Active* = 3000
       | -  *Paused* = 3002
   * - configuration
     - No
     - See :ref:`configuration<ref_portal_integration_update_config>` properties for each individual **channelId**.

.. note:: Please note, if want to you update any property from Configuration object, you need to provide **all required** properties of Configuration object. In other words
          configuration object will be replaced with new one.

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

  :underline:`Web Chat`

  .. code-block:: JSON

      {        
        "allowedOrigins": [
            "localhost",
            "hubster.io",
            "demo1.hubster.io"
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
      - Details
    * - allowedOrigins
      - Yes
      - One or more domains hosting the WebChat component.
    * - start
      - No
      - An array of Hubster messages types TODO:Ross.

  :underline:`Direct`

  .. code-block:: JSON

      {        
        "integrationType": "TODO: Ross",
        "echo": true,
        "webhookUrl": "http://url_end_point",
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
      - Details
    * - integrationType
      - Yes
      - Must be a supported :ref:`integration<ref_api_integration_types>` type.
    * - echo
      - No
      - TODO: Ross.
    * - webhookUrl
      - Yes (If echo = false)
      - TODO: Ross.
    * - start
      - No
      - An array of Hubster messages types TODO:Ross.

Get
***

**GET** */api/v1/integrations/{integrationId}*

**Headers**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Header     
     - Details
   * - Authorization
     - Bearer ``your portal access token``
   * - Content-Type
     - ``application/json``

**Example Response Body** 

.. note:: The response body below is using **TwilioSMS** as an example. However, The :ref:`configuration<ref_portal_integration_create_config>` 
          properties for each channel type differs. Below only configuration object part will be presented since, other preperties like ``name`` will be same.


.. code-block:: JSON

    {
      "integrationId": "00000000 ...",
      "hubId": "00000000 ...",
      "inboundId": "AC1fc1c1722444b0...",
      "integrationTypeId": 2,
      "channelId": 102,
      "name": "Twilio Test Number: 1647...",
      "statusId": 3000,
      "created": "2017-01-01T00:00:00",
      "modified": "2017-01-01T00:00:00",
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
      - Meaning
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

**Response Body Examples**

  :underline:`TwilioSMS`

  .. code-block:: JSON

    {      
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

  :underline:`Messenger`

  .. code-block:: JSON

    {        
      "configuration": {
        "PageAccessToken": "EAAeZ ..."
      }
    }

  :underline:`Web Chat`

  .. code-block:: JSON

    {        
      "configuration": {
        "allowedOrigins": [
          "localhost",
          "hubster.io",
          "demo1.hubster.io"
        ],
        "start":
          [
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
      "configuration": {
        "integrationType": "TODO: Ross",
        "echo": true,
        "webhookUrl": "http://url_end_point",
        "start":
          [
            {
              "type": "text",
              "text": "Welcome to Hubster! How can we help you?"
            }
          ]
        }
    }

  :underline:`Slack`

  .. code-block:: JSON

    {        
      "configuration": {
        "BotAccessToken": "xoxb...",
        "AppAccessToken": "xoxp...",
        "DefaultPublicChannel": "general",
        "TeamId": "T5P19466N"
      }
    }