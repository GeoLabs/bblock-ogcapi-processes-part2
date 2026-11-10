Value of the value field of a Docker execution unit (Requirement /req/docker/schema).

The schema is the fragment quoted in the OGC 20-044 draft, with its references replaced by building block references.

Differences from the draft:

- `required` is a list here. The draft writes `required: image`, which is not a valid schema.

## Draft limitations retained

The draft's `deployment` combines an unrestricted string branch with an enum,
so strings outside `local`, `remote`, `hpc`, and `cloud` remain valid. This is
not silently tightened here. Likewise, the binding maps retain the draft's
`additionalProperties` formulation without adding a missing `type: object`.
Binding objects are checked against the canonical `inputBinding` and
`outputBinding` schemas. The draft example's `inputSeparator` is preserved as an
extension; the declared input binding property is `itemSeparator`.

The local discriminator fix belongs to `executionUnitBase`, not to an amendment
of this draft fragment or a claim that the Docker conformance class is implemented.