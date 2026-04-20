# AI Knowledge Bases

RAG-powered knowledge platform for [[AI-Agents-Overview]]. Combines vector-based retrieval and graph-based reasoning to provide contextually relevant information to AI agents and users.

## Key Capabilities

### Hybrid Search

Dual-vector approach:
- **Semantic search**: dense vector embeddings capture meaning and context
- **Keyword search**: BM25 sparse vectors match exact terms and phrases
- **Weighted reranking**: configurable balance between semantic and keyword results

### Knowledge Graph

When Graph RAG is enabled, structured entities are stored in Neo4j:
- **Entity storage**: structured data with properties and relationships
- **Graph traversal**: explore entity neighborhoods and find paths between entities
- **Automatic splitting**: nested structures split into connected sub-entities

### Automatic Ontology Discovery

The Ontology Agent automatically discovers relationships between entity types:
- Fuzzy matching + LLM evaluation to identify valid relationships
- Background execution with configurable intervals
- Syncs discovered relationships back to the data graph

## MCP Tools for AI Agents

The RAG server exposes MCP tools following a **search + fetch pattern**:
1. `search` — hybrid semantic/keyword search, returns truncated snippets
2. `fetch_document` — retrieve full content of a specific document by ID
3. Graph exploration tools for entity traversal

Any MCP-compatible client can connect (Claude Desktop, VS Code, Cursor, LangGraph agents).

## Supported Data Sources

| Source | Type | Description |
|--------|------|-------------|
| Web Pages | Documents | Crawl sitemaps and web pages |
| AWS | Graph Entities | EC2, S3, RDS, Lambda, EKS, DynamoDB |
| Kubernetes | Graph Entities | Pods, Deployments, Services, CRDs |
| Backstage | Graph Entities | Service catalog entities |
| ArgoCD | Graph Entities | Applications, projects, clusters |
| GitHub | Graph Entities | Organizations, repositories, teams |
| Confluence | Documents | Space pages with incremental sync |
| Slack | Documents | Channel conversations and threads |
| Webex | Documents | Space messages |

## Access Points

| Interface | Description |
|-----------|-------------|
| Web UI | Interactive search and graph visualization |
| API (Swagger) | REST API for programmatic access |
| MCP Endpoint | Model Context Protocol for AI agents |
| Neo4j Browser | Graph database explorer |

## See Also

- [[AI-Platform-Agents]] — agents that consume knowledge base tools
- [[AI-Agents-UI]] — UI includes knowledge base search and graph views
