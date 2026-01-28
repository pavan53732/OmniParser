# 🪐 OmniParser: The Architect Edition

**"Zero-Loss Markdown to AI Task Generator & Project Orchestrator"**

**One system. One law. Scales from one human to one organization.**

> **Note to AI Agents:** You are operating under the **OmniParser Protocol**. Every line of code must be tethered to a specific requirement ID. Do not hallucinate features. Do not omit lines from the Markdown specs. Failure to validate against the "Master Law" will result in Task Rejection.

---

## 🛠 Overview

OmniParser is a universal, local-first **Project Intelligence Hub** built for 2026, with Windows as the sovereign reference platform — designed to scale seamlessly from solo creators to regulated organizations using the same constitutional system. It bridges the gap between raw human intent (Markdown) and granular AI execution by transforming documentation into a **Constitutional Law** that governs a parallel swarm of **AI Providers governed by certification, policy, and budget enforcement**.

---

## ⚙️ Phase 0 — Implementation Law (Canonical Tech Stack & Runtime)

This section defines the **non-negotiable system architecture**. Any implementation that deviates from this law is considered a **Fork**, not a compliant OmniParser.

### Core Architecture Model

OmniParser is a **Local-First, Desktop-Controlled, Service-Oriented System** composed of four sovereign runtimes:

```
┌────────────┐
│   UI Shell │  (Desktop Client)
└─────┬──────┘
      │ IPC / gRPC
┌─────▼──────┐
│   Core Law │  (State Machine + Spec Engine + Orchestrator)
└─────┬──────┘
      │ Task Bus
┌─────▼──────┐
│ Exec Broker│  (Sandbox + CLI + Provider I/O)
└─────┬──────┘
      │ Signed Events
┌─────▼──────┐
│  Data Plane│  (Ledger + Vectors + Snapshots)
└────────────┘
```

All communication paths are **typed, versioned, and cryptographically signed**.

### Provider Selection Law (Global)

OmniParser does not enforce a minimum or maximum number of Providers.

Users may enable any combination of Cloud, Local, or CLI Providers.

System execution is governed by:
- Provider state (DISCOVERED / VALIDATED / CERTIFIED / REGISTERED / ACTIVE / REVOKED_ENDPOINT / REVOKED_PROVIDER)
- Health state
- Policy and budget constraints

**Provider lifecycle and routing visibility are governed by ProviderState.**
**Execution eligibility is governed solely by `ProviderState = ACTIVE`.**

No Provider may execute tasks unless it follows:
DISCOVERED → VALIDATED → CERTIFIED → REGISTERED → ACTIVE

### Provider State Machine (Canonical)

```
ProviderState:
  DISCOVERED         → Endpoint exists and is reachable
  VALIDATED          → Health checks passed, contract compliance confirmed
  CERTIFIED          → Authority signature issued by Core Law
  REGISTERED         → Policy evaluation passed, health verified, eligible for routing
  ACTIVE             → Execution-eligible (CERTIFIED + REGISTERED + POLICY_PASS + HEALTHY)
  REVOKED_ENDPOINT   → Endpoint Instance ID invalidated, Logical Provider returns to DISCOVERED
  REVOKED_PROVIDER   → Logical Provider blocked from all operations (terminal)
```

**State Transition Authority:** Only Core Law may transition Providers between states. The Execution Broker may propose state changes, but Core Law must validate and sign all transitions.

**Registration Rule:**
CERTIFIED Providers enter REGISTERED state only if:
- Policy evaluation passes (PII, domain, network, budget class)
- Health status = HEALTHY
- Registry integrity = HEALTHY

REGISTERED Providers may be downgraded to CERTIFIED (without revocation) if:
- Health degrades
- Policy changes
- Budget class changes

**ACTIVE State Definition:**
```
ACTIVE = CERTIFIED + REGISTERED + POLICY_PASS + HEALTHY
```

Only ACTIVE Providers may execute tasks or participate in quorum.

### Execution Eligibility Law (Canonical)

**Swarm execution requires ≥ 1 Provider in ACTIVE state.**

System may operate in DISCOVERY, SIMULATION, and SPEC modes without execution capability when this requirement is not met.

**Quorum Law:** Only Providers with `ProviderState = ACTIVE` may participate in quorum voting or consensus-based task approval.

### Policy Precedence Law (Canonical)

**Enforcement Order:**
1. **Security / Legal / PII Policy Constraints** (non-bypassable)
2. **Provider State** (ACTIVE required for execution)
3. **Budget Enforcement** (may pause swarm, cannot override 1 or 2)
4. **Routing Optimization** (performance and cost efficiency)

Budget enforcement overrides routing optimization but **never** overrides Security, Legal, or PII policy constraints.

**Visibility Rule:**
ACTIVE indicates technical eligibility only. System execution eligibility is the conjunction of:
`ProviderState = ACTIVE AND SystemState = SPEC_LOCKED`.

### Canonical Technology Stack

**Desktop UI Layer (Human Interface)**

Purpose: Law visualization, Provider Control Panel, Diff Modal, Swarm View

- **Framework:** `Tauri` (Rust Core + Web UI)
- **UI Runtime:** `React + TypeScript`
- **Acceleration:** `CPU-Optimized Rendering` using `Canvas API` / `SVG` and `OffscreenCanvas`.
  - **Agile Rendering:** Physics calculations for the "Swarm View" and "Spatial Maps" are handled by `Web Workers` to ensure 60fps telemetry without GPU dependencies.
  - **Zero-Copy Telemetry:** Uses `SharedArrayBuffer` to stream data from Rust to JS without serialization overhead.
- **IPC Protocol:** `gRPC` over `QUIC` (via `Quinn` / `Tonic`)
- **State Management:** `Zustand` or `Redux Toolkit`
- **Theming Engine:** `CSS Variables + Tokenized Theme Law (theme.md)`

**Hard Law:** The UI **may never directly access filesystem, providers, or secrets**. All actions must go through Core Law APIs.

**Core Law Engine (System Brain)**

Purpose: Spec Engine, State Machine, Orchestrator, Budget Agent, Domain Scoring, Law Export

- **Language:** `Rust`
- **Runtime Model:** Event-driven, async (`Tokio`) + `Wasmtime (Component Model)`
  - **Software Fault Isolation:** All user logic, policy modules, and agent scripts are compiled to WebAssembly (WASM). This creates a mathematically proven memory boundary.
- **API Surface:** `gRPC` (internal), `OpenAPI` (export only)
- **Policy Engine:** `OPA (Open Policy Agent)` for RBAC + Law Validation
  - **Policy Scope:** OPA policies govern RBAC, domain enforcement, provider routing eligibility, budget overrides, and state transition authorization. Policies are evaluated inside Core Law before any state mutation.
- **State Machine Engine:** Deterministic FSM with persisted transitions
- **Cryptography:** `Dilithium (CRYSTALS-Dilithium)` for Post-Quantum signatures, `SHA-3` (Spec Version Hashes, Law Diffs)
  - **Quantum-Resilience:** Utilizes NIST-standard Post-Quantum Cryptography to ensure Law Exports remain secure against future quantum decryption capabilities.

**Hard Law:** No provider, agent, or UI component may mutate state outside the Core Law Engine.

**Execution Broker (Sandbox & Agents)**

Purpose: CLI isolation, Provider I/O mediation, Diff generation, Tool mediation

- **Container Runtime:** `Hyper-V VTL1 (Virtual Trust Level 1)` Isolation + Direct `HCS` (Host Compute Service) API calls.
  - **VTL1 Security:** Executes parts of the Broker in a Secure Mode (VTL1) that is invisible and untouchable even by a compromised OS kernel, similar to Windows Credential Guard.
  - **Silo Containers:** Uses raw HCS API to spin up "Silo" process containers in milliseconds, bypassing Docker overhead.
  - **Capability Fallback:** If Hyper-V is unavailable (e.g., Windows Home), Broker enters SOFTWARE_SANDBOX mode using Restricted Tokens + Job Objects + Filesystem Overlay + Network Firewall Rules. Providers in DISCOVERED or VALIDATED states are disabled in this mode.
- **Sandbox Policy Engine:** Windows Defender Application Control (WDAC) + Restricted Tokens + Job Objects + Hyper-V isolation
  - **Enforcement Model:** WDAC governs OmniParser system binaries only. Dynamic CLI agent execution is enforced via Restricted Tokens + Job Objects + Per-Process ACL sandboxing inside Hyper-V containers. WDAC policies are never modified at runtime.
- **Filesystem Isolation:** Read-only mounts + Diff overlay
  - **Scope Rule:** Only files within the active workspace root may be mounted read-write into the Diff overlay. System, user home, and Program Files directories are always mounted read-only.
- **CLI Wrapping Layer:** `Rust` adapters for each agent
- **Local AI Runtime (Provider Tier):** `Candle` (Hugging Face Rust ML Framework) with `CPU BLAS` (Basic Linear Algebra Subprograms) + `WASM-SIMD` support.
  - **Reflex Agent Mode:** OmniParser can download quantized `.gguf` models and run them **in-process** using optimized CPU vector instructions (AVX2/AVX-512). This provides instant "Reflex" tasks (syntax checking, ghost tests, diff summarization) on *any* modern laptop without requiring a GPU.

