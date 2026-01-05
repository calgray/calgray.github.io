---
title: "ECS Architecture"
categories:
  - blog
tags:
  - gamedev
  - simulation
image: /assets/images/ECS_Simple_Layout.png
header:
  teaser: /assets/images/thumbnails/ECS_Simple_Layout_300w.png
---

Most semi-realtime simulation and game engines use Entity (E) or Entity-Component (EP) architectures, but to harness real cache-optimisation and performance, ECS is the modern pattern for maximizing parallelism without relying on the engine's virtual dispatch.

## What exactly is ECS?

ECS (Entity-Component-System) is a modern pattern for implementing complex scene behaviours that shifts away from polymorphic inheritence and scene-graphs to an flatter architecture with more specialized classes, each with fewer responsibilies.

### Entity

Entities are the primary conceptual objects populating the world/scene. Entities represent the things that require extending with behaviours such as graphics, sounds, physics, subentities, and typically everything that fills in the blank canvas.

Engines with visual editors assist in intuitively providing these things in a drag and drop fashion into what's known as a **scene-graph**. In plain Entity-based architectures, entities are distinct structs/classes that represent multiple behaviours.

### Component

Components improve on the Entity architectures by letting all entities be of a common class, and moves intrinsic properties and attributes of entities to attachable components for improved modularity.

In Entity-Component architectures, components have the additional responsibilty of implementing behaviours, usually via an method interface and able to query sibling components and traverse the scene graph from the entity it's attached to.

In ECS, components **only** represent intrinsic properties of the entity.

### System

Systems are the implementation of component behaviours, and where the heavy compute operations happen.

The defining characteristic of system subroutines is that they get to perform iteratively over a range entities and components, and this range based operation is where there is room for data and instruction residency optimization.

The primary feature of ECS libraries is providing an entity-component registry (similar to a relational database) and fast query functionality to select all entities of certain traits and properties for the system to repeat an operation over hundreds or thouasands of times every frame.

## Why don't modern engines migrate to ECS?

There are two large barriers holding ECS migration back:

* Engine code gets compiled **before** custom code, but optimized systems need to compile **after**.

To avoid virtual dispatch, optimized update loops must compile after the game code with concrete references to functions to utilize concrete dispatch, inlining and as many compile-time optimizations as possible.

* Higher barrier to entry.

Scene designers using the engine editor don't want to have to write system loop code just to preview out-of-the-box components. Young developers also wanting to get started on getting something working in a timely manor don't want to both learn all the OOP details of ECS patterns and optimizations before hello world, even if it means stumbling into the trap that is deep inheritence and poor performance scaling.

To use a powerful engine with custom behaviour, adapting to ECS is up to developers willing to optimize on architecture.

## How does ECS help performance?

Systems in ECS are main loop logic that are no longer virtual calls compiled into the engine, they are compiled last which has the benefit of:

* Linking to concrete types without interface dynamic dispatch for more cache hits
* Have full control of the behaviour loop
* Have control over the layout of the component registry, leading to optimized data locality when system iterate.

## How to add to a game engine?

ECS is an entirely different way of structuring the way a scene updates at runtime.

The first step is realizing that ECS registry effectively replaces the engine scene graph at runtime with a single root node to update. This is okay to perform, many benchmarks reveal that systems (even in high level languages) perform better processing a flat list of components than traversing the scene graph hierarchy.

The registry can be populated dynamically, and many examples show this, but the next step in a solid ECS integration is translating a carefully crafted scene designed in the editor to a performant registry layout. The neat part of this is that:

* the scenegraph deserialize automatically via the engine
* the scene will render bugfree as the engine intended in the editor
* only at the playtest time does ECS conversion run

This keeps any optimization bugs away from designers and continues to let designers to hand scenes to developers using ECS. There is no need to convert ECS back to a scene graph.

<!-- {% thumbnail_img assets/images/ECS_Simple_Layout.png 300 %} -->
