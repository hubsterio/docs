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
      "authToken": "cb8c5367c3c4586ecb589e25570c019e",
      "accountSid": "AC1fc1c1722444b0c6313d3ae988bb000f",
      "numberSid": "PN667435536f4d1cefdf054abf99220d00"
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
      "authToken": "cb8c5367c3c4586ecb589e25570c019e",
      "accountSid": "AC1fc1c1722444b0c6313d3ae988bb000f",
      "numberSid": "PN667435536f4d1cefdf054abf99220d00"    
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