**Hard Law:** All side effects must emit a **Signed Execution Event** before results are accepted by Core Law.

**Execution Signing Authority:** Execution Events must be signed by a Broker Key pair generated at first boot and sealed inside the Secure Agentic Vault. Core Law must verify the Broker signature chain before accepting any Execution, Diff, or Provider result. Broker keys may only be rotated with Owner signature and invalidate all pending tasks.

**Provider Abstraction Layer (PAL)**

Purpose: Normalize all AI providers

- **Transport:** HTTPS (Cloud), HTTP (Local), STDIO → HTTP Bridge (CLI)
- **Schema Validation:** `JSON Schema + Protobuf`
- **Health & Discovery:** provider-native discovery APIs, optional `/models` polling, and certified static manifest overlay, with failure scoring

**Data Plane (Memory & Law Ledger)**

Purpose: Audit, Vector Memory, Snapshots, Export

- **In-Memory Analytics:** `Apache Arrow` format for all zero-copy, columnar data reads. Uses `SIMD` optimizations to scan millions of rows instantly using standard CPU vector extensions.
- **Audit Ledger:** `SQLite (WAL mode)` with cryptographically chained entries (each record stores `prev_hash`, forming an append-only hash chain)
  - **Ledger Identity Rule:** The first ledger entry must include the System Genesis ID (derived from the Owner Key fingerprint + install timestamp). All subsequent entries must include this Genesis ID in their hash payload. Ledgers with mismatched Genesis IDs must be rejected during Law Re-Import.
- **Vector Store:** Embedded `LanceDB` (Python-free, Rust-native) with `CPU-Optimized HNSW Indexing`.
  - **Why LanceDB:** Unlike Qdrant, LanceDB runs entirely in-process (no server overhead) and is optimized for `Apache Arrow` data.
  - **CPU Performance:** Uses Hierarchical Navigable Small World (HNSW) graphs optimized for CPU cache locality, enabling lightning-fast semantic search without needing a GPU accelerator.
  - **Determinism Rule:** Vector embeddings are excluded from Spec Version Hash and reproducibility guarantees. Snapshots must include vector state for restoration but vectors are treated as advisory, not authoritative law.
  - **Replica Rule:** In Governed Mode, vector generation must be centralized to the Authority Leader. Follower nodes may query vectors but must not generate or mutate embedding state.
- **Snapshot Store:** `Zstandard-compressed archives`
- **Search Engine:** Embedded `Meilisearch` binary (bundled, no external service required)

**Hard Law:** All persisted data must be reproducible from Law + Ledger + Snapshots.

### Event Backbone

All system actions emit events:

```rust
Event (Canonical Schema v1) {
  id: UUID
  schema_version: u32
  type: SPEC | TASK | EXECUTION | DIFF | APPROVAL | EXPORT | FAILURE | DISCOVERY
  source: UI | CORE | BROKER
  causal_refs: UUID[]
  provider_id?: string
  provider_state?: "discovered" | "validated" | "certified" | "registered" | "active" | "revoked_endpoint" | "revoked_provider"
  discovery_confidence?: "unauthenticated" | "authenticated" | "verified"
  hash: SHA-3
  signature: {
    broker: Dilithium
    core: Dilithium
  }
  timestamp: hybrid_logical (HLC)
}
```

**HLC Definition:**  
Hybrid Logical Clock is encoded as `{ wall_time_unix_ms: u64, counter: u32, node_id: u16 }` and serialized in little-endian binary form before hashing and signing.

**HLC Node Identity Rule:**
In Governed Mode, node_id is assigned from the Raft cluster membership index and MUST be unique within the authority group.
In Personal and Team Modes, node_id = 0x0001.

**Schema Extension Rule:** `DISCOVERY_EVENT` is a specialization of `Event` with `type = DISCOVERY` and additional required fields `{endpoint_hash, auth_used, response_hash, model_count, discovery_confidence}`.
DISCOVERY_EVENT fields extend the canonical Event schema and MUST be accepted by all schema validators as a valid specialization.

**Discovery Event Authority:** DISCOVERY_EVENT must be signed by the **Execution Broker Key** and countersigned by Core Law before Ledger commit. Core Law MUST verify the Broker signature and attach its own cryptographic signature before the event is written to the Audit Ledger. This ensures discovery telemetry follows the same authority chain as execution events.

**Provider Event Rule:** Providers may only return responses to the Execution Broker. All externally sourced events must be re-issued, signed, and attributed by the Broker before entering the Audit Ledger.

**Schema Evolution Rule:** Core Law must reject any Event with a schema_version greater than the current supported version unless an Architect or Owner explicitly enables forward-compatibility mode. Downgrade of schema_version is prohibited.

Events are append-only and form the **Causal Chain of Truth**.

### Governance Modes (Single System, Scaled Authority)

**Dependency Boundary Rule:** Personal and Team Modes must operate with zero external services. Governed Mode may bind to external infrastructure (PostgreSQL, Raft peers, Central OPA) provided OmniParser itself does not bundle or require these for installation. External services are treated as optional authority backends, not runtime dependencies of the binary.

**Personal Mode (Default)**
- UI + Core + Broker + Data Plane run on the same machine
- No cloud dependency required
- All secrets stored in Secure Agentic Vault (DPAPI/TPM-backed on Windows)

**Team Mode**
- Core runs locally
- Providers + Vector DB optional in private cloud

**Governed Mode (Regulated / Institutional / High-Compliance Use)**
- Core replicated (Raft consensus)
- Shared Audit Ledger (PostgreSQL + cryptographic chaining)
- Central Policy Server (OPA)
- **Authority Leader Rule:** Only the Raft-elected leader node may emit signed State Transitions and Spec Version Hashes. Follower nodes may validate but never author authority events.

**Mode Unification Law**

All Governance Modes operate on the **same OmniParser binary, laws, and architecture**.

Modes differ only in:
- Authority model (single-user vs. multi-approver)
- Policy enforcement level
- Audit and compliance strictness
- Provider certification and trust requirements

There is no consumer, team, or enterprise edition of OmniParser — only different **governance intensities** applied to the same constitutional system.

### Windows Distribution & Packaging Law (Non-Negotiable)

OmniParser must ship as a **self-contained Windows application with no developer or AI-runtime dependencies**. End users must not be required to install developer tools, runtimes, containers, or model servers to operate the system.

**Distribution Guarantee**

A compliant OmniParser build MUST:

- Run on a clean Windows system with **no pre-installed dependencies**
- Operate in **offline mode** with full Law Engine, Broker, Vault, and certified Local Provider functionality (when available)
- Degrade gracefully when cloud Providers are unavailable
- Support both **single-user** and **enterprise-managed** installation flows

**Installer Formats**

OmniParser SHALL be distributed as:

- **`.exe` Installer** — Consumer / Single-user mode
- **`.msi` Installer** — IT-managed or multi-user deployment (schools, labs, studios, teams, companies, regulated environments)

Both formats must be built from the **same signed binary artifacts**.

**Mandatory Installer Payload**

The installer MUST embed:

- **UI Shell:** `omniparser.exe`, embedded Web UI assets, gRPC client stubs, Theme Law engine
- **Core Law Engine:** `core-law.exe`, OPA policy runtime, State machine definitions, Law schema bundles, Law export/import tools
- **Execution Broker:** `broker.exe`, Sandbox profiles, CLI adapters, Diff engine
- **Provider Runtime Layer:** Provider Discovery Engine, PAL HTTP / STDIO adapters, Capability Certification Pipeline, Model Registry Cache, Sandbox Enforcement Profiles, **Discovery Adapter Registry**
- **Data Plane:** SQLite engine, `Apache Arrow` runtime, Vector store binary (LanceDB), Search engine (Meilisearch), Snapshot tooling
- **Secure Agentic Vault:** Windows DPAPI integration, TPM-backed key support (if available), Encrypted keystore
- **System Services:** Background supervisor, Crash recovery service, Auto-update agent

**Provider Discovery & Certification Law (Non-Negotiable)**

OmniParser MUST NOT bundle, embed, or distribute AI engines, model servers, or CLI agents.

Instead, OmniParser operates as a **Sovereign Provider Control Plane** and MUST enforce the following lifecycle:

### Pre-Authentication Live Discovery Law (MANDATORY WHERE SUPPORTED)

OmniParser MUST support **unauthenticated, read-only provider discovery** when a Provider exposes a public or semi-public model catalog endpoint.

**Discovery Authority Model**

Providers are classified into two discovery classes:

```
DISCOVERY_CLASS:
  PUBLIC_CATALOG
  AUTH_GATED
```

**PUBLIC_CATALOG Providers**

Providers that expose model metadata without requiring user credentials.

