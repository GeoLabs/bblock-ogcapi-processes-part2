# CWL Encoding for Process Deployment

This building block defines the **CWL encoding** for Deploy and Replace operations in OGC API - Processes - Part 2.

When using media types `application/cwl+json` or `application/cwl+yaml`, the **entire request body is a CWL document** - not an OGC Application Package wrapper.

## CWL Conformance Class

The CWL conformance class enables deploying processes using Common Workflow Language documents:

- **CWL Workflows** - Multi-step workflow compositions
- **CWL CommandLineTools** - Single command-line tool executions  
- **CWL ExpressionTools** - JavaScript expression evaluations

## Request Structure

### Content-Type Headers

Use one of these media types for CWL-encoded deployments:

- `application/cwl+yaml` - CWL in YAML format (recommended)
- `application/cwl+json` - CWL in JSON format

### Request Body

The body is **directly a CWL document**, for example:

```yaml
cwlVersion: v1.0
class: Workflow
id: water_bodies
label: Water bodies detection
inputs:
  aoi:
    type: string
    doc: Area of interest as bounding box
  stac_items:
    type: string[]
    doc: List of Sentinel-2 STAC items
outputs:
  stac_catalog:
    type: Directory
    doc: Output STAC catalog
steps:
  # workflow steps...
```

## Example: Deploy Request

```http
POST /processes HTTP/1.1
Host: api.example.org
Content-Type: application/cwl+yaml

cwlVersion: v1.0
class: Workflow
id: my-process
# ... complete CWL document
```

## Comparison with JSON Encoding

| Encoding | Content-Type | Request Body |
|----------|-------------|--------------|
| **JSON** (ogcapppkg) | `application/json` | OGC Application Package with `executionUnit` property |
| **CWL** (this) | `application/cwl+yaml` or `application/cwl+json` | Direct CWL document |

## Benefits

- **Native CWL** - Use CWL documents directly without wrapping
- **Tool Ecosystem** - Compatible with CWL tools and validators
- **Workflow Portability** - CWL is portable across platforms
- **Version Control** - CWL files can be versioned independently

## Real-World Example

The example for this building block uses a complete Earth Observation workflow from the Terradue hands-on tutorial:
[Water Bodies Detection Workflow](https://github.com/Terradue/ogc-eo-application-package-hands-on/releases/download/1.5.0/app-water-bodies-cloud-native.1.5.0.cwl)


