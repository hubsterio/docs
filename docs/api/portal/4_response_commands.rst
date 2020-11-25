.. role:: underline
    :class: underline

Response Commands
^^^^^^^^^^^^^^^^^

Creates a Response Command.

**POST** */api/v1/commands/responses/{hubId}*

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
     - The Hub id to create commands for.

**Request Properties**

.. list-table::
   :widths: 15 10 60
   :header-rows: 1

   * - Property     
     - Mandatory
     - Description
   * - name
     - Yes
     - Unique command name per Hub.
   * - category       
     - No
     - Command category.
   * - description       
     - No
     - Command description.
   * - integrationTypeId       
     - Yes
     - | Type of intergration command is used for.
       | Valid options are:
       | -- *Agent* = 3 
       | -- *Customer* = 2
   * - type
     - No
     - | Response command type.
       | Valid options are:
       | -- *message* 
       | -- *event*
   * - response
     - Yes
     - TODO!!
       

**Example Request Body**

.. code-block:: JSON

    {
        "name": "Command-2",    
        "description": "Command-1",
        "category": "Command-1",
        "integrationTypeId": "Agent",
        "type": "event",    
        "responses": [
            {	
                "type": "payload",            
                "payloadType": "type1",
                "payload": {
                    "payload": "Hello"
                }
            }		
        ]
    }

**Response** : 200 (OK)

.. code-block:: JSON

    {
        "commandId": "297c91f3-4347-4834-b008-0175fd2f4c48",
        "hubId": "00000000-0000-0000-0000-0000000000a1",
        "name": "Command-2",
        "category": "Command-1",
        "description": "Command-1",
        "integrationTypeId": "Agent",
        "type": "event",
        "responses": [
            {
                "type": "payload",
                "payloadType": "type1",
                "payload": {
                    "payload": "Hello"
                }
            }
        ]
    }

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


Update
******

Updates a Response Command.

**PUT** */api/v1/commands/responses/{commandId}*

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
   * - commandId
     - The command id affected.

**Request Properties**

.. list-table::
   :widths: 15 10 60
   :header-rows: 1

   * - Property     
     - Mandatory
     - Description
   * - name
     - No
     - Unique command name per Hub.
   * - category       
     - No
     - Command category.
   * - description       
     - No
     - Command description.
   * - integrationTypeId       
     - No
     - | Type of intergration command is used for.
       | Valid options are:
       | -- *Agent* = 3 
       | -- *Customer* = 2
   * - type
     - No
     - | Response command type.
       | Valid options are:
       | -- *message* 
       | -- *event*
   * - response
     - No
     - TODO!!
       

**Example Request Body**

.. code-block:: JSON

    {
        "name": "Command-5",    
        "description": "Command-5",
        "category": "Command-5"        
    }

**Response** : 200 (OK)

.. code-block:: JSON

    {
        "commandId": "297c91f3-4347-4834-b008-0175fd2f4c48",
        "hubId": "00000000-0000-0000-0000-0000000000a1",
        "name": "Command-5",
        "category": "Command-5",
        "description": "Command-5",
        "integrationTypeId": "Agent",
        "type": "event",
        "responses": [
            {
                "type": "payload",
                "payloadType": "type1",
                "payload": {
                    "payload": "Hello"
                }
            }
        ]
    }


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

Deletes a Response Command.

.. warning:: 
    This will do hard delete.


**DELETE** */api/v1/commands/responses/{commandId}*

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
   * - commandId
     - The response command id.

**Response** : 200 (OK)

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

Get
***

Gets a Response Command.

**GET** */api/v1/commands/responses/{commandId}*

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
   * - commandId
     - The response command id to get.


**Response** : 200 (OK)

.. code-block:: JSON

    {
        "commandId": "297c91f3-4347-4834-b008-0175fd2f4c48",
        "hubId": "00000000-0000-0000-0000-0000000000a1",
        "name": "Command-5",
        "category": "Command-5",
        "description": "Command-5",
        "integrationTypeId": "Agent",
        "type": "event",
        "responses": [
            {
                "type": "payload",
                "payloadType": "type1",
                "payload": {
                "payload": "Hello"
                }
            }
        ]
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


Get Collection
**************

Gets a list of Response Commands.

**GET** */api/v1/commands/responses/hub/{hubId}*

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
     - The Hub id to get response commands for.

**Response** : 200 (OK)

.. code-block:: JSON

    
    [
        {
            "commandId": "297c91f3-4347-4834-b008-0175fd2f4c48",
            "hubId": "00000000-0000-0000-0000-0000000000a1",
            "name": "Command-5",
            "category": "Command-5",
            "description": "Command-5",
            "integrationTypeId": "Agent",
            "type": "event",
            "responses": [
                {
                    "type": "payload",
                    "payloadType": "type1",
                    "payload": {
                    "payload": "Hello"
                    }
                }
            ]
        }
    ]
    

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