OmniParser MUST:
- Allow `/models` or equivalent endpoint calls **without API keys**
- Mark results as: `trust.discoveryConfidence = "unauthenticated"`
- Prohibit task execution until certification + auth is complete

**AUTH_GATED Providers**

Providers that require authentication before model listing.

OmniParser MUST:
- Require Secure Vault authorization
- Mark discovery as: `trust.discoveryConfidence = "authenticated"`

**Discovery Safety Rule**

Models discovered without authentication:
- MAY appear in UI
- MAY be used for **capability planning and routing simulation**
- MUST NOT be eligible for execution
- MUST NOT be eligible for quorum voting
- MUST NOT be eligible for budget enforcement

**1. Discover**

- Scan for running Local AI endpoints (e.g., `http://localhost:11434`)
- Detect installed CLI agents via binary path resolution
- Probe MCP servers and Logical Providers and record current ProviderState
- Record provisional endpoints and binaries in ProviderState = DISCOVERED

**2. Validate**

- Execute health checks (`/models`, `--version`, sandbox execution test) on Providers in ProviderState = DISCOVERED
- Verify binary signatures where available
- Confirm full PAL contract compliance

**Lifecycle State Definitions:**
- **DISCOVERED:** Endpoint exists and is reachable
- **VALIDATED:** Health checks passed, contract compliance confirmed
- **CERTIFIED:** Authority signature issued by Core Law

**Conditional Discovery Rule:**  
Providers in `DISCOVERY_MODE = MANUAL` are considered *Discovered* once base endpoint reachability and authentication method are confirmed. Validation occurs as a separate subsequent step.

**3. Certify**

- Assign a **Logical Provider ID**
- Transition Provider to **CERTIFIED** state
- Generate a **Capability Manifest** including:
  - Discovery mode
  - Base URL hash
  - TLS fingerprint (if enabled)
  - Cost model classification
- Store a **Certification Hash** in the Audit Ledger

**Certification Authority Rule:** Provider Certifications must be signed by the Core Law Authority Key. The Execution Broker may propose certification artifacts, but only Core Law may issue, sign, or revoke a Certification Hash. Certification keys are generated at first boot, stored in the Secure Agentic Vault, and bound to the Owner identity.

**Endpoint Mutation Rule:** If Base URL hash or TLS fingerprint changes, Provider MUST transition to REVOKED_ENDPOINT state and return to DISCOVERED state with the same Logical Provider ID but new Endpoint Instance ID.

**REVOKED_ENDPOINT Transition Rule:**
When a Provider enters REVOKED_ENDPOINT:
- Endpoint Instance ID is invalidated in the Registry and Ledger
- Certification Hash is marked STALE
- All cached model manifests are purged
- Core Law automatically transitions the Logical Provider to DISCOVERED
- A full VALIDATED → CERTIFIED → REGISTERED → ACTIVE cycle is required before execution is re-enabled

**Certification Hash State Rule:**
STALE certification hashes:
- Remain in the Audit Ledger for historical verification
- Are excluded from Provider Registry caches
- MUST NOT be referenced by any ACTIVE or REGISTERED Provider
- Are rejected by Law Export as valid authority proofs

**4. Register**

- Insert Provider into the live Provider Registry
- Apply policy gates (PII, domain restrictions, budget class, routing eligibility)
- Enable quorum and fallback participation

**5. Revoke**

- Automatically de-register Providers that fail health, policy, or trust checks
- Mark **Endpoint Instance ID** as REVOKED_ENDPOINT (non-terminal, returns to DISCOVERED) or REVOKED_PROVIDER (terminal)
- **Logical Provider ID** remains reserved for fallback inheritance in REVOKED_ENDPOINT case
- Trigger **Swarm Revalidation**

**Revocation Authority Rule:**
- REVOKED_ENDPOINT: Endpoint-level failure (URL change, TLS mismatch, transient security issue) → Logical Provider may re-enter lifecycle
- REVOKED_PROVIDER: Identity-level failure (Owner revocation, persistent policy violation, cryptographic compromise) → Terminal state

**Provider Identity Model:**
- **Logical Provider ID:** Permanent identity, survives revocation, inheritable by fallback endpoints
- **Endpoint Instance ID:** Bound to specific Base URL + TLS fingerprint, revoked on mutation
- Fallback endpoints inherit **Logical Provider ID** but receive new **Endpoint Instance ID**

**Hard Law:** No Provider may execute a task unless its `ProviderState = ACTIVE` (CERTIFIED + REGISTERED + POLICY_PASS + HEALTHY).

**Canonical Install Layout**

System Scope:
```
C:\Program Files\OmniParser\
├── omniparser.exe
├── core-law.exe
├── broker.exe
├── pal\
├── vault\
├── providers\
│   ├── registry\
│   ├── cache\
│   └── certifications\
│       ├── manifests\
│       ├── fingerprints\
│       └── revocations\
├── data\
│   ├── ledger\
│   ├── vectors\
│   └── snapshots\
├── policy\
├── services\
└── version.json
```

User Scope:
```
C:\Users\%USERNAME%\AppData\Local\OmniParser\
├── workspace\
├── logs\
├── cache\
└── temp\
```

**Registry Authority Rule:**  
The Audit Ledger is the system of record. Provider Registry files and certification manifests are caches and must be fully reconstructible from Ledger entries on startup. Core Law must rebuild the live Provider Registry from the Ledger before allowing Provider execution.

**Registry Recovery Rule:**  
If Provider Registry reconstruction fails, the system MUST enter QUARANTINED state and allow only Law Export and Ledger Repair operations until integrity is restored.

**Quarantine Rule:**
When RegistryState = QUARANTINED:
- No Virtual Providers may be instantiated
- No fallback routing may occur
- No MCP servers may inject context
- UI is limited to Export, Ledger Repair, and Policy View

**Execution Override Rule:**
When RegistryState = QUARANTINED, all Providers are treated as execution-ineligible regardless of ProviderState.

**Windows Security Binding**

OmniParser MUST integrate with native Windows security primitives:

- **Authenticode signing** for all executables and installers, with EV certificates where supported by the distribution channel
- **UAC Elevation** for service installation
- **Windows Defender Trust Registration**
- **DPAPI + TPM** for secret storage
- **Restricted Tokens + Job Objects** for sandboxing
- **Windows Sandbox / Hyper-V Containers** for high-risk CLI execution

**First-Run Boot Protocol**

On first launch, OmniParser MUST:

1. Validate system capabilities (CPU, RAM, disk, virtualization)
2. Initialize Secure Agentic Vault
3. Register background services
4. Create workspace directory
5. Prompt for:
   - Provider discovery scan
   - Provider certification & enablement
   - Governance policy import (optional)

**Auto-Update Law**

OmniParser MUST implement:

- Cryptographically signed update manifests (signed by Owner Key or delegated Organizational Update Key recorded in the Audit Ledger)
- Delta-based binary updates
- Automatic rollback on failed update
- Governance override via private update endpoints or WSUS-compatible feeds

**Governed Deployment Binding**

The `.msi` package MUST support:

```
msiexec /i omniparser.msi /qn
```

And allow:

- Pre-seeded policy bundles
- Pre-configured Provider Registry
- Cloud Provider disablement via org policy

### Compliance Binding

Any implementation claiming to be **OmniParser-Compatible** must:

- Implement the **PAL Interface**
- Enforce the **State Machine**
- Persist a **Cryptographically Signed Audit Ledger**
- Support **Law Export & Re-Import**
- Distribute as a self-contained, signed Windows installer with no embedded AI engines or external runtime dependencies

Failure to meet these conditions classifies the system as a **Derivative**, not OmniParser.

**Implementation Law Immutability:** Phase 0 may only be modified by Owner authority. Any change forces full system re-certification and invalidates all prior Law Exports.

---

## 📖 Terminology Canon

To prevent interpretation drift across implementations, OmniParser defines the following canonical terms:

- **Provider:** A logical AI service entity capable of executing tasks (Cloud, Local, or CLI)
- **Endpoint:** The physical network address or executable path of a Provider
- **Adapter:** Canonical system software component implementing the Provider Abstraction Layer (PAL) contract for a specific Provider class. Adapters are zone-neutral and not subject to trust classification.
- **Logical Provider ID:** Persistent identifier for a Provider, independent of endpoint changes
- **Endpoint Instance ID:** Rotatable binding for a specific endpoint configuration (Base URL + TLS fingerprint)
- **Certification Hash:** Cryptographic proof of Provider validation, signed by Core Law Authority Key
- **Registry State:** Operational health status of the Provider Registry (HEALTHY, TEMPORARY_DEGRADED, QUARANTINED)
- **Discovery Mode:** Method by which Provider models are enumerated (live, manual, static)
- **Provider State:** Canonical lifecycle and trust state of a Logical Provider (DISCOVERED, VALIDATED, CERTIFIED, REGISTERED, ACTIVE, REVOKED_ENDPOINT, REVOKED_PROVIDER)
- **Provider Status (UI Alias):** Presentation-only label derived from ProviderState:
  - CERTIFIED → ProviderState ∈ {CERTIFIED, REGISTERED, ACTIVE}
  - UNCERTIFIED → ProviderState ∈ {DISCOVERED, VALIDATED}
  - REVOKED → ProviderState ∈ {REVOKED_ENDPOINT, REVOKED_PROVIDER}
