# CWL Encoding for Process Deployment

This building block defines the **CWL encoding** for Deploy and Replace operations in OGC API - Processes - Part 2.

When using media types `application/cwl` or `application/cwl+yaml`, the **entire request body is a CWL document** - not an OGC Application Package wrapper.

## CWL Conformance Class

The CWL conformance class enables deploying processes using Common Workflow Language documents.

## Benefits

- **Native CWL** - Use CWL documents directly without wrapping
- **Tool Ecosystem** - Compatible with CWL tools and validators
- **Workflow Portability** - CWL is portable across platforms
- **Version Control** - CWL files can be versioned independently

## Real-World Example

The example for this building block uses a complete Earth Observation workflow from the Terradue hands-on tutorial:
[Water Bodies Detection Workflow](https://github.com/Terradue/ogc-eo-application-package-hands-on/releases/download/1.5.0/app-water-bodies-cloud-native.1.5.0.cwl) that is described [here](https://eoap.github.io/mastering-app-package/app/water-bodies-detection/).


