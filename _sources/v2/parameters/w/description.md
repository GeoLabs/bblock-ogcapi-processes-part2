# Workflow Identifier Parameter (`w`)

This query parameter is used when deploying CWL documents that contain multiple workflow definitions using the `$graph` construct.

## Purpose

When a CWL file defines multiple workflows, the `w` parameter specifies which workflow should be used as the entry point for the deployed process.

## Usage

### Deploy Request with Multiple Workflows

```http
POST /processes?w=main_workflow HTTP/1.1
Host: api.example.org
Content-Type: application/cwl+yaml

cwlVersion: v1.0
$graph:
  - class: Workflow
    id: main_workflow
    # ... main workflow definition
  
  - class: Workflow
    id: alternative_workflow
    # ... alternative workflow definition
```

In this example, `w=main_workflow` tells the server to use the workflow with `id: main_workflow` as the process definition.

## CWL $graph Pattern

The `$graph` pattern in CWL allows packaging multiple related workflows and tools in a single document:

```yaml
cwlVersion: v1.0
$graph:
  - class: CommandLineTool
    id: tool1
    # ...
  
  - class: CommandLineTool
    id: tool2
    # ...
  
  - class: Workflow
    id: main
    steps:
      step1:
        run: "#tool1"
      step2:
        run: "#tool2"
```

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
