---
layout: default
title: Building Tests
has_children: false
permalink: /docs/firmware/testing
parent: Device Firmware
grand_parent: Smart Device
has_toc: false
nav_order: 2
---

# Building Tests

Frequently when developing device firmware, small test programs need to be made to ensure correct operation. These small programs may be useful for troubleshooting in the future or as examples on how to use certain components.

## Goals
- Only a single test should be compiled into the final image.
- Tests should be selected out-of-tree (Using CMake options)
- The image should always compile no matter what is configured

## Implementation
The operation relies on two cmake options, one boolean and one string. The first option, `EMA_BUILD_TESTS` controls whether tests are compiled at all. If set to `ON`, the `TEST` define will be included in your code. The second option, `EMA_TEST`, controls which test is actually used. See below on details on how to set `EMA_TEST`.

## Making new tests
To make a new test, open the file "test/test.c". Within this file is a large `#ifdef`/`#elif` structure. Just add a new `#elif` section in here and name the define similarly to the others. Keep the name you chose in mind, as this name is what you must set `EMA_TEST` to in order to use the new test.

## Setting CMake options in VSCode
After setting up the firmware toolchain as per [Device Firmware](/docs/firmware), you should have a working visual studio setup. From the command pallete (Ctrl+Shift+p), select "Cmake: Edit Cmake Cache (ui)". From here you can search for `EMA_BUILD_TESTS` and `EMA_TEST` in order to set them. When finished, press the button labeled "SAVE".