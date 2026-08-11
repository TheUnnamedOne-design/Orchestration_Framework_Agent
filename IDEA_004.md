# Project Memory

## AI-Powered Engineering Intelligence & Institutional Memory Platform

> **Tagline:** Understand what the code does. Remember why it exists.

------------------------------------------------------------------------

## 1. Project Overview

**Project Memory** is an AI-powered platform that creates a continuously
evolving memory of a software project.

A software project contains much more knowledge than the current source
code. Its real history is distributed across source files, Git commits,
pull requests, issues, discussions, architecture documents, database
schemas, API specifications, tests, deployments, incidents, technical
decisions, experiments, and the people who worked on it.

Project Memory brings this information together and builds a unified
understanding of the project.

Developers can connect an existing GitHub repository and ask questions
such as:

-   What does this project do?
-   How is the system architected?
-   What does this service do?
-   Why does this function exist?
-   Why are we using PostgreSQL instead of MongoDB?
-   Who introduced this workaround?
-   What changed in this module over the last six months?
-   What happened when we previously tried this approach?
-   What services depend on this API?
-   What will break if I change this database table?
-   What files and tests need to change for this feature?

The system answers these questions using the project's actual code,
history, documentation, relationships, and decisions rather than relying
only on the LLM's general knowledge.

The second major purpose of Project Memory is to provide
**project-specific context to AI coding agents**. When a developer wants
to change the system, Project Memory can analyze the requirement,
identify affected components, retrieve historical constraints and
decisions, generate an implementation plan, and package the relevant
context for a coding agent. After the coding agent makes the changes,
Project Memory can analyze the changes, verify consistency, update
documentation, and record the new knowledge.

The long-term goal is to become the **institutional memory and
intelligence layer for software projects**.

------------------------------------------------------------------------

# 2. The Core Problem

Software projects suffer from a recurring problem:

> **The code survives longer than the people who remember why the code
> exists.**

A project may begin with:

``` text
Developer
    ↓
Code
    ↓
Documentation
```

After several years, the knowledge becomes fragmented:

``` text
                         PROJECT
                            |
        +-------------------+-------------------+
        |                   |                   |
       Code               GitHub              Docs
        |                   |                   |
   Modules              Commits              ADRs
   Services             PRs                   Wiki
   APIs                 Issues                README
   Database             Reviews               Specs
   Tests                Discussions           Notes
        |                   |
        +-------------------+
                |
          Human Knowledge
                |
       +--------+---------+
       |        |         |
   Decisions  Failures  Context
```

Important knowledge becomes difficult to recover.

For example, a developer might find:

``` javascript
if (retryCount < 3) {
    retry();
}
```

The code tells them **what** happens.

It may not tell them:

-   Why three retries?
-   Why retry at this layer?
-   Was another approach tried?
-   Did the team experience a production incident?
-   Which external service caused the problem?
-   Why isn't the retry implemented in the client?
-   Which other components depend on this behavior?

That context may exist in:

``` text
PR #142
    ↓
Issue #87
    ↓
Old architecture discussion
    ↓
Commit history
    ↓
Incident report
```

Project Memory reconstructs this context.

------------------------------------------------------------------------

# 3. Core Product Philosophy

Project Memory is based on three questions:

## What?

> What does the system currently do?

This comes from:

-   Source code
-   APIs
-   Database schemas
-   Infrastructure
-   Tests
-   Dependencies
-   Architecture

## Why?

> Why was the system designed and implemented this way?

This comes from:

-   Git history
-   Pull requests
-   Issues
-   Architecture decisions
-   Discussions
-   Experiments
-   Incidents
-   Documentation

## What Next?

> What will happen if we change something, and how should we make the
> change?

This comes from:

-   Dependency relationships
-   Code analysis
-   Architecture
-   Historical constraints
-   Tests
-   APIs
-   Database relationships
-   Previous decisions

Therefore:

