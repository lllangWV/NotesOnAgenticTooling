# Model Context Protocol (MCP) Specification

Last updated: 2026-01-14 by RS Loop

## Overview

Model Context Protocol (MCP) is an open protocol enabling seamless integration between LLM applications and external data sources/tools. Created by Anthropic and open-sourced in November 2024, it's now governed by the Linux Foundation's Agentic AI Foundation (AAIF).

**Current Version**: 2025-11-25

## Adoption

MCP has achieved industry-wide adoption:
- **97 million** monthly SDK downloads (Python + TypeScript)
- **10,000+** active servers
- **First-class client support**: Claude, ChatGPT, Cursor, Gemini, Microsoft Copilot, VS Code

### Major Adopters

| Company | Adoption Date | Integration |
|---------|---------------|-------------|
| Anthropic | Nov 2024 | Creator, Claude Desktop, Claude Code |
| OpenAI | Mar 2025 | ChatGPT, Agents SDK, Responses API |
| Google | 2025 | Gemini, Google DeepMind |
| Microsoft | 2025 | VS Code, Copilot |
| Cursor | 2025 | Full MCP support |

## Architecture

### Two-Layer Design

```
MCP Host (AI Application)
├── MCP Client 1 ──→ MCP Server A (Local)
├── MCP Client 2 ──→ MCP Server B (Local)
├── MCP Client 3 ──→ MCP Server C (Remote)
└── MCP Client 4 ──→ MCP Server C (Remote)
```

**Key Participants**:
- **MCP Host**: AI application coordinating multiple clients (VS Code, Claude Desktop)
- **MCP Client**: Component maintaining 1:1 connection to a server
- **MCP Server**: Program providing context, tools, or capabilities

### Data Layer (Protocol)

Implements **JSON-RPC 2.0** protocol with:
- Lifecycle management (initialization, capability negotiation, termination)
- Server features (tools, resources, prompts)
- Client features (sampling, elicitation, logging)
- Utility features (notifications, progress, cancellation, tasks)

### Transport Layer

| Transport | Use Case | Features |
|-----------|----------|----------|
| **Stdio** | Local processes | Direct stream, optimal performance, no network overhead |
| **Streamable HTTP** | Remote servers | HTTP POST, SSE, OAuth support |

## Core Primitives

### Server-Exposed Primitives

#### 1. Tools
Executable functions AI applications can invoke:

```json
{
  "name": "weather_current",
  "title": "Weather Information",
  "description": "Get current weather for any location",
  "inputSchema": {
    "type": "object",
    "properties": {
      "location": {"type": "string"},
      "units": {"enum": ["metric", "imperial", "kelvin"]}
    },
    "required": ["location"]
  }
}
```

#### 2. Resources
Data sources providing contextual information:
- File contents
- Database records
- API responses

**Key Distinction**: Resources return data but don't execute actionable computations (unlike tools which can have side effects)

#### 3. Prompts
Reusable templates for structured interactions:
- System prompts
- Few-shot examples
- Instruction templates

### Client-Exposed Primitives

- **Sampling**: Servers request LLM completions from client (enables agentic behaviors)
- **Roots**: Servers inquire about URI/filesystem boundaries
- **Elicitation**: Servers request additional information from users

## Lifecycle Management

### Initialization Handshake

**Purpose**:
1. Protocol version negotiation
2. Capability discovery
3. Identity exchange

**Request Example**:
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "initialize",
  "params": {
    "protocolVersion": "2025-06-18",
    "capabilities": {"elicitation": {}},
    "clientInfo": {"name": "example-client", "version": "1.0.0"}
  }
}
```

### Tool Discovery and Execution

```json
// Discovery
{"jsonrpc": "2.0", "id": 2, "method": "tools/list"}

// Execution
{
  "jsonrpc": "2.0",
  "id": 3,
  "method": "tools/call",
  "params": {
    "name": "weather_current",
    "arguments": {"location": "San Francisco", "units": "imperial"}
  }
}
```

## November 2025 Specification Updates

### 1. Async Tasks Primitive
- Experimental "call-now, fetch-later" pattern
- Any request can become asynchronous
- Supports long-running operations

### 2. Enhanced OAuth
- MCP servers classified as OAuth Resource Servers
- Support for OpenID Connect Discovery 1.0
- Better authorization server discovery

### 3. Extension Lanes
- Infrastructure for experimentation
- Clearer separation between method shape and payload schemas
- Easier payload evolution

## Security Model

### Authorization Framework

MCP uses **OAuth 2.1** as foundation:
- Users log in and explicitly authorize agents
- Familiar web OAuth flows and consent screens
- Transport-specific rules (HTTP+SSE should follow spec, STDIO retrieves from environment)

### Security Principles

1. **User Consent and Control**: Explicit consent for data access
2. **Data Privacy**: Hosts obtain explicit user consent
3. **Tool Safety**: Tools require user approval (arbitrary code execution)
4. **LLM Sampling Controls**: Users approve sampling requests

### Known Vulnerabilities

- **Confused Deputy Problem**: Risk of improper permission execution
- **Knostic Research (July 2025)**: ~2,000 internet-exposed MCP servers lacked authentication

### Best Practices

- Never embed client credentials in code
- Use environment variables for secrets
- Never log Authorization headers/tokens
- Implement principle of least privilege
- Select minimum required scopes

## Tool Support Matrix

| Tool | MCP Support | Notes |
|------|-------------|-------|
| **Claude Code** | Full | Dual role (server + client) |
| **Claude Desktop** | Full | Native support |
| **ChatGPT** | Full | Developer mode (Sep 2025) |
| **Cursor** | Full | Tools supported, resources planned |
| **GitHub Copilot** | Full | GA in VS Code 1.102+ |
| **VS Code** | Full | Native integration |
| **Gemini** | Full | First-class support |

## Configuration Examples

### Claude Code

```json
// ~/.claude.json (user scope)
// .mcp.json (project scope)
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {"GITHUB_TOKEN": "${GITHUB_TOKEN}"}
    }
  }
}
```

### Cursor

```json
// .cursor/mcp.json
{
  "servers": {
    "my-server": {
      "command": "node",
      "args": ["./server.js"]
    }
  }
}
```

## Open Questions

- [ ] Performance metrics for MCP implementations across platforms
- [ ] Multi-modal context handling (images, audio, video)
- [ ] Cross-protocol interoperability (MCP + A2A + ACP)
- [ ] Scalability limits for concurrent connections

## Sources

- [MCP Official Site](https://modelcontextprotocol.io/)
- [MCP Specification 2025-11-25](https://modelcontextprotocol.io/specification/2025-11-25)
- [MCP Architecture Overview](https://modelcontextprotocol.io/docs/learn/architecture)
- [Anthropic: Introducing MCP](https://www.anthropic.com/news/model-context-protocol)
- [Linux Foundation AAIF Announcement](https://www.linuxfoundation.org/press/linux-foundation-announces-the-formation-of-the-agentic-ai-foundation)
- [OpenAI MCP Support](https://www.infoq.com/news/2025/10/chat-gpt-mcp/)
- [One Year of MCP](https://www.pento.ai/blog/a-year-of-mcp-2025-review)
- [MCP Enterprise Adoption Guide](https://guptadeepak.com/the-complete-guide-to-model-context-protocol-mcp-enterprise-adoption-market-trends-and-implementation-strategies/)
