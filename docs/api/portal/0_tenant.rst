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
      "tenantId": "00000000...",
      "clientId": "hubster.portal.api.00000000000000000000000000000001",
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
          "value": "00000000..."
        }
      ],
      "secrets": [
        {
          "id": 9,
          "name": "my_secret_1",
          "token": "my secret 1 token here"
        },
        {
          "id": 15,
          "name": "my_secret_3",
          "token": "my secret 3 token here"
        },
        {
          "id": 16,
          "name": "my_secret_4",
          "token": "my secret 4 token here",
          "expiration": "2018-08-30T00:00:00"
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
     - Expiration time for issued token (you can set your own expiration time if needed).

**Example Request Body**

.. code-block:: JSON

    {  
      "name": "my_secret_4",
      "expiration": "2018-08-30"
    }


**Response** : 200 (OK)

.. code-block:: JSON

    {
      "id": 16,
      "name": "my_secret_4",
      "token": "/l8Ls1J1/fEzy7AQNCUKAXdCg1M=",
      "expiration": "2018-08-30T00:00:00"
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