``` text
                    PROJECT MEMORY
                           |
             +-------------+-------------+
             |             |             |
            WHAT          WHY         WHAT NEXT
             |             |             |
           Current      Historical    Change
            State        Context      Intelligence
             |             |             |
             +-------------+-------------+
                           |
                      Project Brain
```

------------------------------------------------------------------------

# 4. What Makes This Different From a Code Chatbot?

A normal code chatbot generally follows:

``` text
User
  ↓
Question
  ↓
LLM
  ↓
Answer
```

Project Memory follows:

``` text
User
  ↓
Question
  ↓
Understand intent
  ↓
Identify project entities
  ↓
Search current code
  ↓
Search project history
  ↓
Traverse relationships
  ↓
Retrieve documentation
  ↓
Retrieve decisions
  ↓
Combine evidence
  ↓
LLM reasoning
  ↓
Evidence-backed answer
```

The important difference is **project context**.

The system should not merely know what a piece of code means according
to generic programming knowledge.

It should know:

> What this code means **inside this specific project**.

------------------------------------------------------------------------

# 5. Primary Users

The platform can serve:

### Individual Developers

Useful when returning to old projects.

### New Team Members

Useful for onboarding and understanding an unfamiliar codebase.

### Senior Engineers

Useful for architecture analysis and change impact.

### Engineering Managers

Useful for understanding project evolution and technical debt.

### AI Coding Agents

Useful as a context and knowledge provider.

### Large Engineering Teams

Useful for preserving institutional knowledge across employee turnover.

------------------------------------------------------------------------

# 6. Initial User Experience

The first MVP should be extremely simple.

## Step 1: Sign Up

The user creates an account.

## Step 2: Connect GitHub

The user authorizes GitHub access.

## Step 3: Select Repository

Example:

``` text
my-company/backend-platform
```

## Step 4: Index Project

The system analyzes:

``` text
Source code
Git history
Pull requests
Issues
Documentation
Dependencies
```

## Step 5: Project Dashboard

The user sees:

``` text
Project Memory

Overview
Architecture
Codebase
Decisions
Experiments
Timeline
Dependencies
APIs
Database
Project Chat
Change Analysis
Agent Context
```

## Step 6: Chat

The user can immediately ask questions about the project.

------------------------------------------------------------------------

# 7. Repository Ingestion Pipeline

When a repository is connected:

``` text
GitHub
  ↓
Repository Fetch
  ↓
Repository Scanner
  ↓
Language Detection
  ↓
AST Parsing
  ↓
Symbol Extraction
  ↓
Dependency Analysis
  ↓
API Detection
  ↓
Database Detection
  ↓
Test Detection
  ↓
Configuration Detection
  ↓
Git History Analysis
  ↓
PR / Issue Ingestion
  ↓
Knowledge Extraction
  ↓
Project Knowledge Store
```

The system should not simply split source code into arbitrary chunks.

It should understand programming structures.

For example:

``` text
Repository
    ↓
src/
    ↓
services/
    ↓
OrderService
    ↓
createOrder()
    ↓
publishOrderCreated()
```

This allows retrieval at the level of actual software entities.

------------------------------------------------------------------------

# 8. Code Understanding

The platform should progressively understand:

### Files

``` text
src/order/order.service.ts
```

### Symbols

``` text
OrderService
createOrder()
cancelOrder()
```

### Dependencies

``` text
OrderService
    ↓
OrderRepository
    ↓
PostgreSQL
```

### APIs

``` text
POST /orders
GET /orders/:id
```

### Events

``` text
ORDER_CREATED
ORDER_CANCELLED
```

### Database

``` text
orders
order_items
users
payments
```

### Tests

``` text
order.service.test.ts
order.integration.test.ts
```

------------------------------------------------------------------------

# 9. AST and Static Analysis

The platform should eventually use AST-based parsing instead of relying
exclusively on LLMs.

AST analysis can identify:

-   Functions
-   Classes
-   Interfaces
-   Imports
-   Exports
-   Function calls
-   Routes
-   Database queries
-   Types
-   Dependencies

For example:

``` text
OrderController
      |
      | calls
      v
OrderService
      |
      | calls
      v
OrderRepository
      |
      | queries
      v
PostgreSQL
```