- **Fallback Endpoint:** Operational replacement for unreachable certified provider (participates in routing)
- **Virtual Provider:** UI-only placeholder for visualization in simulation mode (never executes)
- **Discovery Class:** Authentication requirement for model discovery (PUBLIC_CATALOG, AUTH_GATED)
- **Discovery Confidence:** Trust level of discovered models (unauthenticated, authenticated, verified)

**Discovery Confidence Mapping:**
- `unauthenticated` → Discovered without API key or authentication
- `authenticated` → Discovered with valid authentication credentials
- `verified` → Model metadata fetched from a CERTIFIED provider (orthogonal to provider certification)

---

## 🧠 Phase 1 — Intent Interrogation Engine (Human → System Law)

This phase is designed for both technical and non-technical users. OmniParser converts natural language answers into formal system law without requiring engineering knowledge.

Before OmniParser generates a single line of code, it **interrogates the project's completeness** across all product domains. This phase ensures that vague intent cannot proceed to execution.

### Domain Coverage Requirements

Every project must address the following domains, either through explicit specifications or formal "Out of Scope" declarations:

- **Identity:** Product name, branding, visual identity, logo, color system, typography
- **UI/UX:** User interface patterns, component library, accessibility standards
- **Backend:** API architecture, data models, business logic, integrations
- **Infrastructure:** Hosting, deployment, scaling, monitoring, disaster recovery
- **Security:** Authentication, authorization, data protection, compliance requirements
- **Legal:** Terms of service, privacy policy, licensing, regulatory compliance
- **Monetization:** Pricing model, payment processing, subscription management
- **Analytics:** User tracking, performance monitoring, business intelligence

### Interrogation Protocol

When a domain is missing or incomplete:

1. **Detection:** The Spec Engine calculates a **Domain Coverage Score** across all `.md` files
2. **Blocking:** If coverage < 95%, OmniParser enters **INTERROGATING** state and blocks task generation
3. **Prompting:** A structured questionnaire is presented to the user for each incomplete domain
4. **Capture:** All answers are converted into formal requirement IDs with:
   - Domain tags
   - Version hash
   - Human approval signature
   - Source attribution ("Generated from Phase 1 Interrogation")
5. **Validation:** The system re-calculates Domain Coverage Score and repeats until threshold is met

### Domain Coverage Scoring Model

Domain Coverage Score is computed as:

For each domain D:
```
D_score = (Completed_Requirements / Total_Required_Requirements) × Weight_D
```

Global Score:
```
DomainCoverageScore = Σ(D_score) / Σ(Weight_D)
```

**Default Weights:**
- Security: 2.0
- Legal: 2.0
- Identity: 1.5
- Backend: 1.5
- Infrastructure: 1.5
- UI/UX: 1.0
- Monetization: 1.0
- Analytics: 1.0

A domain is considered "Complete" only when:
- At least one CRITICAL or HIGH requirement exists
- All acceptance_criteria are non-empty
- Domain is not explicitly marked "Out of Scope"

**Total_Required_Requirements** is defined as the greater of:
- System Baseline Requirements for that domain, or
- User-defined requirements for that domain

**Baseline Minimums:**
- Identity: 3
- UI/UX: 3
- Backend: 5
- Infrastructure: 4
- Security: 5
- Legal: 3
- Monetization: 2
- Analytics: 2

**Baseline Profile Sets:**
Baseline Minimums are selected from profiles:
- **SaaS:** Standard baselines (as above)
- **Consumer App:** Identity +2, Legal +1
- **Enterprise System:** Security +3, Legal +2, Infrastructure +2
- **Regulated System:** Security +5, Legal +5, Infrastructure +3

Axiom Bootstrapping selects the profile at project creation.

**Non-Bypassable Domains:**
The following domains may never be marked "Out of Scope":
- Security
- Legal
- Infrastructure

### Assisted Authoring Mode

When enabled, OmniParser:
- Translates free-text answers into structured requirements
- Suggests acceptance_criteria templates
- Highlights missing legal, security, and infrastructure implications
- Provides domain-specific questionnaires for non-technical users

### Design Asset Enforcement Law

If any UI-facing feature exists and no **Identity** domain spec is present, OmniParser **MUST** generate:

- Logo design task (CRITICAL priority)
- App icon task (CRITICAL priority)
- Color system task (HIGH priority)
- Typography system task (HIGH priority)

These tasks **must complete** before frontend implementation tasks are unlocked.

### Spec Promotion Rule

All Human Answers from Phase 1 generate:

- New Requirement IDs with `source: "interrogation"`
- Domain classification tags
- Version hash tied to interrogation session
- Architect-level approval signature
- Immutable audit trail entry

---

## 🏗 Phase 2 — The "Sous-chef" Architecture (Spec Design)

OmniParser doesn't just "read" text; it prepares **"Structured AI Food"** with surgical precision.

- **Recursive Folder Ingestion:** Automatically crawls the entire project directory tree. It doesn't just read files; it indexes the relationship between code, tests, and documentation to build a 360-degree project map.
- **The Internal Spec Engine (Blueprint Designer):** The logic layer that takes "messy" Markdown notes and "re-architects" them into structured Internal Specs. It effectively cleans human "brain-dumps" into a high-fidelity machine blueprint before generating tasks.
  - **Spec Schema:** Each requirement is parsed into: `{id, source_file, line_range, type, priority, domain, dependencies[], constraints[], acceptance_criteria, validation_artifacts[]}`
    - **Domain Field:** Every spec must declare its domain: `"identity" | "ui" | "backend" | "infra" | "security" | "legal" | "monetization" | "analytics"`
  - **Conflict Resolution:** When multiple `.md` files define overlapping requirements, priority follows: `ARCHITECTURE.md` > `SECURITY.md` > `API.md` > `UI.md` > other files. Explicit `@override` tags in Markdown can reverse this hierarchy.
  - **Versioning Model:** Every spec change creates a new version hash derived from a canonicalized AST of all `.md` source files. The Task Ledger tracks which code was generated from which spec version, enabling precise "out-of-sync" detection.
    - **Workspace Boundary Rule:** Only `.md` files within the active workspace root and its subdirectories are included in the Spec Version Hash.
  - **Priority Hierarchy:** Requirements are classified as `CRITICAL` (security/data), `HIGH` (core features), `MEDIUM` (enhancements), `LOW` (polish). Agents always execute higher-priority tasks first.
  - **Ghost Test Auto-Generation:** The engine doesn't just design specs; it automatically generates "spec-derived tests" based on those specs. If a Worker's code fails these tests, it is sent back for a rewrite automatically—ensuring that only code that actually works ever reaches your Diff Modal.
  - **Axiom Bootstrapping:** A library of "Pre-verified Project Laws" (templates). Instead of writing Markdown from scratch, users can click "Start with SaaS Archetype" to instantly generate 80% of the foundational requirements (Auth, DB, API patterns).
- **The GPS System (Traceability):** Every requirement is parsed into an AST with line-number metadata. Code is literally "tethered" to the Markdown source.
- **Markdown-as-Source:** OmniParser treats Markdown as a high-level declarative language. When you update a "Requirement ID" in the MD, OmniParser performs a hot-reload of the entire Task Ledger and identifies which existing code files are now "Out-of-Sync."
- **Parallel Project Graph:** Reads all `.md` files in the workspace simultaneously to detect cross-file dependencies and logic gaps.
- **Smart Chunking:** Breaks docs into "Context Partitions" to prevent AI context drift and ensure 100% focus.
- **Constraint Isolation:** Identifies ```code blocks``` as "Hard Laws" that agents cannot change, while treating text as "Fluid Tasks."
- **Isolated Subagent Windows:** Each agent operates in its own isolated context window, preventing "context clutter" where agents get confused by each other's intermediate steps. This ensures clean, focused reasoning for every task.

---

## ⚖️ The Constitutional Provider Law (Orchestration & Routing)

OmniParser doesn't just "call" an AI; it orchestrates a **Hierarchical Swarm** across a **Certified Provider Registry governed by certification, policy, and budget enforcement**.

### Adapter vs Provider Authority Law

- **Adapters** are canonical system components shipped with OmniParser and are **zone-neutral**
- **Provider Status (UI Alias):** Presentation-only label derived from ProviderState (see Terminology Canon)
- Certification, cost models, quorum eligibility, and policy enforcement are evaluated at the **Logical Provider level**, never at the Adapter level

### 🧩 Provider Abstraction Layer (PAL) — Mandatory Contract

All Providers operate behind a **single, enforceable interface**. Providers are treated as **hot-swappable plugins**, not hard dependencies. OmniParser can lose any provider at runtime without system-wide failure.

