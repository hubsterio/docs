.. role:: underline
    :class: underline

Transfer Commands
^^^^^^^^^^^^^^^^^

Creates a Transfer Command.

**POST** */api/v1/commands/transfers/{hubId}*

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
   * - description       
     - No
     - Command description.
   * - url       
     - Yes
     - Command url.
   * - linkdescription       
     - Yes
     - Command link description description.
   * - mountdelay
     - Yes
     - | Amount of seconds before mount happens.
        
       Default is 0, if no value supplied.

**Example Request Body**

.. code-block:: JSON

    {
        "name": "new cool command",    
        "description": "your perfect description",
        "url": "https://mysite.io",
        "linkdescription": "some info regarding url",
        "mountdelay": "1"
    }

**Response** : 200 (OK)

.. code-block:: JSON

    {
        "commandId": "5a0623b0-d51a-4b3c-ace1-0175e34fae2f",
        "hubId": "00000000-0000-0000-0000-0000000000a1",
        "name": "new cool command",
        "description": "your perfect description",
        "url": "https://mysite.io",
        "linkDescription": "some info regarding url",
        "mountDelay": 1
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

Updates a Transfer Command.

**PUT** */api/v1/commands/transfers/{commandId}*

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
   * - description       
     - No
     - Command description.
   * - url       
     - No
     - Command url.
   * - linkdescription       
     - No
     - Command link description description.
   * - mountdelay
     - No
     - Amount of seconds before mount happens.       

**Example Request Body**

.. code-block:: JSON

    {
        "name": "new cool command",    
        "description": "your perfect description",
        "url": "https://mysite.io",
        "linkdescription": "some info regarding url",
        "mountdelay": "1"
    }

**Response** : 200 (OK)

.. code-block:: JSON

    {
        "commandId": "5a0623b0-d51a-4b3c-ace1-0175e34fae2f",
        "hubId": "00000000-0000-0000-0000-0000000000a1",
        "name": "new cool command",
        "description": "your perfect description",
        "url": "https://mysite.io",
        "linkDescription": "some info regarding url",
        "mountDelay": 1
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

Deletes a Transfer Command.

.. warning:: 
    This will do hard delete.


**DELETE** */api/v1/commands/transfers/{commandId}*

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
     - The transfer command id.

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

Gets a Transfer Command.

**GET** */api/v1/commands/transfers/{commandId}*

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
     - The transfer command id to get.


**Response** : 200 (OK)

.. code-block:: JSON

    {
        "commandId": "5a0623b0-d51a-4b3c-ace1-0175e34fae2f",
        "hubId": "00000000-0000-0000-0000-0000000000a1",
        "name": "new cool command",
        "description": "your perfect description",
        "url": "https://mysite.io",
        "linkDescription": "some info regarding url",
        "mountDelay": 1
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

Gets a list of Transfer Commands.

**GET** */api/v1/commands/transfers/hub/{hubId}*

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
     - The Hub id to get transfer commands for.

**Response** : 200 (OK)

.. code-block:: JSON

    
    [
        {
            "commandId": "5a0623b0-d51a-4b3c-ace1-0175e34fae2f",
            "hubId": "00000000-0000-0000-0000-0000000000a1",
            "name": "new command 2",
            "description": "Ross Dev Hub",
            "url": "https://hubster.io",
            "linkDescription": "some text",
            "mountDelay": "2"
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
