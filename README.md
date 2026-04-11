# Awesome AI Agent Protocols [![Awesome](https://awesome.re/badge.svg)](https://awesome.re) [![License: CC0-1.0](https://img.shields.io/badge/License-CC0_1.0-lightgrey.svg)](https://creativecommons.org/publicdomain/zero/1.0/) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/nicoewawe/awesome-ai-agent-protocols/pulls)

> A curated list of protocols, tools, and services powering the AI agent infrastructure stack — identity, discovery, communication, payments, and governance.

---

## Contents

- [Identity — Proof of Personhood](#-identity--proof-of-personhood)
- [Agent Identity & Trust](#-agent-identity--trust)
- [Agent Discovery](#-agent-discovery)
- [Communication Protocols](#-communication-protocols)
- [Payments & Commerce](#-payments--commerce)
- [Governance & Security](#%EF%B8%8F-governance--security)
- [Contributing](#contributing)

---

## 🪪 Identity — Proof of Personhood

*How do humans behind agents prove they're real and unique? Without this layer, Sybil attacks make every other layer fragile.*

- [World ID](https://world.org/world-id) — Iris-biometric proof-of-personhood with biometric liveness check. 18M+ verified users, but not available all countries.
- [Self Protocol](https://self.xyz) — ZK proofs from passports and national IDs. Covers 60+ countries via NFC chip verification (~1B passports globally). First production ERC-8004 implementation.
- [BrightID](https://brightid.org) — Social-graph-based proof of uniqueness. Decentralised, no biometrics required.
- [Holonym](https://holonym.id) — Privacy-preserving identity verification using ZK proofs from government IDs. Sybil resistance without biometric hardware.
- [Humanity Protocol](https://humanityprotocol.com) — Palm-scan biometric proof-of-personhood. Mobile-first, no dedicated hardware.

---

## 🤖 Agent Identity & Trust

*How do agents prove who they are, who's behind them, and whether they can be trusted?*

### Standards & Specifications

- [W3C Decentralized Identifiers (DIDs)](https://www.w3.org/TR/did-core/) — The foundation. Globally unique, self-sovereign identifiers controlled by the subject, not a central authority. Multiple DID methods exist (`did:web`, `did:key`, `did:ion`, `did:wba`).
- [W3C Verifiable Credentials](https://www.w3.org/TR/vc-data-model-2.0/) — Cryptographically signed, tamper-evident, machine-verifiable credentials. The digital equivalent of physical certificates. Trust triangle: Issuer → Holder → Verifier.
- [ERC-8004](https://eips.ethereum.org/EIPS/eip-8004) — Ethereum standard for on-chain agent identity, reputation, and validation registries. Three registries: identity (NFT-based), reputation (on-chain ratings), validation (capability attestations).

### Implementations

- [Web Bot Auth](https://developers.cloudflare.com/bots/reference/bot-verification/web-bot-auth/) — Cloudflare's cryptographic HTTP message signatures (IETF RFC 9421) for bot/agent identity. Ed25519 keys, `/.well-known/http-message-signatures-directory`. Production-deployed on the Verified Bots Program. [Rust](https://crates.io/crates/web-bot-auth) and [TypeScript](https://www.npmjs.com/package/web-bot-auth) libraries available.
- [World AgentKit](https://docs.world.org/agents/agent-kit/integrate) — Extends x402 with proof-of-personhood verification for agents. Agents register on AgentBook (World Chain), verified via World App. Distinguishes human-backed agents from bots. `npm install @worldcoin/agentkit`.
- [ANP Identity Layer](https://github.com/agent-network-protocol/agent-network-protocol) — Agent Network Protocol uses `did:wba` (DID method anchored to web domains). Decentralised agent identity without blockchain.

---

## 🔍 Agent Discovery

*How do agents find each other and advertise their capabilities?*

- [A2A Agent Cards](https://google.github.io/A2A/) — JSON metadata at `/.well-known/agent-card.json`. Agents self-describe capabilities, authentication requirements, and supported protocols. Part of the A2A specification.
- [AID — Agent Identity & Discovery](https://github.com/agent-community/agent-id) — Radically minimal DNS TXT record-based bootstrap. Agents publish identity and endpoint info via DNS. Protocol-agnostic.
- [agents.json](https://docs.wild-card.ai/) — Structured API workflow contracts on OpenAPI. Agents publish capability manifests at `/.well-known/agents.json`. Stateless, HTTP-native.
- [ANP Agent Description Protocol](https://github.com/agent-network-protocol/agent-network-protocol) — Active and passive agent discovery using JSON-LD. Part of the ANP full-stack protocol.
- [ERC-8004 Registry](https://eips.ethereum.org/EIPS/eip-8004) — On-chain searchable agent identity registry. Agents register as NFTs with queryable capability metadata.

---

## 💬 Communication Protocols

*How do agents talk to tools, to each other, and to users? Three complementary protocols now define the standard communication stack.*

### The Protocol Triangle

| Layer | Protocol | Purpose |
|-------|----------|---------|
| Agent ↔ Tools | **MCP** | Connect agents to external tools, data sources, and APIs |
| Agent ↔ Agent | **A2A** | Coordinate tasks across distributed agent systems |
| Agent ↔ User | **AG-UI** | Stream agent state, tool calls, and interactions to frontends |

- [MCP — Model Context Protocol](https://modelcontextprotocol.io/) — Anthropic. The standard way agents connect to external tools and data. Dynamic tool discovery, bi-directional communication, capability negotiation. 26,000+ MCP servers indexed. Donated to the Linux Foundation's Agentic AI Foundation (Dec 2025). [Spec](https://spec.modelcontextprotocol.io/) · [GitHub](https://github.com/modelcontextprotocol)
- [A2A — Agent2Agent Protocol](https://google.github.io/A2A/) — Google / Linux Foundation. Enterprise agent-to-agent communication. Three interchangeable protocol bindings (JSON-RPC 2.0, gRPC, HTTP+JSON). Task lifecycle management, streaming, push notifications. 150+ supporting organisations. [Spec](https://google.github.io/A2A/specification/) · [GitHub](https://github.com/google/A2A)
- [AG-UI — Agent–User Interaction Protocol](https://docs.ag-ui.com/) — CopilotKit. Event-based protocol connecting agents to user-facing frontends. 16 standardised event types. Transport-agnostic (SSE, WebSocket, HTTP binary). 1st-party support from Microsoft, Google, AWS, LangGraph, and more. [GitHub](https://github.com/ag-ui-protocol/ag-ui)

### Additional Protocols

- [ANP — Agent Network Protocol](https://github.com/agent-network-protocol/agent-network-protocol) — Full-stack decentralised agent protocol with DID identity and meta-protocol negotiation. Agents can dynamically create new communication protocols at runtime.
- [AITP — Agent Interaction & Transaction Protocol](https://docs.near.ai/aitp/) — NEAR AI. Agent commerce and transactions with marketplace primitives. Thread-based conversations with typed message payloads.
- [Agent Protocol](https://github.com/AI-Engineer-Foundation/agent-protocol) — AI Engineer Foundation. Minimal REST interface for agent testing and benchmarking. Simple, unopinionated.

---

## 💰 Payments & Commerce

*How do agents pay for services and conduct transactions?*


- [x402](https://www.x402.org/) — Coinbase. Internet-native payments via HTTP 402. USDC on Base L2. Designed for micropayments — agents pay per API call, per byte, per inference. 500K+ weekly transactions. [GitHub](https://github.com/coinbase/x402)
- [AP2 — Agent Payments Protocol](https://ap2-protocol.org/) — Google + 60 organisations (PayPal, Mastercard, Visa). Open extension for A2A and MCP. Uses Verifiable Digital Credentials (VDCs) for cryptographic proof of purchase intent. Three mandate types: Intent (human-not-present authority), Cart (human-present authorisation), Payment (network signalling). [Spec](https://ap2-protocol.org/specification/) · [GitHub](https://github.com/google-agentic-commerce/AP2)
- [MPP — Machine Payments Protocol](https://datatracker.ietf.org/doc/draft-ryan-httpauth-payment/) — Tempo Labs / Stripe. IETF HTTP Authentication Scheme for machine-to-machine payments. Payment-method agnostic. Uses HTTP 402 status code with `Payment` header.
- [Visa Trusted Agent Protocol (TAP)](https://developer.visa.com/capabilities/trusted-agent-protocol) — Agent verification bridge between traditional card networks and crypto-native payments. x402 compatibility.

---

## 🛡️ Governance & Security

*How do we control, monitor, and secure what agents do?*

### Governance Frameworks

- [Microsoft Agent Governance Toolkit](https://github.com/microsoft/agent-governance-toolkit) — Open-source (MIT). Seven packages: policy engine, execution rings, trust scoring, compliance mapping, MCP Security Scanner, DID + SPIFFE/SVID identity. Runtime security for agents.
- [Google Secure AI Framework (SAIF) for Agents](https://services.google.com/fh/files/misc/secure_ai_framework_for_agents.pdf) — Hybrid defence-in-depth: deterministic policy engines + reasoning-based defences. Three principles: well-defined human controllers, limited powers, observable actions.
- [ServiceNow AI Control Tower](https://www.servicenow.com/products/ai-control-tower.html) — Centralised hub for managing, monitoring, and governing any AI agent (internal or third-party). Part of ServiceNow's AI Agent Fabric with native A2A + MCP support.
- [OWASP Top 10 for Agentic Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/llm-top-10-governance-doc/LLM_AI_Security_and_Governance_Checklist-v1.1.pdf) — Standardised risk taxonomy for agentic AI. Ten threat categories including goal hijacking, tool misuse, identity abuse, and supply chain compromise.

### Observability & Evaluation

- [Langfuse](https://langfuse.com/) — Open-source LLM observability. Acquired by ClickHouse (Jan 2026). 26M+ SDK monthly installs, 19 Fortune 50 clients. Tracing, evaluation, and monitoring for agent workflows.
- [Portkey](https://portkey.ai/) — AI gateway with 10B+ monthly requests. 99.9999% uptime, sub-10ms latency. 40+ pre-built guardrails for agent safety.
- [AgentOps](https://www.agentops.ai/) — Session replays and failure detection for AI agents. Two lines of code to start.
- [Arize Phoenix](https://phoenix.arize.com/) — Open-source agent observability on OpenTelemetry. Framework-agnostic tracing and evaluation.

---

## Contributing

Contributions welcome! Please read the [contribution guidelines](CONTRIBUTING.md) before submitting a PR.

If you know of a protocol, tool, or service that belongs on this list, please open an issue or submit a pull request.

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, the authors have waived all copyright and related or neighbouring rights to this work.
