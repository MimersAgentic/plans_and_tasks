<!-- BLOCK:REQUIRED:FIXED:header -->
# [TASK_TYPE] [TITLE] <!-- OPTIONAL -->
**context_id:** [ID]
**priority:** [HIGH|MEDIUM|LOW]
**complexity:** [SIMPLE|MODERATE|COMPLEX]
**dependencies:** [LIST]
<!-- /BLOCK:REQUIRED:FIXED:header -->

<!-- BLOCK:REQUIRED:FIXED:executive_summary -->
## Executive Summary <!-- OPTIONAL -->
**objective:** [TEXT]
**expected_outcome:** [TEXT]
**success_criteria:** [TEXT]
<!-- /BLOCK:REQUIRED:FIXED:executive_summary -->

<!-- BLOCK:OPTIONAL:DYNAMIC:context -->
## Context <!-- OPTIONAL -->
[FREE-FORM CONTENT - Parser extracts what it can]
<!-- /BLOCK:OPTIONAL:DYNAMIC:context -->

<!-- BLOCK:REQUIRED:FIXED:primary_task -->
### Primary Task <!-- OPTIONAL -->
**id:** [TASK_ID]
**type:** [TYPE]
**description:** [TEXT]
<!-- /BLOCK:REQUIRED:FIXED:primary_task -->

<!-- BLOCK:OPTIONAL:STRUCTURED:subtasks -->
### Subtasks <!-- OPTIONAL -->
<!-- ITEM:subtask -->
**name:** [NAME]
**action:** [TEXT]
**input:** [TEXT]
**output:** [TEXT]
**validation:** [TEXT]
<!-- /ITEM:subtask -->
<!-- /BLOCK:OPTIONAL:STRUCTURED:subtasks -->

<!-- BLOCK:OPTIONAL:DYNAMIC:technical_specs -->
## Technical Specifications <!-- OPTIONAL -->
[FREE-FORM CONTENT - Parser extracts what it can]
<!-- /BLOCK:OPTIONAL:DYNAMIC:technical_specs -->

<!-- BLOCK:OPTIONAL:DYNAMIC:implementation_guidance -->
## Implementation Guidance <!-- OPTIONAL -->
[FREE-FORM CONTENT]
<!-- /BLOCK:OPTIONAL:DYNAMIC:implementation_guidance -->

<!-- BLOCK:OPTIONAL:DYNAMIC:validation_and_testing -->
## Validation and Testing <!-- OPTIONAL -->
[FREE-FORM CONTENT]
<!-- /BLOCK:OPTIONAL:DYNAMIC:validation_and_testing -->

<!-- BLOCK:OPTIONAL:DYNAMIC:resources_and_references -->
## Resources and References <!-- OPTIONAL -->
[FREE-FORM CONTENT]
<!-- /BLOCK:OPTIONAL:DYNAMIC:resources_and_references -->

<!-- BLOCK:REQUIRED:STRUCTURED:output_specification -->
## Output Specification <!-- OPTIONAL -->

<!-- BLOCK:OPTIONAL:STRUCTURED:deliverables -->
### Deliverables <!-- OPTIONAL -->
<!-- ITEM:deliverable -->
**name:** [NAME]
**format:** [FORMAT]
**location:** [PATH]
**content:** [DESCRIPTION]
<!-- /ITEM:deliverable -->
<!-- /BLOCK:OPTIONAL:STRUCTURED:deliverables -->

<!-- /BLOCK:REQUIRED:STRUCTURED:output_specification -->