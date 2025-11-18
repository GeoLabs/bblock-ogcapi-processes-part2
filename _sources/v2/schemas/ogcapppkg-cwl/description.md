# OGC Application Package with CWL Support

This building block extends the OGC Application Package to support Common Workflow Language (CWL) as an encoding format for process descriptions and execution units.

## CWL Conformance Class

According to the OGC API - Processes - Part 2 specification, the CWL conformance class enables:

- Using CWL documents as process descriptions
- Deploying CWL workflows as executable processes
- Supporting CWL CommandLineTool, Workflow, and ExpressionTool types

## Usage

### Process Description with CWL

The `processDescription.process` property can reference or embed a CWL document:

- **CWL CommandLineTool**: Single command-line tool execution
- **CWL Workflow**: Multi-step workflow composition
- **CWL ExpressionTool**: JavaScript expression evaluation
- **OGC Process**: Standard OGC API - Processes description

### Execution Unit with CWL

The `executionUnit` can be specified using:

- **CWL Document**: Direct CWL CommandLineTool, Workflow, or ExpressionTool
- **Container Image**: Docker/OCI container reference (standard approach)
- **Link**: URL reference to external CWL or container
- **Qualified Value**: Inline value with additional metadata

## Benefits

- **Workflow Portability**: CWL workflows are portable across different execution platforms
- **Rich Composition**: Support for complex multi-step workflows with data flow
- **Tool Reusability**: CWL tools can be composed into larger workflows
- **Standard Compliance**: Aligns with established workflow standards in scientific computing

## Example

```yaml
processDescription:
  process:
    class: CommandLineTool
    baseCommand: echo
    inputs:
      message:
        type: string
        inputBinding:
          position: 1
    outputs:
      output:
        type: stdout
executionUnit:
  class: CommandLineTool
  baseCommand: echo
  requirements:
    DockerRequirement:
      dockerPull: alpine:latest
```
