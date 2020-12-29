.. role:: underline
    :class: underline

Interactions
^^^^^^^^^^^^

Get Activities
**************

Get :ref:`Activities <ref_activities>` for a given conversation.

**GET** */api/v1/interactions/activities/{conversationId}*

**Headers**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Header     
     - Description
   * - Authorization
     - Bearer ``your engine access token``
   * - Content-Type
     - ``application/json``

**Url Segments**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Segment     
     - Description
   * - conversationId
     - The **conversationId id** to retrieve :ref:`activities <ref_activities>`.

**Request Properties**

.. list-table::
   :widths: 15 10 60
   :header-rows: 1

   * - Property     
     - Mandatory
     - Description
   * - type
     - Yes
     - | The **sender** or **recipient** integration type that you want to retrieve activities for. 
         For example, if **type** = 'agent', than all activities whereby, 
         the sender or recipient type = 'agent', will be retrieved. 

       | Only the following :ref:`integration types <ref_api_integration_types>` are valid:       
       
       * Customer
       * Agent          
       * Bot

   * - leid
     - No
     - | The last starting point event timestamp that you want to retrieve activities from for the given conversation. 
        The value must be in UNIX epoch time in milliseconds (UTC)

       | Default is 0, if no value supplied.


**Response** : 200 (OK)

.. code-block:: JSON

    [
        {
            "type": "message",
            "eventTrigger": "message:customer",
            "eventId": 1604758399703,
            "externalId": "some_external_id_0001",
            "isEcho": false,
            "interactionId": "1368fd94-bd85-4dcf-84c7-0175a30dead7",
            "flowProcess": "Default",
            "sender": {
                "integrationId": "00000000-0000-0000-0000-000000000020",
                "integrationType": "Customer",
                "channelType": "WebChat",
                "tokenId": "LDDKEgUsKUmjQzwjNAhL1w=="
            },
            "recipient": {
                "integrationId": "00000000-0000-0000-0000-000000000024",
                "integrationType": "Agent",
                "channelType": "Slack",
                "tokenId": "f7cbbd3d-3071-45d7-abed-01744cad6a7e.00000000-0000-0000-0000-000000000024"
            },
            "message": {
                "text": "Hi there!",
                "type": "text"
            }
        },
        {
            "type": "message",
            "eventTrigger": "message:agent",
            "eventId": 1604783877593,
            "externalId": "some_external_id_0002",
            "isEcho": false,
            "interactionId": "13da6b0b-0d66-4277-9e9d-0175a492adda",
            "flowProcess": "Default",
            "sender": {
                "integrationId": "00000000-0000-0000-0000-000000000024",
                "integrationType": "Agent",
                "channelType": "Slack",
                "tokenId": "f7cbbd3d-3071-45d7-abed-01744cad6a7e.00000000-0000-0000-0000-000000000024"
            },
            "recipient": {
                "integrationId": "00000000-0000-0000-0000-000000000020",
                "integrationType": "Customer",
                "channelType": "WebChat",
                "tokenId": "LDDKEgUsKUmjQzwjNAhL1w=="
            },
            "message": {
                "text": "Hello! How can I help you today?",
                "type": "text"
            }
        }
    ]

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
