Summary description of a deployed process, returned in the body of a Deploy response (Requirement /req/deploy-replace-undeploy/deploy-response-body).

The migrated draft `processSummary` maps to the existing public
`ogc.api.processes.part2.v1.schemas.staticIndicator`; no duplicate summary schema is
introduced. Unlike the stripped local draft fragment, this block retains its
`allOf` reference to the full Part 1 `processSummary`, including validation of
`outputTransmission`, and the optional boolean `mutable` with `default: true`.

The schema itself is unchanged by consolidation. Tests and metadata are updated.
A JSON Schema default is an annotation, not an instruction to insert a missing
property. The added mutability contract is local DRU composition, not a claim
that the quoted draft summary fragment itself declares `mutable`.