This structured information becomes part of the project graph.

------------------------------------------------------------------------

# 10. Git Intelligence

Git history is one of the most valuable sources of project memory.

The system should analyze:

``` text
Commits
Branches
Merges
Pull Requests
Issues
Reviews
Discussions
```

For a code entity:

``` text
Function
  ↓
Introduced by commit
  ↓
Commit belongs to PR
  ↓
PR relates to issue
  ↓
Issue contains discussion
```

This creates historical relationships.

The system can answer:

-   Who introduced this?
-   When was it introduced?
-   Why was it introduced?
-   Which issue motivated it?
-   What changed before and after it?
-   Which PR modified it?
-   Has this code caused problems before?

------------------------------------------------------------------------

# 11. Codebase Chat

The chat interface is one of the primary product surfaces.

Example:

### User

> What does the Order Service do?

### Project Memory

> The Order Service manages order creation, validation, state
> transitions, and persistence. It writes orders to PostgreSQL and
> publishes `ORDER_CREATED` after successful persistence.

Then:

### User

> Why does it publish `ORDER_CREATED`?

The system searches:

``` text
OrderService
    ↓
Event publisher
    ↓
ORDER_CREATED
    ↓
Consumers
    ↓
Git history
    ↓
PR discussion
```

It might answer:

> `ORDER_CREATED` was introduced when the notification system was
> separated from the Order Service. The event allows downstream services
> to react without coupling notification logic to order creation. The
> change was introduced in PR #142.

The response should provide evidence.

------------------------------------------------------------------------

# 12. Evidence-Based Answers

One of the most important product requirements is:

> **The AI must distinguish evidence from inference.**

Instead of:

> "This probably exists because..."

The system should produce:

``` text
Answer

...

Evidence

File:
src/order/order.service.ts

Commit:
abc123

Pull Request:
#142

Issue:
#87
```

The user should be able to click the evidence and inspect the original
source.

This makes the system much more trustworthy.

------------------------------------------------------------------------

# 13. Historical Decision Memory

A major feature is extracting and storing engineering decisions.

Example:

``` text
Decision:
Use PostgreSQL

Alternatives:
MongoDB

Reason:
The payment workflow requires strong transactional consistency.

Date:
March 2026

Evidence:
ADR-003
PR #17
Architecture discussion
```

Later, a developer asks:

> Why PostgreSQL?

The system retrieves the original reasoning.

------------------------------------------------------------------------

# 14. Failed Approaches and Experiments

Project Memory should remember things that **did not work**.

For example:

``` text
Experiment:
Redis Pub/Sub for notification delivery

Goal:
Build real-time notification infrastructure

Result:
Rejected

Problem:
Messages could be lost when consumers disconnected.

Alternative:
Redis Streams

Final result:
Redis Streams adopted.
```

Years later:

> Can we use Redis Pub/Sub for this?

The system can answer:

> We previously evaluated Redis Pub/Sub for notification delivery and
> rejected it because message recovery was required when consumers
> disconnected. Redis Streams was selected instead.

This is a major part of **institutional memory**.

------------------------------------------------------------------------

# 15. Architecture Evolution

The platform should understand how the system changed over time.

### Architecture V1

``` text
Frontend
    ↓
Backend
    ↓
PostgreSQL
```

### Architecture V2

``` text
Frontend
    ↓
API
    ↓
Backend
  ├── User
  └── Order
```

### Architecture V3

``` text
Frontend
    ↓
Gateway
    ↓
Services
  ├── User
  ├── Order
  ├── Payment
  └── Notification
           ↓
         Kafka
```

The user can ask:

> Why did we move from V2 to V3?

The platform reconstructs the answer from historical evidence.

------------------------------------------------------------------------

# 16. Project Timeline

The system can create a visual timeline:

``` text
2026

Jan
│
├── Project created
│
├── PostgreSQL selected
│
├── Authentication implemented
│
├── Redis introduced
│
├── Payment service created
│
├── Kafka experiment
│
├── Kafka rejected
│
└── Notification architecture changed
```

