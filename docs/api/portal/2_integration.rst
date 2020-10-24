.. role:: underline
    :class: underline

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
     - | Integration status. 

       | Valid options are:        
       |  - *Active* = 3000
       |  - *Paused* = 3002
       
       | Default is *Active* = 3000, if no value supplied.
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
    - Twilio authorization token.
  * - accountSid
    - Yes
    - Twilio account SID.
  * - numberSid
    - Yes
    - Twilio phone number SID.

**Example Response Body**

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
    - Details
  * - pageAccessToken
    - Yes
    - Facebook page access token.


**Example Response Body**

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
    - Details
  * - allowedOrigins
    - Yes
    - One or more domains hosting the WebChat component.
  * - start
    - No
    - An array of Hubster :ref:`messages types<ref_activities_message_types>`.

**Example Response Body**

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
    - Details
  * - integrationType
    - Yes
    - Must be a supported :ref:`integration<ref_api_integration_types>` type.
  * - echo
    - No
    - If yes, when an activity is received from this integration, it will echo it back.
  * - webhookUrl
    - No
    - | The endpoint to receive Hubster :ref:`Activities<ref_activities>`.
      | If not supplied, activities will be delivered via websockets.        
  * - start
    - No
    - An array of Hubster :ref:`messages types<ref_activities_message_types>`.

**Example Response Body**

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
    - Details
  * - webhookUrl
    - Yes
    - The endpoint to receive Hubster :ref:`Activities<ref_activities>`
  * - events
    - Yes
    - The :ref:`activity event filter(s)<ref_webhooks_events>` to be event on.

**Example Response Body**

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
          "publicSigningKey": "3EF951F619CD4F5E820C73622C0F1A3C",
          "privateSigningKey": "FA96D15568654A4482772E00BA941BCB"
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
     - | Integration status. 

       | Valid options are:        
       |  - *Active* = 3000
       |  - *Paused* = 3002

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
    - Details
  * - allowedOrigins
    - Yes
    - One or more domains hosting the WebChat component.
  * - start
    - No
    - An array of Hubster :ref:`messages types<ref_activities_message_types>`.

**Example Response Body**

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
    - Details
  * - integrationType
    - Yes
    - Must be a supported :ref:`integration<ref_api_integration_types>` type.
  * - echo
    - No
    - If yes, when an activity is received from this integration, it will echo it back.
  * - webhookUrl
    - No
    - | The endpoint to receive Hubster :ref:`Activities<ref_activities>`.
      | If not supplied, activities will be delivered via websockets.        
  * - regenerateKeys
    - No
    - This forces a new set of public/private keys to be generated.
  * - start
    - No
    - An array of Hubster :ref:`messages types<ref_activities_message_types>`.

**Example Response Body**

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
    - Details
  * - webhookUrl
    - Yes
    - The endpoint to receive Hubster :ref:`Activities<ref_activities>`
  * - regenerateKeys
    - No
    - This forces a new set of public/private keys to be generated.
  * - events
    - Yes
    - The :ref:`activity event filter(s)<ref_webhooks_events>` to be event on.

**Example Response Body**

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
          "publicSigningKey": "3EF951F619CD4F5E820C73622C0F1A3C",
          "privateSigningKey": "FA96D15568654A4482772E00BA941BCB"
      }
  }


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
          properties for each channel type differs. Below only configuration object part will be presented since, other properties like ``name`` will be same.


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
        "webhookUrl": "https://url_end_point.com",
        "start":[
            {
              "type": "text",
              "text": "Welcome to Hubster! How can we help you?"
            }
          ]
        }
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
      - Details
    * - webhookUrl
      - Yes
      - The endpoint to receive Hubster :ref:`Activities<ref_activities>`
    * - events
      - Yes
      - The :ref:`activity event filter(s)<ref_webhooks_events>` to be event on.

  **Example Response Body**

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
            "publicSigningKey": "3EF951F619CD4F5E820C73622C0F1A3C",
            "privateSigningKey": "FA96D15568654A4482772E00BA941BCB"
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

