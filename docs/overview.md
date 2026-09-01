# Overview

[简体中文](overview.zh-CN.md) | [Docs Index](README.md)

## Purpose

IP packet codecs, protocol dispatch helpers, and checksum utilities for Gnalloy raw transports.

This module sits above transports and below application handlers. It translates bytes or Gnalloy messages into protocol objects, and translates outbound protocol objects back to bytes. It does not open sockets or own EventLoops.

## Repository Identity

- Module path: `gnalloy.org/codec-ip`
- GitHub repository: `github.com/gnalloy/codec-ip`
- Default branch: `dev`
- License: Apache-2.0

## Package Map
- `gnalloy.org/codec-ip` (`ip`)

## Direct Gnalloy Dependencies
- `gnalloy.org/gnalloy`
- `gnalloy.org/transport-raw`

## Direct Dependents in the Current Module Plan
- `gnalloy.org/examples`

## Architecture Position

Gnalloy keeps the core small and dependency-light. This repository is a replaceable module around one responsibility, connected through explicit Go packages instead of runtime discovery.

## Compatibility

The public import path is `gnalloy.org/codec-ip`. Until the first stable tag is published, use `@dev` or an explicit pseudo-version selected by your dependency policy.
