# Awesome AI Agent Protocols & Verification

> A curated list of AI agent protocols organized around the **Trust Agent Stack**: Provenance, Governance, and Action.

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

---

## The Trust Agent Stack

Three layers of concern for trustworthy AI agent systems:

1. **Provenance** — *Who is acting?* Identity, origin, and discovery for both the agent and the human/organization behind it.
2. **Governance** — *What are they allowed to do?* Policy enforcement, access control, security risk management, and the trust signals (reputation, validation, attestation) that inform those decisions.
3. **Action** — *How do they affect the world?* Communication transports, tool use, and payments — anything that lets an agent produce effects.

Some protocols span multiple layers (for example, A2A provides both an Agent Card for Provenance and a task execution surface for Action). These are cross-listed with full entries in each relevant section.

---

## Contents

- [Provenance](#provenance)
  - [Human Identity](#human-identity)
  - [Agent Identity](#agent-identity)
- [Governance](#governance)
- [Action](#action)
  - [Communication / Transport](#communication--transport)
  - [Tool](#tool)
  - [Payments](#payments)
- [Protocol Comparison](#protocol-comparison)
- [Contributing](#contributing)
- [License](#license)

---

## Provenance

Identity, origin, and discovery for the entities that act in agent systems — both the agents themselves and the humans or organizations behind them.

### Human Identity

Privacy-preserving methods for proving and asserting *human* presence and identity online, enabling humans to be distinguished from (or vouch for) AI agents.

| Protocol / Paper | Authors | Description | Links |
|------------------|---------|-------------|-------|
| **World ID** | Tools for Humanity / World Foundation (Worldcoin), v4.0 2025 | Open-source decentralized Proof-of-Human (PoH) protocol that lets people prove they are unique humans without revealing their identity. Uses iris biometrics captured by the purpose-built Orb hardware combined with anonymized multi-party computation (AMPC) and zero-knowledge proofs. World ID v4.0 introduces account abstraction: a World ID becomes a record in the on-chain `WorldIDRegistry` with multiple authorized keys, supporting multi-device authenticators, key rotation, and recovery. Crucially for agent systems, it supports *agent-on-behalf-of-human* delegation, allowing AI agents to act under a revocable PoH binding while preserving per-human rate limits. | [Whitepaper](https://whitepaper.world.org/) / [Protocol v4.0 Spec](https://github.com/worldcoin/world-id-protocol/blob/main/docs/world-id-4-specs/README.md) / [Developer Docs](https://docs.world.org/world-id) |
| **Self (Self Pass)** | Self Protocol, 2025 | Privacy-first, open-source identity protocol built on zero-knowledge proofs. Self Pass verifies real-world identity attributes — age, nationality, sanctions status, proof-of-human — from passports, national IDs, Aadhaar, and KYC attestations across 60+ countries, without revealing the underlying personal data. Users verify once with the Self app, then selectively disclose attributes across any application that integrates the protocol. *(See [Provenance › Agent Identity](#agent-identity) for Self Agent ID, which extends this verification to AI agents.)* | [Docs](https://docs.self.xyz/) / [Self Pass](https://docs.self.xyz/self-pass/self-pass) |
| **Personhood Credentials** | Adler & Hitzig (OpenAI), Jain (Microsoft), et al., 2024 | Proposes privacy-preserving digital credentials proving a bearer is human without revealing identity. Uses zero-knowledge proofs for unlinkable pseudonymity. Analyzes limitations of existing countermeasures (CAPTCHAs, economic barriers, AI detection, biometrics) and addresses sockpuppets, bot attacks, and misleading agents. | [Paper](https://arxiv.org/abs/2408.07892) |

### Agent Identity

Standards for identifying, discovering, and attesting to agent identity across systems and organizations. Includes both the identity surface itself (cards, DIDs, NFTs, certificates) and the discovery mechanisms that resolve agents on the network.

| Protocol | Authors | Description | Links |
|----------|---------|-------------|-------|
| **A2A Agent Card** | Google / The Linux Foundation, 2025 | The Agent Card is A2A's identity and capability surface: a structured document describing an agent's name, skills, supported transports, endpoints, and authentication requirements. Clients use it to discover, authenticate, and select counterparties before initiating tasks. *(See [Action › Communication / Transport](#communication--transport) for the full A2A protocol.)* | [Specification (v1.0.0)](https://a2a-protocol.org/latest/specification/) |
| **ANP Identity (`did:wba`)** | GaoWei Chang / ANP Community, 2024 | ANP's Identity & Secure Communication layer defines `did:wba`, a DID method anchored in web-based authority, paired with ECDHE-based encrypted channels. Provides cryptographic agent identity decoupled from any single central registry. *(See [Action › Communication / Transport](#communication--transport) for the full ANP protocol.)* | [White Paper](https://agent-network-protocol.com/specs/white-paper) |
| **AITP Identity** | NEAR Foundation, 2025 | AITP anchors agent identity in NEAR-based decentralized accounts, enabling cross-trust-boundary interaction backed by verifiable on-chain accounts. *(See [Action › Communication / Transport](#communication--transport) for the full AITP protocol.)* | [Specification (v0.1.0)](https://aitp.dev/) |
| **Agent Identity & Discovery (AID)** | Agent Community, 2026 | Minimal, DNS-first bootstrap standard for discovering agent endpoints. Uses DNS TXT records at `_agent.<domain>` with semicolon-delimited key-value pairs. Protocol-agnostic (supports MCP, A2A, OpenAPI tokens). | [Specification (v1.2.0)](https://aid.agentcommunity.org/docs/specification) |
| **Agent Name Service (ANS)** | Huang (DistributedApps.ai), Narajala (AWS), Habler (Intuit), Sheriff (Cisco), 2025 | DNS-inspired registry for secure agent discovery and lifecycle management. Uses PKI certificates for verifiable identity, a Protocol Adapter Layer supporting A2A/MCP/ACP, and capability-aware resolution. | [Paper](https://arxiv.org/abs/2505.10609) |
| **ERC-8004 Identity Registry** | De Rossi (MetaMask), Crapis (Ethereum), Ellis (Google), Reppel (Coinbase), 2025 | The Identity Registry component of ERC-8004: an Ethereum standard for trustless agent identity using ERC-721 NFTs to anchor each agent on-chain, providing portable identity across applications. *(See [Governance](#governance) for ERC-8004's reputation and validation registries.)* | [EIP-8004](https://eips.ethereum.org/EIPS/eip-8004) |
| **Self Agent ID** | Self Protocol, 2026 | On-chain identity registry binding AI agent keys to Self Protocol human proofs. Each agent receives a soulbound ERC-721 NFT backed by a ZK passport verification, providing trustless proof-of-human for autonomous agents. Implements the ERC-8004 Identity Registry with a Proof-of-Human extension, plus matching Reputation and Validation registries. Sybil-resistant via per-human nullifiers; proofs are time-bounded (default one year or document expiry). Deployed on Celo Mainnet/Sepolia with SDKs in TypeScript, Python, and Rust. *(See [Provenance › Human Identity](#human-identity) for Self Pass, the underlying human verification layer.)* | [Overview](https://docs.self.xyz/self-agent-id/overview) / [GitHub](https://github.com/selfxyz/self-agent-id) / [Live App](https://selfagentid.xyz) |

---

## Governance

Policy enforcement, access control, security risk management, and the trust signals (reputation, validation, attestation) that inform those decisions. This layer is *what an agent is allowed to do*, and *what evidence we have that it should be allowed*.

| Tool / Framework | Authors | Description | Links |
|------------------|---------|-------------|-------|
| **Agent Governance Toolkit** | Microsoft, 2025 | Runtime governance infrastructure for autonomous AI agents. Provides deterministic policy enforcement (<0.1ms latency), Ed25519 cryptographic identity, SPIFFE/SVID zero-trust identity, 4-tier privilege rings with execution sandboxing, and SRE tooling (SLOs, error budgets, chaos engineering). Covers all 10 OWASP Agentic Top 10 risks. Includes an MCP Security Scanner for tool poisoning detection. SDKs for Python, TypeScript, .NET, Rust, and Go. | [GitHub](https://github.com/microsoft/agent-governance-toolkit) |
| **ERC-8004 Reputation & Validation** | De Rossi (MetaMask), Crapis (Ethereum), Ellis (Google), Reppel (Coinbase), 2025 | The Reputation and Validation Registry components of ERC-8004. Supports tiered trust proportional to value at risk — from reputation systems through stake-secured re-execution, zkML proofs, and TEE attestations. *(See [Provenance › Agent Identity](#agent-identity) for ERC-8004's identity registry.)* | [EIP-8004](https://eips.ethereum.org/EIPS/eip-8004) |

---

## Action

Anything that lets an agent affect the world: communication with other agents and services, tool use, and payments.

### Communication / Transport

Standards for how agents exchange information — with each other, with tools, and with users — including the underlying transport substrates (JSON-RPC, gRPC, REST, DIDs, DNS).

| Protocol | Proposer | Description | Links |
|----------|----------|-------------|-------|
| **Agent2Agent (A2A)** | Google / The Linux Foundation, 2025 | Open standard for communication between independent AI agent systems. Three-layer design: canonical data model (Protocol Buffers), abstract operations, and protocol bindings (JSON-RPC, gRPC, HTTP/REST). Supports async tasks, streaming, push notifications, and human-in-the-loop workflows. *(See [Provenance › Agent Identity](#agent-identity) for the Agent Card identity surface.)* | [Specification (v1.0.0)](https://a2a-protocol.org/latest/specification/) |
| **Agent Network Protocol (ANP)** | GaoWei Chang / ANP Community, 2024 | Open-source protocol for secure, decentralized agent communication. Three-layer architecture: Identity & Secure Communication, Meta-Protocol (AI-driven protocol negotiation), and Application layer (Agent Description Protocol in JSON-LD). Includes discovery, description, and transaction specifications. *(See [Provenance › Agent Identity](#agent-identity) for `did:wba` identity.)* | [White Paper](https://agent-network-protocol.com/specs/white-paper) |
| **Agent Interaction & Transaction Protocol (AITP)** | NEAR Foundation, 2025 | Enables agents to communicate securely across trust boundaries. Built on Chat Threads (inspired by OpenAI Threads API) and an extensible Capabilities system for structured interactions. Supports multimodal input, generative UI, payments, and human-in-the-loop. Vision: HTTP/HTML equivalent for agent-to-agent commerce. *(See [Provenance › Agent Identity](#agent-identity) for AITP identity, and [Payments](#payments) for its payment capabilities.)* | [Specification (v0.1.0)](https://aitp.dev/) / [Vision](https://aitp.dev/vision) |
| **Agent Protocol** | AI Engineer Foundation, 2024 | REST API specification (OpenAPI 3.0) defining a standard control interface for agents. Core abstractions: Tasks (goals), Steps (units of work), and Artifacts (outputs). Supports multipart file upload/download, CORS, and flexible auth (API keys, OAuth 2.0, JWT). | [Specification (v1)](https://agentprotocol.ai/specification/) |
| **agents.json** | Wild Card AI, 2025 | Open specification that extends OpenAPI to formally describe contracts for LLM-agent interactions. Introduces Flows (multi-step API call sequences) and Links (action stitching). Discoverable at `.well-known/agents.json`. Stateless by design, requiring minimal changes to existing APIs. | [Specification (v0.1.0)](https://github.com/wild-card-ai/agents-json) |

### Tool

Standards for exposing tools, resources, and capabilities to agents so they can invoke them as part of their reasoning.

| Protocol | Proposer | Description | Links |
|----------|----------|-------------|-------|
| **Model Context Protocol (MCP)** | Anthropic, 2024 | Standardizes integration between LLM applications and external data sources/tools. Three-component architecture (host, client, server) using JSON-RPC 2.0. Servers expose resources, prompts, and tools; clients provide sampling, roots, and elicitation. Inspired by Language Server Protocol. | [Architecture](https://modelcontextprotocol.io/specification/2025-11-25/architecture) / [Specification](https://modelcontextprotocol.io/specification/2025-11-25) |

### Payments

Protocols enabling agents to send and receive payments as part of their actions in the world. Both protocols listed here repurpose the long-dormant HTTP `402 Payment Required` status code as a payment-challenge surface, but differ in scope: x402 ships a Coinbase-led reference SDK and ecosystem, while MPP is an IETF-track HTTP authentication scheme proposed by Tempo Labs and Stripe.

| Protocol | Authors | Description | Links |
|----------|---------|-------------|-------|
| **x402** | Reppel, Caspers, Leffew, Organ, Kim, Dalal (Coinbase), 2025 | Open payment standard that uses HTTP `402 Payment Required` to let AI agents and web services autonomously pay for API access, data, and digital services without API keys, accounts, or subscriptions. V1 (May 2025) shipped single-call exact payments using stablecoins like USDC on Base; V2 (December 2025) added a CAIP-based unified multi-chain payment interface, dynamic `payTo` routing, wallet-based reusable sessions (SIWx), automatic discovery, and a plugin-driven SDK. Now stewarded by the independent x402 Foundation (with Coinbase and Cloudflare). | [V1 Whitepaper](https://www.x402.org/) / [V2 Announcement](https://www.x402.org/writing/x402-v2-launch) / [GitHub](https://github.com/coinbase/x402) |
| **Machine Payments Protocol (MPP)** | Ryan, Moxey, Meagher (Tempo Labs), Weinstein, Kaliski (Stripe), 2026 | Open protocol for machine-to-machine payments that defines a `Payment` HTTP authentication scheme on top of HTTP `402`, submitted as IETF Internet-Draft `draft-ryan-httpauth-payment-01`. Payment-method agnostic — stablecoins, cards, and bank transfers all flow through one interface — with idempotency, security, and receipts as first-class primitives. Servers issue a `WWW-Authenticate: Payment` challenge; clients reply with `Authorization: Payment` containing a Credential, and successful responses return a `Payment-Receipt`. Reference SDKs maintained by Tempo Labs and Wevm. | [Overview](https://mpp.dev/overview) / [IETF Draft](https://datatracker.ietf.org/doc/draft-ryan-httpauth-payment/) / [paymentauth.org](https://paymentauth.org/) |

---

## Protocol Comparison

| Protocol | Layer(s) | Type | Transport | Identity | Discovery | Trust Model |
|----------|----------|------|-----------|----------|-----------|-------------|
| Personhood Credentials | Provenance | Human identity | Cryptographic / ZK | Issuer-anchored | N/A | Issuer + ZK-proof |
| World ID | Provenance | Human identity (PoH) | On-chain `WorldIDRegistry` + ZKP | Iris biometric via Orb, multi-key authenticators | Authenticator-mediated | AMPC + ZK uniqueness proof |
| Self (Self Pass) | Provenance | Human identity | ZK proofs / Self app | Government ID / passport-backed | Self app | Selective ZK attribute disclosure |
| Self Agent ID | Provenance + Governance | Agent identity (PoH-bound) | Soulbound ERC-721 on Celo | Self human-PoH binding | On-chain registry | ERC-8004 + Proof-of-Human extension |
| A2A | Provenance + Action | Inter-agent | JSON-RPC, gRPC, REST | Agent Cards | Agent Cards / OpenAPI | Enterprise auth |
| ANP | Provenance + Action | Inter-agent | HTTP, DID-based | `did:wba` + ECDHE | `.well-known` + search services | Zero-trust, multi-DID |
| AITP | Provenance + Action | Inter-agent | HTTP | NEAR identity | Registry / intent resolution | Trust boundaries + capabilities |
| AID | Provenance | Discovery | DNS TXT | Ed25519 public key | DNS-first (`_agent.`) | Auth hints (PAT, OAuth, mTLS, JWT) |
| ANS | Provenance | Discovery / Registry | HTTP | PKI certificates, DID | DNS-inspired registry | Certificate-based |
| ERC-8004 | Provenance + Governance | Trust / Identity | Ethereum | ERC-721 NFT | On-chain registry | Tiered (reputation, stake, zkML, TEE) |
| Agent Governance Toolkit | Governance | Runtime governance | In-process / SDK | Ed25519, SPIFFE/SVID | N/A | Policy + cryptographic identity |
| MCP | Action (Tool) | Context-oriented | JSON-RPC 2.0, HTTP | Host-managed | Capability negotiation | User consent |
| agents.json | Action (Comm) | API bridge | HTTP (OpenAPI) | Service-level | `.well-known/agents.json` | API auth (keys, OAuth, Bearer) |
| Agent Protocol | Action (Comm) | Execution | REST (OpenAPI 3.0) | Implementation-defined | N/A | API keys, OAuth 2.0, JWT |
| x402 | Action (Payments) | M2M payment | HTTP 402 + headers | Wallet-based (SIWx, CAIP-122) | V2 Discovery extension | Onchain settlement (multi-chain) |
| MPP | Action (Payments) | M2M payment | HTTP 402 + `Payment` auth scheme | Payment-method credentials | N/A | Method-agnostic (stablecoin, card, bank) |

---

## Contributing

Contributions welcome! Please read the [contributing guidelines](CONTRIBUTING.md) first.

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)