Clicking an event should reveal:

``` text
What changed?
Why?
Who made the change?
Which files?
Which PR?
Which issue?
What decision resulted?
What was the outcome?
```

------------------------------------------------------------------------

# 17. Knowledge Graph

The platform should eventually represent the project as a graph.

### Entities

``` text
Project
Repository
Service
Module
Function
Class
API
Database
Table
Event
Commit
Pull Request
Issue
Decision
Experiment
Requirement
Test
Deployment
Incident
Developer
Document
```

### Relationships

``` text
CALLS
DEPENDS_ON
INTRODUCED_BY
MODIFIED_BY
TESTED_BY
PUBLISHES
CONSUMES
IMPLEMENTS
AFFECTS
CAUSED
REPLACED
REJECTED
DOCUMENTED_BY
RELATED_TO
```

Example:

``` text
Decision
   |
   | caused
   v
Architecture Change
   |
   | affected
   v
Order Service
   |
   | publishes
   v
ORDER_CREATED
   |
   | consumed by
   v
Notification Service
```

This allows complex project questions to be answered using graph
traversal.

------------------------------------------------------------------------

# 18. Hybrid Retrieval Architecture

The system should not rely on a single RAG mechanism.

A strong architecture combines:

## Relational Database

For structured information:

``` text
Projects
Repositories
Commits
PRs
Issues
Decisions
Experiments
Users
```

## Vector Database

For semantic retrieval:

``` text
Code
Documentation
PR discussions
Commit descriptions
Issues
Decision records
```

## Knowledge Graph

For relationships:

``` text
Service → calls → Repository
Service → publishes → Event
Commit → modifies → Function
PR → implements → Issue
Decision → affects → Architecture
```

The retrieval system combines all three.

``` text
                   USER QUESTION
                         |
             +-----------+-----------+
             |                       |
       Semantic Search          Graph Search
             |                       |
        Vector DB                Graph DB
             |                       |
             +-----------+-----------+
                         |
                  Structured Search
                         |
                   Re-ranking
                         |
                   Evidence Set
                         |
                        LLM
                         |
                Answer + Citations
```

------------------------------------------------------------------------

# 19. Why Simple RAG Is Not Enough

Suppose the user asks:

> Why does this function exist?

Vector search might retrieve:

``` text
Function description
Related code
Documentation
```

But the real answer might be:

``` text
Function
 ↓
Git blame
 ↓
Commit
 ↓
PR
 ↓
Issue
 ↓
Discussion
```

This is fundamentally a **relationship and historical reasoning
problem**.

Therefore Project Memory combines:

``` text
Semantic Retrieval
+
Structured Queries
+
Graph Traversal
+
Git Analysis
+
LLM Reasoning
```

------------------------------------------------------------------------

# 20. Change Impact Analysis

The second major product capability is understanding proposed changes.

The developer says:

> I want to add email notifications when an order is completed.

The system analyzes:

``` text
Requirement
    ↓
Current Architecture
    ↓
Relevant Services
    ↓
Existing Events
    ↓
Database
    ↓
APIs
    ↓
Tests
    ↓
Documentation
    ↓
Historical Decisions
```

It might produce:

### Affected Components

``` text
OrderService
NotificationService
EventPublisher
EmailService
```

### Existing Infrastructure

``` text
ORDER_COMPLETED event already exists.
```

### Database

``` text
notification_preferences
notification_logs
```

### Tests

``` text
Order integration tests
Notification tests
Email integration tests
```

### Historical Constraints

``` text
Existing architecture decision requires
asynchronous notification processing.
```

------------------------------------------------------------------------

# 21. Implementation Plan Generation

The platform can then create:

``` text
Implementation Plan

1. Extend ORDER_COMPLETED event.
2. Add email notification consumer.
3. Reuse existing notification queue.
4. Add notification preference check.
5. Add email delivery service integration.
6. Add integration tests.
7. Update API and architecture documentation.
```

