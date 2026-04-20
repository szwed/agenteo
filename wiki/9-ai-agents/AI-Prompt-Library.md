# AI Prompt Library

Curated prompt collection for [AI Agents Overview](AI-Agents-Overview.md) multi-agent orchestration. Prompts are meta-level (coordination, decision-making, troubleshooting) and tested for real-world platform engineering workflows.

## Available Prompts

### 1. Basic Prompt

Simple agent routing and coordination.

**Key features**:
- Smart routing to specialized agents (ArgoCD, AWS, Jira, GitHub, PagerDuty, etc.)
- Two-phase task management: planning (create task plan) then execution (call agents, track progress)
- Preserves agent messages verbatim with minimal wrapper
- Direct presentation of results

**Best for**: simple queries, single-agent routing, straightforward multi-step tasks.

### 2. Deep Agent Prompt

Advanced orchestration with parallel execution and incident engineering.

**Key features**:
- **TODO-based execution**: mandatory `write_todos` plan for all operational requests
- **Parallel execution**: independent agents run simultaneously
- **Agent workspace**: in-memory coordination prevents garbled output from parallel agents
- **Error recovery**: automatic retry with available options
- **Structured user input**: `UserInputMetaData` format with text, select, boolean field types

**Incident management personas** (built-in):
- **Incident Investigator**: root cause analysis (PagerDuty + Jira + Kubernetes/Komodor + RAG + Confluence)
- **Incident Documenter**: post-incident reports and follow-up actions
- **MTTR Analyst**: Mean Time To Recovery metrics and improvement reports
- **Uptime Analyst**: service availability metrics and SLO compliance

**Best for**: complex multi-agent workflows, incident management, parallel execution, large-scale platform health reports.

## Choosing the Right Prompt

| Criteria | Basic | Deep Agent |
|----------|-------|------------|
| Simple agent routing | Yes | Overkill |
| Multi-step with dependencies | Limited | Yes |
| Parallel execution | No | Yes |
| Incident engineering | No | Yes |
| Structured user input | No | Yes |
| Response overhead | Minimal | Higher |

## Integration

Both prompts work with:
- Specialized agents ([AI Platform Agents](AI-Platform-Agents.md))
- RAG knowledge base ([AI Knowledge Bases](AI-Knowledge-Bases.md))
- Agent workspace (in-memory coordination)
- A2A protocol for agent-to-agent communication
