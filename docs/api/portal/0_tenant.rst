.. role:: underline
    :class: underline

Tenants
^^^^^^^

Get Client
**********

**GET** */api/v1/tenants/clients/{clientId}*

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
      "tenantId": "B205B3EC-A9D7-4243-B88C-017533957DEB",
      "clientId": "hubster.portal.api.B205B3ECA9D74243B88C017533957DEB",
      "name": "Hubster Portal API Client (Public)",
      "enabled": true,
      "allowedScopes": [
        "hubster-portal-api"
      ],
      "claims": [
        {
          "type": "role",
          "value": "admin"
        },
        {
          "type": "tenant",
          "value": "B205B3EC-A9D7-4243-B88C-017533957DEB"
        }
      ],
      "secrets": [
        {
          "id": 9,
          "name": "my secret 1",
          "token": "SMWvD7WUAn8bkdl..."
        },
        {
          "id": 15,
          "name": "my secret 2",
          "token": "SMWvD7WUAn8bkdl..."
        },
        {
          "id": 16,
          "name": "my secret 3",
          "token": "SMWvD7WUAn8bkdl...",
          "expiration": "2030-01-31T00:00:00"
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


Add Client Token
****************

**POST** */api/v1/tenants/clients/{clientId}/tokens*

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
     - Unique tenant name for Hub.
   * - expiration       
     - No
     - | Expiration date when this token will no longer be valid. If no expiration date 
       | was provide, then this token lives forever.     

**Example Request Body**

.. code-block:: JSON

    {  
      "name": "my secret 3",          
      "expiration": "2030-01-31T00:00:00"
    }


**Response** : 200 (OK)

.. code-block:: JSON

    {
      "id": 16,
      "name": "my secret 3",
      "token": "7AQNCUKAXdCg1M...",
      "expiration": "2030-01-31T00:00:00"
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

Delete Client Token
*******************

**DELETE** */api/v1/tenants/clients/{clientId}/tokens/{tokenId}*

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
    * - 408
      - Timed out. The request timed out.
    * - 429
      - Too many requests. API usage limit has been reached.
    * - 500
      - Internal server error. There was an internal issue with the service.
    * - 503
      - Service unavailable. The service is unavailable.