The plan is grounded in the existing project.

------------------------------------------------------------------------

# 22. Agent Context Generation

The implementation plan can be transformed into an **agent context
package**.

Example:

``` text
TASK

Add email notifications after successful order completion.

CURRENT ARCHITECTURE

OrderService publishes ORDER_COMPLETED.
NotificationService consumes domain events.

RELEVANT FILES

src/order/order.service.ts
src/events/order-completed.ts
src/notification/
src/email/

HISTORICAL DECISIONS

ADR-17:
Notifications must be asynchronous.

CONSTRAINTS

Do not introduce another queue.

EXISTING PATTERNS

Use existing event consumer architecture.

TESTS

order.integration.test.ts
notification.integration.test.ts
```

This can be provided to a coding agent.

------------------------------------------------------------------------

# 23. Integration With Coding Agents

Project Memory should not necessarily compete with coding agents.

Instead, it can provide them with project-specific intelligence.

``` text
                    PROJECT MEMORY
                          |
                    Change Analysis
                          |
                    Implementation Plan
                          |
                    Context Package
                          |
          +---------------+---------------+
          |               |               |
      Coding Agent    Coding Agent    Coding Agent
          |               |               |
       Codex          Claude Code       Cursor
```

The coding agent performs the actual implementation.

Project Memory provides the **memory and context**.

------------------------------------------------------------------------

# 24. Post-Change Verification

After an agent changes the code:

``` text
Code Change
    ↓
Project Memory
    ↓
Impact Analysis
    ↓
Run Tests
    ↓
Architecture Validation
    ↓
Documentation Validation
    ↓
Memory Update
```

The platform can detect things such as:

-   A new API was added but not documented.
-   A database field changed but migration documentation was not
    updated.
-   A change violates a recorded architecture decision.
-   Tests covering affected behavior were not updated.
-   A dependency relationship changed.
-   A previously documented architecture diagram is now stale.

------------------------------------------------------------------------

# 25. Continuous Memory Updating

The project memory must be a living system.

GitHub webhooks can notify the platform about:

``` text
Commit pushed
Pull request opened
Pull request updated
Pull request merged
Issue created
Issue closed
Release published
```

The pipeline becomes:

``` text
GitHub Event
    ↓
Webhook
    ↓
Event Processor
    ↓
Change Analysis
    ↓
Knowledge Extraction
    ↓
Graph Update
    ↓
Vector Update
    ↓
Project Summary Update
```

The result is:

``` text
Existing Project Memory
        +
New Project Event
        ↓
Updated Project Memory
```

------------------------------------------------------------------------

# 26. Living Documentation

Project Memory can eventually maintain:

``` text
Architecture Documentation
API Documentation
Database Documentation
Module Documentation
Decision Records
Project Timeline
Dependency Documentation
```

The platform compares documentation with the actual code.

Example:

> API documentation describes `POST /orders` as returning `Order`, but
> the current implementation returns `OrderResponse`.

The platform can flag:

``` text
Documentation Drift Detected
```

------------------------------------------------------------------------

# 27. Project Digital Twin

The long-term version becomes a digital representation of the project.

``` text
Requirements
      ↕
Decisions
      ↕
Architecture
      ↕
Code
      ↕
Database
      ↕
APIs
      ↕
Tests
      ↕
Infrastructure
      ↕
History
```

Every layer is connected.

This enables sophisticated reasoning.

Example:

> What happens if we replace PostgreSQL with MongoDB?

The system can analyze:

``` text
Database models
Queries
Transactions
Services
APIs
Tests
Reports
Infrastructure
Architecture decisions
```

and identify risks.

------------------------------------------------------------------------

# 28. Example End-to-End Scenario

Imagine a company has a five-year-old e-commerce project.

A new developer joins.

They see:

``` text
PaymentService
```

They ask:

> Why does this service use an idempotency key?

Project Memory finds:

``` text
Current code
    ↓
Git blame
    ↓
Commit
    ↓
PR
    ↓
Incident
```

It answers:

