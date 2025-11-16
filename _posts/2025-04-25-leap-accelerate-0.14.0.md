---
title: "icrar-leap-accelerate 0.14.0 released"
categories:
  - blog
  - project
tags:
  - project
  - release
  - leap
header:
  teaser: /assets/images/posts/leap/ionosphere.png
---

Leap in 2023-2024 has gone through a major transformation of delivering python bindings as it's new public interface through [pybind11](https://pybind11.readthedocs.io). The Leap CLI is now completely rewritten in python under the new name `leap-cli`.

## Preview

`leap-cli` is now composed of subcommands, notably `batch/realtime` for selecting between different approaches to processing input, and `dump/plot` for selecting output format.

    $leap-cli batch plot --help

    Usage: leap_cli batch plot [OPTIONS] MS

    Arguments:
      MS  [required]

    Options:
      -o, --outfile VIDEO_FILEPATH    the output video filepath
      -i, --impl STR                  [default: cpu]
      -s, --start INT                 [default: 0]
      -e, --end INT
      -n, --interval INT
      -m, --min_baseline_threshold METERS
                                      [default: 0.0m]
      -d, --directions RA_DEC         [default: [[0.0, 0.0]]]
      --compute-cal1 / --no-cal1      [default: compute-cal1]
      -r, --reference-antenna INT     reference antenna index. None uses the last
                                      index.
      -v, --verbosity LOG_LEVEL       [default: WARNING]
      --help                          Show this message and exit.

    $leap-cli batch plot mwa/1197638568-split.ms -d "[[7.09767229e-01, -1.98773609e-04]]" -n 12 -o leap.png

![ska low first iamge](/assets/images/posts/leap/Figure_1.png)

## Release Notes

    ### 0.14.0

    Added

    * Added tracing I matrix when tracing is enabled.
    * Added support for MSv4 Zarr MeasurementSets.
    * Added SKA calibration model conversion example.
    * Added MacOS support including system memory size checks.
    * Added support for python>=3.10,<3.14 and numpy>=1.26.0,<3.0.0.
    * Added C++17 support.