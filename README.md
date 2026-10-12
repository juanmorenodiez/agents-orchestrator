# Generic Agent Orchestrator (GAO)

A modular, project-agnostic multi-agent orchestration framework for AI-assisted software development, built around OpenAI Codex.

> **Status: Early Development — v0.1**
>
> The initial agent contracts have been defined. Orchestration policies, project profiles, Skills integration, and automated installation are planned for future iterations.

## 1. Overview

Generic Agent Orchestrator (GAO) aims to provide a reusable multi-agent architecture that can be integrated into different software repositories.

The framework separates **agent responsibilities** from **project-specific capabilities**, allowing the same agents to operate across different technology stacks.

Target domains include:

- Software Engineering
- Data Engineering
- Machine Learning and AI
- Cloud and Infrastructure Engineering

The core principle is simple:

**Generic Agents + Project Context + Specialized Skills = Adaptable Development Workflows**

Rather than creating a separate agent for every programming language or technology, GAO uses a small set of generic agents that adapt to each project's requirements, architecture, tools, and conventions.

## 2. Architecture

GAO follows a hierarchical multi-agent architecture.

The main orchestrator will coordinate specialized agents responsible for software architecture, implementation, testing, and code review.

```text
                  User Request
                       |
                       v
                +--------------+
                | Orchestrator |
                +--------------+
                       |
          +------------+------------+
          |            |            |
          v            v            v
      Architect    Developer    QA Engineer
                       |
                       v
                    Reviewer
```

*Conceptual diagram. Actual delegation will depend on task complexity, dependencies, and required validation. Agents are not required to execute in a fixed sequence.*

### Architecture Principles

- **Project-agnostic:** Core agents remain independent of specific technologies.
- **Modular:** Agent contracts and Skills can evolve independently.
- **Reusable:** The framework is intended to be deployable across multiple repositories.
- **Context-aware:** Agents respect each project's architecture and conventions.
- **Selective delegation:** Tasks are delegated only when specialization provides value.
- **Validation-driven:** Results must include evidence of relevant checks and limitations.
- **Least privilege:** Agent capabilities are restricted according to their responsibilities.

## 3. Core Agents

GAO currently defines four generic subagent contracts.

### Architect

Responsible for technical analysis and solution design.

Responsibilities:
- Analyze requirements and existing architecture.
- Identify affected components and dependencies.
- Design interfaces and component interactions.
- Evaluate technical trade-offs.
- Produce actionable implementation guidance.

**Execution mode:** Read-only.

### Developer

Responsible for implementing software changes.

Responsibilities:
- Develop features and fix bugs.
- Refactor existing implementations.
- Follow established project conventions.
- Preserve compatibility and existing behavior.
- Perform focused implementation validation.

**Execution mode:** Workspace-write.

### QA Engineer

Responsible for functional verification and automated testing.

Responsibilities:
- Analyze acceptance criteria.
- Design and implement test cases.
- Execute authorized tests.
- Identify functional defects and regressions.
- Report testing evidence and coverage limitations.

**Execution mode:** Workspace-write.

### Reviewer

Responsible for independent technical assessment.

Responsibilities:
- Inspect code changes.
- Detect correctness and security issues.
- Identify regressions and maintainability risks.
- Evaluate architectural consistency.
- Provide prioritized, actionable findings.

**Execution mode:** Read-only.

### Agent Contracts

Each agent follows a common contract defining:

1. Role and mission.
2. Responsibilities.
3. Required inputs.
4. Expected outputs.
5. Permissions and constraints.
6. Completion criteria.

Agents use a shared reporting structure with the following execution outcomes:

- `completed`: Assigned responsibilities have been fulfilled.
- `blocked`: The agent cannot proceed without resolving a dependency or constraint.
- `failed`: The assigned task could not be completed.

A completed agent task does not necessarily mean that the overall user request has been accepted.

## 4. Project-Agnostic Specialization

GAO is designed to separate generic responsibilities from technical expertise.

For example, the same Developer agent could operate in different environments:

| Project Type | Example Skills |
|---|---|
| Software Engineering | Python, APIs, frontend, testing |
| Data Engineering | SQL, PySpark, ETL, data quality |
| Machine Learning | Model training, evaluation, MLOps |
| Cloud Engineering | Infrastructure as Code, CI/CD, deployment |

Specialization will be provided through project context, reusable Skills, and supported tools.

Project profiles will allow repositories to select relevant capabilities without duplicating the Core agent contracts.

*Skills integration and project profiles are planned features.*

## 5. Repository Structure

Current initial structure:

```text
agents-orchestrator/
├── agents/
│   ├── architect.toml
│   ├── developer.toml
│   ├── qa-engineer.toml
│   └── reviewer.toml
└── README.md
```

Additional directories will be introduced as their corresponding components are implemented.

## 6. Working with Codex

GAO targets OpenAI Codex as its initial execution environment.

The framework maintains agent definitions independently so they can later be installed into individual projects.

Codex project-level custom agents use the following directory:

```text
.codex/
└── agents/
    ├── architect.toml
    ├── developer.toml
    ├── qa-engineer.toml
    └── reviewer.toml
```

### Current Manual Setup

1. Ensure OpenAI Codex is installed and configured.
2. Copy the agent TOML files into the target repository's `.codex/agents/` directory.
3. Start a new Codex session in the target repository.
4. Ask Codex to delegate an appropriate task to a custom agent.
5. Inspect the agent's output and verify compliance with its contract.

Example task:

```text
Use the architect agent to analyze the current
repository architecture and identify potential
improvements. Do not modify any files.
```

**Important:** Agent instructions describe expected behavior but are not equivalent to enforced security boundaries. File access and command execution remain subject to Codex sandbox configuration, approvals, and execution environment.

Automated installation is not yet implemented.

## 7. Development Roadmap

### Phase 1 — Agent Contracts

- [x] Define Architect contract.
- [x] Define Developer contract.
- [x] Define QA Engineer contract.
- [x] Define Reviewer contract.
- [ ] Validate custom agents in Codex.

### Phase 2 — Orchestration Core

- [ ] Define the main Orchestrator contract.
- [ ] Establish delegation policies.
- [ ] Establish task input and output schemas.
- [ ] Define error handling and escalation rules.
- [ ] Define integration and validation workflows.

### Phase 3 — Skills System

- [ ] Establish a reusable Skills registry.
- [ ] Create common software development Skills.
- [ ] Integrate reviewed external Skills.
- [ ] Define project-specific Skills selection.

### Phase 4 — Project Integration

- [ ] Define project profiles.
- [ ] Implement a configuration and installation mechanism.
- [ ] Support reuse across different repositories.
- [ ] Validate profile compatibility.

### Phase 5 — Evaluation and Optimization

- [ ] Create representative test scenarios.
- [ ] Compare GAO workflows against standard Codex execution.
- [ ] Evaluate implementation quality, latency, and resource usage.
- [ ] Optimize delegation policies based on measured results.

## 8. Long-Term Vision

GAO aims to become a lightweight, extensible orchestration framework that provides consistent development workflows across heterogeneous software projects.

Future capabilities may include automated workflow validation, improved execution isolation, reusable project configurations, and structured agent evaluation.

The objective is not to maximize the number of agents involved in a task, but to improve software delivery quality, reliability, and maintainability through effective coordination.

---

**Project Status:** v0.1 — Initial Agent Contracts

**Primary Execution Platform:** OpenAI Codex

**Architecture:** Hierarchical, modular, project-agnostic multi-agent system