> Idempotency was introduced after duplicate payment callbacks caused
> duplicate order creation in production. The original incident was
> tracked in INC-217. PR #481 introduced the current implementation. The
> idempotency key is stored in the payment transaction table and is
> checked before processing callbacks.

The developer then asks:

> Can we remove it?

The system responds:

> Not safely. Payment callbacks are still processed asynchronously and
> the provider can retry delivery. Removing the mechanism would
> reintroduce the failure mode addressed by INC-217.

That is the experience we want.

------------------------------------------------------------------------

# 29. Another End-to-End Scenario: Adding a Feature

Developer:

> I want to add email notifications when an order is completed.

Project Memory:

``` text
Requirement
    ↓
Understand current system
    ↓
Find ORDER_COMPLETED
    ↓
Find consumers
    ↓
Find notification infrastructure
    ↓
Find email infrastructure
    ↓
Find related decisions
    ↓
Find tests
```

It produces:

``` text
Affected Components:
- OrderService
- EventPublisher
- NotificationService
- EmailService

Existing Event:
ORDER_COMPLETED

Existing Queue:
notification-events

Relevant Decision:
ADR-17 requires asynchronous notifications.

Potential Files:
...

Tests:
...
```

Then:

> Generate implementation context.

Project Memory creates the context package and sends it to the coding
agent.

The coding agent changes the repository.

Project Memory then:

``` text
Analyzes diff
    ↓
Runs/reads tests
    ↓
Checks affected architecture
    ↓
Updates project knowledge
    ↓
Records new decision/change
```

------------------------------------------------------------------------

# 30. MVP Definition

The first MVP should **not** attempt to understand every possible
programming language or every engineering system.

The MVP should be:

# GitHub Project Memory

### Inputs

``` text
GitHub Repository
Commits
Pull Requests
Issues
README / Docs
```

### Processing

``` text
Repository indexing
Code parsing
Git analysis
Semantic chunking
Embeddings
Basic project graph
```

### Interface

``` text
Project dashboard
Code explorer
Chat
Timeline
Evidence viewer
```

### Questions

``` text
What does this project do?
Explain this file.
Explain this service.
Why does this function exist?
Who introduced this?
What changed recently?
What depends on this?
Why was this architecture chosen?
```

### Output

Evidence-backed answers with links to:

``` text
Code
Commit
PR
Issue
Documentation
```

This is already a real and useful product.

------------------------------------------------------------------------

# 31. Development Roadmap

## Phase 1 --- Repository Intelligence

Build:

``` text
GitHub OAuth
Repository cloning
File indexing
Code parsing
Basic search
LLM chat
```

Goal:

> Chat with a repository.

------------------------------------------------------------------------

## Phase 2 --- Semantic Retrieval

Add:

``` text
Embeddings
Vector database
Semantic search
Hybrid retrieval
Chunking strategies
Re-ranking
```

Goal:

> Find relevant project knowledge accurately.

------------------------------------------------------------------------

## Phase 3 --- Git History

Add:

``` text
Commits
Blame
Branches
PRs
Issues
```

Goal:

> Answer historical questions.

------------------------------------------------------------------------

## Phase 4 --- Project Graph

Add:

``` text
Code entities
Dependencies
Calls
APIs
Events
Database relationships
Git relationships
```

Goal:

> Understand relationships within the project.

------------------------------------------------------------------------

## Phase 5 --- Decision & Experiment Memory

Extract:

``` text
Decisions
Alternatives
Reasons
Constraints
Experiments
Failures
Results
```

Goal:

> Answer "why?" questions.

------------------------------------------------------------------------

## Phase 6 --- Architecture Intelligence

Generate:

``` text
Architecture diagrams
Service maps
Dependency graphs
Database diagrams
API maps
```

Goal:

> Visualize the system.

------------------------------------------------------------------------

## Phase 7 --- Change Impact Analysis

Input:

``` text
Feature request
```

Output:

``` text
Affected files
Affected services
Affected database
Affected APIs
Affected tests
Risks
Historical constraints
Implementation plan
```

