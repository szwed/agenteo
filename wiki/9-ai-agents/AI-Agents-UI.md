# AI Agents UI

A2A Message Visualizer for [AI Agents Overview](AI-Agents-Overview.md). Built with Next.js 15 and React 19.

## Layout

3-panel interface:
- **Left panel**: chat history and navigation sidebar
- **Center panel**: chat interface with final output rendering
- **Right panel**: real-time A2A message stream visualization

## Routes

| Route | Description |
|-------|-------------|
| `/use-cases` | Browse and execute common platform engineering scenarios (default landing) |
| `/chat` | Interactive chat with A2A streaming |
| `/knowledge-bases/ingest` | Manage data sources and ingestion jobs |
| `/knowledge-bases/search` | Hybrid search (semantic + keyword) |
| `/knowledge-bases/graph` | Knowledge graph visualization |

## A2A Protocol Support

A2A Spec conformant. Supports event types:
- `task` — task lifecycle events
- `artifact-update` — streaming content and artifacts
- `status-update` — completion state

**A2UI widget support** (A2UI v0.8 spec): buttons, forms, cards, lists, tables, progress bars, select, input.

## Real-Time Streaming

Live visualization of SSE (Server-Sent Events) with filters and inspection. Displays all streamed content as it arrives.

## Tech Stack

- **Framework**: Next.js 15, App Router, React Server Components
- **UI**: React 19, Tailwind CSS, Radix UI
- **State**: Zustand
- **A2A**: `@a2a-js/sdk` via `A2ASDKClient` wrapper
- **Graph**: Sigma.js (`@react-sigma/core`)
- **Markdown**: react-markdown with Prism syntax highlighting

## Configuration

Connects to the supervisor at `SUPERVISOR_URL` (default: `http://localhost:8000`).

```bash
# Development
npm run dev

# Docker Compose (includes supervisor)
make caipe-ui-docker-compose
```

## See Also

- [AI Use Cases](AI-Use-Cases.md) — pre-built skills shown in the use cases gallery
- [AI Knowledge Bases](AI-Knowledge-Bases.md) — knowledge base views (ingest, search, graph)
