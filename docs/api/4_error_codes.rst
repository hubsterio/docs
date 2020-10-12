.. _ref_api_error_codes:

Error Codes
===========

Below are a list of all possible REST API error codes for all Hubster API related services. 

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
