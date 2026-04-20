# AI Agents Security

Security model for [[AI-Agents-Overview]] multi-agent system.

## Authentication

- **OAuth / OIDC**: users authenticate via Keycloak (federated with company SSO)
- Backstage UI obtains access token via OIDC flow
- Access token passed to Supervisor via A2A protocol

## Agent-to-Agent Security

The A2A protocol secures communication between supervisor and sub-agents:

1. User authenticates via Keycloak, UI receives access token
2. UI calls Supervisor with access token over A2A
3. Supervisor validates token against Keycloak JWKS keys
4. Supervisor requests **down-scoped token** for sub-agent tasks (principle of least privilege)
5. Sub-agent validates down-scoped token before executing
6. MCP tool server checks policy engine before API calls

## Authorization

- **MCP servers** handle authorization and scope validation for tool execution
- **Policy engine** evaluates claims, scopes, and resource rules at the tool layer
- Custom entitlements defined in Keycloak (e.g., `github.read`, `argocd.app.create`, `mcp.tools.kb.query`)

## Enterprise Deployment

- **Agent identity**: gateway-level identity (SLIM/Agentgateway) with OAuth tokens
- **Distributed tracing**: end-to-end visibility across agent interactions
- **Policy enforcement**: centralized policy engine for tool access control
- See [[AI-Agents-Architecture]] stages 5-6 for enterprise patterns

## See Also

- [[Platform-Mesh-Security]] — broader platform AuthN/AuthZ context
- [[Security]] — compliance automation, key management, secrets management
- [[AI-Agents-Architecture]] — how security fits into the architecture evolution
