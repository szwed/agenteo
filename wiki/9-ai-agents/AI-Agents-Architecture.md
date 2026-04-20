# AI Agents Architecture

Solution architecture evolution of [[AI-Agents-Overview]], from simple agent to enterprise multi-agent system.

## Architecture Stages

### 1. Simple ReAct Agent

Single agent that reasons about a task and takes action. Proof point that agents can support platform operations with a focused persona.

### 2. Agent + MCP Tools

Added platform services (ArgoCD, GitHub, Jira, Kubernetes) connected via MCP protocol. The agent can create pull requests, manage tickets, trigger deployments, and interact with the platform ecosystem.

### 3. Supervisor Agent (MAS)

Single agent no longer sufficient. A supervisor agent coordinates multiple specialized sub-agents. The supervisor plans, delegates, and integrates results into consistent workflows.

### 4. Hierarchical Supervisor with A2A Protocol

Distributed sub-agents communicating through the A2A (Agent-to-Agent) protocol. Creates a hierarchical structure where agents securely exchange tasks across environments.

### 5. Enterprise: Gateway Transport + OAuth Agent Identity

Gateway (SLIM/Agentgateway) as transport between agents. OAuth-based Agent Identity enforces authentication and authorization at the transport layer.

### 6. Enterprise: Advanced Integrations

Full enterprise deployment with:
- Distributed tracing
- Policy enforcement
- Knowledge retrieval (RAG)
- Backstage integration (Internal Developer Portal)
- VS Code integration
- Secure, scalable, open-source reference system

## Sub-Agent Architecture

Each agent follows a consistent layered pattern:

```
User Client (A2A) → A2A Protocol → ReAct Agent (LangGraph) → MCP Adapter → MCP Server → External API
```

The A2A protocol handles transport. The agent graph layer (LangGraph/Strands) handles reasoning. MCP servers handle tool execution against external APIs.

## See Also

- [[AI-Platform-Agents]] — available platform agents
- [[AI-Agents-Security]] — OAuth, A2A security, policy enforcement
- [[AI-Knowledge-Bases]] — RAG knowledge retrieval layer
