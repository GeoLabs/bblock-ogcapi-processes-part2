Schema of an OGC Application Package document (Requirement /req/ogcapppkg/schema).

The source is the fragment quoted in the OGC 20-044 draft, with its references
replaced by building block references.

The `docker-example` test is the example from the draft with a top-level `title` added.
The local JSON-LD context preserves `executionUnit` and `processDescription` as
opaque JSON literals, including links, arrays and custom executable documents.
Their contents are validated by JSON Schema, not interpreted as RDF classes.

## Local compatibility and composition

The draft `executionUnit` reference maps to
`ogc.api.processes.part2.v1.schemas.executionUnitValue`, the canonical single-or-array
property-value contract. An `anyOf` additionally accepts the existing public
`ogc.api.processes.part2.v1.schemas.executionUnit` legacy flat container contract.
Only this package's legacy branch excludes `value`; the global legacy schema
is unchanged. Thus an invalid qualified Docker payload cannot escape validation
by also carrying a top-level `image`.

The former direct Part 1 `link` and `qualifiedValue` alternatives are removed:
links and custom qualified values remain supported through `executionUnitBase`,
with Docker/CWL payload validation enforced there. An untyped qualified value
is not an execution unit.

When present, `processDescription.process` composes Part 1 `process` with
`staticIndicator` to retain the full process structure and validate the optional
DRU `mutable` flag. These compatibility/composition rules are local fixes, not
an amendment of the official draft. Draft limitations in the container and
binding schemas remain documented on those blocks.