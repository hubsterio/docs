.. role:: underline
    :class: underline

Authentication
^^^^^^^^^^^^^^

Client Credentials - Portal
***************************

**POST** */connect/token*

**Headers**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Header     
     - Details
   * - Content-Type
     - ``application/x-www-form-urlencoded``

.. note:: The request body has to be raw text (string).


**Request Properties**

.. list-table::
   :widths: 15 10 60
   :header-rows: 1

   * - Property     
     - Mandatory
     - Details
   * - grant_type
     - Yes
     - Has to be ``client_credentials``.
   * - client_id       
     - Yes
     - | portal client token, for example ``hubster.portal.api.00000000000000000000000000000001``.
       | Portal token consists of:        
       | **hubster.portal.api** - predefined string.
       | ...000001 - Hub Id.
   * - client_secret       
     - Yes
     - ``eyJhbGciOiJSUzI1NiIsImtpZCI...``

**Example Reponse Body** 

.. code-block:: JSON

    {
        "access_token": "eyJhbGciOiJSUzI1NiIsImtpZCI...",
        "expires_in": 2592000,
        "token_type": "Bearer",
        "scope": "hubster-portal-api"
    }

Client Credentials - Engine
***************************

**POST** */connect/token*

**Headers**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Header     
     - Details
   * - Content-Type
     - ``application/x-www-form-urlencoded``

.. note:: The request body has to be raw text (string).


**Request Properties**

.. list-table::
   :widths: 15 10 60
   :header-rows: 1

   * - Property     
     - Mandatory
     - Details
   * - grant_type
     - Yes
     - Has to be ``client_credentials``.
   * - client_id       
     - Yes
     - | engine token, for example ``hubster.engine.api.00000000000000000000000000000001``.
       | Engine tokens consists of:        
       | **portal.engine.api** - predefined string.
       | ...000001 - Hub Id.
   * - client_secret       
     - Yes
     - ``eyJhbGciOiJSUzI1NiIsImtpZCI...``

**Example Reponse Body** 

.. code-block:: JSON

    {
        "access_token": "eyJhbGciOiJSUzI1NiIsImtpZCI...",
        "expires_in": 2592000,
        "token_type": "Bearer",
        "scope": "hubster-engine-api"
    }