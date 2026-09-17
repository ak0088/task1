# System Architecture & Technical Specifications

## 1. High-Level Workflow
```mermaid
graph TD
    subgraph Client ["🖥️ Client Application (React 19 + Tailwind CSS)"]
        UI[User Interface & Dashboards]
        KPI[Real-time KPI & Health Score Widget]
        AgentUI[Agent Execution Workspace]
        NotesUI[Colourful & Short Notes Explorer]
        ExportUI[GitHub Code Exporter Modal]
    end

    subgraph Server ["⚡ Gateway & Controller Layer (Express + TypeScript)"]
        AuthMid[JWT & OAuth Authentication]
        ProjCtrl[Project & State Controller]
        AgentOrch[Multi-Agent Orchestrator]
        KeyVault[Centralized API Key & Quota Vault]
    end

    subgraph Agents ["🧠 Autonomous Intelligence Pipeline"]
        A1[Idea Validator Agent]
        A2[Topic Refiner Agent]
        A3[Timeline Planner Agent]
        A4[Risk Assessor Agent]
        A5[Documentation Generator Agent]
        Chat[AI Academic Mentor Chatbot]
    end

    subgraph AI ["✨ AI Reasoning Engine"]
        Gemini[Google Gemini 2.5 Flash]
        Fallback[Deterministic Academic Heuristic Engine]
    end

    subgraph DB ["💾 Storage & Persistence Layer"]
        SQLite[(SQLite Database / ACID Storage)]
    end

    subgraph External ["🌐 External Ecosystem & Integrations"]
        GitHub[GitHub REST API (Repo & Code Push)]
        OAuthProv[Google & GitHub OAuth Providers]
    end

    UI --> AuthMid
    UI --> ProjCtrl
    AgentUI --> AgentOrch
    ExportUI --> GitHub

    AuthMid --> OAuthProv
    ProjCtrl --> SQLite
    AgentOrch --> KeyVault
    KeyVault --> Gemini
    Gemini -.->|Quota fallback| Fallback
    AgentOrch --> A1 & A2 & A3 & A4 & A5 & Chat
    A1 & A2 & A3 & A4 & A5 --> ProjCtrl
    ProjCtrl --> KPI

```

## 2. Textual Workflow Architecture
```text
+-------------------------------------------------------------------------------+
|                       AGPPTPPMA ARCHITECTURAL FLOW                           |
+-------------------------------------------------------------------------------+
|                                                                               |
|  [CLIENT LAYER: React 19 + Tailwind + Motion UI]                               |
|   |--> Student Dashboard & KPI Health Scores (0-100)                          |
|   |--> 5-Agent Interactive Workspace & Live Visualizers                       |
|   |--> Colourful Flashcard Notes & Viva Voce Quick Revision                  |
|   |--> Workflow Architecture & System Flow Diagram                            |
|   +--> One-Click GitHub Direct Code Exporter                                  |
|         |                                                                     |
|         v (REST API + JWT Bearer Auth)                                        |
|  [GATEWAY LAYER: Express.js + Auth & Key Vault]                               |
|   |--> OAuth 2.0 (Google & GitHub SSO Authentication)                         |
|   |--> Centralized Gemini API Key & Quota Policy Engine                       |
|   +--> Context Assembly Engine (Historical state aggregation)                |
|         |                                                                     |
|         v (Stateful Orchestration)                                            |
|  [INTELLIGENCE LAYER: 5 Autonomous Agents + AI Mentor]                        |
|   +--- (1) Idea Validator   -----> Feasibility & Academic Novelty             |
|   +--- (2) Topic Refiner    -----> Problem Statement & Scope                 |
|   +--- (3) Timeline Planner -----> Work Breakdown Structure & Milestones      |
|   +--- (4) Risk Assessor    -----> Threat Severity Matrix & Mitigations      |
|   +--- (5) Document Gen     -----> Full IEEE Proposal & Master Report         |
|   +--- (6) AI Mentor Chat   -----> Interactive Step-by-Step Advisor           |
|         |                                                                     |
|         +---> [AI ENGINE: Gemini 2.5 Flash <---> Fallback Heuristics]         |
|         |                                                                     |
|         v (Atomic Transactions)                                               |
|  [STORAGE & EXPORT LAYER]                                                     |
|   +---> SQLite Database (ACID, Foreign Key Cascades)                          |
|   +---> GitHub REST API (Direct Commit & Repository Push)                     |
|   +---> JSZip Archive Packager (Complete Source Code Bundle)                  |
+-------------------------------------------------------------------------------+
```

## 3. Data Flow Specification
### Step 1: Student / Client UI -> Express Gateway
- **Protocol**: `HTTP POST / JSON`
- **Payload**: Project Title, Description & Domain
- **Description**: Student creates or updates project specifications

### Step 2: Express Gateway -> SQLite Database
- **Protocol**: `SQL INSERT / PRAGMA`
- **Payload**: Project & User Record
- **Description**: Persists project parameters with relational foreign key linkage

### Step 3: Express Gateway -> Context Assembler
- **Protocol**: `In-Memory Engine`
- **Payload**: Historic Agent Outputs & Status
- **Description**: Gathers cumulative project state for contextual agent prompting

### Step 4: Agent Controller -> Gemini AI / Fallback
- **Protocol**: `REST / HTTPS API`
- **Payload**: Structured Prompt & Schema Rules
- **Description**: Executes autonomous agent reasoning with graceful deterministic fallback

### Step 5: Agent Controller -> Milestone & Risk DB
- **Protocol**: `SQL Batch Insert`
- **Payload**: Structured Deliverables & Mitigations
- **Description**: Automatically populates project roadmap and risk matrix tables

### Step 6: Health Calculator -> Client Dashboard
- **Protocol**: `REST Response`
- **Payload**: Health Score (0-100) & Status Metrics
- **Description**: Re-evaluates health metrics and updates KPI widgets in real-time

### Step 7: Client UI -> GitHub API Gateway
- **Protocol**: `REST API / Bearer Token`
- **Payload**: Full Codebase & Documentation Files
- **Description**: Directly creates repo on GitHub and commits full project codebase


## 4. Security & Compliance
- Bearer JWT token verification for all authenticated endpoints.
- Role-based authorization isolating student modifications from faculty mentor oversight.
- Data sanitization and parameterized SQL statements preventing injection attacks.
