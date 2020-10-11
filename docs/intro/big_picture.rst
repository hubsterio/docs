The Big Picture
===============

Hubster’s 10,000 - foot, High Level Architecture
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Hubster’s platform was designed with simplicity in mind, yet power enough to allow a business to extend the platform to meet their specific needs, on a per hub basis. 

Engine
******

.. image:: images/arch_full.png

**Hubster’s Engine workflow and feature annotation:**

#. Customer channels initiate a conversation with the engine
#. The engine detects the request and reverse engineers [link to UX] the channel’s proprietary format to common Hubster format.
#. The engine reads the channel’s Hub configuration and determines if there are any preliminary pipeline actions to take:
#. Once preliminary actions have been completed, the engine then determines if there are any auxillary actions to take:

    * Are there any custom plugins configured?
    * Are there any webhooks configure and what filter rule should be triggered?
    * Are there any keyword spotting phrases configured and if so, what CRM endpoint should be invoked?
    * What is the active business destination (agent or bot)?

#. If an agent is the **active business destination**, the engine will send the rendered response to the agent's configured endpoint.
#. If a bot is the **active business destination**, the engine will send appropriate response to the bot's configured endpoint.


The Hub Anatomy	
^^^^^^^^^^^^^^^

Engine Pipeline
^^^^^^^^^^^^^^^

Bring your own Integration (BYOI)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

UX Multi-rendering/Response Framework
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
