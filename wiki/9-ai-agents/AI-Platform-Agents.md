# AI Platform Agents

Specialized sub-agents that integrate with essential engineering tools via MCP servers and the A2A protocol.

## Available Agents

| Agent | Purpose |
|-------|---------|
| ArgoCD | GitOps continuous delivery for Kubernetes |
| Backstage | Developer portal and service catalog |
| Confluence | Team collaboration and documentation |
| GitHub | Source code management and collaboration |
| GitLab | Source code management (alternative to GitHub) |
| Jira | Project management and issue tracking |
| Komodor | Kubernetes troubleshooting and monitoring |
| AWS | Cloud infrastructure and EKS management |
| PagerDuty | Incident management and on-call scheduling |
| VictorOps | Incident management and on-call operations |
| Slack | Team communication and collaboration |
| Splunk | Log analytics and monitoring |
| Webex | Team communication and collaboration |
| Weather | Weather information (demo/testing agent) |

## Architecture Pattern

Each agent follows a common pattern:
- Built with agentic frameworks (LangGraph, Strands, etc.)
- Exposes capabilities via **MCP Server** (Model Context Protocol)
- Communicates with other agents via **A2A protocol** (Agent-to-Agent)
- Receives tasks from the Supervisor agent

## Creating New Agents

1. Fork the Petstore/Template agent as starting point
2. Generate MCP tools from OpenAPI spec using `openapi-mcp-codegen`
3. Implement agent logic with chosen framework
4. Configure A2A server binding
5. Register with the Supervisor

Tool: [openapi-mcp-codegen](https://github.com/cnoe-io/openapi-mcp-codegen) — generates MCP server code from any OpenAPI specification.

See also: [[AI-Agents-Architecture]], [[AI-Agents-Overview]], [[Developer-Portal]], [[CI-CD]], [[Observability]]
