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
- **OGC API - Processes Part 2** (`ogc.api.processes.part2.v1.api`) - OpenAPI definition for DRU operations

### Schemas
- **Execution Unit Property Value** (`ogc.api.processes.part2.v1.schemas.executionUnitValue`) - Canonical `executionUnit` property: a single unit or an array
- **Execution Unit Base** (`ogc.api.processes.part2.v1.schemas.executionUnitBase`) - One link or qualified container, CWL or custom unit
- **Qualified Execution Unit Value** (`ogc.api.processes.part2.v1.schemas.qualifiedExecutionUnitValue`) - Part 2-owned arbitrary JSON payload and Part 1 v1 format qualifiers
- **Execution Unit Container** (`ogc.api.processes.part2.v1.schemas.executionUnitContainer`) - Nested Docker/OCI `value` payload, including resources and bindings
- **Input Binding** (`ogc.api.processes.part2.v1.schemas.inputBinding`) - Container input command-line binding
- **Output Binding** (`ogc.api.processes.part2.v1.schemas.outputBinding`) - Container output glob binding
- **Execution Unit (legacy flat)** (`ogc.api.processes.part2.v1.schemas.executionUnit`) - Existing flat container contract, preserved unchanged
- **OGC Application Package** (`ogc.api.processes.part2.v1.schemas.ogcapppkg`) - Standard application package format
- **OGC Application Package with CWL** (`ogc.api.processes.part2.v1.schemas.ogcapppkg-cwl`) - CWL-enabled application package
- **Process Summary DRU** (`ogc.api.processes.part2.v1.schemas.staticIndicator`) - Extended process summary for DRU operations

### Canonical schema consolidation (2026-11-09)

The seven draft schema blocks are consolidated under `_sources/part2/v1/schemas`.
References migrating from `ogc.api.processes.part2.schemas.*` must use:

| Draft suffix | Canonical identifier |
| --- | --- |
| `executionUnit` | `ogc.api.processes.part2.v1.schemas.executionUnitValue` |
| `executionUnitBase` | `ogc.api.processes.part2.v1.schemas.executionUnitBase` |
| `executionUnitContainer` | `ogc.api.processes.part2.v1.schemas.executionUnitContainer` |
| `inputBinding` | `ogc.api.processes.part2.v1.schemas.inputBinding` |
| `outputBinding` | `ogc.api.processes.part2.v1.schemas.outputBinding` |
| `ogcapppkg` | `ogc.api.processes.part2.v1.schemas.ogcapppkg` |
| `processSummary` | `ogc.api.processes.part2.v1.schemas.staticIndicator` |

**Canonical versus legacy:** `executionUnitValue` describes the value of the
application package's `executionUnit` property: a single link/qualified value,
or an array of those. A canonical Docker unit has `type: docker` and a nested
`value` containing `image`. The existing public `executionUnit` schema continues
to describe a **flat** object with `type` and `image`; its schema is unchanged,
so existing consumers are not silently switched to a single-or-array contract.
`ogcapppkg` accepts both contracts with `anyOf`, but excludes a `value` property
on its legacy branch only, preventing a flat `image` from masking an invalid
canonical Docker payload. Direct link/qualifiedValue shortcuts are removed;
links and custom qualified values remain supported via the canonical branch.

The migrated `processSummary` reuses `staticIndicator`, retaining the full
Part 1 `processSummary` constraints (including `outputTransmission`) plus the
optional boolean `mutable`, annotated with `default: true`. No stripped duplicate
summary is introduced. Packages also compose `staticIndicator` into
`processDescription.process`, so a supplied mutability flag is checked there.

### Draft fidelity and local composition fixes

Descriptions and schema fragments preserve the draft text where possible.
The container's scalar `required: image` and the single-element array form of
`items` are normalized to valid JSON Schema forms, as in the migrated blocks.
The raw CWL v1.2 remote schema reference is retained because the draft's relative
CWL schema is not supplied.

The `executionUnitBase` discriminator is an explicit **local composition fix**,
not an amendment of the official draft: Docker/OCI types must validate the full
container payload, even with `mediaType: application/cwl`; otherwise that media
type selects CWL validation (with or without `type`), and only the remaining
custom types use the generic qualified-value fallback. Link-only units exclude
`value`, preventing another payload bypass. Custom scripts such as `type: python`
with an empty object payload remain valid.

