Value of the executionUnit property of an OGC Application Package: one execution unit, or an array of them.

The schema is the fragment quoted in the OGC 20-044 draft, with its references replaced by building block references.

Differences from the draft:

- `items` is a single schema here, not the one-element array written in the draft: the array form is not a valid schema in OpenAPI 3.0 or JSON Schema 2020-12.

## Canonical versus legacy contract

The draft's `executionUnit` schema is published here as
`ogc.api.processes.part2.v1.schemas.executionUnitValue`: this is the **property value**,
not the container payload itself. Each element uses `executionUnitBase`, including
the local composition fixes documented there.

The legacy flat contract, now `ogc.api.processes.part2.v1.schemas.executionUnit`, is deliberately
unchanged: it remains the legacy flat `{ "type": "docker", "image": "..." }`
contract. It must not be used as the canonical single-or-array schema.