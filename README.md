# FermentAI 🧠⚡

> **Agentic Knowledge Fermentation Engine** — Your data evolves like fine wine, not dead storage.

[📖 **中文文档**](README.zh.md) | [English](README.md)

[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![Ollama](https://img.shields.io/badge/Ollama-Compatible-green.svg)](https://ollama.com)
[![RAG](https://img.shields.io/badge/RAG-Agentic%20RAG%202.0-orange.svg)](docs/architecture.md)

---

**Build a domain-expert LLM on consumer hardware. No fine-tuning. No GPU cluster. No vendor lock-in.**

---

## 🎯 What FermentAI Solves

| Pain Point | FermentAI's Answer |
|------------|-------------------|
| Fine-tuning costs $$$ | **Zero training cost** — enhanced retrieval replaces weight updates |
| Static vector DBs | **Living knowledge graph** — connections form and decay naturally |
| Agent silos | **Multi-agent orchestration** — Claude, GPT, local LLMs share one brain |
| Data privacy nightmares | **100% local deployment** — your data never leaves your server |
| Knowledge rot | **Heat-driven curation** — hot topics surface, stale content fades |

---

## 🔬 Core Innovation: Knowledge Fermentation

> Like brewing — raw material (data) + yeast (usage) + time = value

```
Traditional:  Store → Query → Done (data stays dead)
FermentAI:    Store → Query → Trace → Accumulate → Trigger → Evolve → Smarter queries
               ↑_____________________________________________________________↓
```

**Three fermentation cycles:**

| Cycle | Trigger | Action |
|-------|---------|--------|
| **Conversation → Knowledge** | Topic queried ≥ 3× in 30 days | Auto-download latest papers, link to conversations |
| **Code → Knowledge** | Module reused ≥ 3× | Link to algorithm papers, insert citations, generate best-practice guides |
| **Agent → Agent** | ≥ 10 task samples accumulated | Rank agents by task type, auto-route future tasks to best performers |

---

## 🏗️ Architecture

```
┌──────────────────────────────────────────────────────────────┐
│                    AGENT LAYER (Claude / GPT / Local LLM)     │
│  Unified API Gateway  →  Agent Registry  →  Dynamic Router    │
└────────────────────────────┬─────────────────────────────────┘
                             ↓
┌──────────────────────────────────────────────────────────────┐
│                 FERMENTATION ENGINE                           │
│  Triggers → Rules Engine → Executor → Insight Generator      │
│  (high-freq query → auto-research)  (code reuse → link paper) │
└────────────────────────────┬─────────────────────────────────┘
                             ↓
┌──────────────────────────────────────────────────────────────┐
│                 FOUR-TIER KNOWLEDGE VAULTS                    │
│  Knowledge (Chroma)  │  Conversations  │  Code  │  Meta-Graph │
│  papers · concepts   │  history · tags  │ snippets · patterns │
└──────────────────────────────────────────────────────────────┘
```

---

## ⚡ Quick Start

```bash
# Clone
git clone https://github.com/Invovel/FermentAI.git && cd FermentAI

# Install
pip install -r requirements.txt

# Pull embedding model (Ollama)
ollama pull nomic-embed-text

# Build knowledge graph from your Obsidian vault
export FERMENT_VAULT_PATH="/path/to/your/vault"
python fermentai build

# Start API server
python fermentai serve
```

```python
# Query your domain-expert system
import requests
r = requests.post("http://localhost:8000/query", json={
    "query": "Latest advances in RAG for protein design",
    "top_k": 5,
    "use_hyde": True,
    "use_rerank": True
})
print(r.json()["answer"])
```

---

## 📊 vs Traditional Approaches

| | Fine-Tuning | Vanilla RAG | FermentAI |
|--|:-:|:-:|:-:|
| **Cost to build** | $$$$ GPU cluster | $$ Mid | $ **Consumer laptop** |
| **Update cost** | Re-train | Re-index | **Auto-evolves** |
| **Knowledge linking** | ❌ None | ❌ None | ✅ **Graph-driven** |
| **Dynamic ranking** | ❌ Static | ❌ Static | ✅ **Heat-weighted** |
| **Multi-agent** | ❌ | ❌ | ✅ **Capability router** |
| **Explainability** | ❌ Black box | ⚠️ Partial | ✅ **Full provenance** |
| **Privacy** | ⚠️ Cloud | ⚠️ Cloud | ✅ **100% local** |

---

## 🎯 Use Cases

### Lab Knowledge Hub
> "Our bioinformatics lab has 10 years of papers. FermentAI connects them into a living graph — new members onboard in days, not months."

### Personal Compound Knowledge
> "I query 'diffusion models' repeatedly. FermentAI noticed, auto-downloaded 3 new papers, and pushed a notification. My knowledge is actively growing."

### Enterprise Asset Intelligence
> "Company docs scattered across Confluence, GitHub, Slack. FermentAI unified them into one graph. Support agents query with precision. Dev agents reuse proven code."

---

## 🛠️ Tech Stack

| Component | Technology |
|-----------|------------|
| Vector DB | Chroma (local, lightweight) |
| Knowledge Graph | Custom graph engine (NetworkX + weighted edges) |
| Embedding | Ollama `nomic-embed-text` (free, local) |
| Generation | Ollama / Claude / OpenAI / any compatible API |
| Retrieval | Hybrid: Vector + BM25 + RRF fusion + Cross-Encoder rerank |
| Query Enhancement | Multi-Query expansion + HyDE (Hypothetical Document Embeddings) |
| Frontend | Obsidian (vault browser) + FastAPI (REST API) |

---

## 🗺️ Roadmap

- [x] Knowledge graph construction
- [x] Heat-driven retrieval
- [x] Core fermentation rules
- [ ] Multi-agent capability registry & router
- [ ] Auto literature search & ingest
- [ ] Code-paper auto-linking
- [ ] Cross-lab knowledge federation
- [ ] Web UI dashboard

---

## 📚 Documentation

| Document | Content |
|----------|---------|
| [Architecture](docs/architecture.md) | Full system design & data flow |
| [Fermentation](docs/fermentation.md) | Trigger-rule-executor mechanism |
| [Agent Integration](docs/agent-integration.md) | Multi-agent protocol |
| [API Reference](docs/api.md) | REST API endpoints |
| [Deployment](docs/deployment.md) | Lab server setup |
| [Expert Consultation](docs/expert-consultation.md) | Questions for domain experts |

---

## 💬 Seeking Expert Feedback

We are actively seeking guidance from:

- **LLM Architects** — multi-agent orchestration, hallucination mitigation
- **Knowledge Graph Experts** — large-scale graph construction, temporal KG
- **RAG Researchers** — advanced retrieval, domain adaptation, evaluation
- **Lab PIs** — real-world knowledge management, workflow integration

📧 **Contact**: indegceyuan@outlook.com

See [Expert Consultation Questions](docs/expert-consultation.md) for details.

---

## 📄 License

MIT License — see [LICENSE](LICENSE). Free for personal & academic use. Commercial use requires authorization.

---

## 🙏 Acknowledgments

Built on the shoulders of giants:
- [LangChain](https://github.com/langchain-ai/langchain) — RAG infrastructure
- [Ollama](https://github.com/ollama/ollama) — Local model runtime
- [Chroma](https://github.com/chroma-core/chroma) — Vector database
- [Obsidian](https://obsidian.md) — Knowledge base frontend

---

<p align="center">
  <b>Ferment Knowledge, Grow Intelligence</b><br>
  <i>Made with ❤️ by <a href="https://github.com/Invovel">Invovel</a></i>
</p>
