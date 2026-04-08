# Awesome AI Agent Protocols & Verification

> A curated list of AI agent protocols, specifications for communication, identity, trust, and verification.

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

---

## Contents

- [Communication Protocols](#communication-protocols)
  - [Context-Oriented Protocols](#context-oriented-protocols)
  - [Inter-Agent Protocols](#inter-agent-protocols)
  - [Meta-Protocols](#meta-protocols)
  - [API-to-Agent Bridges](#api-to-agent-bridges)
  - [Execution & Task Protocols](#execution--task-protocols)
- [Agent Identity & Discovery](#agent-identity--discovery)
- [Trust & Verification](#trust--verification)
- [Governance & Security](#governance--security)
- [Personhood & Human-AI Distinction](#personhood--human-ai-distinction)
- [Protocol Stack](#protocol-stack)
- [Communication Protocol Comparison](#communication-protocol-comparison)

---

## Communication Protocols

Standards and specifications for how AI agents exchange information with tools, resources, and each other.

### Context-Oriented Protocols

| Protocol | Proposer | Description | Links |
|----------|----------|-------------|-------|
| **Model Context Protocol (MCP)** | Anthropic, 2024 | Standardizes integration between LLM applications and external data sources/tools. Three-component architecture (host, client, server) using JSON-RPC 2.0. Servers expose resources, prompts, and tools; clients provide sampling, roots, and elicitation. Inspired by Language Server Protocol. | [Architecture](https://modelcontextprotocol.io/specification/2025-11-25/architecture) / [Specification](https://modelcontextprotocol.io/specification/2025-11-25) |

### Inter-Agent Protocols

| Protocol | Proposer | Description | Links |
|----------|----------|-------------|-------|
| **Agent2Agent (A2A)** | Google / The Linux Foundation, 2025 | Open standard for communication between independent AI agent systems. Three-layer design: canonical data model (Protocol Buffers), abstract operations, and protocol bindings (JSON-RPC, gRPC, HTTP/REST). Supports async tasks, streaming, push notifications, and human-in-the-loop workflows. | [Specification (v1.0.0)](https://a2a-protocol.org/latest/specification/) |
| **Agent Network Protocol (ANP)** | GaoWei Chang / ANP Community, 2024 | Open-source protocol for secure, decentralized agent communication. Three-layer architecture: Identity & Secure Communication (using `did:wba` method + ECDHE encryption), Meta-Protocol (AI-driven protocol negotiation), and Application layer (Agent Description Protocol in JSON-LD). Includes discovery, description, and transaction specifications. | [White Paper](https://agent-network-protocol.com/specs/white-paper) |
| **Agent Interaction & Transaction Protocol (AITP)** | NEAR Foundation, 2025 | Enables agents to communicate securely across trust boundaries. Built on Chat Threads (inspired by OpenAI Threads API) and an extensible Capabilities system for structured interactions. Supports multimodal input, generative UI, payments, and human-in-the-loop. Vision: HTTP/HTML equivalent for agent-to-agent commerce. | [Specification (v0.1.0)](https://aitp.dev/) / [Vision](https://aitp.dev/vision) |

### Meta-Protocols

| Protocol | Authors | Description | Links |
|----------|---------|-------------|-------|
| **Agora** | Marro et al., 2024 | Communication protocol layer addressing the agent communication trilemma: balancing versatility, portability, and efficiency. Agents negotiate protocols dynamically using natural language and LLM-driven code generation. Demonstrated with a 100-agent network. | [Paper](https://arxiv.org/abs/2410.11905) |

### API-to-Agent Bridges

| Protocol | Proposer | Description | Links |
|----------|----------|-------------|-------|
| **agents.json** | Wild Card AI, 2025 | Open specification that extends OpenAPI to formally describe contracts for LLM-agent interactions. Introduces Flows (multi-step API call sequences) and Links (action stitching). Discoverable at `.well-known/agents.json`. Stateless by design, requiring minimal changes to existing APIs. | [Specification (v0.1.0)](https://github.com/wild-card-ai/agents-json) |

### Execution & Task Protocols

| Protocol | Proposer | Description | Links |
|----------|----------|-------------|-------|
| **Agent Protocol** | AI Engineer Foundation, 2024 | REST API specification (OpenAPI 3.0) defining a standard control interface for agents. Core abstractions: Tasks (goals), Steps (units of work), and Artifacts (outputs). Supports multipart file upload/download, CORS, and flexible auth (API keys, OAuth 2.0, JWT). | [Specification (v1)](https://agentprotocol.ai/specification/) |

## Agent Identity & Discovery

Protocols for discovering, registering, and identifying AI agents across systems and organizations.

| Protocol | Authors | Description | Links |
|----------|---------|-------------|-------|
| **Agent Identity & Discovery (AID)** | Agent Community, 2026 | Minimal, DNS-first bootstrap standard for discovering agent endpoints. Uses DNS TXT records at `_agent.<domain>` with semicolon-delimited key-value pairs. Protocol-agnostic (supports MCP, A2A, OpenAPI tokens). | [Specification (v1.2.0)](https://aid.agentcommunity.org/docs/specification) |
| **Agent Name Service (ANS)** | Huang (DistributedApps.ai), Narajala (AWS), Habler (Intuit), Sheriff (Cisco), 2025 | DNS-inspired registry for secure agent discovery and lifecycle management. Uses PKI certificates for verifiable identity, a Protocol Adapter Layer supporting A2A/MCP/ACP, and capability-aware resolution. | [Paper](https://arxiv.org/abs/2505.10609) |

## Trust & Verification

Frameworks and on-chain protocols for establishing trust between agents without pre-existing relationships.

| Paper / Protocol | Authors | Description | Links |
|------------------|---------|-------------|-------|
| **ERC-8004: Trustless Agents** | De Rossi (MetaMask), Crapis (Ethereum), Ellis (Google), Reppel (Coinbase), 2025 | Ethereum standard for trustless agent interaction via three on-chain registries: Identity (ERC-721), Reputation, and Validation. Supports tiered trust proportional to value at risk -- from reputation systems to stake-secured re-execution, zkML proofs, and TEE attestations. | [EIP-8004](https://eips.ethereum.org/EIPS/eip-8004) |

## Governance & Security

Toolkits and frameworks for runtime governance, policy enforcement, and security of AI agent systems.

| Tool / Framework | Authors | Description | Links |
|------------------|---------|-------------|-------|
| **Agent Governance Toolkit** | Microsoft, 2025 | Runtime governance infrastructure for autonomous AI agents. Provides deterministic policy enforcement (<0.1ms latency), Ed25519 cryptographic identity, SPIFFE/SVID zero-trust identity, 4-tier privilege rings with execution sandboxing, and SRE tooling (SLOs, error budgets, chaos engineering). Covers all 10 OWASP Agentic Top 10 risks. Includes an MCP Security Scanner for tool poisoning detection. SDKs for Python, TypeScript, .NET, Rust, and Go. | [GitHub](https://github.com/microsoft/agent-governance-toolkit) |

## Personhood & Human-AI Distinction

Privacy-preserving methods for distinguishing humans from AI agents online.

| Paper | Authors | Description | Links |
|-------|---------|-------------|-------|
| **Personhood Credentials** | Adler & Hitzig (OpenAI), Jain (Microsoft), et al., 2024 | Proposes privacy-preserving digital credentials proving a bearer is human without revealing identity. Uses zero-knowledge proofs for unlinkable pseudonymity. Analyzes limitations of existing countermeasures (CAPTCHAs, economic barriers, AI detection, biometrics) and addresses sockpuppets, bot attacks, and misleading agents. | [Paper](https://arxiv.org/abs/2408.07892) |

---

## Protocol Stack

These protocols operate at different layers and are often **complementary, not competing**. You might use AID to discover an agent, ERC-8004 to verify trust, and A2A to communicate.

```
┌───────────────────────────────────────────────────┐
│              Execution & Control                  │
│                Agent Protocol                     │
├───────────────────────────────────────────────────┤
│              Communication                        │
│  Context:     MCP (agent ↔ tools)                 │
│  Inter-Agent: A2A · ANP · AITP                    │
│  Meta:        Agora                               │
├───────────────────────────────────────────────────┤
│              API Adaptation                       │
│                agents.json                        │
├───────────────────────────────────────────────────┤
│              Identity & Trust                     │
│                ERC-8004                           │
├───────────────────────────────────────────────────┤
│              Discovery                            │
│                AID · ANS                          │
├───────────────────────────────────────────────────┤
│              Governance (cross-cutting)            │
│                Microsoft Agent Governance Toolkit  │
└───────────────────────────────────────────────────┘
```

> **Note:** ANP spans multiple layers — it bundles its own discovery (`.well-known`), identity (`did:wba`), meta-protocol negotiation, and communication into a single full-stack protocol.

## Communication Protocol Comparison

The protocols below are comparable — they all define how agents exchange messages.

| | MCP | A2A | ANP | AITP |
|---|---|---|---|---|
| **Scope** | Agent ↔ tools/resources | Agent ↔ agent | Agent ↔ agent | Agent ↔ agent |
| **Transport** | JSON-RPC 2.0 | JSON-RPC, gRPC, REST | HTTP + DID auth | HTTP |
| **Identity** | Host-managed | Agent Cards | `did:wba` (W3C DID) | NEAR identity |
| **Discovery** | Capability negotiation | Agent Cards | `.well-known` + search | Registry / intent resolution |
| **Architecture** | Centralized (host) | Federated (enterprise) | Decentralized (P2P) | Federated (NEAR) |
| **Best for** | Tool integration | Enterprise orchestration | Open agent networks | Agent commerce |


---

## Contributing

Contributions welcome! Please read the [contributing guidelines](CONTRIBUTING.md) first.

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)
