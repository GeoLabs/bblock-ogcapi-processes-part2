# OGC API - Processes - Part 2: Deploy, Replace, Undeploy

This API extends OGC API - Processes - Part 1: Core with dynamic process lifecycle management capabilities.

## Conformance Classes

This API supports the following conformance classes:

- **Deploy, Replace, Undeploy (DRU)**: Core process lifecycle management
- **CWL Encoding**: Support for Common Workflow Language as process description format

## Operations

### Deploy Process (POST /processes)

Deploy a new process to the server using an OGC Application Package. The deployed process becomes immediately available for execution.

**Request Body**: OGC Application Package (ogcapppkg)

**Response**: Process summary with deployment confirmation

### Replace Process (PUT /processes/{processId})

Replace an existing process with a new version. The process definition is updated atomically.

**Path Parameter**: `processId` - Identifier of the process to replace

**Request Body**: OGC Application Package (ogcapppkg)

**Response**: Updated process summary

### Undeploy Process (DELETE /processes/{processId})

Remove a deployed process from the server. The process will no longer be available for new executions.

**Path Parameter**: `processId` - Identifier of the process to undeploy

**Response**: Confirmation of process removal

## Key Concepts

### OGC Application Package

The OGC Application Package (ogcapppkg) is a standardized format for describing deployable processes. It includes:

- **Process Description**: Metadata, inputs, and outputs definition
- **Execution Unit**: Container specification (Docker/OCI) with resource requirements
- **Configuration**: Runtime parameters and constraints

### Execution Units

Execution units specify how processes are executed using containerization:

- **Type**: `docker` or `oci`
- **Image**: Container image reference
- **Deployment**: Target environment (local, remote, HPC, cloud)
- **Config**: Resource requirements (CPU, memory, storage, timeout)

### Process Mutability

Processes deployed via Part 2 are mutable by default, indicated by the `mutable: true` property in the process summary. This distinguishes them from static processes that cannot be modified through the API.

## CWL Support

The API supports Common Workflow Language (CWL) as an alternative encoding format for process descriptions and execution units:

- **Content Types**: `application/cwl+json`, `application/cwl+yaml`
- **CWL Types**: CommandLineTool, Workflow, ExpressionTool
- **Benefits**: Workflow portability, rich composition, tool reusability

When deploying with CWL encoding, the `processDescription.process` and `executionUnit` can be CWL documents, enabling seamless integration with existing CWL-based workflow systems.
