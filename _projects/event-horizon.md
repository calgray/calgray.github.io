---
permalink: /event-horizon/
title: "event-horizon"
categories:
  - project
tags:
  - project
  - event-horizon
---

`event-horizon` is a general-purpose event library that provides various event-system for building event-driven systems.

There are four key components to event-horizon:

- **Event** User event source instance where events trigger.
- **EventData** User data model broadcasted as the event argument.
- **EventListener** One of potentially multiple instances that subscribe to the event. Production ready listeners are provided.
- **EventProtocol** User function or method implementation that is eventually invoked by the listener.

Note: All **EventListener** share the same single callable protocol as an **EventProtocol**. If concurrent dispatching is not required, an EventProtocol function/lambda can simply be used implace of the **EventListener**.

![diagram](https://cdn.prod.website-files.com/64a7eed956ba9b9a3c62401d/652647842f2ab6136d54c600_Feature%20image%20-%20Event%20driven%20programming.jpg)

Follow this space for the first release!

