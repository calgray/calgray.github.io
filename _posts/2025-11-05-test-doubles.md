---
title: "Test Doubles"
categories:
  - blog
tags:
  - testing
header:
  teaser: assets/images/posts/testing/thumbnails/test-doubles-overview_300w.png
---

To save on resources and time when testing a software product or application, substitute software components and layers using test doubles.

## Summary

| Type          | Reproduces                                                 | Executes Original Code | Behavioral Fidelity                    | Typical Purpose                                                   | Example                                                 |
| ------------- | ---------------------------------------------------------- | ---------------------- | -------------------------------------- | ----------------------------------------------------------------- | ------------------------------------------------------- |
| **Stub**      | Minimal interface — fixed outputs only                     | ❌                     | Very low                               | Isolate a unit under test by providing the bare minimum responses | A function that always returns `200 OK` without logic   |
| **Fake**      | Simplified but working implementation                      | ❌                     | Low–Medium                             | Speed up tests or development with lightweight logic              | In-memory DB that mimics CRUD but stores data in a list |
| **Mock**      | Interface with expectations on interactions                | ❌                     | Medium                                 | Verify that a component calls dependencies correctly              | Verifying `sendEmail()` was called once with args X     |
| **Simulator** | Modeled functional behavior (approximated dynamics)        | ❌                     | High (functional)                      | Predict or observe system behavior under controlled conditions    | Flight simulator modeling aerodynamics numerically      |
| **Emulator**  | Full operational semantics — identical observable behavior | ✅                     | Very high (causal & binary compatible) | Run or analyze software built for another system                  | QEMU running an ARM binary on x86                       |

## Types

### Stub

A stub provides the bare minimum behaviour to satisfy an interface.

Think of how a car requires 4 wheels to be taken off a jack; a pile of bricks is a stub meeting the bare minimum for the wheel mounting interface.

Do ✅:

* Return predefined responses.
* Log warnings.
* Raise exception on pre-condition failure.
* Raise exception on post-condition failure.

Don't ❌:

* Record interactions as interal state.
* Provide additional behaviour outside of satisfying the interface.
* Implement behaviour that is beyond constant time complexity.

Unlike most doubles, stubs can be suitable for production, such as when a polymorphic API does not support optional composition. For example, a function callback that must point to a function; a stub function is a reasonable design choice.

### Fake

A fake is a custom component that provides limited or degraded behaviours of the real component.

Unlike most doubles, Fakes don't necessarily match a desired production interface. Fakes are primarily utilities for faking the complex behaviours and may be decoupled from versioned interfaces for reusability via composition inside other test doubles.

### Mock

A mock is a behavioural test double usually used in unit tests that:

* is interface compliant
* is behaviourally compliant where it needs to be
* have additional observational behaviors that may violate immutability constraints

The advantage of using mocks in testing is that they:

* Can utilize **fake** behaviour to run much faster than the real components
* Can utilize **spy** behaviour to observe how it was interacted with by the real component, such as:
  * Call counts
  * Call order
  * Call arguments

### Simulator

Simulators are large, complex, executable models for the behaviour of another system. The advantage of simulators is that they support running under controlled and typically configurable conditions, unlike the conditions of the real system.

### Emulator

Emulators are systems that substitute for an entire platform and execute the real system instructions inside it. They typically perform 1-to-1 translations of entire hardware layers to decouple testing from physically scarce hardware.

Very similar to emulators are compatibility layers, which intentionally simplify or skip certain behaviours deemed not important for typical use, or serve as an adapter for inputs and outputs.

## Testing Resources

https://principal-it.eu/blog.html

<!-- {% thumbnail_img assets/images/posts/testing/test-doubles-overview.png 300 %} -->