Goal:

> Understand changes before implementing them.

------------------------------------------------------------------------

## Phase 8 --- Coding Agent Integration

Add:

``` text
Agent context generation
MCP
Coding agent integration
Patch/PR workflows
```

Goal:

> Let another agent implement changes using Project Memory.

------------------------------------------------------------------------

## Phase 9 --- Continuous Memory

Add:

``` text
GitHub webhooks
Event processing
Incremental indexing
Memory updates
Documentation drift detection
```

Goal:

> Make project memory continuously up to date.

------------------------------------------------------------------------

## Phase 10 --- Verification

Add:

``` text
Tests
Architecture validation
Documentation validation
Change verification
Agent output review
```

Goal:

> Verify that AI-generated changes fit the project.

------------------------------------------------------------------------

## Phase 11 --- Advanced Project Intelligence

Add:

``` text
Technical debt
Security analysis
Performance analysis
Incident memory
Deployment history
Infrastructure
Cloud resources
Production telemetry
```

Goal:

> Understand the complete software lifecycle.

------------------------------------------------------------------------

# 32. Suggested Technical Architecture

A possible long-term architecture:

``` text
                         USER
                           |
                    Web Application
                           |
                       API Gateway
                           |
                  Project Intelligence API
                           |
        +------------------+------------------+
        |                  |                  |
   Ingestion Service   Query Service     Agent Service
        |                  |                  |
        |                  |                  |
   +----+----+             |            +----+----+
   |         |             |            |         |
GitHub    Repository       |       Planner     Context
           Parser          |        Agent       Agent
                           |
                    Retrieval Layer
                           |
            +--------------+--------------+
            |              |              |
       PostgreSQL      Vector DB      Graph DB
            |              |              |
            +--------------+--------------+
                           |
                       LLM Layer
                           |
                    Tool / MCP Layer
                           |
              +------------+------------+
              |            |            |
           GitHub       Coding Agent   CI/Test
```

------------------------------------------------------------------------

# 33. Backend Components

The backend can eventually be split into services.

### API Service

Handles:

``` text
Authentication
Projects
Users
Chat
Configuration
```

### Ingestion Service

Handles:

``` text
Repository fetching
Parsing
Git history
PRs
Issues
Documents
```

### Knowledge Service

Handles:

``` text
Entities
Relationships
Project graph
Memory
```

### Retrieval Service

Handles:

``` text
Vector search
Graph queries
Keyword search
Re-ranking
Evidence selection
```

### Agent Service

Handles:

``` text
Planning
Reasoning
Tool calls
Context generation
Change analysis
```

### Worker System

Handles:

``` text
Indexing
Embeddings
Large repository analysis
Webhook processing
Background AI jobs
```

------------------------------------------------------------------------

# 34. Technologies

A possible stack:

## Frontend

``` text
React
TypeScript
Next.js
Tailwind
React Flow
```

React Flow can be used for interactive architecture/knowledge graphs.

## Backend

``` text
Node.js
TypeScript
Express / Fastify
```

## Database

``` text
PostgreSQL
Redis
```

## Vector Search

Initially:

``` text
pgvector
```

Later:

``` text
Qdrant
Weaviate
Milvus
```

## Graph

Initially, graph relationships can be modeled in PostgreSQL.

Later:

``` text
Neo4j
```

if graph complexity justifies it.

## AI

``` text
LLM
Embeddings
Structured Outputs
Tool Calling
RAG
Agents
MCP
```

## Code Analysis

Use language-specific parsers / AST tooling.

For JavaScript and TypeScript:

``` text
TypeScript Compiler API
Tree-sitter
```

Other languages can be added progressively.

## Infrastructure

``` text
Docker
CI/CD
Cloud
Redis
Message queues
Observability
```

------------------------------------------------------------------------

# 35. Important Engineering Challenges

This project is valuable partly because the hard problems are real.

## Challenge 1 --- Large repositories

A million-line repository cannot simply be placed into an LLM context.

Need:

