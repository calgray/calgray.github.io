---
permalink: /athreading/
title: "athreading"
categories:
  - project
tags:
  - project
  - athreading
---

`athreading` is a Python library that allows you to run synchronous I/O functions asynchronously using asyncio via background threads. It provides decorators to adapt synchronous functions and generators, enabling them to operate without blocking the event loop.

This was primarily to written to bridge the gap for synchronous `etcd3` clients to run in asynchronous codebases managing dozens or hundreds of concurrent connections.

For the latest version, see https://github.com/calgray/athreading/releases
