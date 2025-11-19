# Workflow Identifier Parameter (`w`)

This query parameter is used when deploying CWL documents that contain multiple workflow definitions using the `$graph` construct.

## Purpose

When a CWL file defines multiple workflows, the `w` parameter specifies which workflow should be used as the entry point for the deployed process.

## Default Behavior

If the `w` parameter is not provided:
- The server may use the first workflow in the `$graph`
- Or return an error if the choice is ambiguous
- Server-specific behavior should be documented

## Example

Deploy a workflow from a multi-workflow CWL file:

```bash
curl -X POST "https://api.example.org/processes?w=water_bodies" \
  -H "Content-Type: application/cwl+yaml" \
  --data-binary @app-water-bodies.cwl
```
