Portal
======

Hubs
^^^^

Create
******

Creates new Hub.

**POST** */api/v1/hubs*

**Headers**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Header     
     - Details
   * - Authorization
     - Bearer ``{{your_portal_token}}``
   * - Content-Type
     - ``application/json``

**Request Properties**

.. list-table::
   :widths: 15 15 60
   :header-rows: 1

   * - Property     
     - Mandatory
     - Details
   * - name
     - Yes
     - Unique Hub name for tenant.
   * - description       
     - No
     - Hub description.
   * - statusId
     - Yes
     - Hub status. Valid options are:

       | 
       | -  *Active* = 2000
       | -  *Paused* = 2002

**Example Request Body**

.. code-block:: JSON

    {
        "name": "Your New Cool Hub Name",
        "description": "Provide some brief description for your new Hub",
        "statusId": 2000
    }

**Response**

.. code-block:: JSON

    {
        "hubId": "3bc1e69f-c520-446f-ab2c-01751fd66a31",
        "tenantId": "00000000-0000-0000-0000-000000000001",
        "name": "Ross Dev Hub22",
        "description": "Ross Dev Hub22",
        "statusId": 2000,
        "created": "2020-10-13T02:42:26.9932101Z",
        "modified": "2020-10-13T02:42:26.9932101Z"
    }

| :ref:`HTTP Status Codes<ref_api_status_codes>`
| :ref:`Hub Errors<ref_api_portal_error_codes>`

Integrations
^^^^^^^^^^^^