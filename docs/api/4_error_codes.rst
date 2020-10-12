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
    * - 408
      - Timed out. Your request was timed out.
    * - 409
      - Conflict. You request has caused a conflict.
    * - 410
      - Not available. The request you are trying to invoke is no longer available.
    * - 417
      - Expectation Failed. The operation was aborted.
    * - 429
      - Too many requests. You have reach your API usage limits.
    * - 500
      - Internal server error. There was an internal issue with the Hubster service.
    * - 501
      - Not implemented. The service you requested is not implemented.
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
     - 401
     - Unauthorized access.
   * - IDT000103 
     - 501 
     - Requested operation is not implemented.
   * - IDT000104 
     - 410
     - Requested resource or operation is not available.
   * - IDT000105 
     - 404
     - Requested resource was not found.
   * - IDT000106 
     - 409
     - Resource you are trying to create already exists.
   * - IDT000107 
     - 417
     - Current request or operation is not valid.
   * - IDT000108 
     - 408 
     - Request took too long to execute and timed out.
   * - IDT000109 
     - 417 
     - Requested action was aborted.
   * - IDT000110 
     - 403 
     - Requested action is not allowed.
   * - IDT000200 
     - 400 
     - Required query parameter was not supplied.
   * - IDT000201 
     - 400
     - One or more parameters have invalid format.
   * - IDT000202 
     - 400
     - Please correct supplied format for used parameter(s).
   * - IDT000203 
     - 400
     - Provided ``GUID`` has bad format.
   * - IDT000204 
     - 400
     - Provided date has bad format.
   * - IDT000205 
     - 400
     - One or more parameters have invalid date format.
   * - IDT000206 
     - 400
     - Provided parameter value is not supported (out of range).
   * - IDT000207 
     - 400
     - Provided parameter is out of predefined range.
   * - IDT000208 
     - 400
     - Provided parameter has to be greater than zero.
   * - IDT000209 
     - 400
     - Parameter must be greater than or equal to zero.
   * - IDT000210 
     - 400
     - Invalid Number format provided.
   * - IDT000211 
     - 400
     - Invalid email format provided.
   * - IDT000212 
     - 400
     - Criteria parameter is required when supplying a ``searchBy`` parameter.
   * - IDT000300 
     - 400
     - Token request root body was empty.
   * - IDT000301 
     - 400
     - Token request is missing required property.
   * - IDT000302
     - 400
     - Token request operaion has failed while authenticating user.
   * - IDT000303
     - 400
     - Token request has invalid client scopes.
   * - IDT000397
     - 400
     - Token request could not find ``Client``.
   * - IDT005000
     - 400
     - User request root body was empty.
   * - IDT005001
     - 400
     - User request required property is missing.
   * - IDT005002
     - 400
     - User email is not in proper format.
   * - IDT005003
     - 400
     - User request can have only one claim of type ``name``.
   * - IDT005004
     - 400
     - User provider type is not supported.
   * - IDT005005
     - 400
     - User is not allowed to manage password through Hubster's Identity Server.
   * - IDT005096
     - 400
     - User ``name`` is already taken.
   * - IDT005097
     - 400
     - User not found.
   * - IDT005100
     - 400
     - Claim type is missing .
   * - IDT005101
     - 400
     - Claim type is not allowed.
   * - IDT005102
     - 400
     - Claim/value has been defined more than once and is not permissible.
   * - IDT005200
     - 400
     - Client request root body was empty.
   * - IDT005201
     - 400
     - Client request required property is missing.
   * - IDT005202
     - 400
     - Client must contain at least one ``Scope``.
   * - IDT005203
     - 400
     - Client duplicate scopes detected.
   * - IDT005204
     - 400
     - Client scopes cannot contain any empty strings.
   * - IDT005205
     - 400
     - Specified client scope does not exist.
   * - IDT005206
     - 400
     - Client ``Id`` already exists.
   * - IDT005207
     - 400
     - Client ``tenant Id`` does not exists.
   * - IDT005208
     - 400
     - Client token name already exists.
   * - IDT005297
     - 400
     - Client not found.
   * - IDT005300
     - 400
     - Client secret empty root body was supplied.
   * - IDT005301
     - 400
     - Client secret required property is missing.
   * - IDT005397
     - 400
     - Client secret not found.
   * - IDT005400
     - 400
     - Tenant empty root body was supplied.
   * - IDT005401
     - 400
     - Tenant required property is missing.
   * - IDT005402
     - 400
     - Tenant already exists.
   * - IDT005497
     - 400
     - Tenant not found.
   * - IDT005500
     - 400
     - External login request root body was empty.
   * - IDT005501
     - 400
     - External login required property is missing.
   * - IDT005502
     - 400
     - External login does not support specidied authentication provider.


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
     - 401
     - Unauthorized access.
   * - PRT000103 
     - 501 
     - Requested operation is not implemented.
   * - PRT000104 
     - 410
     - Requested resource or operation is not available.
   * - PRT000105 
     - 404
     - Requested resource was not found.
   * - PRT000106 
     - 409
     - Resource you are trying to create already exists.
   * - PRT000107 
     - 417
     - Current request or operation is not valid.
   * - PRT000108 
     - 408 
     - Request took too long to execute and timed out.
   * - PRT000109 
     - 417 
     - Requested action was aborted.
   * - PRT000110 
     - 403 
     - Requested action is not allowed.
   * - PRT000200 
     - 400 
     - Required query parameter was not supplied.
   * - PRT000201 
     - 400
     - One or more parameters have invalid format.
   * - PRT000202 
     - 400
     - Please correct supplied format for used parameter(s).
   * - PRT000203 
     - 400
     - Provided ``GUID`` has bad format.
   * - PRT000204 
     - 400
     - Provided date has bad format.
   * - PRT000205 
     - 400
     - One or more parameters have invalid date format.
   * - PRT000206 
     - 400
     - Provided parameter value is not supported (out of range).
   * - PRT000207 
     - 400
     - Provided parameter is out of predefined range.
   * - PRT000208 
     - 400
     - Provided parameter has to be greater than zero.
   * - PRT000209 
     - 400
     - Parameter must be greater than or equal to zero.
   * - PRT000210 
     - 400
     - Invalid Number format provided.
   * - PRT000211 
     - 400
     - Invalid email format provided.
   * - PRT000212 
     - 400
     - Criteria parameter is required when supplying a ``searchBy`` parameter.
   * - PRT000300
     - 400
     - Root body section is missing.
   * - PRT000301
     - 400
     - Reuqired property is missing.
   * - PRT000302
     - 400
     - Property has is invalid type.
   * - PRT000303
     - 400
     - Validation failed. Property not supported.
   * - PRT000304
     - 400
     - Request parameter has bad format. Expected to be a valid ``decimal`` value.
   * - PRT000305
     - 400
     - Request parameter has bad format. Expected to be a valid ``GUID`` value.
   * - PRT000306
     - 400
     - Request collection must contain one or more elements.
   * - PRT000307
     - 400
     - Messaged was empty.
   * - PRT000308
     - 400
     - Request body must contain Location, either an address and/or latitude/longitude coordinates.
   * - PRT000400
     - 400
     - Tenant already exists.
   * - PRT000401
     - 400
     - User already exists.
   * - PRT000599
     - 400
     - User not found.
   * - PRT000600
     - 400
     - Name already exists.
   * - PRT000699
     - 400
     - Hub not found.
   * - PRT000700
     - 400
     - An integration with name already exists.
   * - PRT000701
     - 400
     - An integration with same name has already been assign to a hub. You can only add this channel once across all hubs.
   * - PRT000799
     - 400
     - Integration not found.

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
     - 401
     - Unauthorized access.
   * - ENG000103 
     - 501 
     - Requested operation is not implemented.
   * - ENG000104 
     - 410
     - Requested resource or operation is not available.
   * - ENG000105 
     - 404
     - Requested resource was not found.
   * - ENG000106 
     - 409
     - Resource you are trying to create already exists.
   * - ENG000107 
     - 417
     - Current request or operation is not valid.
   * - ENG000108 
     - 408 
     - Request took too long to execute and timed out.
   * - ENG000109 
     - 417 
     - Requested action was aborted.
   * - ENG000110 
     - 403 
     - Requested action is not allowed.
   * - ENG000200 
     - 400 
     - Required query parameter was not supplied.
   * - ENG000201 
     - 400
     - One or more parameters have invalid format.
   * - ENG000202 
     - 400
     - Please correct supplied format for used parameter(s).
   * - ENG000203 
     - 400
     - Provided ``GUID`` has bad format.
   * - ENG000204 
     - 400
     - Provided date has bad format.
   * - ENG000205 
     - 400
     - One or more parameters have invalid date format.
   * - ENG000206 
     - 400
     - Provided parameter value is not supported (out of range).
   * - ENG000207 
     - 400
     - Provided parameter is out of predefined range.
   * - ENG000208 
     - 400
     - Provided parameter has to be greater than zero.
   * - ENG000209 
     - 400
     - Parameter must be greater than or equal to zero.
   * - ENG000210 
     - 400
     - Invalid Number format provided.
   * - ENG000211 
     - 400
     - Invalid email format provided.
   * - ENG000212 
     - 400
     - Criteria parameter is required when supplying a ``searchBy`` parameter.
   * - ENG002000
     - 400
     - Provided tenant is invalid.
   * - ENG002001
     - 400
     - Your account is disabled.
   * - ENG002002
     - 400
     - Account evaluation period has expired.
   * - ENG003000
     - 400
     - Conversation request requires ``body`` to be present.
   * - ENG003001
     - 400
     - Conversation request is missing required property.
   * - ENG003002
     - 400
     - Conversation request parameter has bad format. Expected to be a valid ``GUID`` value.
   * - ENG005000
     - 400
     - Direct Inbound request requires ``body`` to be present.
   * - ENG005001
     - 400
     - Direct Inbound request is missing required property.
   * - ENG005002
     - 400
     - Direct Inbound request does not support provided property.
   * - ENG005003
     - 400
     - Direct Inbound request must contain one of the following sections: ``root.message`` or ``root.action``.
   * - ENG005004
     - 400
     - Direct Inbound request can only contain one root with the following sections: ``root.message`` or ``root.action``.
   * - ENG005015
     - 400
     - Direct Inbound request collection must contain one or more elements.
   * - ENG005020
     - 400
     - Direct Inbound request parameter has bad format. Expected to be a valid ``GUID`` value.
   * - ENG005021
     - 400
     - Direct Inbound request parameter has bad format. Expected to be a valid ``decimal`` value.
   * - ENG005023
     - 400
     - Direct Inbound request body was empty.
   * - ENG005024
     - 400
     - Direct Inbound request body must contain ``Location``, either an ``address`` and/or ``latitude/longitude`` coordinates.
   * - ENG005500
     - 400
     - Hub does not exist.
   * - ENG005501
     - 400
     - Provided Hub does not have any Agent or Bot integration configured to receive or interact with customer messages.
   * - ENG006000
     - 400
     - Provided integration does not exist.
   * - ENG006500
     - 400
     - Provided conversation does not exist.
   * - ENG006501
     - 400
     - Customer is no longer responding to messages.
   * - ENG006502
     - 400
     - Your Hubster integration has been terminated and is no longer active. Please contact your Administrator.
   * - ENG006503
     - 400
     - Conversation was paused.
   * - ENG007500
     - 400
     - Conversation encountered a web related issue.
   * - ENG007501
     - 400
     - Conversation encountered a web security related issue.
   * - ENG007502
     - 400
     - Conversation encountered a runtime related issue.
   * - ENG007510
     - 400
     - Customer failed to receive your message. This was due to an unauthorized issue on their end. Please check with your Administrator.
   * - ENG007511
     - 400
     - A web related issue was detected on Hub.
   * - ENG007512
     - 400
     - An unreachable web-endpoint was detected on Hub.
   * - ENG008000
     - 400
     - Message Spark encountered a web related issue.
   * - ENG008001
     - 400
     - Message Spark encountered a web security related issue.
   * - ENG008002
     - 400
     - Message Spark encountered a runtime related issue.
   * - ENG008500
     - 400
     - No upload files were provided.
   * - ENG008501
     - 400
     - Invalid ``URL`` was provided.
   * - ENG008502
     - 400
     - File you submitted was not received by the other party.
   * - ENG008503
     - 400
     - The other party tried to send you a file but failed.
   * - ENG009000
     - 400
     - Invalid command. You must have an actually command in front of the double colon e.g. ``::mycommand [args]...``
   * - ENG009001
     - 400
     - Unknown command.
   * - ENG009200
     - 400
     - Command was not found. Please type ``::{1} --list`` to see the full list of available commands.
   * - ENG009201
     - 400
     - No commands have been configured for this hub.
   * - ENG009202
     - 400
     - No commands were found for the category.
   * - ENG009299
     - 400
     - There was an error while executing command. Please contact technical support.

