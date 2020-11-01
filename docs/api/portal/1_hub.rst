.. role:: underline
    :class: underline

Hubs
^^^^

Create
******

Creates a Hub.

**POST** */api/v1/hubs*

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

**Request Properties**

.. list-table::
   :widths: 15 10 60
   :header-rows: 1

   * - Property     
     - Mandatory
     - Description
   * - name
     - Yes
     - Unique Hub name for tenant.
   * - description       
     - Yes
     - Hub description.
   * - closeDormantConversation       
     - No
     - | The number of days to close this conversation if dormant. If no value 
         was supplied or is equal to 0 (zero), the conversation will remain open. 
       
       It should be noted that conversations can be closed by the business at any time.
   * - statusId
     - No
     - | Hub status.
       |
       | Valid options are:        
       | -- *Active* = 2000
       | -- *Paused* = 2002

       Default is *Active* = 2000, if no value supplied.

**Example Request Body**

.. code-block:: JSON

    {
        "name": "Your New Cool Hub Name",
        "description": "This hub is cool",
        "closeDormantConversation": 30,
        "statusId": 2000
    }

**Response** : 200 (OK)

.. code-block:: JSON

    {
        "hubId": "3bc1e69f-c520-446f-ab2c-01751fd66a31",
        "tenantId": "abc1e69f-c888-875f-ee2c-45789fd66a00",
        "name": "Your New Cool Hub Name",
        "description": "This hub is cool",    
        "closeDormantConversation": 30,
        "statusId": 2000
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


Update
******

Updates a Hub.

**PUT** */api/v1/hubs/{hubId}*

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
   * - name
     - No
     - Unique Hub name for tenant.
   * - description       
     - No
     - Hub description.
   * - closeDormantConversation       
     - No
     - | The number of days to close this conversation if dormant. If no value 
         was supplied or is equal to 0 (zero), the conversation will remain open.

       It should be noted that conversations can be closed by the business
       at any time.
   * - statusId
     - No
     - | Hub status.

       | Valid options are:        
       | -- *Active* = 2000
       | -- *Paused* = 2002

       Default is *Active* = 2000, if no value supplied.

**Example Request Body**

.. code-block:: JSON

     {
        "name": "Your New Cool Hub Name",
        "description": "This hub is cool",
        "closeDormantConversation": 30,
        "statusId": 2000
     }

**Response** : 200 (OK)

.. code-block:: JSON

    {
        "hubId": "3bc1e69f-c520-446f-ab2c-01751fd66a31",
        "tenantId": "abc1e69f-c888-875f-ee2c-45789fd66a00",
        "name": "Your New Cool Hub Name",
        "description": "This hub is cool",    
        "closeDormantConversation": 30,
        "statusId": 2000
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

Deletes a Hub.

.. warning:: 
    This will delete all integrations and their registrations to their service provider.


**DELETE** */api/v1/hubs/{hubId}*

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

**Response** : 200 (OK)

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

Get
***

Gets a Hub.

**GET** */api/v1/hubs/{hubId}*

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
     - The hub id to get.


**Response** : 200 (OK)

.. code-block:: JSON

    {
        "hubId": "3bc1e69f-c520-446f-ab2c-01751fd66a31",
        "tenantId": "abc1e69f-c888-875f-ee2c-45789fd66a00",
        "name": "Your New Cool Hub Name",
        "description": "This hub is cool",    
        "closeDormantConversation": 30,
        "statusId": 2000
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


Get Collection
**************

Gets a list of Hubs.

**GET** */api/v1/hubs*

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

**Request Arguments**

.. list-table::
   :widths: 15 10 60
   :header-rows: 1

   * - Argument     
     - Mandatory
     - Description
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
