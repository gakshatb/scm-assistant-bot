# SCM Assistant — Supply Chain Chatbot (Flowise)

**Trinamix**

## Public Chatbot URL

🔗 **[https://cloud.flowiseai.com/chatbot/d53d83bd-9ec2-4b15-a7ee-6bbd6ab1e4b7](https://cloud.flowiseai.com/chatbot/d53d83bd-9ec2-4b15-a7ee-6bbd6ab1e4b7)**

---

## Data Sources

| File | Description | Chunks |
|---|---|---|
| `SupplyChain_Governance_Policy_v3_2_1.pdf` | 10-section supplier governance policy — tier thresholds, SLAs, penalties, audit rules, disruption response | 35 |
| `supplier_performance_data.csv` | 2,000 purchase orders · 116 suppliers · 27 columns | 4,000 |

---

## Chunk Configuration

### Config — Chunk Size 500, Overlap 50

| Loader | Chunks | Characters |
|---|---|---|
| Policy-PDF | 35 | 13,758 |
| Supplier-CSV | 4,000 | 1,338,412 |
| **Total** | **4,035** | **1,352,170** |
---

## Architecture

```
User Query
    ↓
HuggingFace Inference Embeddings (all-MiniLM-L6-v2)
    ↓
Qdrant Vector Store (scm-store collection, 4035 vectors, dim=384)
    ↓ Top-10 chunks retrieved
Conversational Retrieval QA Chain
    ↓
Groq LLM (llama-3.1-8b-instant)
    ↓
Response
```
---
## Repository Structure
```
scm-assistant-bot/
├── scm_assistant.json
├── README.md
├── .gitignore
└── screenshots/
```

---

*Built by Akshat B Gupta (gakshatb)*
