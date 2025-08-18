<!-- BLOCK:FIXED:header -->
# DEVELOPMENT gRPC Communication Foundation
**Context ID:** MINIDEV_GRPC_001
**Priority:** HIGH
**Estimated Complexity:** MEDIUM
**Dependencies:** Go runtime, gRPC framework, Protocol Buffers
<!-- /BLOCK:FIXED:header -->

<!-- BLOCK:FIXED:executive_summary -->
## Executive Summary
**Objective:** Establish the fundamental communication backbone of the agentic system by creating a minimalist Orchestrator and LLM Gateway that can communicate via gRPC
**Expected Outcome:** Working gRPC communication between Orchestrator and LLM Gateway with defined service contracts
**Success Criteria:** Successful gRPC call from Orchestrator to LLM Gateway with proper request/response handling and passing integration tests
<!-- /BLOCK:FIXED:executive_summary -->

<!-- BLOCK:DYNAMIC:context -->
## Context
This is the foundation sprint (Cycle 1) for the MimersAgentic system as defined in "Iterativ Udviklingsplan for et AI-drevet Agentisk System.md". The goal is to establish basic inter-service communication using gRPC protocol between core components.
<!-- /BLOCK:DYNAMIC:context -->

<!-- BLOCK:FIXED:primary_task -->
## Task Definition
### Primary Task
**ID:** GRPC_FOUNDATION_001
**Type:** IMPLEMENTATION
**Description:** Create gRPC service contracts and implement basic Orchestrator-Gateway communication with proper testing
<!-- /BLOCK:FIXED:primary_task -->

<!-- BLOCK:STRUCTURED:subtasks -->
### Subtasks
<!-- SUBTASK:START -->
**name:** Define gRPC Service Contract
**action:** Create .proto file defining LLMGateway service contract
**input:** Service requirements and message structures
**output:** llm_gateway.proto with generated Go code
**validation:** Proto file compiles and generates valid Go client/server code
<!-- SUBTASK:END -->

<!-- SUBTASK:START -->
**name:** Implement LLM Gateway Service
**action:** Create gRPC server implementing LLMGateway service
**input:** Generated proto code and service interface
**output:** Functional gRPC server with Prompt method
**validation:** Server starts and responds to gRPC calls
<!-- SUBTASK:END -->

<!-- SUBTASK:START -->
**name:** Implement Orchestrator Client
**action:** Create gRPC client connecting to LLMGateway service
**input:** Generated proto code and client interface
**output:** Functional gRPC client with gateway communication
**validation:** Client successfully calls gateway and receives responses
<!-- SUBTASK:END -->

<!-- SUBTASK:START -->
**name:** End-to-End Integration Test
**action:** Create comprehensive test verifying Orchestrator-Gateway communication
**input:** Running services and test scenarios
**output:** Passing integration test suite
**validation:** All tests pass demonstrating successful communication
<!-- SUBTASK:END -->
<!-- /BLOCK:STRUCTURED:subtasks -->

<!-- BLOCK:DYNAMIC:technical_specs -->
## Technical Specifications
### Code Requirements
- **Language:** Go 1.19+
- **Framework:** gRPC-Go
- **Libraries:** google.golang.org/grpc, google.golang.org/protobuf
- **Patterns:** gRPC service architecture, client-server communication
### Quality Standards
- **Code Style:** Go standard formatting (gofmt)
- **Testing:** Integration tests for end-to-end communication
- **Documentation:** Proto file documentation and inline comments
- **Performance:** Low-latency gRPC communication
### Functional Requirements
1. **gRPC Service Contract**: LLMGateway service with Prompt RPC method
2. **Message Structures**: PromptRequest with text field, PromptResponse with text field
3. **Gateway Server**: Implements LLMGateway service on configurable port
4. **Orchestrator Client**: Connects to gateway and calls Prompt method
5. **Integration Test**: Verifies end-to-end communication flow
<!-- /BLOCK:DYNAMIC:technical_specs -->

<!-- BLOCK:DYNAMIC:implementation -->
## Implementation Plan
### Phase 1: Service Contract Definition
1. Create llm_gateway.proto file
2. Define LLMGateway service interface
3. Define PromptRequest and PromptResponse messages
4. Generate Go client and server code
### Phase 2: Service Implementation
1. Implement LLM Gateway gRPC server
2. Implement Prompt method with hardcoded response
3. Add configurable port listening
4. Implement Orchestrator gRPC client
5. Add gateway connection and communication functions
### Phase 3: Testing & Integration
1. Create integration test suite
2. Test server startup and client connection
3. Test end-to-end communication flow
4. Verify response handling and error cases
<!-- /BLOCK:DYNAMIC:implementation -->

<!-- BLOCK:DYNAMIC:validation -->
## Acceptance Criteria
- [ ] Proto file defines LLMGateway service with Prompt RPC method
- [ ] PromptRequest message contains text field (string)
- [ ] PromptResponse message contains text field (string)
- [ ] gRPC client and server code generated successfully for Go
- [ ] Gateway server implements LLMGateway service
- [ ] Prompt method returns hardcoded, non-empty string
- [ ] Server listens on configurable port
- [ ] Orchestrator client connects to LLMGateway service
- [ ] Client function takes string input, calls Prompt method, returns response
- [ ] Integration test starts gateway server (or connects to running instance)
- [ ] Test calls Orchestrator client function
- [ ] Test asserts response matches hardcoded gateway response
- [ ] All integration tests pass
<!-- /BLOCK:DYNAMIC:validation -->

<!-- BLOCK:STRUCTURED:deliverables -->
## Output Specification
### Deliverables
<!-- DELIVERABLE:START -->
**name:** gRPC Service Contract
**format:** Protocol Buffer definition
**location:** /gRPC/llm_gateway.proto
**content:** LLMGateway service definition with Prompt RPC method and message structures
<!-- DELIVERABLE:END -->
<!-- DELIVERABLE:START -->
**name:** LLM Gateway Service
**format:** Go source code
**location:** /gateway/main.go
**content:** gRPC server implementation with configurable port and hardcoded responses
<!-- DELIVERABLE:END -->
<!-- DELIVERABLE:START -->
**name:** Orchestrator Client
**format:** Go source code
**location:** /orchestrator/main.go
**content:** gRPC client implementation with gateway communication functions
<!-- DELIVERABLE:END -->
<!-- DELIVERABLE:START -->
**name:** Integration Test Suite
**format:** Go test code
**location:** /orchestrator/main_test.go
**content:** End-to-end tests verifying Orchestrator-Gateway communication
<!-- DELIVERABLE:END -->
<!-- /BLOCK:STRUCTURED:deliverables -->

<!-- BLOCK:DYNAMIC:notes -->
## Notes
- This is Cycle 1 of the iterative development plan
- Focus on establishing basic communication foundation
- Keep implementations minimal but functional
- Ensure proper error handling for network communication
- Follow gRPC best practices for service definition and implementation
<!-- /BLOCK:DYNAMIC:notes -->

<!-- BLOCK:FIXED:estimated_time -->
## Estimated Time
**Total:** 4-6 hours
- Proto definition and code generation: 1 hour
- Gateway service implementation: 1.5 hours
- Orchestrator client implementation: 1.5 hours
- Integration testing and debugging: 1-2 hours
<!-- /BLOCK:FIXED:estimated_time -->