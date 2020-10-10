Error Codes
===========

Below are a list of all possible REST API errors codes for Hubster API related services. 

The following standard HTTP Status codes are used.

.. list-table::
    :widths: 5 50
    :header-rows: 1   

    * - HTTP Status
      - Meaning
    * - 200
      - OK response is correct. The body of the response will include 
        the data requested.
    * - 201
      - OK response is correct. No response content will be returned.
    * - 400
      - Bad request. The body of the response will have more info.
    * - 401
      - Unauthorized. Your token is invalid.
    * - 403
      - Forbidden. You do not have access to the requested resource.
    * - 429
      - Too many requests. You have reach your API usage limits.
    * - 500
      - Internal server error. There was an internal issue with the Hubster service.
    * - 503
      - Service unavailable. The Hubster service is unavailable.


Identity
^^^^^^^^

Below is a full list of all possible Hubster Identity REST API error codes.

.. list-table::
   :widths: 15 15 70
   :header-rows: 1

   * - Error
     - HTTP Status
     - Description
   * - IDT000100
     - 500
     - System Error
   * - IDT00010
     - 403
     - Forbidden



Portal
^^^^^^
Below is a full list of all possible Hubster Portal REST API error codes.

.. list-table::
   :widths: 15 15 70
   :header-rows: 1

   * - Error
     - HTTP Status
     - Description
   * - PRT000100
     - 500
     - System Error
   * - PRT00010
     - 403
     - Forbidden

Engine
^^^^^^

Below is a full list of all possible Hubster Engine REST API error codes.

.. list-table::
   :widths: 15 15 70
   :header-rows: 1

   * - Error
     - HTTP Status
     - Description
   * - ENG000100
     - 500
     - System Error
   * - ENG00010
     - 403
     - Forbidden
