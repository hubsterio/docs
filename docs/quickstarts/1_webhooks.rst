Webhooks
========

This section describes the necessary considerations along with an example, **on-how-to** prepare your webhook endpoint, 
to safely trust incoming messages sent by Hubster. This only applies to integration types that support 
webhooks such as the integration types below:

* System
* Direct
* BYOI (Bring your own Integration)

.. warning:: For **Direct** and **BYOI** integration types, they have the option to either receive 
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

**Note**: you can also get an existing custom integration result by calling: **GET** */api/v1/integrations/{integrationId}*

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

.. warning:: Please make sure all **private keys** are stored securely. 
             If you suspect your private key has been compromised,  
             delete the compromised custom integration and recreate a new one. 
             A new public/private key set will be regenerated. 

C# Sample
*********

Below is an example code snippet using **C# ASP.NET Core**. This sample validates that 
the request is trusted using HMAC, and once trusted, consumes the activities. 
The code is fairly straight forward and should be easily transferable to other programing languages. 

The main steps are as follows:

    #. Extract the **Signature** from the request header 
    #. Extract the **Public Key** from the request header 
    #. Obtain the **Private Key** from your secure keystore and convert it to a **UTF8** byte array
    #. Obtain the raw request body in string format and convert it to a **UTF8** byte array
    #. Produce the a HMAC hash (signature) by using the raw request body and applying the **Private Key**
    #. Take the signature produced from the step above and convert it a string using **UTF8** encoding
    #. Compare if signatures match
    #. If signatures don't match then respond as Unauthorized, otherwise, consume the :ref:`activities<ref_activities>` as needed

.. code-block:: CSHARP

    public void Test()
    {
        JwtSecurityTokenHandler.DefaultMapInboundClaims = false;

        services.AddAuthentication(options =>
            {
                options.DefaultScheme = "Cookies";
                options.DefaultChallengeScheme = "oidc";
            })
            .AddCookie("Cookies")
            .AddOpenIdConnect("oidc", options =>
            {
                options.Authority = "https://localhost:5001";

                options.ClientId = "mvc";
                options.ClientSecret = "secret";
                options.ResponseType = "code";

                options.SaveTokens = true;
            });        
    }

.. note:: If you're using **.NET Core**, the following nuget package has all the activity models
          predefined and can be useful when consuming activities 
          - `Hubster.Abstractions <https://www.nuget.org/packages/Hubster.Abstractions/1.0.1>`_

          .. code-block:: CSHARP

            Install-Package Hubster.Abstractions -Version 1.0.1     

.. https://www.nuget.org/packages/Hubster.Abstractions/1.0.1
.. Install-Package Hubster.Abstractions -Version 1.0.1


System Integration Activity Event Filters
*****************************************

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
      
.. warning:: Once all retries attempts have been exhausted, Hubster will send a notification to the tenant account holder
             with details to as to why the endpoint has failed. It is up to the the account holder to rectify 
             their integration issue. 

