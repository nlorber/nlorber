# Nathan Lorber

AI/ML Engineer with 3+ years of experience building production ML and LLM systems end-to-end. Background in Physics (MSc, Strasbourg/CERN) and Data Science (CentraleSupélec).

Currently focused on applied ML, LLM tooling, and AI security.

## Projects

> These projects use synthetic data and mock APIs. Architecture and design patterns are inspired by production systems.

### [transaction-classifier](https://github.com/nlorber/transaction-classifier)
Multi-class classification system that predicts French accounting codes from financial transaction data. XGBoost with domain-specific feature engineering (entity detection, fiscal period signals, SEPA fields), temporal train/val split, multi-client isolation, and a FastAPI inference API with hot-reload and artifact checksums.

```mermaid
flowchart LR
    DB[(Postgres\nper-client)] --> FE[Feature Pipeline\nTF-IDF · domain · numeric · date]
    FE --> XGB[XGBoost\n+ Optuna HPO]
    XGB --> ART[Versioned Artifacts\natomic symlink promotion]
    ART --> API[FastAPI\nhot-reload · multi-client]
```

**Python · XGBoost · scikit-learn · FastAPI · Optuna · SHAP**

### [mcp-rest-bridge](https://github.com/nlorber/mcp-rest-bridge)
Production-ready MCP server template for wrapping any REST API as LLM-usable tools, prompts, and resources. Includes JWT auth with auto-refresh, allowlist-based field filtering, dual transport (stdio + HTTP), and a 22-scenario LLM-as-judge adversarial test suite covering prompt injection, privilege escalation, and data isolation attacks.

```mermaid
flowchart LR
    LLM[LLM Client] -->|MCP| SRV[MCP Server\ntools · prompts · resources]
    SRV -->|JWT auth| API[REST API]
    SRV --> FLT[Allowlist Filter\nfield-level protection]
    SRV --> ADV[Adversarial Tests\n22 scenarios · LLM-as-judge]
```

**TypeScript · MCP · Zod · Vitest · Claude API**

### [hybrid-recsys](https://github.com/nlorber/hybrid-recsys)
Multilingual content recommendation engine combining dual retrieval (dense embeddings + TF-IDF), Reciprocal Rank Fusion, and optional LLM re-ranking with automatic fallback. Per-language Annoy indexes, duration-aware scoring, and a FastAPI serving layer.

```mermaid
flowchart LR
    Q[Query] --> EMB[Dense Embeddings]
    Q --> TF[TF-IDF]
    EMB --> ANN[Annoy ANN Search\nper-language indexes]
    TF --> ANN
    ANN --> RRF[RRF Fusion]
    RRF --> LLM[LLM Re-rank\nwith fallback]
    LLM --> API[FastAPI]
```

**Python · OpenAI embeddings · scikit-learn · Annoy · spaCy · FastAPI**

### [llm-firewall](https://github.com/nlorber/llm-firewall)
Personal project exploring LLM security. Fine-tuned DeBERTa-v3-base classifier for prompt threat detection (injection, jailbreak, exfiltration, escalation) with a LangGraph orchestration layer that routes ambiguous prompts to a Claude LLM judge. The hybrid approach cuts LLM API costs by ~80-90% vs. classifying every prompt with an LLM.

```mermaid
flowchart LR
    P[Prompt] --> CLS[DeBERTa Classifier\n~10ms]
    CLS -->|CLEAN| PASS[Pass]
    CLS -->|GRAY| JDG[Claude Judge\n~500ms]
    CLS -->|BLOCK| BLK[Block + Log]
    JDG -->|PASS| PASS
    JDG -->|BLOCK| BLK
```

**Python · PyTorch · HuggingFace Transformers · DeBERTa-v3 · LangGraph · Claude API · SHAP · FastAPI · Docker**

## Stack

**Portfolio:** Python · TypeScript · XGBoost · scikit-learn · FastAPI · MCP · RAG · Zod · Docker · Optuna · spaCy

**Also used professionally:** PyTorch · TensorFlow · LangChain · Kubernetes · Terraform · Snowflake · dbt · AWS · Azure

## Contact

[LinkedIn](https://linkedin.com/in/nathan-lorber) · nlorber2211@gmail.com
