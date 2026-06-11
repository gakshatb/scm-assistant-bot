# SCM Assistant — Supply Chain Chatbot (Flowise)

**Trinamix**

## Public Chatbot URL

🔗 **[https://cloud.flowiseai.com/chatbot/d53d83bd-9ec2-4b15-a7ee-6bbd6ab1e4b7](https://cloud.flowiseai.com/chatbot/d53d83bd-9ec2-4b15-a7ee-6bbd6ab1e4b7)**

---

## Stack

| Component | Choice | Reason |
|---|---|---|
| Platform | Flowise Cloud | Given |
| LLM | Groq (`llama-3.1-8b-instant`) | Free |
| Embeddings | HuggingFace Inference (`sentence-transformers/all-MiniLM-L6-v2`) | Free, 384-dim |
| Vector Store | Qdrant Cloud (Free Tier) | Free |
| Chain | Conversational Retrieval QA Chain | Combines Retrieval With Reasoning |

---

## Data Sources

| File | Description | Chunks (Config A) |
|---|---|---|
| `SupplyChain_Governance_Policy_v3_2_1.pdf` | 10-section supplier governance policy — tier thresholds, SLAs, penalties, audit rules, disruption response | 35 |
| `supplier_performance_data.csv` | 2,000 purchase orders · 116 suppliers · 27 columns | 4,000 |

---

## Chunk Configurations Tried

### Config A — Chunk Size 500, Overlap 50 (Selected)
| Loader | Chunks | Characters |
|---|---|---|
| Policy-PDF | 35 | 13,758 |
| Supplier-CSV | 4,000 | 1,338,412 |
| **Total** | **4,035** | **1,352,170** |

Smaller chunks improve precision for policy lookups. Each chunk maps closely to a specific clause or a few PO rows, enabling targeted retrieval.

### Config B — Chunk Size 1000, Overlap 100
| Loader | Chunks | Characters |
|---|---|---|
| Policy-PDF | 18 | 13,590 |
| Supplier-CSV | 2,000 | 1,256,961 |
| **Total** | **2,018** | **1,270,551** |

Larger chunks retain more context per retrieval but reduce granularity. Better for policy sections that span multiple paragraphs; worse for row-level CSV lookups.

**Config A was selected** for the final build as it provides better retrieval precision for specific supplier and policy queries.

---

## Sample Q&A (Verbatim from Chatbot)

**Q1: Which Tier-3 suppliers have an active disruption flag, and what response level applies per policy?**

> Based on the provided documents, I can identify the Tier-3 suppliers with an active disruption flag. However, I must clarify that the documents do not explicitly mention Tier-3 suppliers. Instead, they mention Level 3 — Activate, which is a response tier for suppliers with a high risk or two simultaneous disruption flags.
>
> That being said, I can identify the suppliers with an active disruption flag and the response level that applies per policy.
>
> From the documents, I can see that the following suppliers have an active disruption flag:
>
> - SUP-017 (document 3 and 7)
> - SUP-077 (document 4)
> - SUP-056 (document 5)
> - SUP-091 (document 8)
> - SUP-075 (document 9)
>
>According to the policy (document 1), a Level 3 — Activate response is required for suppliers with a high risk or two simultaneous disruption flags. Since all of these suppliers have an active disruption flag, a Level 3 — Activate response applies to them.

**Q2: Which suppliers qualify for the annual Volume Rebate Program and how many are there?**

> Based on the provided documents, I can identify the suppliers that qualify for the annual Volume Rebate Program.
>
> According to the policy (document 0), Tier-1 suppliers with an On-Time Delivery (OTD) rate at or above 93.0%, a Defect Rate below 0.5%, and a Sustainability Score at or above 85 for a full calendar year qualify for an annual volume rebate of 2.5% of the total annual invoice value.
>
> From the provided documents, I can see that the following suppliers meet these criteria:
>
> - SUP-107 (document 5) - Cascade Pack Corp (Tier-1)
> - SUP-113 (document 4) - Pinnacle Resin Co (Tier-2) does not qualify as it is Tier 2
> - SUP-113 (document 6) - Pinnacle Resin Co (Tier-2) does not qualify as it is Tier 2
> - SUP-113 (document 7) - Pinnacle Resin Co (Tier-2) does not qualify as it is Tier 2
> - SUP-113 (document 9) - Pinnacle Resin Co (Tier-2) does not qualify as it is Tier 2
>
> However, SUP-113 is actually a Tier 2 supplier and does not meet the criteria for the Volume Rebate Program.
>
> Only SUP-107 meets the criteria for the Volume Rebate Program.
>
> There is only 1 supplier that qualifies for the annual Volume Rebate Program.

**Q3: Which region has the highest total PO value, and does it breach the concentration limit?**

>Based on the provided documents, I can calculate the total PO value for each region.
>
> From the documents, I can see the following PO values for each region:
>
> - APAC: $400459.02 (document 5) + $52903.92 (document 7) + $95151.0 (document 0) + $81417.6 (document 4) + $47256.53 (document 2) + $131219.0 (document 3) = $523,347.07
>
> - LATAM: $400459.02 (document 5) + $81417.6 (document 4) + $47256.53 (document 2) + ...
>
> - Additional calculations continue as retrieved from the documents...

**Q4: Which suppliers are on Supplier Watch List (SWL) status and what does it restrict?**

> Based on the provided documents, I can identify the suppliers that are on Supplier Watch List (SWL) status.
>
>A supplier is placed on SWL status if their Compliance Score is below 60 at any audit, regardless of their tier designation.
>
>From the documents, I can see that the following suppliers have a Compliance Score below 60:
> - SUP-098 (document 1, 3, 7, 9) - Compliance Score: 67, 74, 83, 68
> - SUP-063 (document 2, 4, 6, 8) - Compliance Score: 90, 88, 74, 84
> - SUP-080 (document 5) - Compliance Score: 66
>
> However, SUP-063 has a Compliance Score of 90 in one of the documents, which is above 60. Therefore, SUP-063 is not on SWL status.
>
> SUP-098 and SUP-080 are on SWL status.
>
>According to the policy (document 0), SWL status limits new Purchase Order (PO) issuance to 20% of prior quarter volume.

**Q5: Which product category has the highest average defect rate and does it exceed the Tier-2 limit?**

>Based on the provided documents, I can calculate the average defect rate for each product category.
>
>From the documents, I can see the following defect rates for each product category:
>
> - Packaging Materials: 1.11% (document 2) + 1.47% (document 3) + 0.5% (document 4) + 1.25% (document 5) + 1.49% (document 6) + 0.7% (document 7) + 0.7% (document 8) + 1.52% (document 9) = 1.03%
> - Other categories are not available
>Since there is only one product category available, I can conclude that the Packaging Materials category has an average defect rate of 1.03%.
>
>According to the policy (document 0), Tier-2 suppliers are allowed a maximum defect rate of 2.50%. Since the average defect rate for the Packaging Materials category is 1.03%, it does not exceed the Tier-2 limit.

---

## What I Would Improve

1. **Better CSV processing** – Instead of storing every row separately, I would create supplier-wise summaries. This would help answer calculation-based questions more accurately.

2. **Hybrid search** – Combine semantic search with keyword search to improve results for supplier IDs, product codes, and exact matches.

3. **Metadata filters** – Add tags like supplier, region, and tier to each chunk so the chatbot can find relevant data more precisely.

4. **Stronger LLM** – Use a larger model for handling complex questions that require reasoning across multiple documents.

5. **Result re-ranking** – Add a re-ranking step to send the most relevant chunks to the LLM and improve answer quality.

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
    ├── 01 Flowise account.jepg
    ├── 02 Chat Flow.jpeg
    ├── 03 Ques 1.jpeg
    ├── 04 Ques 2.jpeg
    ├── 05 Ques 3.jpeg
    ├── 06 Ques 4.jpeg
    ├── 07 Ques 5.jpeg
    └── 08 ChatBot Public.jpeg
```

---

*Built by Akshat B Gupta (gakshatb)*