**Canonical Adapter Interface:**
```ts
ProviderAdapter {
  id: string
  type: "cloud" | "local" | "cli"

  capabilities: {
    modalities: ["text", "vision", "audio", "tooling"]
    maxContext: number
    supportsJSON: boolean
    supportsStreaming: boolean
    supportsFunctions: boolean
  }

  auth: {
    method: "api_key" | "oauth" | "oauth_browser" | "local"
    scopeModel: "global" | "per-task" | "per-agent"
  }

  limits: {
    rpm: number
    tpm: number
    maxParallel: number
  }

  discovery: {
    mode: "live" | "manual" | "static"
    endpoint?: string
    class: "PUBLIC_CATALOG" | "AUTH_GATED"
    authRequiredForModels: boolean
    discoveryConfidence: "unauthenticated" | "authenticated" | "verified"
    lastRefresh: HLC
  }

  trust: {
    state: "discovered" | "validated" | "certified" | "registered" | "active" | "revoked_endpoint" | "revoked_provider"
    costModel: "verified" | "user-declared" | "heuristic"
    certificationHash: string
  }

  health(): HealthStatus
  models(): ModelDescriptor[]
  execute(request: NormalizedRequest): NormalizedResponse
}
```

**Certification Rule:**  
ProviderState is assigned to **Logical Providers** during lifecycle transitions and stored in the Provider Registry.  
Adapters are canonical system components and are not subject to state classification.

**Discovery Confidence Rule:**
- `unauthenticated`: Model metadata fetched without authentication
- `authenticated`: Model metadata fetched with valid credentials
- `verified`: Model metadata fetched from a CERTIFIED provider (does not imply provider is certified because of discovery)

Providers that cannot implement this contract **cannot join the swarm**.

| Pattern | Role | Primary Models |
|:--------|:-----|:---------------|
| **The Manager** | Task Decomposition & Routing | Claude 3.5 Opus / Gemini 1.5 Pro |
| **The Workers** | Fast, High-Volume Code Generation | Groq (Llama 3.1), DeepSeek-V3 |
| **The Auditors** | Multi-Modal Visual & Logic Review | Gemini 1.5 Pro / GPT-4o |
| **The Fixers** | Local File-System & CLI Execution | Aider / Claude Code / Goose |

### Provider Ecosystem (Certified Cloud, Local, and CLI Providers)

## Provider Classes (Canonical, Not Vendor-Bound)

OmniParser recognizes **Provider Classes**, not vendor identities.

**Cloud Provider Class**

Any HTTPS endpoint implementing:
- Native `/models` discovery OR
- OpenAI-compatible `/v1/models` contract OR
- Certified static manifest

**Local Provider Class**

Any localhost HTTP runtime exposing:
- `/models`
- `/health`
- Execution endpoint

**CLI Provider Class**

Any executable supporting:
- `--version`
- Sandbox execution
- Diff output contract

**Vendor names MAY appear only as UI presets — never as system law.**

### Discovery Adapter Registry

OmniParser MUST ship a **Provider Discovery Adapter Registry**:

```ts
DiscoveryAdapter {
  providerClass: "cloud" | "local"
  match: {
    urlPattern?: RegExp
    headerPattern?: RegExp
    responseShape?: JSONSchema
  }
  modelsEndpoint: string
  authHint: "none" | "optional" | "required"
}
```

This enables discovery of:
- OpenAI, Anthropic, Google Gemini
- OpenRouter, Groq, Mistral AI, Hugging Face, Together AI, Kilo Code
- Cline, Roo Coder (OAuth)
- Ollama, LM Studio
- Generic OpenAI-compatible servers

**Without vendor-specific hardcoding.**

---

### OAuth Browser-Based Providers

**Cline** and **Roo Coder** use OAuth 2.0 browser-based authentication flow:

**Authentication Flow:**
1. User initiates provider connection in Provider Control Panel
2. OmniParser opens system default browser to provider's OAuth endpoint
3. User logs in and authorizes OmniParser access
4. Provider redirects to local callback URL with authorization code
5. OmniParser exchanges code for access token and refresh token
6. Tokens are stored in Secure Agentic Vault

**Token Management:**
- Access tokens are automatically refreshed before expiration
- Refresh tokens are encrypted and bound to Owner identity
- Token revocation triggers immediate provider de-registration

**Security Model:**
- OAuth flow uses PKCE (Proof Key for Code Exchange) for additional security
- Local callback server runs only during authentication (ephemeral)
- All tokens are stored encrypted in Secure Agentic Vault
- Browser-based auth requires user interaction and cannot be automated

**Discovery Mode:** `MANUAL` (requires OAuth completion before model discovery)

**OAuth Discovery Class Rule:** OAuth Browser-Based Providers are always classified as `DISCOVERY_CLASS = AUTH_GATED` and are ineligible for unauthenticated discovery.

---

### Generic Provider — OpenAI-Compatible Adapter

**Purpose:**  
A universal adapter for any endpoint implementing the OpenAI API contract, including:
- Self-hosted gateways (vLLM, TGI, LMDeploy)
- Private enterprise inference stacks
- Academic model servers
- Future cloud providers

**Adapter Status:** Canonical System Adapter (Mandatory, Zone-Neutral)  
**Default State:** DISCOVERED  
**Promotion Rule:** Logical Providers instantiated through this adapter may execute only after reaching ACTIVE state.

**Required Configuration Fields:**
- Base URL (`http://` or `https://`)
- API Key / Token
- Default Model ID
- Max Context Window
- Max Output Tokens

**Optional Fields:**
- Custom Headers
- Organization ID
- TLS Certificate Fingerprint (Pinning)
- Proxy Settings

**Header Policy Rule:**  
Custom headers are subject to Core Law validation. Reserved headers (`Authorization`, `Host`, `Content-Length`, `User-Agent`) may not be overridden.

**Discovery Logic:**
1. Attempt provider-native discovery endpoint if declared
2. If unavailable, attempt OpenAI-compatible:
   ```
   GET {baseUrl}/v1/models
   ```
3. If successful → mark `DISCOVERY_MODE = LIVE`
4. If both fail → require manual model entry and mark `DISCOVERY_MODE = MANUAL`

**Budget Classification:**
- Default: `COST_UNVERIFIED`
- Requires user-declared token pricing or heuristic estimation

**Certification Flow**

CERTIFICATION requires:
- Successful `/v1/models` discovery
- TLS fingerprint pin (required for HTTPS endpoints)
- Token accounting validation
- Execution dry-run with ghost tests
- Owner signature

**Transport Trust Rule:** Logical Providers discovered over non-TLS or unpinned TLS may never be CERTIFIED regardless of other validation criteria. Loopback addresses (127.0.0.0/8, ::1) are exempt from TLS requirements.

**Cost Enforcement Rule:**

Users may enable any Provider Adapter. Routing, quorum, and governance eligibility of **Logical Providers** are restricted by certification and cost model:
Cost model classification modifies routing preference and quorum eligibility only.
It MUST NOT override `ProviderState = ACTIVE` as the sole execution gate.
- `verified`: Eligible for quorum voting and Governed Mode
- `user-declared`: Eligible for routing but excluded from quorum
- `heuristic`: Restricted to simulation and non-quorum execution

**Budget Precedence Rule:** Budget enforcement overrides routing optimization but **never** overrides Security, Legal, or PII policy constraints. See Policy Precedence Law (Phase 0) for complete enforcement hierarchy.

---

**Local Provider Examples (HTTP):**
Ollama, LM Studio, and any OpenAI-compatible localhost endpoint.

**CLI Agent Examples:**
Aider, GPT Engineer, Goose, GitHub Copilot CLI, Claude Code, Gemini CLI, OpenCode CLI, Blackbox CLI, Crush, Codex, Warp AI, Droid, Qwen CLI, and any executable implementing the CLI Provider contract.

All CLI agents execute inside a **Sandboxed Execution Broker**:

```
Agent → Task → Broker → Ephemeral Container → CLI → Diff → Validator → Human Approval
```

Direct filesystem, network, or shell access from agents is **strictly prohibited**. All side effects must be mediated by the Sandboxed Execution Broker and recorded in the Audit Ledger.

**MCP Server Integration:** OmniParser serves as a Host for **Model Context Protocol** servers, allowing agents to fetch live data from SQL, Google Drive, and internal Slack channels to ground their reasoning in real-world truth.

**MCP Integrity Rule:** All MCP responses must be wrapped in a Signed Context Envelope issued by the Provider Abstraction Layer. Core Law must verify the envelope signature and source certification status before allowing MCP data to be merged into task context.

**MCP Certification Status:** MCP servers are classified as CERTIFIED, UNCERTIFIED, or REVOKED.

UNCERTIFIED MCP servers:
- May be used for simulation and capability planning
- May NOT be used for Security, Legal, or Infrastructure domains

REVOKED MCP servers:
- Are fully blocked

Enforcement is executed at the Provider Abstraction Layer and validated by Core Law before request dispatch.

### MCP Provider Governance Law (Mandatory)

MCP servers are treated as **Logical Providers of class "context"** and MUST follow the same ProviderState lifecycle as execution providers.