``` text
Hierarchical indexing
Chunking
Symbol-level retrieval
Summaries
Caching
Incremental indexing
```

## Challenge 2 --- Stale knowledge

Code changes continuously.

Need:

``` text
Webhooks
Incremental indexing
Change detection
Memory invalidation
```

## Challenge 3 --- Hallucination

The AI must not invent project history.

Need:

``` text
Evidence
Citations
Confidence
Source ranking
```

## Challenge 4 --- Historical reasoning

"Why?" often requires traversing:

``` text
Code → Commit → PR → Issue → Discussion
```

Need graph-based retrieval.

## Challenge 5 --- Contradictory information

Documentation may say one thing while code does another.

The system should identify:

``` text
Documentation
vs
Code
vs
Historical decision
```

and explicitly flag conflicts.

## Challenge 6 --- Agent safety

If the system eventually controls coding agents:

``` text
Permissions
Approval
Sandboxing
Tests
Verification
Audit logs
```

become essential.

------------------------------------------------------------------------

# 36. What the Project Ultimately Becomes

At maturity, Project Memory becomes:

``` text
                  SOFTWARE PROJECT
                         |
        +----------------+----------------+
        |                |                |
       CODE           HISTORY         KNOWLEDGE
        |                |                |
     Services         Commits         Decisions
     APIs             PRs             Experiments
     DB               Issues          Failures
     Tests            Incidents       Constraints
        |                |                |
        +----------------+----------------+
                         |
                  PROJECT MEMORY
                         |
          +--------------+--------------+
          |              |              |
        Search         Graph          AI
          |              |              |
          +--------------+--------------+
                         |
                PROJECT INTELLIGENCE
                         |
        +----------------+----------------+
        |                |                |
       Chat        Change Analysis     Agents
        |                |                |
        |                |                |
        |          Implementation       Coding
        |               Plan             Agent
        |                |                |
        +----------------+----------------+
                         |
                     Verification
                         |
                   Memory Updated
```

The final product answers:

### What does the project do?

**Current-state understanding.**

### Why does it work this way?

**Historical and decision memory.**

### What happened before?

**Project timeline and experiments.**

### What will break if we change it?

**Impact analysis.**

### How should we change it?

**Implementation planning.**

### Can an AI agent implement it?

**Context generation + agent integration.**

### What happened after the change?

**Verification + continuous memory update.**

------------------------------------------------------------------------

# 37. Final Product Definition

> **Project Memory is an AI-powered institutional memory and engineering
> intelligence platform for software projects. It continuously
> understands a project's code, architecture, APIs, database,
> documentation, Git history, decisions, experiments, failures, and
> evolution. Developers can chat with the project to understand what the
> system does and why it works the way it does, analyze the impact of
> proposed changes, generate implementation plans, and provide
> project-specific context to coding agents. As the project evolves,
> Project Memory continuously updates its knowledge and preserves the
> reasoning behind the system for future developers and AI agents.**

The fundamental promise is:

> **Your code remembers what your team forgot.**

Or more specifically:

> **Understand what the code does. Remember why it exists. Know what
> will change before you change it.**

------------------------------------------------------------------------

# 38. Long-Term Vision

The ultimate goal is not to create another repository search tool.

It is to create a **persistent engineering intelligence layer** that
sits above the software development lifecycle.

``` text
Requirements
      ↓
Architecture
      ↓
Design Decisions
      ↓
Implementation
      ↓
Code
      ↓
Tests
      ↓
Deployment
      ↓
Production
      ↓
Incidents
      ↓
Lessons
      ↓
New Decisions
      ↓
New Implementation
```

Project Memory connects this entire cycle.

Eventually, a new developer---or a new AI agent---can enter a
ten-year-old project and ask:

> "Teach me this system."

And instead of reading thousands of files manually, the platform can
explain:

``` text
What the system does
How it is structured
Why it was designed this way
How it evolved
What approaches failed
What constraints exist
Where the technical debt is
What is dangerous to change
What depends on what
What should be changed
How to change it safely
```

That is the ultimate vision of **Project Memory**.
