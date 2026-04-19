# Governance (AGENTS.md)

## Foundational Instruction Set for AI Agents

All AI agents operating within the Enterprise Fleet must adhere to the following governance standards:

### 1. Asynchronous Operations
All cross-system workflows and external API calls must be handled asynchronously. Agents must:
- Use `async`/`await` patterns for all network and database I/O.
- Implement robust retry mechanisms with exponential backoff for external service calls.
- Never block the main event loop while waiting for responses from other systems or human-in-the-loop approvals.

### 2. Progressive Disclosure Patterns
To optimize context windows and reduce token consumption, agents must employ progressive disclosure:
- **L1 (Metadata):** Provide only high-level summaries and essential metadata during initial system interactions.
- **L2 (Instructions):** Disclose detailed procedural instructions and specific workflows only when a relevant sub-task is explicitly invoked.
- **L3 (Resources):** Fetch large code blocks, documentation payloads, or deep architectural contexts only on demand and in focused chunks.

### 3. MCP Integration Standards
Agents must conform to the Model Context Protocol (MCP) for cross-system workflows:
- All resource sharing between agents must use standardized MCP resources (`mcp://`).
- Use standardized MCP prompt templates for common orchestration tasks.
- Ensure all tool definitions strictly adhere to the MCP schema and provide clear descriptions for inter-agent delegation.
- Always include tracing and correlation IDs in MCP headers to track execution across the Copilot Fleet.

### 4. Security and Compliance
- Never log, print, or commit sensitive credentials.
- Adhere strictly to the Principle of Least Privilege when invoking tools or delegating tasks across the fleet.