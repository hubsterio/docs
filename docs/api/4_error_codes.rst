Error Codes
===========

Below are a list of all possible REST API error codes for Hubster API related services. 

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
      - PRTernal server error. There was an internal issue with the Hubster service.
    * - 503
      - Service unavailable. The Hubster service is unavailable.


Identity
^^^^^^^^

Below is a full list of all possible Hubster Identity REST API error codes.

.. list-table::
   :widths: 15 5 70
   :header-rows: 1

   * - Error
     - HTTP Status
     - Description
   * - IDT000100
     - 500
     - System Error.
   * - IDT000101
     - 403
     - Forbidden.
   * - IDT000102
     - 400 
     - Unauthorized access.
   * - IDT000103 
     - 400 
     - Requested operation is not implemented.
   * - IDT000104 
     - 400 
     - Requested resource or operation is not available.
   * - IDT000105 
     - 400 
     - Requested resource was not found.
   * - IDT000106 
     - 400
     - Resource you are trying to create already exists.
   * - IDT000107 
     - 400
     - Current request or operation is not valid.
   * - IDT000108 
     - 400 
     - Request took too long to execute and timed out.
   * - IDT000109 
     - 400 
     - Requested action was aborted.
   * - IDT000110 
     - 400 
     - Requested action is not allowed.


Portal
^^^^^^
Below is a full list of all possible Hubster Portal REST API error codes.

.. list-table::
   :widths: 15 5 70
   :header-rows: 1

   * - Error
     - HTTP Status
     - Description
   * - PRT000100
     - 500
     - System Error.
   * - PRT000101
     - 403
     - Forbidden.
   * - PRT000102
     - 400 
     - Unauthorized access.
   * - PRT000103 
     - 400 
     - Requested operation is not implemented.
   * - PRT000104 
     - 400 
     - Requested resource or operation is not available.
   * - PRT000105 
     - 400 
     - Requested resource was not found.
   * - PRT000106 
     - 400
     - Resource you are trying to create already exists.
   * - PRT000107 
     - 400
     - Current request or operation is not valid.
   * - PRT000108 
     - 400 
     - Request took too long to execute and timed out.
   * - PRT000109 
     - 400 
     - Requested action was aborted.
   * - PRT000110 
     - 400 
     - Requested action is not allowed.

Engine
^^^^^^

Below is a full list of all possible Hubster Engine REST API error codes.

.. list-table::
   :widths: 15 5 70
   :header-rows: 1

   * - Error
     - HTTP Status
     - Description  
   * - ENG000100
     - 500
     - System Error.
   * - ENG000101
     - 403
     - Forbidden.
   * - ENG000102
     - 400 
     - Unauthorized access.
   * - ENG000103 
     - 400 
     - Requested operation is not implemented.
   * - ENG000104 
     - 400 
     - Requested resource or operation is not available.
   * - ENG000105 
     - 400 
     - Requested resource was not found.
   * - ENG000106 
     - 400
     - Resource you are trying to create already exists.
   * - ENG000107 
     - 400
     - Current request or operation is not valid.
   * - ENG000108 
     - 400 
     - Request took too long to execute and timed out.
   * - ENG000109 
     - 400 
     - Requested action was aborted.
   * - ENG000110 
     - 400 
     - Requested action is not allowed.


