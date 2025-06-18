# OracleGuard AI – Architecture Design

## 🚀 Overview

OracleGuard AI is an AI-powered platform built to **detect**, **analyze**, **simulate**, and **mitigate** oracle manipulation risks in DeFi smart contracts. Inspired by the **UwU Lend exploit (June 2024)**—a flash-loan attack that artificially inflated CRV prices and led to a ~$19.5 M loss—OracleGuard AI combines static analysis, AI reasoning, and on-chain simulation to help developers and auditors catch and remediate weak oracle designs **before** they can be exploited.

---

## 🏛️ System Architecture

Below is a high-level component diagram illustrating how **User**, **API**, **Core Modules**, and **External Integrations** collaborate to produce risk reports and recommendations.

```mermaid
graph TD
  %% Clients
  subgraph Client
    U["User / Developer"]
  end

  %% API Layer
  subgraph API_Layer
    API["API / Dashboard"]
  end

  %% Core System
  subgraph Core_System
    Scanner["Oracle Scanner"]
    LLM["LLM Reasoning Engine"]
    Sim["Attack Simulation Engine"]
    Risk["Risk Scoring Engine"]
    Mitigation["Mitigation Suggestion Engine"]
    Report["Report Generator"]
  end

  %% External Integrations
  subgraph External_Integrations
    RPC["Ethereum / EVM RPC"]
    Fork["Chain Fork (Anvil/Foundry)"]
    LLM_API["LLM API (OpenAI / Local)"]
    Explorer["Etherscan / Block Explorer"]
  end

  %% Core Flows
  U --> API
  API --> Scanner
  API --> LLM
  API --> Report

  Scanner --> LLM
  LLM --> Sim
  Sim --> Risk
  Risk --> Mitigation
  Mitigation --> Report
  Report --> API

  %% External Data Fetch
  Scanner --> Explorer
  Sim --> RPC
  Sim --> Fork
  LLM --> LLM_API
```
## End-to-end interaction
The end-to-end interaction from contract submission to report delivery, emphasizing the role of each core module.
```mermaid
sequenceDiagram
    participant U as User
    participant API as API / Dashboard
    participant Agent as OracleGuard AI Agent
    participant Scanner as Oracle Scanner
    participant LLM as LLM Engine
    participant Sim as Simulation Engine
    participant Risk as Risk Scorer
    participant Report as Report Generator

    U->>API: Submit contract address or source code
    API->>Agent: Forward contract details
    Agent->>Scanner: Parse contract (AST/ABI)
    Scanner-->>Agent: Oracle patterns & dependencies

    Agent->>LLM: Analyze oracle design & vulnerability
    LLM-->>Agent: Provide security assessment

    alt Simulation enabled
        Agent->>Sim: Execute flash-loan manipulation test
        Sim-->>Agent: Return simulation impact data
    end

    Agent->>Risk: Compute overall risk score
    Risk-->>Agent: Return risk level & metrics

    Agent->>Report: Generate comprehensive report
    Report-->>API: Report ready
    API-->>U: Display risk profile & recommended fixes

```