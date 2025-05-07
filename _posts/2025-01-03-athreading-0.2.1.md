---
title: "athreading 0.2.1 released"
categories:
  - blog
  - project
tags:
  - project
  - release
---

`athreading` is a Python library that allows you to run synchronous I/O functions asynchronously using asyncio via background threads. It provides decorators to adapt synchronous functions and generators, enabling them to operate without blocking the event loop.

In versions >=0.2.0, `athreading` adds support for both Python 3.9 nogil, and Python 3.13 with free threading enabled to utilize parallelism and multicore goodness when the python GIL is disabled.

See [https://github.com/calgray/athreading](https://github.com/calgray/athreading) and [PyPI](https://pypi.python.org/pypi/athreading) for installation.

**Changes in Code of Conduct:** `athreading` has adopted the [Contributor Covenant](https://www.contributor-covenant.org) code of conduct. Check out the `athreading` [code of conduct](https://github.com/calgray/athreading/blob/main/CODE_OF_CONDUCT.md) for up to date details for project contributors.
{: .notice}

### Release Notes

#### 0.2.1

Added

    Added contributing document.
    Added code of conduct.

Changed

    Updated release workflow process.
    Updated Readme.
    Test dependencies audited.

#### 0.2.0

Added

    Added support for python 3.13 with free threading.
    Added support for python 3.9 with nogil.
    Added support for providing explicit background executor to decorators.
    Added call and iterate benchmarks.

Changed

    Changed call, iterate and generate to higher-order-function decorators.