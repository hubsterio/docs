.. role:: underline
    :class: underline

Response Commands
^^^^^^^^^^^^^^^^^

Create
******

Creates a Response Command.

**POST** */api/v1/commands/responses/{hubId}*

**Headers**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Header     
     - Description
   * - Authorization
     - Bearer ``your portal access token``
   * - Content-Type
     - ``application/json``

**Url Segments**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Segment     
     - Description
   * - hubId
     - The Hub id to create commands for.

**Request Properties**

.. list-table::
   :widths: 15 10 60
   :header-rows: 1

   * - Property     
     - Mandatory
     - Description
   * - name
     - Yes
     - Unique command name per Hub.
   * - category       
     - No
     - Command category.
   * - description       
     - No
     - Command description.
   * - integrationTypeId       
     - Yes
     - | Type of integration command is used for.
       | Valid options are:
       | -- *agent*
       | -- *customer*
   * - type
     - Yes
     - | Response command type.
       | Valid options are:
       | -- *message* 
       | -- *event*
   * - responses
     - Yes
     - A list of :ref:`Message <ref_activities_message_types>` or :ref:`Event <ref_activities_event_types>` types.
       

**Example Request Body**

.. code-block:: JSON

    {          
      "name": "contact-eva.green",
      "category": "contacts",
      "description": "Eva's Contact",
      "integrationTypeId": "customer",
      "type": "message",
      "responses": [
          {
              "type": "text",
              "text": "Below is my contact info"
          },
          {
              "type": "contact",
              "imageUrl": "https://image.png",
              "title": "Eva Green",
              "properties": [
                  {
                      "key": "Title",
                      "value": "Mighty Health"
                  },
                  {
                      "key": "Address",
                      "value": "108 Kirkbride Crescent, Maple, ON",
                      "type": "address;work"
                  },
                  {
                      "key": "Cell",
                      "value": "+1 (714) 873-6202",
                      "type": "phone;cell"
                  },
                  {
                      "key": "Email",
                      "value": "eva@mightyhealth.com",
                      "type": "email"
                  }
              ],
              "channels": [
                  {
                      "type": "Webchat",
                      "metadata": [
                          {
                              "key": "caption-show",
                              "value": "true"
                          },
                          {
                              "key": "caption-color",
                              "value": "white"
                          }
                      ]
                  }
              ]
          }
      ]
    }

**Response** : 200 (OK)

.. code-block:: JSON

    {
      "commandId": "00000000-0000-0000-0000-000000000005",
      "hubId": "00000000-0000-0000-0000-0000000000a1",
      "name": "contact-eva.green",
      "category": "contacts",
      "description": "Eva's Contact",
      "integrationTypeId": "customer",
      "type": "message",
      "responses": [
          {
              "type": "text",
              "text": "Below is my contact info"
          },
          {
              "type": "contact",
              "imageUrl": "https://image.png",
              "title": "Eva Green",
              "properties": [
                  {
                      "key": "Title",
                      "value": "Mighty Health"
                  },
                  {
                      "key": "Address",
                      "value": "108 Kirkbride Crescent, Maple, ON",
                      "type": "address;work"
                  },
                  {
                      "key": "Cell",
                      "value": "+1 (714) 873-6202",
                      "type": "phone;cell"
                  },
                  {
                      "key": "Email",
                      "value": "eva@mightyhealth.com",
                      "type": "email"
                  }
              ],
              "channels": [
                  {
                      "type": "Webchat",
                      "metadata": [
                          {
                              "key": "caption-show",
                              "value": "true"
                          },
                          {
                              "key": "caption-color",
                              "value": "white"
                          }
                      ]
                  }
              ]
          }
      ]
    }

.. list-table::
    :widths: 10 50
    :header-rows: 1   

    * - HTTP Status
      - Description
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


Update
******

Updates a Response Command.

**PUT** */api/v1/commands/responses/{commandId}*

**Headers**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Header     
     - Description
   * - Authorization
     - Bearer ``your portal access token``
   * - Content-Type
     - ``application/json``

**Url Segments**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Segment     
     - Description
   * - commandId
     - The command id affected.

**Request Properties**

.. list-table::
   :widths: 15 10 60
   :header-rows: 1

   * - Property     
     - Mandatory
     - Description
   * - name
     - Yes
     - Unique command name per Hub.
   * - category       
     - No
     - Command category.
   * - description       
     - No
     - Command description.
   * - integrationTypeId       
     - Yes
     - | Type of integration command is used for.
       | Valid options are:
       | -- *agent*
       | -- *customer*
   * - type
     - Yes
     - | Response command type.
       | Valid options are:
       | -- *message* 
       | -- *event*
   * - responses
     - Yes
     - A list of :ref:`Message <ref_activities_message_types>` or :ref:`Event <ref_activities_event_types>` types.
       

**Example Request Body**

.. code-block:: JSON

    {
      "category": "Office contacts",
      "description": "Eva's Office Contact",
    }

**Response** : 200 (OK)

