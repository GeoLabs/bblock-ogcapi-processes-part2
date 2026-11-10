One execution unit: a link, or a qualified value holding a container image, a CWL document or a custom type.

The source is the schema fragment quoted in the OGC 20-044 draft, with its
references replaced by building block references. The descriptions of container,
CWL and custom script encodings retain the draft's intent.

## Local schema composition fixes (not amendments of the official draft)

- The draft refers to `../cwl/cwl.yaml`, which it does not include. This block uses the CWL v1.2 schema URL that the draft gives in a comment.
- The draft's third `anyOf` branch accepts any `type`, allowing invalid Docker
  values to bypass the container branch. Here an `if`/`then`/`else` discriminator
  gives `type: docker` or `type: oci` priority and validates `value` against
  `ogc.api.processes.part2.v1.schemas.executionUnitContainer`.
- Otherwise `mediaType: application/cwl` selects the raw remote CWL schema,
  including when `type` is absent. A custom type cannot bypass this check.
- The remaining custom branch requires a string `type` excluding `docker` and
  `oci`. Scripts such as `type: python` retain the qualified-value contract;
  an empty object is a valid custom payload.
- The Part 1 `qualifiedValue` `allOf` is retained; `value` is also explicitly
  required here. Link-only units exclude `value`, so a qualified value with an
  additional `href` cannot escape payload validation through the link branch.

These are local validation/composition fixes. They do not claim changes to the
official draft or runtime support for Docker/CWL deployment. Other draft
limitations, including the loose deployment enum, are documented on
`executionUnitContainer` rather than silently corrected.