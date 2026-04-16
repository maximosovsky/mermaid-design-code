# Multi-Agent Collaboration (Notion Clean Style)

This diagram demonstrates the interaction pattern of multiple highly specialized AI agents. Rendered using new semantic shapes (hexagons for agents, cylinders for databases) and the `Notion Clean` style.

## Pipeline Flow

> User → Orchestrator → Task Planner → Delegation to 2 Agents → Tools / Memory → Collect Results → Synthesis → User Response

## Components Breakdown

### 1. 🚀 Mission Control (Management Layer)
- **Orchestrator Agent**: Primary entry point. Receives user prompts. Rendered as a `hex` (hexagon) shape and uses the accent color for highlighting.
- **Task Planner**: Parses the prompt and breaks it down into subtasks.
- **Synthesis Engine**: A synthesizer agent (`hex`) that aggregates disparate responses from specialized agents into a single final output.

### 2. 👥 Specialist Agents (Execution)
- **Research Agent**: Responsible for information retrieval, writes results to the shared vector database.
- **Coding Agent**: Generates code, invokes external tools.
- **Review Agent**: Receives PRs (results) from the Coding Agent and validates them before final synthesis.
All execution agents use the `hex` shape with the `clrNotionAccent` class.

### 3. 🗄️ Shared Resources
- **Vector Memory**: `cylinder` shape. Acts as long-term or shared memory where the Research Agent writes and others can read from. Uses basic `clrNotionBase` styling.
- **Tool execution**: `diamond` shape. Represents the infrastructure tool layer (API calls, terminals, etc.) invoked by the Coding Agent.

This approach ensures a clear separation of concerns. The Notion Clean style reduces visual noise, focusing attention exclusively on the execution agents and their primary data flows.
