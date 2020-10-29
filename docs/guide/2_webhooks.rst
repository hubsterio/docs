Webhooks
========

This section describes the necessary considerations along with an example, **on-how-to** prepare your webhook endpoint, 
to safely trust incoming messages sent by Hubster. This only applies to integration types that support 
webhooks such as the integration types below:

* System
* Direct
* BYOI (Bring your own Integration)

.. warning:: 
    For **Direct** and **BYOI** integration types, they have the option to either receive 
    activities via **webhooks** vs **websockets**. If an integration has been configured using websockets and 
    its endpoint is unreachable, Hubster will not enforce it's :ref:`retry policy<ref_webhooks_retry>` as websockets 
    adhere to **fire-and-forget** paradigm.


HMAC Signature Validation
*************************

If your custom integration was configured to receive activities via webhooks, it's important to 
ensure that the request your integration receives comes from a trusted source, in this case Hubster.

Hubster uses the `HMAC <https://en.wikipedia.org/wiki/HMAC/>`_ when signing and verify signatures. 
When you :ref:`create<ref_portal_integration_create_config>` and configured your custom integration for a given hub, 
the results of the request will yield two properties - **publicSigningKey** and **privateSigningKey** respectively. 

To obtain your customer integration's public/private key pair, just call the following API: 

**GET** */api/v1/integrations/{integrationId}* 

.. code-block:: JSON

    {
        "integrationTypeId": "System",
        "channelId": "System",
        "name": "My cool integration name.",        
        "configuration": {
            "events": [
                "message"
            ],
            "webhookUrl": "https://url_end_point.com",
            "publicSigningKey": "3EF951F619CD4F5E820C73622C0F1A3C",
            "privateSigningKey": "FA96D15568654A4482772E00BA941BCB"
        }
    }

The **publicSigningKey** is not used by Hubster when signing the request. However, the business can use 
the **publicSigningKey** as a reference key to obtain their **privateSigningKey** from where they manage their secrets. 

.. warning::
    Please make sure all **private keys** are stored securely. 
    If you suspect your private key was compromised, you can regenerate new **public/private key pair** by 
    updating your custom integration. Click :ref:`here<ref_integration_update_direct>` for more info.    

C# Sample
*********

Below is an example code snippet using **C# ASP.NET Core**. This sample validates that 
the request is trusted using HMAC, and once trusted, consumes the activities. 
The code is fairly straight forward and should be easily transferable to other programing languages. 

The main steps are as follows:

    #. Extract the **Signature** from the request header 
    #. Extract the **Public Key** from the request header 
    #. Obtain the **Private Key** from your secure keystore and convert it to a **UTF8** byte array
    #. Obtain the raw request body in byte array form
    #. Produce the a **HMAC** hash (signature) by using the raw request body and applying the **Private Key**
    #. Take the signature array produced from the step above and convert to 64 base encoding
    #. Compare if signatures match
    #. If signatures match then consume the :ref:`activities<ref_activities>` as needed
    #. If signatures don't match then return **Forbidden** (403) 


This sample is based off APS.NET Core, using C#. To see the full example, 
head over to Hubster's public `sample <https://github.com/hubsterio/samples>`_  repo. 

.. code-block:: CSHARP

    [ApiController]
    [Route("[controller]")]
    public class WebhooksController : ControllerBase
    {
        [HttpPost("activities")]
        public async Task<IActionResult> ReceiveActivities()
        {
            var publicKey = Request.Headers["x-hubster-public-key"].ToString();
            var headerSignature = Request.Headers["x-hubster-signature"].ToString();

            if (string.IsNullOrWhiteSpace(publicKey) 
            || string.IsNullOrWhiteSpace(headerSignature))
            {
                return StatusCode((int)HttpStatusCode.Forbidden, "Forbidden");
            }

            var privateKey = await GetPrivateKeyAsync(publicKey);

            var rawBody = new byte[(int)Request.ContentLength];
            await Request.BodyReader.AsStream().ReadAsync(rawBody);

            // now preform HMAC signature check

            using (var hasher = new HMACSHA256(privateKey))
            {
                var byteSignature = hasher.ComputeHash(rawBody);
                var signature = Convert.ToBase64String(byteSignature);

                if (signature != headerSignature)
                {
                    _logger.LogWarning("Invalid signature");
                    return StatusCode((int)HttpStatusCode.Forbidden, "Forbidden");
                }
            }

            // at this point the request is now trusted 
            // and it came from Hubster

            var json = Encoding.UTF8.GetString(rawBody);
            var activityConverter = new DirectMessageJsonConverter();
            var activities = JsonConvert.DeserializeObject<SystemOutboundDataModel>(json, activityConverter);

            // you now have a list of activities you can process, etc.
            
            return Ok(); 
        }

        private Task<byte[]> GetPrivateKeyAsync(string publicKey)
        {
            // NOTE: for sake of sample, we are hard-coding the private key
            // however, you should use the public key as an indexer to get
            // the private key in some secure store like KeyVault, etc. 

            var privateKey = "FA96D15568654A4482772E00BA941BCB";
            var bPrivateKey = Encoding.UTF8.GetBytes(privateKey);

            return Task.FromResult(bPrivateKey);
        }
    }