.. code-block:: JSON

    {
      "commandId": "00000000-0000-0000-0000-000000000005",
      "hubId": "00000000-0000-0000-0000-0000000000a1",
      "name": "contact-eva.green",
      "category": "Office contacts",
      "description": "Eva's Office Contact",
      "integrationTypeId": "customer",
      "type": "message",
      "responses": [
          {
              "type": "text",
              "text": "Below is my contact info"
          },
          {
              "type": "contact",
              "imageUrl": "https://image.png",
              "title": "Eva Green",
              "properties": [
                  {
                      "key": "Title",
                      "value": "Mighty Health"
                  },
                  {
                      "key": "Address",
                      "value": "108 Kirkbride Crescent, Maple, ON",
                      "type": "address;work"
                  },
                  {
                      "key": "Cell",
                      "value": "+1 (714) 873-6202",
                      "type": "phone;cell"
                  },
                  {
                      "key": "Email",
                      "value": "eva@mightyhealth.com",
                      "type": "email"
                  }
              ],
              "channels": [
                  {
                      "type": "Webchat",
                      "metadata": [
                          {
                              "key": "caption-show",
                              "value": "true"
                          },
                          {
                              "key": "caption-color",
                              "value": "white"
                          }
                      ]
                  }
              ]
          }
      ]
    }

.. list-table::
    :widths: 10 50
    :header-rows: 1   

    * - HTTP Status
      - Description
    * - 200
      - OK response. The body of the response will include the data requested.
    * - 400
      - Bad request. The body of the response will have :ref:`more info<ref_api_portal_error_codes>`.
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

Delete
******

Deletes a Response Command.


**DELETE** */api/v1/commands/responses/{commandId}*

**Headers**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Header     
     - Description
   * - Authorization
     - Bearer ``your portal access token``
   * - Content-Type
     - ``application/json``

**Url Segments**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Segment     
     - Description
   * - commandId
     - The response command id.

**Response** : 200 (OK)

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

Get
***

Gets a Response Command.

**GET** */api/v1/commands/responses/{commandId}*

**Headers**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Header     
     - Description
   * - Authorization
     - Bearer ``your portal access token``
   * - Content-Type
     - ``application/json``

**Url Segments**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Segment     
     - Description
   * - commandId
     - The response command id to get.


**Response** : 200 (OK)

.. code-block:: JSON

    {
      "commandId": "00000000-0000-0000-0000-000000000005",
      "hubId": "00000000-0000-0000-0000-0000000000a1",
      "name": "contact-eva.green",
      "category": "Office contacts",
      "description": "Eva's Office Contact",
      "integrationTypeId": "customer",
      "type": "message",
      "responses": [
          {
              "type": "text",
              "text": "Below is my contact info"
          },
          {
              "type": "contact",
              "imageUrl": "https://image.png",
              "title": "Eva Green",
              "properties": [
                  {
                      "key": "Title",
                      "value": "Mighty Health"
                  },
                  {
                      "key": "Address",
                      "value": "108 Kirkbride Crescent, Maple, ON",
                      "type": "address;work"
                  },
                  {
                      "key": "Cell",
                      "value": "+1 (714) 873-6202",
                      "type": "phone;cell"
                  },
                  {
                      "key": "Email",
                      "value": "eva@mightyhealth.com",
                      "type": "email"
                  }
              ],
              "channels": [
                  {
                      "type": "Webchat",
                      "metadata": [
                          {
                              "key": "caption-show",
                              "value": "true"
                          },
                          {
                              "key": "caption-color",
                              "value": "white"
                          }
                      ]
                  }
              ]
          }
      ]
    }

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


Get Collection
**************

Gets a list of Response Commands.

**GET** */api/v1/commands/responses/hub/{hubId}*

**Headers**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Header     
     - Description
   * - Authorization
     - Bearer ``your portal access token``
   * - Content-Type
     - ``application/json``

**Url Segments**

.. list-table::
   :widths: 15 60
   :header-rows: 1

   * - Segment     
     - Description
   * - hubId
     - The Hub id to get response commands for.

**Response** : 200 (OK)

.. code-block:: JSON

    
    [
        {
          "commandId": "00000000-0000-0000-0000-000000000005",
          "hubId": "00000000-0000-0000-0000-0000000000a1",
          "name": "contact-eva.green",
          "category": "Office contacts",
          "description": "Eva's Office Contact",
          "integrationTypeId": "customer",
          "type": "message",
          "responses": [
              {
                  "type": "text",
                  "text": "Below is my contact info"
              },
              {
                  "type": "contact",
                  "imageUrl": "https://image.png",
                  "title": "Eva Green",
                  "properties": [
                      {
                          "key": "Title",
                          "value": "Mighty Health"
                      },
                      {
                          "key": "Address",
                          "value": "108 Kirkbride Crescent, Maple, ON",
                          "type": "address;work"
                      },
                      {
                          "key": "Cell",
                          "value": "+1 (714) 873-6202",
                          "type": "phone;cell"
                      },
                      {
                          "key": "Email",
                          "value": "eva@mightyhealth.com",
                          "type": "email"
                      }
                  ],
                  "channels": [
                      {
                          "type": "Webchat",
                          "metadata": [
                              {
                                  "key": "caption-show",
                                  "value": "true"
                              },
                              {
                                  "key": "caption-color",
                                  "value": "white"
                              }
                          ]
                      }
                  ]
              }
          ]
        },        
        {
            "commandId": "00000000-0000-0000-0000-000000000006",
            "hubId": "00000000-0000-0000-0000-0000000000a1",
            "name": "Command-5",
            "category": "Command-5",
            "description": "Command-5",
            "integrationTypeId": "agent",
            "type": "event",
            "responses": [
                {
                    "type": "payload",
                    "payloadType": "type1",
                    "payload": {
                        "payload": "Hello"
                    }
                }
            ]
        }
    ]
    

.. list-table::
    :widths: 10 50
    :header-rows: 1   

    * - HTTP Status
      - Description
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