**MCP State Machine:**
- MCP servers enter the Provider State Machine at DISCOVERED
- Must pass VALIDATED → CERTIFIED → REGISTERED → ACTIVE before context injection
- Are subject to the same policy gates (PII, domain restrictions, health checks)
- Must emit signed context envelopes validated by Core Law

**MCP Policy Enforcement:**
- ACTIVE MCP servers may inject context into task execution
- CERTIFIED (but not REGISTERED) MCP servers may be queried for simulation only
- DISCOVERED/VALIDATED MCP servers are UI-visible but execution-blocked
- REVOKED_PROVIDER MCP servers are fully blocked from all operations

**MCP Context Authority Rule:**
All MCP responses must be wrapped in a Signed Context Envelope issued by the Provider Abstraction Layer. Core Law must verify the envelope signature and source ProviderState before allowing MCP data to be merged into task context.

**Compute-Orchestration Law:** OmniParser uses **Heuristic Routing** to determine where a task should run:
- **Heavy Logic:** Routed to Gemini 1.5 Pro / Claude 3.5 (Cloud).
- **Sensitive Logic / PII:** Forced to run on a **CERTIFIED Provider that satisfies the active policy rule `ALLOW_PII = true` and `NETWORK_ACCESS = false`.**
- **Boilerplate / Simple UI:** Routed to **Groq** for sub-second execution.
- **The "CFO" Budget Agent:** A specialized background monitor that calculates the estimated token cost of a task before it is sent to the swarm.
  - **Budget Authority Rule:** The Budget Agent may propose a transition to BUDGET_PAUSED. Core Law must validate policy compliance and cryptographically sign the transition before it is committed to the Audit Ledger.
  - **Authority Rule:** The Budget Agent may autonomously transition the system into BUDGET_PAUSED state but may never transition the system out of it. Resume authority is restricted to Architect or Owner signatures.
  - **Budget Pause Rule:** BUDGET_PAUSED does not modify ProviderState. It globally blocks transition into SWARM_DEPLOYED regardless of ProviderState.
  - **Budget Grace Rule:** When entering BUDGET_PAUSED, in-flight executions are allowed a maximum grace period (default 5 minutes). After expiry, the Broker MUST terminate remaining tasks and emit FAILURE events signed by Core Law.
  - **Budget Pause TTL Rule:**  
BUDGET_PAUSED must include a signed expiration timestamp (default 24h). On expiry, the system transitions to SPEC_LOCKED and requires human revalidation before redeployment.
  - **Hard Spending Caps:** Users can set a "Daily Token Budget" per project. If the Swarm reaches 90% of the budget, OmniParser pauses and triggers a "Budget Alert" popup.
  - **Budget Override Authority:** Only an Architect or Owner may raise spending caps or resume a paused swarm. All overrides require a signed justification recorded in the Audit Ledger.
  - **Spec Lock Dependency:** A paused swarm may only be resumed if system state is SPEC_LOCKED. Budget overrides cannot bypass spec validation or domain coverage gates.
  - **Cost Normalization Law:** All Provider costs must be normalized into `(InputTokens × Rate_in) + (OutputTokens × Rate_out) + (ToolCalls × Rate_tool) + (Modalities × Rate_modality)` before budget comparison is applied.
    - **Token Unit Definition:** A normalized token is defined as the provider-reported token unit for UTF-8 encoded text, mapped to a canonical integer count by the Adapter using the Provider Registry's conversion table.
    - **Unit Binding Rule:** All Providers must report token usage in normalized UTF-8 token units as defined by the Provider Registry. Adapters must convert provider-native token metrics into this unit before cost calculation.

### 📡 Normalized Request Protocol (NRP)

All Providers receive the same internal task format. Adapters translate this into provider-native APIs.

```json
{
  "task_id": "REQ-23.4",
  "mode": "generate | audit | test | fix",
  "inputs": {
    "spec_refs": ["auth.md:44-72"],
    "context": "…",
    "files": ["src/auth.ts"]
  },
  "constraints": {
    "immutable_blocks": true,
    "output_schema": "diff"
  },
  "execution_limits": {
    "max_tokens": 4000,
    "timeout_ms": 20000
  }
}
```

No provider may receive raw Markdown or filesystem access directly. All I/O passes through this protocol.

**Orchestration Patterns:**
- **Sequential (Pipeline):** For standard Build → Test → Deploy flows.
- **Magnetic (Task-Specific):** For complex, open-ended research where the Manager dynamically pulls in specialists.
- **Quorum (Voting):** For critical logic where multiple independent Providers must agree on the code before it reaches the Diff Modal. Quorum requires ≥ 2 providers by default, configurable by policy.
- **The Refinement Loop (Internal QA):** A specialized loop where the Auditor can send a rejection report directly back to the Worker for a second pass. This happens before you are notified, so you don't waste time reviewing "lazy" AI mistakes.

**Discovery Strategy:** OmniParser maintains a live **Provider Registry**. Model discovery is performed via provider-native endpoints when available, or via certified static manifests when discovery is not supported. Results are cached with health, capability, and failure-rate metadata. Routing decisions are made exclusively from this registry, not static configuration. Offline operation uses certified `fallbackModels` per provider class.

**Adapter Rule:** Providers lacking a native `/models` endpoint must supply a static ModelDescriptor manifest as part of certification. The Registry treats this as authoritative until re-certification.

**Provider Registry Law:** The Provider Registry must remain consistent with certification and policy enforcement rules. Missing or unreachable providers are replaced by certified fallback endpoints of the same class where available.

**Registry State Model:**
```
RegistryState:
  HEALTHY          → All certified providers reachable
  TEMPORARY_DEGRADED → Fallback endpoints active
  QUARANTINED      → Integrity failure, export-only mode
```

Discovery mode and Registry state are orthogonal properties.

**Class Coverage Rule:** Providers from Cloud, Local, and CLI classes may be represented in the Registry based on user configuration and policy.

**Virtual Fallback Providers** may be instantiated for UI visualization only when explicitly enabled by policy or simulation mode. They are UI-visible placeholders only, never required for system operation, and may never participate in execution, routing decisions, or quorum consensus.

**Fallback Endpoint vs Virtual Provider:**
- **Fallback Endpoint:** Operational replacement for unreachable certified provider (inherits Provider ID, participates in routing)
- **Virtual Provider:** UI-only placeholder for visualization in simulation mode (never participates in execution)

**Provider Identity Rule:** Provider IDs refer to logical identities, not physical endpoints.
Fallback endpoints inherit the Provider ID they replace and do not increase registry cardinality.

**Fallback Telemetry Rule:**
Fallback endpoints inherit the Logical Provider ID but MUST expose a distinct Endpoint Instance ID.
UI and Registry MUST surface Endpoint Instance ID for health, latency, and capability metrics to prevent telemetry ambiguity.

**Offline Exception:** During first-run or air-gapped operation, the Provider Registry may enter a TEMPORARY_DEGRADED state where certified fallback providers are virtualized locally until cloud endpoints are reachable. All active Providers must pass certification and policy validation before entering SWARM_DEPLOYED state.

### 🧯 Failure Containment (State-Based)

Logical Providers are segmented by **ProviderState** to prevent cascade failure:

- **ACTIVE:** May execute tasks and participate in quorum (CERTIFIED + REGISTERED + POLICY_PASS + HEALTHY)
- **REGISTERED:** Certified but blocked by policy or health (routing-only visibility)
- **CERTIFIED:** Identity verified, not yet registered
- **VALIDATED:** Health checks passed, awaiting certification
- **DISCOVERED:** Endpoint reachable, awaiting validation
- **REVOKED_ENDPOINT:** Endpoint Instance invalidated; Logical Provider returns to DISCOVERED
- **REVOKED_PROVIDER:** Logical Provider fully isolated; blocked from all operations (terminal)

---

## 🛡 The Zero-Loss Guarantee

**What OmniParser Guarantees:**
- **Complete Traceability:** Every line of generated code maps to a specific Markdown source line and requirement ID.
- **Validation Coverage:** All code passes through automated checks (syntax, linting, type safety, and spec-derived ghost tests) before reaching the Diff Modal.
- **Human Approval Gate:** No code writes to disk without explicit user acceptance via the Diff Modal.
- **Audit Trail:** Every agent action, decision, and file modification is logged with cryptographic signatures.

**What OmniParser Does NOT Guarantee:**
- Semantic correctness of generated code
- Architectural quality or design patterns
- Perfect interpretation of human intent

**System Boundaries:** OmniParser ensures process integrity and traceability, not output perfection. The human remains the final arbiter of code quality.

**Quality Assurance Mechanisms:**
- **Task Generation Gate:** No Provider may receive a task until:
  - All Phase 1 domains are either completed or explicitly marked "Out of Scope"
  - A **Domain Coverage Score ≥ 95%** is achieved
  - The project has passed **SPEC_LOCKED** state validation
