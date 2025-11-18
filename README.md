# OGC API - Processes - Part 2: Deploy, Replace, Undeploy

This repository contains the [OGC Building Blocks](https://blocks.ogc.org) for **OGC API - Processes - Part 2: Deploy, Replace, Undeploy (DRU)**.

## Overview

This Building Block extends [OGC API - Processes - Part 1: Core](https://ogcincubator.github.io/bblocks-ogcapi-processes/) with dynamic process lifecycle management capabilities, enabling:

- **Deploy** - Add new processes to the server using OGC Application Packages
- **Replace** - Update existing processes with new versions
- **Undeploy** - Remove processes from the server

## Building Blocks

This repository provides the following building blocks:

### API
- **OGC API - Processes Part 2** (`ogc.api.processes.v2.api`) - Complete OpenAPI definition for DRU operations

### Schemas
- **Execution Unit** (`ogc.api.processes.v2.schemas.executionUnit`) - Process execution unit definition
- **OGC Application Package** (`ogc.api.processes.v2.schemas.ogcapppkg`) - Standard application package format
- **OGC Application Package with CWL** (`ogc.api.processes.v2.schemas.ogcapppkg-cwl`) - CWL-enabled application package
- **Process Summary DRU** (`ogc.api.processes.v2.schemas.processSummaryDRU`) - Extended process summary for DRU operations

### Responses
- **Deploy Success** (`ogc.api.processes.v2.responses.deploySuccess`) - HTTP 201 response for successful deployment
- **Replace Success** (`ogc.api.processes.v2.responses.replaceSuccess`) - HTTP 200 response for successful replacement
- **Undeploy Success** (`ogc.api.processes.v2.responses.undeploySuccess`) - HTTP 200 response for successful undeployment
- **Duplicate Process Error** (`ogc.api.processes.v2.responses.duplicateProcess`) - HTTP 409 error for duplicate deployments
- **Immutable Process Error** (`ogc.api.processes.v2.responses.immutableProcess`) - HTTP 403 error for operations on immutable processes

## Specification

These building blocks implement the draft specification:
- [OGC API - Processes - Part 2: Deploy, Replace, Undeploy (20-044)](http://docs.ogc.org/DRAFTS/20-044.html)

## Documentation

The automation-generated documentation for these building blocks is available at:
- **Published**: [https://geolabs.github.io/bblock-ogcapi-processes-part2/](https://geolabs.github.io/bblock-ogcapi-processes-part2/)

## Dependencies

This Building Block depends on:
- [OGC API - Processes - Part 1: Core](https://ogcincubator.github.io/bblocks-ogcapi-processes/)
- [Common Workflow Language (CWL) Building Blocks](https://ogcincubator.github.io/bblocks-cwl/)

## Usage

For detailed information on how to use and customize this template, see [USAGE.md](USAGE.md).

## Status

**Status**: Under development

These building blocks are aligned with the draft OGC API - Processes Part 2 specification and are subject to change.