Events
^^^^^^^^

Below is a full list of all possible Hubster Events REST API error codes.

.. list-table::
   :widths: 15 5 70
   :header-rows: 1

   * - Error
     - HTTP Status
     - Description
   * - EVT000100
     - 500
     - System Error.
   * - EVT000101
     - 403
     - Forbidden.
   * - EVT000102
     - 401
     - Unauthorized access.
   * - EVT000103 
     - 501 
     - Requested operation is not implemented.
   * - EVT000104 
     - 410
     - Requested resource or operation is not available.
   * - EVT000105 
     - 404
     - Requested resource was not found.
   * - EVT000106 
     - 409
     - Resource you are trying to create already exists.
   * - EVT000107 
     - 417
     - Current request or operation is not valid.
   * - EVT000108 
     - 408 
     - Request took too long to execute and timed out.
   * - EVT000109 
     - 417 
     - Requested action was aborted.
   * - EVT000110 
     - 403 
     - Requested action is not allowed.
   * - EVT000200 
     - 400 
     - Required query parameter was not supplied.
   * - EVT000201 
     - 400
     - One or more parameters have invalid format.
   * - EVT000202 
     - 400
     - Please correct supplied format for used parameter(s).
   * - EVT000203 
     - 400
     - Provided ``GUID`` has bad format.
   * - EVT000204 
     - 400
     - Provided date has bad format.
   * - EVT000205 
     - 400
     - One or more parameters have invalid date format.
   * - EVT000206 
     - 400
     - Provided parameter value is not supported (out of range).
   * - EVT000207 
     - 400
     - Provided parameter is out of predefined range.
   * - EVT000208 
     - 400
     - Provided parameter has to be greater than zero.
   * - EVT000209 
     - 400
     - Parameter must be greater than or equal to zero.
   * - EVT000210 
     - 400
     - Invalid Number format provided.
   * - EVT000211 
     - 400
     - Invalid email format provided.
   * - EVT000212 
     - 400
     - Criteria parameter is required when supplying a ``searchBy`` parameter.
   * - EVT001000
     - 400
     - Missing conversation id (cid).
   * - EVT001001
     - 400
     - Missing integration Id (iId).
   * - EVT001002
     - 400
     - Access forbidden to this conversation.