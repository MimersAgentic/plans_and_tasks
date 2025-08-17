# Protocol Buffer Definitions for Development Cycles

This document defines the `proto3` schemas for managing development cycles within the MimerAgentic project. We define two primary structures:
1.  `MiniDev`: Represents a full development sprint, a collection of related tasks with a clear goal.
2.  `LooseTask`: Represents a single, standalone task that is not part of a larger sprint.

These definitions will serve as the foundation for our task and state management system.

---

## 1. MiniDev Sprint Definition

A `MiniDev` is a time-boxed collection of tasks aimed at achieving a larger goal. It is the primary unit of work for iterative development.

`::BEGREB`
**MiniDev (Sprint):** En samling af relaterede opgaver, der er grupperet under et fælles mål og en tidsramme. Svarer til et "sprint" i agile metoder.

### `minidev.proto`

```protobuf
syntax = "proto3";

package mimer_agentic.planning;

import "google/protobuf/timestamp.proto";
import "task.proto"; // Assuming LooseTask is defined in task.proto

// Enum for the overall status of the MiniDev sprint
enum MiniDevStatus {
  STATUS_UNSPECIFIED = 0;
  PLANNED = 1;
  ACTIVE = 2;
  COMPLETED = 3;
  ARCHIVED = 4;
}

// Represents a full development sprint
message MiniDev {
  string sprint_id = 1;         // Unique identifier for the sprint (e.g., "sprint_2024_w34")
  string sprint_goal = 2;       // The primary objective of this sprint
  MiniDevStatus status = 3;     // The current status of the sprint
  
  repeated LooseTask tasks = 4; // The list of tasks included in this sprint
  
  google.protobuf.Timestamp start_date = 5; // Planned start date
  google.protobuf.Timestamp end_date = 6;   // Planned end date
  
  repeated string linked_documents = 7; // Paths or URLs to relevant design docs, etc.
}
```

---

## 2. Loose Task Definition

A `LooseTask` is a granular, standalone unit of work. It can exist independently or as part of a `MiniDev` sprint.

`::BEGREB`
**LooseTask:** En enkeltstående, atomisk opgave, der kan udføres uafhængigt.

### `task.proto`

```protobuf
syntax = "proto3";

package mimer_agentic.planning;

import "google/protobuf/timestamp.proto";

// Enum for the status of a single task
enum TaskStatus {
  STATUS_UNSPECIFIED = 0;
  PENDING = 1;
  IN_PROGRESS = 2;
  COMPLETED = 3;
  BLOCKED = 4;
}

// Represents a single, standalone task
message LooseTask {
  string task_id = 1;           // Unique identifier for the task
  string title = 2;             // A short, descriptive title
  string description = 3;       // A more detailed explanation of what needs to be done
  TaskStatus status = 4;        // The current status of the task
  
  string assignee_id = 5;       // ID of the agent or user responsible
  
  repeated string dependency_task_ids = 6; // List of task_ids this task depends on
  
  google.protobuf.Timestamp created_at = 7;
  google.protobuf.Timestamp last_updated = 8;
}
```