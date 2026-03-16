# AI Voice Collection Agent - HLD (High Level Document)

**Document Version Control**

| Version | Date       | Author   | Change Description                                      |
|---------|------------|----------|--------------------------------------------------------|
| 1.0     | 2026-03-10 | Md Sahil | Initial draft — database schema, Excel templates, architecture overview. |
| 2.0     | 2026-03-15 | Md Sahil | Added 7-layer intelligence stack, 21-state machine, reason flows, objection playbook. |
| 3.0     | 2026-03-17 | Md Sahil | Full HLD — call orchestrator, DPD-bucket prompts, compliance engine, deployment architecture. |

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Collection Call Process Flow](#2-collection-call-process-flow)
3. [System Overview](#3-system-overview)
4. [Infrastructure Architecture](#4-infrastructure-architecture)
5. [Technology Stack](#5-technology-stack)
6. [7-Layer Intelligence Stack](#6-7-layer-intelligence-stack)
7. [Architecture Design](#7-architecture-design)
8. [Module Descriptions](#8-module-descriptions)
9. [Data Design](#9-data-design)
10. [Deployment Architecture](#10-deployment-architecture)
11. [Compliance & Regulatory](#11-compliance--regulatory)
12. [Risks & Mitigations](#12-risks--mitigations)
13. [Success Metrics & KPIs](#13-success-metrics--kpis)
14. [AI Call Execution Flow](#14-ai-call-execution-flow)

---

## 1. Introduction

### 1.1 Purpose

The **AI Voice Collection Agent** aims to digitize and automate the end-to-end **overdue (OD) loan collection calling process** for Sampurna Financial Services Pvt. Ltd. and other MFI/NBFC clients via a multi-tenant SaaS platform.

#### ❌ Previous Challenges

**Manual Calling Process Issues:**
- ❌ Human callers make 40-60 calls/day with inconsistent quality
- ❌ No structured disposition capture — reasons logged in free text
- ❌ Broken promises not tracked or followed up systematically
- ❌ No DPD-based tone variation — same approach for 15 DPD and 150 DPD
- ❌ Third-party calls (60% of all calls) handled poorly
- ❌ No compliance enforcement — threats, abuse, unauthorized disclosure
- ❌ Language barriers — callers can't speak all regional languages

#### ✅ Solution Objectives

**AI-Powered Collection System Benefits:**
- ✅ 1000+ calls/day with consistent negotiation quality
- ✅ Structured disposition: OD reason, P2P date, P2P amount, willingness score
- ✅ Automated promise tracking with broken-promise re-queuing
- ✅ DPD-bucket-specific tone (soft → firm → urgent → recovery)
- ✅ 23 OD reason conversation flows with domain-expert handling
- ✅ 18 objection counter-scripts for mid-call pushback
- ✅ RBI Fair Practices Code compliance enforced at app layer
- ✅ Multi-language support (Hindi, Bengali, English + expandable)

#### 📑 Problem Statement

The current OD collection process relies on human callers using WhatsApp, personal phones, and Excel sheets. Disposition data is unstructured, promise tracking is manual, and there is no systematic approach to handle sensitive cases (death, domestic violence) or comply with RBI regulations. This results in low recovery rates, compliance risk, and inability to scale.

### 1.2 🎯 Scope

#### ✅ In Scope
- AI voice agent for OD collection calls (full-duplex)
- Multi-tenant database with RLS and configurable OD buckets
- Excel upload pipeline with field mapping per tenant
- 21-state call state machine with JSON-driven reason flows
- Objection detection and counter-script injection
- Compliance guardrails (blocked phrases, DNC, time window)
- P2P tracker with automatic broken-promise re-queuing
- Call recording, transcript logging, disposition capture
- Batch calling with retry logic and concurrency control
- Dashboard for call analytics and campaign monitoring

#### ❌ Out of Scope
- Inbound call handling (Phase 2)
- Automated payment reconciliation (manual in Phase 1)
- WhatsApp/SMS follow-up automation (Phase 2)
- Fine-tuned ML classifier for objection detection (Phase 3)

---

## 2. Collection Call Process Flow

### 📊 End-to-End OD Collection Flow

```mermaid
graph TD
    A["📤 Excel Upload<br/>Borrower Data"] --> B["🔄 Field Mapping<br/>Per Tenant"]
    B --> C["💾 Database<br/>Load & Validate"]
    C --> D["📋 Campaign<br/>Created"]
    D --> E["📊 Queue<br/>Prioritized"]
    E --> F{"✅ Pre-Call<br/>Compliance?"}
    F -->|Fail| G["⏭️ Skip &<br/>Reschedule"]
    F -->|Pass| H["📞 AI Dials<br/>Customer"]
    H --> I{"📱 Customer<br/>Answers?"}
    I -->|No| J["🔁 Retry<br/>Later"]
    I -->|Yes| K["🤖 AI<br/>Conversation"]
    K --> L["📝 Disposition<br/>Captured"]
    L --> M["💾 Save to DB<br/>+ Recording"]
    M --> N{"PTP<br/>Captured?"}
    N -->|Yes| O["📊 P2P Tracker<br/>Created"]
    N -->|No| P["🔁 Re-queue<br/>Follow-up"]
    O --> Q{"Payment<br/>Received?"}
    Q -->|Yes| R["✅ KEPT"]
    Q -->|Partial| S["⚠️ PARTIAL"]
    Q -->|No| T["❌ BROKEN<br/>Re-queue HIGH"]

    style A fill:#e3f2fd
    style B fill:#e3f2fd
    style C fill:#e3f2fd
    style D fill:#f3e5f5
    style E fill:#f3e5f5
    style F fill:#fff3e0
    style G fill:#ffcdd2
    style H fill:#f3e5f5
    style I fill:#fff3e0
    style J fill:#ffcdd2
    style K fill:#c8e6c9
    style L fill:#c8e6c9
    style M fill:#c8e6c9
    style N fill:#fff3e0
    style O fill:#fff9c4
    style P fill:#ffcdd2
    style Q fill:#fff3e0
    style R fill:#a5d6a7
    style S fill:#fff9c4
    style T fill:#ffcdd2
```

**[Diagram 1: Complete OD Collection Flow — Upload to Promise Tracking]**

---

### 2.1 Data Flow Diagram

#### Level-0: System Context

```mermaid
graph TB
    subgraph entities["External Entities"]
        direction LR
        MFI["👔 MFI Staff"]
        BORR["👤 Borrower"]
        ADMIN["⚙️ Tenant Admin"]
    end

    subgraph system["System"]
        PROCESS["🤖 AI VOICE<br/>COLLECTION<br/>PLATFORM"]
    end

    subgraph datastores["Data Stores"]
        direction TB
        D1["D1: Borrower Database"]
        D2["D2: Loan & OD Data"]
        D3["D3: Call Logs"]
        D4["D4: Dispositions"]
        D5["D5: P2P Tracker"]
    end

    MFI -->|Excel Upload| PROCESS
    ADMIN -->|Config & Policies| PROCESS
    PROCESS -->|Voice Call| BORR

    PROCESS -->|Store| D1
    PROCESS -->|Store| D2
    PROCESS -->|Store| D3
    PROCESS -->|Store| D4
    PROCESS -->|Store| D5

    style MFI fill:#FFA500,stroke:#FF8C00,stroke-width:2px,color:#000
    style BORR fill:#FFA500,stroke:#FF8C00,stroke-width:2px,color:#000
    style ADMIN fill:#FFA500,stroke:#FF8C00,stroke-width:2px,color:#000
    style PROCESS fill:#1E90FF,stroke:#0047AB,stroke-width:3px,color:#fff
    style D1 fill:#9D4EDD,stroke:#7B2CBF,stroke-width:2px,color:#fff
    style D2 fill:#9D4EDD,stroke:#7B2CBF,stroke-width:2px,color:#fff
    style D3 fill:#9D4EDD,stroke:#7B2CBF,stroke-width:2px,color:#fff
    style D4 fill:#9D4EDD,stroke:#7B2CBF,stroke-width:2px,color:#fff
    style D5 fill:#9D4EDD,stroke:#7B2CBF,stroke-width:2px,color:#fff
```

**[Diagram 2: Data Flow Level-0]**

#### 📋 Color Coding

| Color | Element | Meaning |
|-------|---------|---------|
| 🟠 **Orange** | External Entities | MFI Staff, Borrower, Admin |
| 🔵 **Blue** | Core Process | AI Voice Collection Platform |
| 🟣 **Purple** | Data Stores | Databases & trackers |

---

#### Level-1: Detailed Processes

```mermaid
graph TD
    MFI["👔 MFI Staff"]
    BORR["👤 Borrower"]

    P1["1.0<br/>Data Ingestion<br/>& Mapping"]
    P2["2.0<br/>Queue<br/>Management"]
    P3["3.0<br/>Pre-Call<br/>Compliance"]
    P4["4.0<br/>Build Borrower<br/>Context"]
    P5["5.0<br/>Execute<br/>AI Call"]
    P6["6.0<br/>Capture<br/>Disposition"]
    P7["7.0<br/>Promise<br/>Tracking"]

    D1["D1: Borrower<br/>& Loan Data"]
    D2["D2: Call Queue"]
    D3["D3: Call Logs<br/>& Recordings"]
    D4["D4: Dispositions"]
    D5["D5: P2P<br/>Tracker"]

    MFI -->|Excel Upload| P1
    P1 --> P2
    P2 --> P3
    P3 --> P4
    P4 --> P5
    P5 --> P6
    P6 --> P7
    P7 -->|Re-queue broken| P2

    P1 -.->|Store| D1
    P2 -.->|Store| D2
    P5 -.->|Store| D3
    P6 -.->|Store| D4
    P7 -.->|Store| D5

    P5 -->|Voice Call| BORR

    style MFI fill:#FFA500,stroke:#FF8C00,stroke-width:2px,color:#000
    style BORR fill:#FFA500,stroke:#FF8C00,stroke-width:2px,color:#000
    style P1 fill:#1E90FF,stroke:#0047AB,stroke-width:2px,color:#fff
    style P2 fill:#1E90FF,stroke:#0047AB,stroke-width:2px,color:#fff
    style P3 fill:#FF6B6B,stroke:#CC5555,stroke-width:2px,color:#fff
    style P4 fill:#1E90FF,stroke:#0047AB,stroke-width:2px,color:#fff
    style P5 fill:#1E90FF,stroke:#0047AB,stroke-width:2px,color:#fff
    style P6 fill:#1E90FF,stroke:#0047AB,stroke-width:2px,color:#fff
    style P7 fill:#1E90FF,stroke:#0047AB,stroke-width:2px,color:#fff
    style D1 fill:#9D4EDD,stroke:#7B2CBF,stroke-width:2px,color:#fff
    style D2 fill:#9D4EDD,stroke:#7B2CBF,stroke-width:2px,color:#fff
    style D3 fill:#9D4EDD,stroke:#7B2CBF,stroke-width:2px,color:#fff
    style D4 fill:#9D4EDD,stroke:#7B2CBF,stroke-width:2px,color:#fff
    style D5 fill:#9D4EDD,stroke:#7B2CBF,stroke-width:2px,color:#fff
```

**[Diagram 3: Data Flow Level-1]**

| Color | Element | Meaning |
|-------|---------|---------|
| 🟠 **Orange** | External Entities | MFI Staff, Borrower |
| 🔵 **Blue** | Processes (1.0–7.0) | Main business operations |
| 🔴 **Red** | Process 3.0 | Critical: Compliance check |
| 🟣 **Purple** | Data Stores (D1–D5) | Databases & storage |

---

## 3. 🌐 System Overview

### 3.1 System Overview

The **AI Voice Collection Agent** serves as a **full-duplex AI calling platform** that connects microfinance companies with overdue borrowers through intelligent, context-aware voice conversations.

**Key Platform Features:**
- Full-duplex AI voice agent using LiveKit + Sarvam + Gemini
- 21-state call state machine with JSON-driven reason flows
- Multi-tenant database with per-company field mapping
- DPD-bucket-specific negotiation strategy
- App-level compliance enforcement (not prompt-dependent)
- Promise tracking with automated broken-promise follow-up

```mermaid
graph TB
    FE["📊 Dashboard<br/>HTML/CSS/JS"]
    API["⚡ FastAPI<br/>Port 8000"]
    LK["🎙️ LiveKit<br/>WebRTC + SIP"]
    AGENT["🤖 AI Agent<br/>livekit_agent.py"]
    PG["🗄️ PostgreSQL<br/>16 Tables"]
    RD["⚡ Redis<br/>Cache"]

    FE -->|HTTPS| API
    API -->|Query| PG
    AGENT -->|Media| LK
    AGENT -->|Context| PG
    AGENT -->|Cache| RD

    style FE fill:#e3f2fd
    style API fill:#fff3e0
    style LK fill:#f3e5f5
    style AGENT fill:#c8e6c9
    style PG fill:#fff9c4
    style RD fill:#fce4ec
```

**[Diagram 4: System Architecture Overview]**

### 3.2 🎯 Key Objectives

| Category | Objective | Outcome |
|----------|-----------|---------|
| Business | Replace manual calling with AI | 10x call volume, consistent quality |
| Business | Structured disposition capture | OD reason + P2P in every call |
| Business | Multi-tenant SaaS | Sell to other MFIs/NBFCs |
| Technical | Domain-expert AI (not generic bot) | 7-layer intelligence stack |
| Technical | Provider-agnostic architecture | Switch STT/TTS/LLM via env vars |
| Operational | Automated promise tracking | Broken-promise re-queue |
| Compliance | RBI Fair Practices Code | Hard-coded app-level enforcement |
| Language | Hindi + Bengali + English | Expandable to 10+ Indian languages |

---

## 4. Infrastructure Architecture

### 4.1 Hosting Environment

| Component | Environment | Purpose |
|-----------|-------------|---------|
| FastAPI Backend | Azure VM (Ubuntu) | Core API, telephony routing, dashboard |
| LiveKit Agent | Azure VM | AI voice agent worker process |
| LiveKit Server | Azure VM | WebRTC media server + SIP bridge |
| PostgreSQL | Self-hosted Supabase | 16-table multi-tenant database |
| Redis | Docker container | Context caching (15-min TTL) |
| Qdrant | Docker container | Vector DB for RAG/objection search |
| Nginx | Azure VM | SSL termination + reverse proxy |

### 4.2 🔒 Security & Networking

#### Security Measures
- ✅ HTTPS enforced (TLS 1.2+) with Let's Encrypt SSL
- ✅ Firewall rules restrict access to ports 443, 8000, 7880
- ✅ Row-Level Security (RLS) on all tenant-scoped tables
- ✅ JWT authentication for dashboard users
- ✅ SIP trunk authentication for telephony
- ✅ Call recordings encrypted at rest

### 4.3 📐 Logical Topology

```mermaid
graph TB
    subgraph "Client Layer"
        DASH["📊 Dashboard<br/>HTML/CSS/JS<br/>HTTPS"]
        PHONE["📱 Borrower Phone<br/>PSTN"]
    end

    subgraph "API Layer"
        API["⚡ FastAPI<br/>Port 8000<br/>JWT Auth"]
        AGENT["🤖 AI Agent<br/>LiveKit Worker"]
    end

    subgraph "Media Layer"
        LK["🎙️ LiveKit Server<br/>:7880 WS<br/>:5060 SIP"]
    end

    subgraph "Data Layer"
        PG["🗄️ PostgreSQL<br/>RLS Enabled"]
        RD["⚡ Redis<br/>Context Cache"]
    end

    subgraph "Security"
        TLS["🔐 Nginx + TLS<br/>SSL Termination"]
    end

    DASH -->|HTTPS| TLS
    TLS -->|Proxy| API
    PHONE -->|PSTN → SIP| LK
    LK -->|Audio| AGENT
    AGENT -->|Query| PG
    AGENT -->|Cache| RD
    API -->|Query| PG

    style DASH fill:#e3f2fd
    style PHONE fill:#e3f2fd
    style API fill:#fff3e0
    style AGENT fill:#c8e6c9
    style LK fill:#f3e5f5
    style PG fill:#fff9c4
    style RD fill:#fce4ec
    style TLS fill:#ffcdd2
```

**[Diagram 5: Logical Topology]**

---

## 5. Technology Stack

### 5.1 Stack Components

| Layer | Primary Technology | Why Chosen | Notes |
|-------|-------------------|-----------|-------|
| Frontend | HTML/CSS/JS | Simple, no build steps, fast iteration | Dashboard + login |
| Backend | FastAPI (Python) | Async, Pydantic validation, OpenAPI | Telephony + API + uploads |
| Voice Agent | LiveKit Agents Framework | Production WebRTC, built-in VAD pipeline | Full-duplex voice |
| STT | Sarvam AI (saaras:v3) | Best Indian language accuracy | Hindi/Bengali/English |
| TTS | Sarvam AI (bulbul:v2) | Natural Indian voices | Multi-language |
| VAD | Silero VAD | Lightweight, accurate speech detection | Runs on CPU |
| LLM | Google Gemini 2.0 Flash | Fast, cheap, good multilingual | 300ms response |
| Database | PostgreSQL + Supabase | ACID, JSONB, RLS, pgvector ready | 16 tables |
| Cache | Redis 7 | Context caching, session memory | 15-min TTL |
| Vector DB | Qdrant | RAG search, objection embeddings | Phase 3 |
| Telephony | JIO SIP + Exotel | Dual-mode, runtime switchable | Provider-agnostic |
| Deployment | Docker Compose | Environment parity, easy scaling | Azure VM |
| Reverse Proxy | Nginx | SSL termination, load balancing | Let's Encrypt |

### 5.2 Component-to-Tool Mapping

```mermaid
graph LR
    VOICE["Voice Pipeline"] --> LK["LiveKit"]
    STT_C["Speech-to-Text"] --> SAR["Sarvam STT"]
    TTS_C["Text-to-Speech"] --> SAR2["Sarvam TTS"]
    AI["AI Reasoning"] --> GEM["Gemini 2.0"]
    DB_C["Database"] --> PG["PostgreSQL"]
    CACHE_C["Caching"] --> RD["Redis"]
    TEL["Telephony"] --> SIP["JIO SIP / Exotel"]
    DEPLOY["Deployment"] --> DOCK["Docker Compose"]

    style LK fill:#f3e5f5
    style SAR fill:#e3f2fd
    style SAR2 fill:#e3f2fd
    style GEM fill:#fff3e0
    style PG fill:#c8e6c9
    style RD fill:#fce4ec
    style SIP fill:#ffcdd2
    style DOCK fill:#eceff1
```

**[Diagram 6: Component-to-Tool Mapping]**

---

## 6. 🧠 7-Layer Intelligence Stack

### 6.1 Architecture Overview

The AI agent's intelligence is built in **7 layers** stacked around the LLM. The LLM provides language capability; everything else is built in Python + JSON.

```mermaid
graph TD
    L1["🎙️ Layer 1: Voice Pipeline<br/>LiveKit + Sarvam + Silero + Gemini"]
    L2["📊 Layer 2: Borrower Context<br/>7 DB Queries + Redis Cache"]
    L3["🔄 Layer 3: State Machine<br/>21 States + 23 Reason Flows"]
    L4["🎯 Layer 4: Objection Playbook<br/>18 Counter-Scripts"]
    L5["📈 Layer 5: DPD-Bucket Prompts<br/>Soft → Firm → Urgent → Recovery"]
    L6["📝 Layer 6: Disposition Engine<br/>Structured Capture"]
    L7["🛡️ Layer 7: Compliance<br/>Blocked Phrases + DNC + Limits"]

    L1 --> L2
    L2 --> L3
    L3 --> L4
    L4 --> L5
    L5 --> L6
    L6 --> L7

    style L1 fill:#eceff1
    style L2 fill:#e3f2fd
    style L3 fill:#e3f2fd
    style L4 fill:#fff3e0
    style L5 fill:#f3e5f5
    style L6 fill:#c8e6c9
    style L7 fill:#ffcdd2
```

**[Diagram 7: 7-Layer Intelligence Stack]**

### 6.2 Layer Details

| Layer | Purpose | Implementation | Files |
|-------|---------|---------------|-------|
| Layer 1 | Audio I/O + language generation | LiveKit Agents + Sarvam plugins + Gemini | `livekit_agent.py` |
| Layer 2 | Borrower profile, OD, history, risk | 7 parallel async DB queries, Redis cache | `context_builder.py` |
| Layer 3 | Call flow control, reason handling | 21-state machine, JSON reason trees | `state_machine.py`, `reason_flows.json` |
| Layer 4 | Mid-call objection countering | Keyword match → counter-script injection | `objection_playbook.json`, `objection_registry.py` |
| Layer 5 | DPD-based negotiation tone | SMA0=soft, SMA1=firm, SMA2=urgent, NPA=recovery | `prompting.py` |
| Layer 6 | Structured output | PTP capture, willingness, escalation flags | `state_machine.py` (disposition) |
| Layer 7 | Regulatory compliance | Blocked phrases, DNC, time limits, max calls | `compliance_filter.py` |

---

## 7. Architecture Design

### 7.1 🧩 Components

```mermaid
graph TB
    subgraph "Core Modules"
        SM["🔄 State Machine<br/>21 States, Transitions"]
        RF["📘 Reason Flows<br/>23 JSON Trees"]
        OBJ["🎯 Objection Playbook<br/>18 Counter-Scripts"]
        CTX["📊 Context Builder<br/>7 DB Queries"]
    end

    subgraph "Support Modules"
        CF["🛡️ Compliance Filter<br/>Blocked Phrases, DNC"]
        PR["📋 Prompt Builder<br/>DPD-Bucket Tone"]
        IR["🧠 Intent Router<br/>Language + Intent"]
        CP["🔌 Context Provider<br/>Mock + Postgres"]
    end

    SM -->|Loads| RF
    SM -->|Checks| OBJ
    SM -->|Uses| PR
    SM -->|Uses| IR
    SM -->|Uses| CF
    SM -->|Gets Context| CTX
    CTX -->|Maps to| CP

    style SM fill:#e3f2fd
    style RF fill:#c8e6c9
    style OBJ fill:#fff3e0
    style CTX fill:#e3f2fd
    style CF fill:#ffcdd2
    style PR fill:#f3e5f5
    style IR fill:#fff9c4
    style CP fill:#eceff1
```

**[Diagram 8: Core Module Architecture]**

### 7.2 🔄 Component Interactions

| Step | Interaction |
|------|-------------|
| Step 1 | Queue picks next call → Compliance pre-check (time, DNC, limits) |
| Step 2 | Context builder runs 7 parallel DB queries → builds 50+ field context |
| Step 3 | State machine initializes with context → loads reason_flows.json + objection_playbook.json |
| Step 4 | AI greets borrower → state = GREETING → customer responds |
| Step 5 | Intent router classifies response → state machine transitions |
| Step 6 | If reason detected → JSON reason flow drives conversation steps |
| Step 7 | If objection detected → counter-script injected into LLM prompt |
| Step 8 | Compliance filter checks every AI response before TTS |
| Step 9 | Disposition captured → saved to DB → P2P tracker auto-created |

### 7.3 📊 Sequence Diagram (Happy Path: Borrower Answers)

```mermaid
sequenceDiagram
    actor B as Borrower
    participant LK as LiveKit + SIP
    participant AGENT as AI Agent
    participant SM as State Machine
    participant DB as PostgreSQL

    AGENT->>LK: Create Room + SIP Dial
    LK->>B: Phone Rings
    B->>LK: Answers Call
    LK->>AGENT: Audio Connected

    AGENT->>SM: start() → GREETING
    SM->>AGENT: "Namaste, {name} ji?"
    AGENT->>LK: TTS Audio
    LK->>B: AI Speaks

    B->>LK: "Haan bolchi"
    LK->>AGENT: STT Text
    AGENT->>SM: handle_user_turn()
    SM->>SM: State → IDENTIFY → VERIFY → CONSENT

    AGENT->>SM: handle_user_turn("Haan bolun")
    SM->>SM: State → INFORM_DUES
    SM->>AGENT: "3 kisti baki, ₹11595"

    B->>LK: "Swami hospital e"
    LK->>AGENT: STT Text
    AGENT->>SM: handle_user_turn()
    SM->>SM: Detect: MEDICAL_EMERGENCY
    SM->>SM: Load JSON reason flow
    SM->>AGENT: "Sunke dukh hua. Treatment?"

    B->>LK: "Ektu bhalo hochhe"
    AGENT->>SM: advance_reason_flow("recovering")
    SM->>AGENT: "Chhota amount diye shuru korun?"

    B->>LK: "1000 taka debo 15 tarikhe"
    AGENT->>SM: PTP Captured
    SM->>AGENT: "Confirm: ₹1000, 15 tarikh?"
    B->>LK: "Haan thik ache"

    AGENT->>SM: finalize_disposition()
    SM->>DB: Save PARTIAL_PTP
    Note over DB: Auto-trigger creates<br/>P2P tracker entry

    AGENT->>LK: End Call
```

**[Diagram 9: Complete Happy Path — Borrower Answers, Medical Reason, PTP Captured]**

---

## 8. Module Descriptions

### 📞 8.1 Call Orchestrator

**What it does:**
Main loop — picks calls from queue, checks compliance, builds context, dials customer, runs conversation, saves disposition.

**Key Flows:**
1. CampaignRunner continuously picks from call_queue (SELECT FOR UPDATE SKIP LOCKED)
2. CompliancePreCheck validates time window, DNC, max calls, cool-off
3. ContextBuilder runs 7 parallel DB queries, caches in Redis
4. LiveKit room created, SIP dial initiated
5. Conversation loop runs until disposition captured

**Concurrency:** asyncio.Semaphore(5) — max 5 simultaneous calls per worker

---

### 🔄 8.2 State Machine (21 States)

**What it does:**
Controls the entire call flow — from greeting to disposition. Every state has specific instructions for the LLM.

**States:**

| Category | States | Count |
|----------|--------|-------|
| Opening | GREETING, IDENTIFY_RECEIVER, VERIFY_RIGHT_PARTY, CONSENT | 4 |
| Third Party | THIRD_PARTY_MESSAGE, THIRD_PARTY_LOCATE, THIRD_PARTY_CALLBACK | 3 |
| Collection | INFORM_DUES, REASON_PROBE, HANDLE_REASON | 3 |
| Negotiation | NEGOTIATE, OFFER_PARTIAL, COMMITMENT_CAPTURE, RECAP | 4 |
| Special | ALREADY_PAID_VERIFY, DISPUTE_HANDLE, INSURANCE_CLAIM, ESCALATE, DNC_ACKNOWLEDGE | 5 |
| Closing | CLOSE | 1 |
| **Total** | | **21** |

---

### 🌳 8.3 Reason Flow Engine

**What it does:**
JSON-driven conversation trees for 23 OD reasons. When AI detects a reason (e.g., "husband hospital e"), it loads the matching multi-step flow from `reason_flows.json`.

**Key Flows:**
1. Customer gives reason → intent_router classifies into 23 categories
2. reason_registry loads matching JSON flow → returns ReasonFlow object
3. State machine enters HANDLE_REASON → follows JSON steps
4. Each step has: agent_action, expected_responses, next_step_map
5. Flow exits to NEGOTIATE or CLOSE when complete

**All 23 Reasons:**

| Category | Reasons |
|----------|---------|
| Death / Medical | BORROWER_DECEASED, SPOUSE_DECEASED, MEDICAL_EMERGENCY, MENTAL_HEALTH |
| Income Loss | NO_INCOME, JOB_LOSS, BUSINESS_LOSS, SALARY_DELAYED, AGRICULTURAL_LOSS |
| Relationship | LOAN_GIVEN_TO_OTHER, DIVORCE_SEPARATION, DOMESTIC_VIOLENCE, GROUP_LEADER_ISSUE |
| Dispute | DISPUTE_AMOUNT, DISPUTE_SERVICE, ALREADY_PAID |
| Behavioral | FORGOT, WILLFUL_DEFAULT, BORROWER_ABSCONDED, BORROWER_MIGRATED |
| External | NATURAL_DISASTER, FAMILY_PROBLEM, OTHER |

---

### 🎯 8.4 Objection Playbook

**What it does:**
Detects mid-call pushback during negotiation (e.g., "paisa nahi hai") and injects tested counter-scripts into the LLM prompt.

**18 Objections:**

| Category | Objections | Strategy Example |
|----------|-----------|-----------------|
| 💰 Money (4) | CANT_PAY_ANYTHING, SARCASTIC_SMALL_AMOUNT, WILL_CLOSE_FULL_LATER, OTHER_LOANS_PRIORITY | Accept ₹200 and upsell |
| 🏃 Avoidance (4) | WILL_PAY_LATER_VAGUE, BUSY_RIGHT_NOW, BORROWER_NOT_HOME, PHONE_NOT_MINE | Pin down exact date |
| 😠 Hostile (3) | DO_WHATEVER_YOU_WANT, THREATENING_LEGAL, ASK_FOR_SUPERVISOR | Stay calm, state consequences |
| 📋 Claims (4) | ALREADY_PAID_CLAIM, AMOUNT_IS_WRONG, LOAN_NOT_FOR_ME, BLAMING_COMPANY | Verify details, separate issues |
| ❤️ Sensitive (3) | STAFF_COMPLAINT, EMOTIONAL_BREAKDOWN, DECEASED_FAMILY | Stop payment talk, empathize |

---

### 🛡️ 8.5 Compliance Engine

**What it does:**
Hard-coded guardrails enforced at app layer — the LLM cannot bypass these.

| Check | When | How |
|-------|------|-----|
| Time window (8AM–7PM) | Pre-call | `TenantPolicy.within_call_window()` |
| DNC flag | Pre-call | `clients.dnc_flag` check |
| Max 3 calls/day | Pre-call | COUNT from call_logs today |
| 30-min cool-off | Pre-call | Last call_end comparison |
| Blocked phrases | Every AI response | `ComplianceFilter.filter()` before TTS |
| DNC keywords | Every customer turn | `is_dnc_request()` hard-coded |
| No OD to third party | State-level | THIRD_PARTY_MESSAGE instructions |
| Banking day enforcement | PTP capture | `TenantPolicy.next_working_day()` |

---

### 📊 8.6 Analytics & Dashboard

**Dashboards:**
- Call volume by campaign, date, agent
- Disposition distribution (PTP / PARTIAL / REFUSED / CALLBACK)
- P2P promise tracking (KEPT / BROKEN / PENDING)
- OD reason distribution across portfolio
- DPD bucket migration tracking
- Average call duration and turns per disposition
- Objection frequency by category

**Built with:** HTML/CSS/JS + FastAPI REST endpoints + read-only SQL views

---

## 9. Data Design

### 9.1 Database Schema (16 Tables)

```mermaid
erDiagram
    tenants ||--o{ clients : has
    tenants ||--o{ loans : has
    tenants ||--o{ call_campaigns : runs

    clients ||--o{ loans : takes
    clients ||--o{ p2p_tracker : promises

    loans ||--o{ loan_outstanding : snapshots
    loans ||--o{ payment_history : payments

    call_campaigns ||--o{ call_queue : generates
    call_queue ||--o{ call_logs : produces
    call_logs ||--o{ call_dispositions : captures

    tenants {
        uuid id PK
        string company_name
        jsonb config_json
    }

    clients {
        int id PK
        uuid tenant_id FK
        string client_name
        string phone_primary
        boolean dnc_flag
    }

    call_dispositions {
        int id PK
        int call_log_id FK
        string disposition_code
        string od_reason
        date p2p_date
        decimal p2p_amount
        int willingness_score
    }

    p2p_tracker {
        int id PK
        int client_id FK
        date promised_date
        decimal promised_amount
        string status
        int breach_count
    }
```

**[Diagram 10: Database ER Diagram]**

### 9.2 Key Tables

| Table | Purpose | Key Fields |
|-------|---------|-----------|
| tenants | Multi-tenant company config | id, company_name, config_json |
| clients | Borrower master data | client_name, phone, dnc_flag, preferred_language |
| loans | Loan details | loan_amount, emi_amount, total_installments |
| loan_outstanding | OD snapshot (latest per loan) | total_od, days_past_due, od_bucket |
| payment_history | All payments received | payment_date, amount, mode |
| call_campaigns | Batch campaign definition | campaign_name, start_date, status |
| call_queue | Individual call items | client_id, priority, status, attempt_count |
| call_logs | Call execution records | call_start, duration, transcript_json |
| call_dispositions | Structured call outcomes | disposition_code, od_reason, p2p_date, p2p_amount |
| p2p_tracker | Promise monitoring | promised_date, status (KEPT/BROKEN/PARTIAL) |
| tenant_config | Per-tenant OD buckets, dispositions | config_type, config_data |
| field_mappings | Excel column mapping per tenant | standard_field, tenant_column_name |
| org_units | Branch/center hierarchy (self-referencing) | unit_name, parent_id |
| officers | Field officer directory | officer_name, contact_no |
| users | System users with roles | username, role, branch_access |
| upload_logs | Excel upload audit trail | filename, row_count, status |

---

## 10. Deployment Architecture

### 10.1 Docker Compose Services

```mermaid
graph TB
    subgraph "Docker Compose"
        SVC_API["⚡ backend<br/>FastAPI :8000"]
        SVC_AGENT["🤖 livekit-agent<br/>AI Worker"]
        SVC_LK["🎙️ livekit-server<br/>:7880 + :5060"]
        SVC_PG["🗄️ postgres<br/>:5432"]
        SVC_RD["⚡ redis<br/>:6379"]
        SVC_QD["🔍 qdrant<br/>:6333"]
    end

    SVC_API --> SVC_PG
    SVC_API --> SVC_RD
    SVC_API --> SVC_QD
    SVC_AGENT --> SVC_LK
    SVC_AGENT --> SVC_PG
    SVC_AGENT --> SVC_RD

    style SVC_API fill:#fff3e0
    style SVC_AGENT fill:#c8e6c9
    style SVC_LK fill:#f3e5f5
    style SVC_PG fill:#fff9c4
    style SVC_RD fill:#fce4ec
    style SVC_QD fill:#e3f2fd
```

**[Diagram 11: Docker Compose Services]**

### 10.2 External API Dependencies

| Service | Purpose | Fallback |
|---------|---------|----------|
| Sarvam AI | STT + TTS for Indian languages | Deepgram / Azure Speech |
| Google Gemini | LLM response generation | GPT-4o / Claude |
| JIO SIP | Primary telephony trunk | Exotel |
| Exotel | Secondary telephony | Twilio (future) |

---

## 11. Compliance & Regulatory

### 11.1 RBI Fair Practices Code Mapping

| RBI Requirement | Implementation | Status |
|----------------|---------------|--------|
| No calls outside 8AM–7PM | `TenantPolicy.within_call_window()` | ✅ |
| No abusive/threatening language | `ComplianceFilter.BLOCKED_PHRASES` | ✅ |
| Respect DNC requests | `is_dnc_request()` hard-coded detection | ✅ |
| No third-party disclosure | State: THIRD_PARTY_MESSAGE — no OD mention | ✅ |
| No threats of legal action | Blocked: "police", "jail", "court bhejenge" | ✅ |
| Maintain call records | CallMediaRecorder + transcript_json | ✅ |
| Borrower identity verification | State: VERIFY_RIGHT_PARTY before OD inform | ✅ |

### 11.2 Data Retention

| Data Type | Retention | Storage |
|-----------|----------|---------|
| Call recordings | 12 months | Blob Storage |
| Call transcripts | 24 months | PostgreSQL |
| Dispositions | 36 months | PostgreSQL |
| P2P tracker | 36 months | PostgreSQL |
| Audit logs | 36 months | PostgreSQL |

---

## 12. Risks & Mitigations

| Risk | Impact | Probability | Mitigation |
|------|--------|------------|------------|
| Sarvam STT accuracy in noisy calls | Low transcription quality | Medium | Fallback to Deepgram; filler filter in `intent_router.py` |
| LLM generates non-compliant response | Regulatory violation | Low | `ComplianceFilter` runs on EVERY response before TTS |
| Customer uses unseen objection phrasing | Objection missed | Medium | Phase 2: pgvector semantic matching; Phase 3: fine-tuned classifier |
| SIP trunk downtime | Calls can't be placed | Low | Dual-mode telephony (JIO SIP + Exotel runtime switch) |
| Database overload during batch calling | Slow context building | Low | Redis cache (15-min TTL); asyncio.gather for parallel queries |
| Borrower death reported incorrectly | Inappropriate payment push | Medium | DECEASED_REPORT → INSURANCE_CLAIM state; no payment discussion |
| Broken promise rate high | Low recovery | Medium | Automated re-queue with HIGH priority; DPD-tone escalation |

---

## 13. Success Metrics & KPIs

```mermaid
graph TD
    KPI1["📞 Call Volume<br/>Target: 1000+/day"]
    KPI2["✅ PTP Rate<br/>Target: 40%+ calls"]
    KPI3["💰 Promise Kept Rate<br/>Target: 60%+ promises"]
    KPI4["📊 Disposition Quality<br/>Target: 95%+ structured"]
    KPI5["🛡️ Compliance Rate<br/>Target: 100%"]
    KPI6["⏱️ Avg Call Duration<br/>Target: 2-4 minutes"]
    KPI7["🎯 Objection Handle Rate<br/>Target: 80%+ detected"]

    GOAL["🎯 Overall Goal:<br/>2x Recovery Rate<br/>vs Human Callers"]

    KPI1 -.-> GOAL
    KPI2 -.-> GOAL
    KPI3 -.-> GOAL
    KPI4 -.-> GOAL
    KPI5 -.-> GOAL
    KPI6 -.-> GOAL
    KPI7 -.-> GOAL

    style KPI1 fill:#e3f2fd
    style KPI2 fill:#c8e6c9
    style KPI3 fill:#fff9c4
    style KPI4 fill:#f3e5f5
    style KPI5 fill:#ffcdd2
    style KPI6 fill:#fff3e0
    style KPI7 fill:#fce4ec
    style GOAL fill:#a5d6a7
```

**[Diagram 12: KPI Dashboard]**

### ✅ Transparency & Auditability
All calls recorded with transcripts, dispositions, and state transitions logged for complete audit trail.

### ✅ Compliance Readiness
100% adherence to RBI Fair Practices Code with hard-coded app-level enforcement, not prompt-dependent.

---

## 14. 🔄 AI Call Execution Flow

### 14.1 🛠️ Pre-requisites

#### 📞 Telephony Setup
- JIO SIP trunk configured with LiveKit SIP bridge
- Exotel account as backup telephony provider
- SIP trunk IDs stored in `.env`

#### 📊 Data Setup
- Excel uploaded with borrower + loan + outstanding data
- Field mapping configured per tenant
- Campaign created with call queue populated

### 14.2 🤖 Call Execution — Single Turn Flow

| Step | Action |
|------|--------|
| 1. Audio Capture | Customer speaks → LiveKit captures audio frames |
| 2. VAD Detection | Silero VAD detects speech end (0.8s silence) |
| 3. STT Transcription | Sarvam STT converts audio → text |
| 4. DNC Check | Hard-coded keyword scan for "stop calling" |
| 5. Objection Scan | Keyword match against 18 objection trigger phrases |
| 6. State Instruction | State machine provides current state guidance |
| 7. Prompt Assembly | 6-section prompt built (~4000 chars) |
| 8. LLM Generation | Gemini generates response (SPEAK + META format) |
| 9. Response Parsing | Split speech text from metadata JSON |
| 10. Compliance Filter | Blocked phrase check before TTS |
| 11. State Update | Metadata routed to state machine methods |
| 12. TTS Synthesis | Sarvam TTS converts text → audio |
| 13. Audio Publish | LiveKit → SIP → PSTN → customer hears |

### 14.3 📊 Complete Call Timeline

```mermaid
graph TD
    A["📞 Queue Picks Call<br/>Step 0"] -->|Compliance| B["✅ Pre-Check Passed<br/>Step 1"]
    B -->|DB Query| C["📊 Context Built<br/>Step 2"]
    C -->|LiveKit| D["🎙️ Room Created<br/>Step 3"]
    D -->|SIP Dial| E["📱 Customer Phone Rings<br/>Step 4"]
    E -->|Answers| F["🤖 AI Greets<br/>GREETING"]
    F -->|Response| G{"Who Answered?"}

    G -->|Borrower| H["✅ VERIFY → CONSENT<br/>→ INFORM_DUES"]
    G -->|Family| I["⚠️ THIRD_PARTY<br/>→ CALLBACK"]
    G -->|Wrong Number| J["❌ CLOSE<br/>WRONG_NUMBER"]

    H --> K["🧠 REASON_PROBE<br/>Listen & Classify"]
    K -->|Reason Detected| L["📘 HANDLE_REASON<br/>JSON Flow Steps"]
    K -->|No Specific| M["💰 NEGOTIATE<br/>DPD-Bucket Tone"]

    L --> M
    M --> N["📋 COMMITMENT_CAPTURE<br/>Date + Amount + Mode"]
    N --> O["✅ RECAP<br/>Confirm PTP"]
    O --> P["🏁 CLOSE<br/>Save Disposition"]
    I --> P

    P --> Q["💾 Save to DB<br/>+ Recording"]
    Q --> R["📊 P2P Tracker<br/>Auto-Created"]

    style A fill:#e3f2fd
    style B fill:#c8e6c9
    style C fill:#e3f2fd
    style D fill:#f3e5f5
    style E fill:#f3e5f5
    style F fill:#c8e6c9
    style G fill:#fff3e0
    style H fill:#c8e6c9
    style I fill:#fff9c4
    style J fill:#ffcdd2
    style K fill:#e3f2fd
    style L fill:#f3e5f5
    style M fill:#fff3e0
    style N fill:#e3f2fd
    style O fill:#c8e6c9
    style P fill:#eceff1
    style Q fill:#fff9c4
    style R fill:#a5d6a7
```

**[Diagram 13: Complete AI Call Timeline — Queue to P2P Tracker]**

---

## Appendix: Complete File Architecture

```mermaid
graph TB
    subgraph "Voice Pipeline"
        LA["🤖 livekit_agent.py<br/>AI Agent Worker"]
    end

    subgraph "OD Layer 3 Engine"
        SM["🔄 state_machine.py<br/>21 States"]
        CT["📋 contracts.py<br/>Enums & Dataclasses"]
        IR["🧠 intent_router.py<br/>Language + Intent"]
        PR["📋 prompting.py<br/>DPD-Bucket Tone"]
        RR["📘 reason_registry.py<br/>JSON Loader"]
        OR["🎯 objection_registry.py<br/>Keyword Matcher"]
        CF["🛡️ compliance_filter.py<br/>Blocked Phrases"]
        CB["📊 context_builder.py<br/>7 DB Queries"]
        CP["🔌 context_provider.py<br/>Mock + Postgres"]
    end

    subgraph "Data Files"
        RF["📘 reason_flows.json<br/>23 Reason Trees"]
        OP["🎯 objection_playbook.json<br/>18 Counters"]
    end

    subgraph "Services"
        API["⚡ main.py<br/>FastAPI"]
        TEL["📞 telephony/<br/>JIO SIP + Exotel"]
        DB["🗄️ database/<br/>Call Logs DB"]
    end

    LA --> SM
    SM --> CT
    SM --> IR
    SM --> PR
    SM --> RR
    SM --> OR
    SM --> CF
    SM --> CB
    CB --> CP
    RR --> RF
    OR --> OP
    LA --> API
    API --> TEL
    API --> DB

    style LA fill:#c8e6c9
    style SM fill:#e3f2fd
    style CT fill:#e3f2fd
    style IR fill:#fff9c4
    style PR fill:#f3e5f5
    style RR fill:#c8e6c9
    style OR fill:#fff3e0
    style CF fill:#ffcdd2
    style CB fill:#e3f2fd
    style CP fill:#eceff1
    style RF fill:#c8e6c9
    style OP fill:#fff3e0
    style API fill:#fff3e0
    style TEL fill:#f3e5f5
    style DB fill:#fff9c4
```

**[Diagram 14: Complete File Architecture]**

---

**Document End**

**Generated:** 2026-03-17
**Version:** 3.0
**Format:** Markdown with Mermaid Diagrams (GitHub-Compatible)

**Key Features in v3.0:**
✅ 21-state call state machine with JSON-driven reason flows
✅ 23 OD reason conversation trees (no code changes to add new reasons)
✅ 18 objection counter-scripts with keyword matching
✅ DPD-bucket-specific negotiation tone (soft → urgent → recovery)
✅ App-level compliance engine (blocked phrases, DNC, time limits)
✅ Multi-tenant database with RLS and configurable OD buckets
✅ Provider-agnostic architecture (switchable STT/TTS/LLM/telephony)
✅ Automated P2P tracker with broken-promise re-queuing
✅ Full call recording + transcript logging + structured dispositions
✅ Dual telephony mode (JIO SIP + Exotel) with runtime switching