Unrelated draft constraints are not silently corrected: `deployment` still
accepts any string because of its unrestricted `anyOf` branch; binding maps
retain the draft's missing object-type assertion; expression-language questions
and the example's `inputSeparator` extension remain. Schema validation neither
evaluates bindings nor demonstrates runtime conformance. See each block's
description for the distinction between faithful draft fragments and local fixes.

The 21 migrated JSON fixtures are retained, supplemented by regression fixtures
for mutability, container validation and composition bypasses. Negative fixtures
use the `-fail.json` suffix. Examples expose positive fixtures through
`examples.yaml`. Local JSON Schema checks are separate from the registry build
and its JSON-LD/RDF checks.

### Responses
- **Deploy Success** (`ogc.api.processes.part2.v1.responses.deploySuccess`) - HTTP 201 response for successful deployment
- **Replace Success** (`ogc.api.processes.part2.v1.responses.replaceSuccess`) - HTTP 200 response for successful replacement
- **Undeploy Success** (`ogc.api.processes.part2.v1.responses.undeploySuccess`) - HTTP 200 response for successful undeployment
- **Duplicate Process Error** (`ogc.api.processes.part2.v1.responses.duplicateProcess`) - HTTP 409 error for duplicate deployments
- **Immutable Process Error** (`ogc.api.processes.part2.v1.responses.immutableProcess`) - HTTP 403 error for operations on immutable processes

## Specification

These building blocks implement the draft specification:
- [OGC API - Processes - Part 2: Deploy, Replace, Undeploy (20-044)](http://docs.ogc.org/DRAFTS/20-044.html)

## Documentation

The automation-generated documentation for these building blocks is available at:
- **Published**: [https://geolabs.github.io/bblock-ogcapi-processes-part2/](https://geolabs.github.io/bblock-ogcapi-processes-part2/)

## Dependencies

This is **Part 2 version 1.0 draft (OGC 20-044)**, not version 2.0.
The namespace is `ogc.api.processes.part2.v1.*`; block `version` fields remain
independent revision metadata. The normative Part 1 dependency is version 1.0,
OGC 18-062r2, not the GeoLabs Part 1 version 2.0 draft fork.

The imported dual-edition GeoLabs register is
<https://geolabs.github.io/bblocks-ogcapi-processes/build/register.json>.
Its independently hosted upstream v1 definitions use explicit
`ogc.api.processes.part1.v1.*` IDs for `link`, `format`,
`process`, `processSummary`, exceptions, responses and parameters.
There is no direct or transitive block dependency on `ogc.api.processes.part1.v2.*`;
the imported register hosts both editions, but Part 2 selects v1 only.
The source pin and attribution are documented in the Part 1 register's README.
The missing upstream `qualifiedValue` is not replaced with the incompatible
`qualifiedInputValue`: `qualifiedExecutionUnitValue` is explicitly owned here,
accepting arbitrary JSON `value` types and the original format qualifiers
(`mediaType`, `encoding`, `schema`). Container and CWL discrimination is still
enforced by `executionUnitBase`; custom numeric/string payloads are tested.

**Breaking publication change:** old `ogc.api.processes.v2.*` IDs become
`ogc.api.processes.part2.v1.*`; the legacy flat schema contract is preserved,
not its old identifier. Publish the dual-edition Part 1 register first, then this
register, then the combined standard register. Ignored local URL mappings and
read-only sibling mounts are used by Part 2 and the combined register until
those publications are available. Other consumers
must be assessed separately; no aliases, commit or push are created here.

This Building Block depends on:
- [OGC API - Processes - Part 1: Core, GeoLabs v1 definitions](https://geolabs.github.io/bblocks-ogcapi-processes/)
- [Common Workflow Language (CWL) Building Blocks](https://ogcincubator.github.io/bblocks-cwl/)

## Usage

For detailed information on how to use and customize this template, see [USAGE.md](USAGE.md).

## Status

**Status**: Under development

These building blocks are aligned with the draft OGC API - Processes Part 2 specification and are subject to change.


