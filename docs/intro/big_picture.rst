The Big Picture
===============

High Level Architecture
^^^^^^^^^^^^^^^^^^^^^^^

Hubster’s platform was designed with simplicity in mind, yet power enough to allow a business to extend the platform to meet their specific needs, on a per hub basis. 

**Engine**

.. image:: images/arch_full.png

**Hubster’s Engine workflow and feature annotation:**

#. A customer channel initiates a conversation with the engine
#. The engine reads the channel’s :ref:`hub<ref_hub_anatomy>` configuration and starts the :ref:`pipeline<ref_pipeline>` workflow
#. The pipeline :ref:`reverse engineers<ref_ux_framework>` the channel’s proprietary format and constructs a common Hubster format known as an **activity**
#. Based on the hub’s configuration and channel :ref:`source type<ref_source>`, the pipeline determines the appropriate **preliminary** flow actions required
#. The pipeline then determines the appropriate **auxiliary** flow actions required
#. Once both **preliminary** and **auxiliary** flows have been executed, the pipeline then determines the **active business destination** and reverse engineers the activity to the proprietary format specific to the destination source – agent or bot
#. The agent may initiate a **takeover** from a bot, handles the request, and eventually hands the conversation back to the bot. Conversely, if the bot has difficulty handling a request, the bot can initiate a **handover** and redirect the conversation to the agent.

.. _ref_hub_anatomy:

The Hub Anatomy	
^^^^^^^^^^^^^^^

.. _ref_pipeline:

Pipeline
^^^^^^^^


Bring your own Integration (BYOI)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


.. _ref_ux_framework:

UX Multi-rendering/Response Framework
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
