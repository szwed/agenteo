# AI Agents Overview

Community AI Platform Engineering (CAIPE, pronounced "cape") is an open-source Multi-Agentic AI System (MAS) for Platform Engineering, SRE, and DevOps. It is developed by the [CNOE](https://cnoe.io/) Agentic AI SIG.

## What It Does

The platform provides a secure, scalable, persona-driven multi-agent system with built-in knowledge base retrieval. It coordinates specialized AI agents that interact with platform tools (ArgoCD, GitHub, Jira, PagerDuty, AWS, Kubernetes, etc.) via MCP servers and the A2A protocol.

## Key Features

- **Persona-driven**: configurable profiles (platform-engineer, devops-engineer, incident-engineer) with curated agent sets
- **Knowledge base retrieval**: hybrid search (semantic + keyword) with knowledge graph support
- **Secure**: OAuth authentication, A2A protocol for agent-to-agent communication, policy enforcement
- **Scalable**: from single ReAct agent to enterprise distributed multi-agent deployment
- **Integrations**: Backstage (Internal Developer Portal) and VS Code

## Goals

- Curated MAS reference implementation for platform teams
- Ecosystem of practitioners sharing reusable configurations
- Reusable prompt libraries for platform engineering workflows
- Open-source, community-driven under CNOE governance

## Sub-Pages

| Page | Description |
|------|-------------|
| [AI Agents Architecture](AI-Agents-Architecture.md) | Solution architecture evolution (6 stages) |
| [AI Platform Agents](AI-Platform-Agents.md) | Available platform agents and development guide |
| [AI Knowledge Bases](AI-Knowledge-Bases.md) | RAG-powered knowledge platform |
| [AI Prompt Library](AI-Prompt-Library.md) | Curated prompt collection for multi-agent orchestration |
| [AI Agents Security](AI-Agents-Security.md) | Security model (OAuth, A2A, policy enforcement) |
| [AI Use Cases](AI-Use-Cases.md) | Platform engineer use cases, personas, and skills |
| [AI Agents UI](AI-Agents-UI.md) | A2A Message Visualizer (Next.js) |

## Links

- GitHub: [cnoe-io/ai-platform-engineering](https://github.com/cnoe-io/ai-platform-engineering)
- Docs: [cnoe-io.github.io/ai-platform-engineering](https://cnoe-io.github.io/ai-platform-engineering/)
- CNCF Slack: `#cnoe-sig-agentic-ai`
