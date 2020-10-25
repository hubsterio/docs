.. role:: underline
    :class: underline

.. _ref_auth:

Authentication
**************

**POST** */connect/token*

**Headers**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Header     
     - Description
   * - Content-Type
     - ``application/x-www-form-urlencoded``


**Request Properties**

.. list-table::
   :widths: 15 10 60
   :header-rows: 1

   * - Property     
     - Mandatory
     - Description
   * - grant_type
     - Yes
     - Has to be ``client_credentials``.
   * - client_id       
     - Yes
     - | The client id of the Hubster service you plan to authenticate against.
       
       | Typical, it will be one of following:       
       |  - **hubster.portal.api.000000000....**
       |  - **hubster.engine.api.000000000....**

       | Please refer to :ref:`Identity to API Resource Interaction<ref_api_identity_interaction>` for the resources accessible
       | on a per **client_id** basis.
   * - client_secret       
     - Yes
     - The client secret for the **client_id** used.

.. note:: 
    | The request body is of **grant_type** see the following example format below:

    | *grant_type=client_credentials&client_id=hubster.portal.api.0000000...&client_secret=SMWvD7W...*

**Response** : 200 (OK)

.. code-block:: JSON

    {
        "access_token": "eyJhbGciOiJSUzI1NiIsImtpZCI...",
        "expires_in": 2592000,
        "token_type": "Bearer",
        "scope": "hubster-portal-api"
    }

