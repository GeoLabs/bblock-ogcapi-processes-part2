# OGC API - Processes - Part 2: Deploy, Replace, Undeploy

This API extends OGC API - Processes - Part 1: Core with dynamic process lifecycle management capabilities.

## Conformance Classes

This API supports the following conformance classes:

- **Deploy, Replace, Undeploy (DRU)**: Core process lifecycle management
- **OGC Application Package**: Standardized format for process deployment packages
- **Docker**: Container-based execution units using Docker/OCI images
- **CWL Encoding**: Support for Common Workflow Language as process description format

## Operations

### Deploy Process (POST /processes)

Deploy a new process to the server using an OGC Application Package. The deployed process becomes immediately available for execution.

### Replace Process (PUT /processes/{processId})

Replace an existing process with a new version. The process definition is updated atomically.

### Undeploy Process (DELETE /processes/{processId})

Remove a deployed process from the server. The process will no longer be available for new executions.

## Key Concepts

### OGC Application Package

The OGC Application Package (ogcapppkg) is a standardized format for describing deployable processes. It includes:

- **Process Description**: Metadata, inputs, and outputs definition
- **Execution Unit**: Container specification (Docker/OCI) with resource requirements or a CWL (by value encoded as a JSON object or by reference).

### Execution Units

Execution units specify how processes are executed using containerization:

- **Type**: `docker` or `oci`
- **Image**: Container image reference
- **Deployment**: Target environment (local, remote, HPC, cloud)
- **Config**: Resource requirements (CPU, memory, storage, timeout)

#### CWL as Execution Unit

An Execution Unit can also be a CWL document, provided either by reference (via `href`) or by value (inline):

- **By reference**: Use `href` pointing to a CWL file with `type: "application/cwl"`
  ```json
  {
    "executionUnit": {
      "href": "https://example.com/workflow.cwl",
      "type": "application/cwl"
    }
  }
  ```
  
- **By value**: Embed the CWL document directly with `value` (JSON object) and `mediaType: "application/cwl+json"`
  ```json
  {
    "executionUnit": {
      "value": { "cwlVersion": "v1.0", ... },
      "mediaType": "application/cwl+json"
    }
  }
  ```

When using CWL as the execution unit within an OGC Application Package:
- The `processDescription` property becomes **optional**, as CWL documents already contain all necessary metadata (inputs, outputs, documentation)
- If provided, `processDescription` can **override** specific process metadata defined in the CWL (e.g., custom title, description, or additional metadata)

### Process Mutability

Processes deployed via Part 2 are mutable by default, indicated by the `mutable: true` property in the process summary. This distinguishes them from static processes that cannot be modified through the API.

## CWL Support

The API supports Common Workflow Language (CWL) as an encoding format for process descriptions and execution units:

- **Content Types**: `application/cwl+yaml`,`application/cwl`
- **CWL Types**: Workflow (inside a `$graph`)
- **Benefits**: Workflow portability, rich composition, tool reusability

### Multi-Workflow CWL Documents

When deploying CWL documents containing multiple workflows (using the `$graph` pattern), you can specify which workflow to deploy using the `w` query parameter:

- **With `w` parameter**: Explicitly select a workflow by its identifier (e.g., `POST /processes?w=my-workflow`)
- **Without `w` parameter**: The first workflow in the `$graph` will be automatically selected
- **Process ID mapping**: A one-to-one relationship exists between the CWL workflow identifier and the resulting `processId`

This allows deploying multiple processes from a single CWL document by making multiple POST requests with different `w` parameter values.