- **Acceptance Criteria Gate:** A Diff cannot enter COMMITTING state unless all linked acceptance_criteria are validated by:
  - Approved by an Operator
  - Validated by an Architect or Owner
  - Spec-derived tests, or
  - Explicit Architect sign-off
  - **Override Quota:** Architect sign-off without tests is limited to 5 overrides per project version. This is a quality enforcement mechanism and does not restrict provider selection. Exceeding quota forces test generation before further commits.
- **Dual-Key Validation:** Every task must pass a **Vertical Logic Check** (Parent/Child relationship) and a **Horizontal Traceability Check** (Markdown Line vs. Code).
- **Contextual Logic Checksum:** Before execution, OmniParser runs a checksum to ensure that a requirement in `auth.md` doesn't contradict a requirement in `database.md`. It flags "Requirement Conflicts" to the user before a single token is spent.
- **Implicit Intent Extraction:** High-level logic that proposes inferred technical requirements (such as error handling or state cleanup) as **draft spec entries**. All inferred requirements must be explicitly approved in the Diff Modal before becoming binding law.
- **The Auditor Swarm:** A multi-agent "Reviewer" system (e.g., Gemini 1.5 Pro) that audits the "Creator" agent's code before you ever see it.
  - **Ambiguity Triggers:** When an agent calculates a **Confidence Score** below 85% for a requirement, it pauses and triggers a Human-in-the-Loop popup. It highlights the exact Markdown line and asks for clarification before writing code.
    - **Confidence Score Formula:** `ConfidenceScore = (ValidationRate × 0.4 + TestSuccessRate × 0.3 + SpecCoverage × 0.3)` with domain-specific weight adjustments (security tasks prioritize validation at 0.5, reducing other weights proportionally).
- **Autonomous Replanning:** If a sub-task fails (e.g., a broken test or API timeout), OmniParser doesn't stop. It triggers a "Recovery Agent" to analyze the logs, update the Task Ledger, and propose an alternative path to the user.
- **Self-Healing Roadmaps:** After every accepted Diff, OmniParser re-reads the codebase and "Heals" the remaining tasks based on the new reality.
- **Shadow Simulation:** Run ultra-cheap "Dry Runs" to predict architecture errors before spending high-end tokens.
- **Agentic Observability (Trace-to-Law):** Every agent action is logged using OpenTelemetry standards. OmniParser records **inputs, outputs, execution metadata, policy decisions, and validation results**—never internal reasoning, chain-of-thought, system prompts, or hidden provider messages. This ensures full auditability while respecting provider ToS and privacy regulations.
  - **Export Rule:** Telemetry is stored locally by default. External export endpoints are disabled in offline mode and must be explicitly enabled by Architect or Owner policy.
  - **Task Causality Chain:** Every task stores:
    - Source domain
    - Trigger condition (spec gap, dependency change, human request)
    - Missing signal that caused task creation
    - Human answer (if from Phase 1 Interrogation)
  - **Discovery Telemetry Law:** Every `/models` fetch MUST emit:
    ```
    DISCOVERY_EVENT {
      provider_id
      endpoint_hash
      auth_used: true | false
      response_hash
      model_count
      discovery_confidence
      timestamp
      signature: {
        broker
        core
      }
    }
    ```
    This structure is a projection of the canonical Event schema and does not weaken signature requirements.
    UI must allow:
    - "View Discovery Proof"
    - Showing raw response hash + endpoint + trust label

---

## 🔒 Security & Identity

- **Human Authority Levels:** OmniParser enforces role-based access control for all critical operations:
  - **Bootstrap Rule:** The first user to initialize OmniParser becomes the default Owner. Ownership may only be transferred via a signed Owner-to-Owner delegation recorded in the Audit Ledger.
  - **Viewer:** Read-only access to specs, tasks, and audit logs
  - **Architect:** Approve specs, configure providers, set budgets, and mark domains as "Out of Scope"
  - **Operator:** Approve diffs and commit code changes
  - **Owner:** Manage identities, access Secure Agentic Vault, and modify system policies (personal, team, or organizational scope)
  - **Authority Enforcement:** No Diff or Spec Promotion may occur without an Architect or Owner signature.
  - **Human Signature Law:** All human approvals must be signed using local private key or organization SSO identity token. Signatures are stored as detached cryptographic proofs in the Audit Ledger.
- **Secure Agentic Vault:** Multi-provider API keys are never exposed to the AI. OmniParser acts as a secure "Identity Hub," providing agents with temporary, scoped OAuth tokens for external MCP servers (Slack, GitHub, Jira).
  - **Key Authority Rule:** System signing keys are generated on first boot, stored in the Secure Agentic Vault, and bound to the Owner identity. Key export is prohibited. Rotation requires Owner signature and invalidates all prior Law Exports.
- **Secrets Boundary:** Agents never receive raw credentials, tokens, or private keys—only time-bound, task-scoped capability handles issued by the Secure Agentic Vault.
- **NHI (Non-Human Identity) Status:** Every agent in the swarm is assigned a unique **Machine Identity**. OmniParser enforces **Least Privilege RBAC**, ensuring a "UI Worker" can never access the "Security Vault" or "Financial MCP" without explicit per-task escalation.
- **Audit Logging:** Every agent action—every file read and every command run—is cryptographically signed and stored in a local SQLite ledger for total accountability.

---

## 🎨 Agentic UX: Design Archetypes

Users don't need to know the code; they only need to know the "Vibe."

- **Visual Archetypes:** Pick a "Vibe" (e.g., *Sleek SaaS*, *Cyberpunk*, *Minimalist Apple*). OmniParser generates the technical `theme.md` laws automatically.
- **Vision-to-Task:** Drag-and-drop a Figma screenshot or napkin sketch. OmniParser "sees" the UI and writes the sub-tasks for the agents.
- **Kinetic Bento Grid:** A highly optimized UI using `OffscreenCanvas` and `Web Workers` to visualize the "Agent Swarm" activity in real-time. Physics calculations for the Dependency Map are handled by background threads to ensure the main UI remains responsive.
- **Windows 11 Mica Effect:** Translucent app window that adopts the user's desktop color for seamless OS integration.
- **Tactile Feedback:** When an agent is "Thinking," task cards pulse with subtle, high-frequency animations.
- **The Swarm View:** A hexagonal grid displaying all **registry-visible Providers**—ACTIVE ones glow, CERTIFIED are dim-highlighted, fallback and virtual providers are dimmed.
  - **Efficiency Benchmarking:** The hexagonal grid also displays real-time "Accuracy %" and "Token Density" metrics for each certified AI Provider. You can see at a glance which AI is delivering the highest accuracy and efficiency for your workload.
- **Spatial Dependency Map:** A visual canvas showing how a single line of Markdown in one file "gathers" data from three other files to create a sub-task.
- **Project Health Dashboard:** Real-time operational metrics for project governance:
  - **Spec Coverage %:** Percentage of project domains with complete specifications
  - **Domain Completeness %:** Phase 1 interrogation completion status
  - **Failed Task Rate:** Percentage of tasks rejected by Auditor or ghost tests
  - **Replan Frequency:** How often Autonomous Replanning is triggered
  - **Human Override Rate:** Percentage of AI decisions requiring human intervention
  - **Budget Burn Rate:** Token consumption velocity vs. Daily Token Budget

---

## ⚙️ Provider Control Panel (User Configuration Law)

OmniParser exposes all **registered AI Providers** through a unified **Provider Control Panel**, accessible from the top-left **⚙️ Gear Menu** in the application UI. This is the **only** place where Providers can be enabled, configured, or authorized.

### Provider Selection & Activation
- Users can **enable or disable Providers** individually.
- Disabled Providers are fully removed from routing, quorum, and fallback logic.
- **Execution Capability:** See Execution Eligibility Law (Phase 0).

**Registry vs Routing Law:** The Provider Registry maintains logical Provider IDs per the Provider Selection Law. User disablement removes a Provider from the Active Routing Pool only. Disabled Providers may be replaced by Virtual Fallback Providers for UI visualization when simulation mode is enabled.

### Provider Configuration Modes
Each Provider supports one or more of the following configuration paths:

- **Cloud Provider**
  - API Key or OAuth-based authentication
  - Model selection from the live Provider Registry
  - Capability preview (context size, modalities, streaming, function support)

- **Local Provider**
  - Local endpoint configuration (e.g., `http://localhost:11434`)
  - Model discovery via `/models`
  - Hardware capability detection (VRAM, RAM, GPU/CPU mode)

- **CLI Agent**
  - Executable path configuration
  - Sandbox profile selection (container image, filesystem scope, network policy)
  - Permission preview (read-only, write, execute, MCP access)

### Security Enforcement
- API keys, tokens, and credentials are stored **only** inside the Secure Agentic Vault.
- The UI never exposes raw secrets after initial entry.
- Providers receive **time-bound, task-scoped capability handles**, never permanent credentials.

### Compliance & Policy Indicators
Each Provider entry displays:
- **Provider Status:** Certified / Uncertified / Revoked
- **Discovery Mode:** Live / Manual / Static
- **Compliance Flags:** PII Allowed / No PII / Logging Restrictions
- **Health Status:** Healthy / Degraded / Offline
- **Capability Summary:** Modalities, max context, tool support

