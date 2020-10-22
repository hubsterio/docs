Welcome to Hubster's Documentation Portal
=========================================

.. image:: images/logo.png
   :align: center

Hubster is an open-ended *Unified Message Platform as a Service* **(PaaS)** and like all good platforms, we try our best to adhere to industry standards and best practices.

So, what is meant by an **Open-ended** platform? An open-end platform allows a business to extend the platform by enabling the business to bring in their own integration or plugins. 

At Hubster, we provide following ways on how you can extend our platform: 

   | **Integration (BYOI)**: 
   | If you have an integration that Hubster does not currently support or it is unique to your business, you can easily add it to the mix using our direct API. There are no limits on how many customer, agent, bot, or CRM integrations you can add.

   | **Pipeline plugins (BYOP)**
   | Businesses can control the message pipeline by injecting their custom plugins. You can enrich messages, alter, or even control the follow how messages are redirected to any given participant involved in the conversation.

   | **Webhooks**
   | Businesses can add their own webhooks and will only be triggered based on *filter rules*. This is a great way to monitor certain activities that are important to the business. It should be noted that standard Webhooks are based on a one-way communication protocol know as *fire-and-forget*. 

   | **Dynamic Commands**
   | Dynamic commands are a powerful concept allowing agents and/or bots through simple text, instruct Hubster to invoke your backend service to formulate the appropriate response. For example, if your business provides a command to a list a line of clothing specific to the user’s profile, your system can check to see what are the best options and construct a targeted response that is meaningful to the end user.

Our :ref:`APIs<ref_api_overview>` are designed using **REST** principles and most of our payloads are structured using **JSON**. Any exception to this rule will be noted where necessary.

.. note:: Hubster APIs incorporate cross-origin resource sharing (**CORS**) whereby facilitating web applications to freely use our API in an authenticated and secure manner.

| **Please help us make this experience even better**
| If you find any errors or a section is not as clear or lacking details, please don't hesitate to contact us at support@hubster.io

.. toctree::
   :maxdepth: 3
   :hidden:
   :caption: Introduction

   intro/0_big_picture
   intro/1_terminology
   intro/2_integrations
   intro/3_support

.. toctree::
   :maxdepth: 3
   :hidden:
   :caption: Quickstarts

   quickstarts/0_overview
   quickstarts/1_webhooks

.. toctree::
   :maxdepth: 3
   :hidden:
   :caption: Topics

.. toctree::
   :maxdepth: 3
   :hidden:
   :caption: API

   api/0_overview
   api/1_identity
   api/2_portal
   api/3_engine
   api/4_activities
   api/5_types
   api/6_error_codes   
   