.. note:: 
    | If you're using **.NET Core**, the following nuget package contains all the activity model definitions.    
    | `Hubster.Abstractions <https://www.nuget.org/packages/Hubster.Abstractions/1.0.2>`_

    .. code-block:: CSHARP

      Install-Package Hubster.Abstractions -Version 1.0.2   

    To see a list of activity models, see our public 
    `github <https://github.com/hubsterio/Hubster.Abstractions/tree/develop/Hubster.Abstractions/Models/Direct>`_  
    for direct reference.


Webhook - Payload 
*****************

Webhook endpoints will receive a payload that looks similar to the JSON snippet shown below.
The root node contains the **conversation** details and the **activities** node contains 
one or more :ref:`activities<ref_activities>`.

.. code-block:: JSON

    {
      "hubId": "00000000-0000-0000-0000-000000000001",
      "tenantId": "00000000-0000-0000-0000-000000000002",
      "integrationId": "00000000-0000-0000-0000-000000000003",
      "conversationId": "00000000-0000-0000-0000-000000000004",
      "conversationProperties": {
        "profile": {
          "device": "Direct",
          "full name": "Some customer name",
          "prop1": "value1",
          "prop2": "value2"
        },
        "additional": {
          "prop1": "value1",
          "prop2": "value2"
        }
      },	
      "activities": [
        {
          "type": "message",
          "eventTrigger": "message:customer",
          "eventId": 1603933721542,
          "externalId": "my-external-id",
          "isEcho": false,
          "interactionId": "00000000-0000-0000-0000-000000000005",
          "flowProcess": "Default",
          "sender": {
            "integrationId": "00000000-0000-0000-0000-000000000001",
            "integrationType": "Customer",
            "channelType": "Direct",
            "tokenId": "t+8qymYD1jp7wDSHG+3eUA=="
          },
          "recipient": {
            "integrationId": "00000000-0000-0000-0000-000000000006",
            "integrationType": "Agent",
            "channelType": "Direct",
            "tokenId": "971480cb-938c-4dfd-be4e-01756c833490.00000000-0000-0000-0000-000000000003"
          },
          "message": {
            "type": "text",
            "text": "Hi there!"			
          }
        }
      ]
    }


Direct - Payload 
****************

The Direct outbound payload is similar to the Webhook outbound payload accept that, rather than
having a collection of activities, the activities will be replaced with an :ref:`activity<ref_activities>` node.

.. code-block:: JSON

    {      
      "hubId": "00000000-0000-0000-0000-000000000001",
      "tenantId": "00000000-0000-0000-0000-000000000002",
      "integrationId": "00000000-0000-0000-0000-000000000003",
      "conversationId": "00000000-0000-0000-0000-000000000004",
      "conversationProperties": {
        "profile": {
          "device": "Direct",
          "full name": "Some customer name",
          "prop1": "value1",
          "prop2": "value2"
        },
        "additional": {
          "prop1": "value1",
          "prop2": "value2"
        }
      },	
      "activity": {
          "type": "message",
          "eventTrigger": "message:customer",
          "eventId": 1603933721542,
          "externalId": "my-external-id",
          "isEcho": false,
          "interactionId": "00000000-0000-0000-0000-000000000005",
          "flowProcess": "Default",
          "sender": {
            "integrationId": "00000000-0000-0000-0000-000000000001",
            "integrationType": "Customer",
            "channelType": "Direct",
            "tokenId": "t+8qymYD1jp7wDSHG+3eUA=="
          },
          "recipient": {
            "integrationId": "00000000-0000-0000-0000-000000000006",
            "integrationType": "Agent",
            "channelType": "Direct",
            "tokenId": "971480cb-938c-4dfd-be4e-01756c833490.00000000-0000-0000-0000-000000000003"
          },
          "message": {
            "type": "text",
            "text": "Hi there!"			
          }
      }    
    }




Activity Event Filters
**********************

Below are list of of activity events that **system** integrations can register too. 
System integrations must register to at least one event but can register to more as deemed necessary.
Hubster will only send events once, to one of the following events if triggered.

.. _ref_webhooks_events:

.. list-table::
    :widths: 5 50
    :header-rows: 1

    * - Event
      - Description
    * - message
      - Hubster will notify the webhook on **all message** activities for the given hub.
    * - message:customer
      - Hubster will only notify the webhook on **all customer message** activities for the given hub.
    * - message:agent
      - Hubster will only notify the webhook on all **agent message activities** for the given hub.
    * - message:bot
      - Hubster will only notify the webhook on all **bot message activities** for the given hub.

.. _ref_webhooks_retry:

Webhook Retry Policy
********************

.. list-table::
    :widths: 10 20 20
    :header-rows: 1

    * - Retry Attempt      
      - Next Retry Period
      - Timeout Before Retry
    * - 0 x 2 minutes
      - 0 minutes (immediate)
      - 10 seconds
    * - 1 x 2 minutes
      - 2 minutes
      - 10 seconds
    * - 2 x 2 minutes
      - 4 minutes
      - 10 seconds
    * - 3 x 2 minutes
      - 6 minutes
      - 10 seconds
    * - 4 x 2 minutes
      - 8 minutes
      - 10 seconds
    * - 5 x 2 minutes
      - 10 minutes
      - 10 seconds
      
.. warning:: 
    Once all retries attempts are exhausted, Hubster will send a **notification** to the tenant account holder
    with details to as to why the endpoint failed. It is up to the the account holder to rectify 
    their integration issue. 