### Model Trust Labels (MANDATORY UI LAW)

Every model in the dropdown MUST display:

```
[ ACTIVE ]         → Execution-eligible (policy + health + certification passed)
[ CERTIFIED ]      → Certified, not yet execution-eligible
[ DISCOVERED ]     → Live fetched, unauthenticated
[ MANUAL ]         → User-entered
[ FALLBACK ]       → Static manifest / offline
```

**UI Trust State Visibility:** Intermediate provider states (VALIDATED, REGISTERED) are internal-only and never rendered in UI. Only final execution eligibility states are displayed.

**Execution Rule**

Only models labeled `[ACTIVE]` may be routed to SWARM_DEPLOYED state.

### Routing Visibility
Users can preview how OmniParser will route tasks:
- Which Providers qualify for **Worker, Auditor, and Quorum roles**
- Which Providers are excluded due to policy, certification status, or health status

### Simulation Mode

Users may enable:

```
MODE = DISCOVERY_SIMULATION
```

This allows:
- Routing visualization
- Quorum preview
- Budget simulation
- Capability matching

Using **unauthenticated discovered models**

Execution remains hard-blocked.

**Simulation Safety Rule:** `MODE = DISCOVERY_SIMULATION` hard-locks system state to `SPEC_LOCKED` and prohibits transition to `SWARM_DEPLOYED` regardless of Provider status.

### Change Control
- Any Provider configuration change triggers a **Swarm Revalidation Pass**
- Active tasks are paused, re-evaluated, and either resumed or re-routed
- Configuration changes are logged in the **Audit Ledger** with timestamp and machine identity

### Provider Validation Mode
- Users can run a **"Dry Test"** per Provider before activation:
  - Auth validation (API key or OAuth flow)
  - Model list fetch and capability detection
  - Sandbox permission check (for CLI agents)
  - Token budget simulation (estimated cost per 1K tokens)

---

## 🌐 Advanced Integrations (2026 Standard)

- **MCP Server Hub:** Connect agents to local/cloud **Model Context Protocol** servers (Google Drive, Slack, SQL) to inject real-world context into tasks.
  - **Offline Mode Restriction:** Cloud-based MCP servers are automatically disabled in offline mode. Only Local MCP servers may be queried.
- **Vector Memory:** A local project database that "learns" your coding style and design preferences over time.
- **Contextual "DNA" Persistence:** OmniParser maintains a **Long-Term Memory Vector Store** of your project's architectural decisions. If you chose "Modular Monolith" in Task 1, the agents will automatically reject "Microservices" patterns in Task 100 without being reminded.
- **Immutable Project Snapshots (Time-Travel):** Captures the exact state of the project (MD + Code + Agent State) at every task milestone. Allows for one-click "Time-Travel" to revert the entire project if an agentic path fails.
- **Voice-Driven "Architect Mode":** Native Windows voice integration allowing the user to dictate structural changes to the Markdown "Law" on the fly, triggering immediate task re-parsing.
- **Agent Sync Server (Conflict Resolution):** A specialized coordinator that ensures parallel agents working in different folders don't use conflicting variable names or architectural patterns.
  - **Optimistic Concurrency Control (OCC):** When parallel agents target the same file, OmniParser issues a Temporal File Lock. If a collision is detected, the Manager performs a Semantic Merge of the two Diffs before presenting a single, unified "Conflict-Free Diff" to the human Architect.
- **ALM (Agent Lifecycle Management):** OmniParser handles the full lifecycle of every agent—from **Initialization** (context loading) to **Decommissioning** (memory wiping and token-usage finalization). No "zombie" agents are left running in the background.
- **Diff Approval Modal:** The mandatory gatekeeper. All agent changes are presented as interactive Diffs. No agent writes to disk without human "Acceptance."

---

## 🔄 System State Machine

OmniParser operates as a formal state machine to prevent race conditions, logical corruption, and invalid transitions.

### Valid States

- **IDLE:** No active project; awaiting user input
- **INGESTING:** Scanning workspace, parsing `.md` files, building project graph
- **INTERROGATING:** Phase 1 active; blocking on incomplete domain coverage
- **SPEC_LOCKED:** All domains complete; internal specs finalized and versioned
- **BUDGET_PAUSED:** Token budget exceeded; swarm halted, no new tasks dispatched, active executions allowed to complete or timeout safely
- **SWARM_DEPLOYED:** Providers actively executing tasks
- **AWAITING_APPROVAL:** Diffs generated; human review required
- **COMMITTING:** Approved changes being written to disk
- **HEALING:** Post-commit spec revalidation and task replanning
- **RECOVERY:** System restart detected mid-transition; validates filesystem, spec hash, and task ledger before resuming or rolling back
- **QUARANTINED:** Validation failure state; read-only mode, export-only, Owner intervention required
- **ARCHIVED:** Project snapshot saved; system ready for new cycle

### Illegal Transitions

The following state transitions are **strictly prohibited** and will trigger system halt:

- `SWARM_DEPLOYED → INGESTING` (cannot re-ingest while agents are active)
- `COMMITTING → INTERROGATING` (cannot interrogate during file writes)
- `HEALING → SWARM_DEPLOYED` (must pass through `SPEC_LOCKED` validation first)
- `AWAITING_APPROVAL → INGESTING` (must complete or reject current cycle)
- `BUDGET_PAUSED → COMMITTING` (cannot commit while budget enforcement is active)
- `BUDGET_PAUSED → SWARM_DEPLOYED` (must return to SPEC_LOCKED or receive signed override first)

### State Enforcement

All state transitions are:
- Logged in the Audit Ledger with cryptographic signatures
- Validated against the transition matrix before execution
- Reversible only through explicit "Abort" or "Rollback" commands with Owner authority

**Budget Resume Rule:** Exiting BUDGET_PAUSED requires a signed Architect or Owner override and a successful revalidation of Domain Coverage and Spec Version Hash.

**Quarantine Exit Rule:** The system may exit QUARANTINED state only through an Owner-signed RECOVERY_OVERRIDE action. This action triggers a full filesystem integrity scan, Spec Version Hash recomputation, Provider Registry re-certification, and Domain Coverage re-evaluation before allowing transition to IDLE or SPEC_LOCKED.

**Spec Unlock Authority:** Only an Architect or Owner may transition the system out of SPEC_LOCKED. Unlocking invalidates the current Spec Version Hash and forces full Domain Re-Scoring.

**Crash Recovery Protocol:** On startup, OmniParser must enter RECOVERY state if last recorded state was not ARCHIVED or IDLE. The system validates filesystem integrity, spec hash consistency, and task ledger completeness before resuming or rolling back. If validation fails more than 3 consecutive times, system enters **QUARANTINED** state—read-only mode, export-only, Owner intervention required.



---

## 🚀 Execution Flow

0. **Initialize Runtime (Phase 0 — Implementation Law):** Core Law Engine, Broker, Data Plane, and Secure Agentic Vault are started. If any component fails health checks, system enters QUARANTINED state.
1. **Interrogate Intent (Phase 1 — Intent Law):** OmniParser scans for domain coverage. If < 95%, it enters INTERROGATING state and prompts for missing domains (Identity, Legal, Monetization, etc.).
2. **Define the Law (Phase 2 — Spec Design):** Drop your parallel `.md` files into the root. OmniParser ingests, resolves conflicts, and locks specs.
3. **Choose the Archetype:** Set the visual law for the UI/UX or use Axiom Bootstrapping templates.
4. **Deploy the Swarm:** Route tasks to optimal Providers (e.g., Groq for speed, Claude for logic). CFO Budget Agent monitors token costs.
5. **Approve, Commit & Heal:** Accepted Diffs trigger:
   - File writes (COMMITTING state)
   - Spec revalidation (HEALING state)
   - Domain re-scoring
   - Swarm replanning if coverage drops below threshold
   - State transition to ARCHIVED or back to SPEC_LOCKED for next cycle

---

## 📤 Law Export

OmniParser is not a black box. Full project law can be exported at any time as:

- **OpenAPI Spec:** Complete API contract derived from backend domain specs
- **Architecture Diagram:** Visual representation of component dependencies and data flows
- **Compliance Report:** Audit trail, domain coverage, and security posture summary. Compliance outputs are informational and do not constitute legal, regulatory, or professional advice.
- **Build Manifest:** Reproducible build instructions with provider versions and token costs

All exports are cryptographically signed and versioned to match the Spec Version Hash.

### Law Re-Import Rule

Imported laws must pass:
- Signature verification
- Version compatibility check
- Full Domain Coverage re-scan

Failed imports enter INTERROGATING state.

### Law Diff Mode

OmniParser can generate a cryptographic diff between two exported laws showing:
- Added requirements
- Removed requirements
- Domain shifts
- Authority signature changes

---

**OmniParser: The Architect Edition** — A secure, professional, and observable digital workforce for 2026.