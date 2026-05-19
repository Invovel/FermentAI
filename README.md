# FermentAI 🧠⚡

> **Local Domain AI Ecosystem** — Research, Store, Ferment, Orchestrate. All on your own hardware.

[English](README.md) | [📖 **中文文档**](README.zh.md)

[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![Ollama](https://img.shields.io/badge/Ollama-Compatible-green.svg)](https://ollama.com)
[![RAG](https://img.shields.io/badge/RAG-Agentic%20RAG%202.0-orange.svg)](docs/architecture.md)

---

**Not a RAG tool. Not a private server. It's an entire AI ecosystem that turns your laptop into a self-evolving domain-expert lab.**

---

## 🎯 One Sentence

FermentAI is **three subsystems working as one** — auto research & data collection, knowledge fermentation & storage, and multi-agent orchestration — giving you a **self-evolving AI lab** that runs entirely locally.

---

## 🧩 What's Inside

FermentAI is NOT a single tool. It's three coordinated subsystems:

```
┌─────────────────────────────────────────────────────────────────┐
│                                                                  │
│   Research-Skill              LLM-Wiki              Agent-team   │
│   ┌──────────────┐       ┌──────────────┐       ┌─────────────┐ │
│   │  Data Pipe   │  ──→  │ Fermentation │  ──→  │ Orchestrator│ │
│   │              │       │   Engine     │       │             │ │
│   │ arXiv search │       │ Knowledge    │       │ Claude      │ │
│   │ GitHub scan  │       │ Graph        │       │ GPT         │ │
│   │ Paper ingest │       │ Hotness/Decay│       │ Local LLM   │ │
│   │ Auto-download│       │ Hybrid Search│       │ Dynamic route│ │
│   └──────────────┘       └──────────────┘       └─────────────┘ │
│         ↑                      ↑                      ↑         │
│         └──────────────────────┼──────────────────────┘         │
│                     Fermentation Engine                          │
│              (connects, weights, evolves all data)               │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

| Subsystem | Role | Analogy |
|-----------|------|---------|
| **Research-Skill** | Auto data collection | The **hands** — searches, downloads, ingests |
| **LLM-Wiki** | Knowledge fermentation & storage | The **memory** — stores, connects, ranks, decays |
| **Agent-team** | Multi-agent orchestration | The **brain** — routes tasks, learns patterns, collaborates |

**And the Fermentation Engine ties them all together** — data flows in, connections form, hotness rises and falls, agents learn from each other.

---

## 🔬 Core Innovation: Knowledge Fermentation

> Raw data → Usage traces → Auto-connections → Evolving intelligence

```
Traditional tools:
  Search → Read → Forget (data is dead)

FermentAI:
  Research-Skill finds papers → LLM-Wiki stores & connects them
  → You query → Agent-team routes to best LLM → Answer generated
  → Trace recorded → High-frequency topics auto-trigger new research
  → Knowledge graph updates weight → Everything gets smarter
  → ↓
  Next query benefits from everything that happened before
```

---

## 🏗️ Full Architecture

```
┌──────────────────────────────────────────────────────────────────┐
│                      USER INTERFACE                               │
│    Obsidian (knowledge browser)  |  CLI  |  REST API  |  Web UI  │
└────────────────────────────┬─────────────────────────────────────┘
                             ↓
┌──────────────────────────────────────────────────────────────────┐
│                  AGENT-TEAM (Orchestrator)                        │
│                                                                    │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐           │
│  │ Capability   │  │ Dynamic      │  │ Experience   │           │
│  │ Registry     │→│ Router       │→│ Pool         │           │
│  │              │  │              │  │              │           │
│  │ Claude: bio  │  │ Task→Agent   │  │ "GPT always  │           │
│  │ GPT: code    │  │ match+route  │  │  fails this"  │           │
│  │ Local: review│  │ fallback     │  │ "Claude FTW" │           │
│  └──────────────┘  └──────────────┘  └──────────────┘           │
│                                                                    │
│  Tasks are auto-routed. Agents learn from each other's results.   │
└────────────────────────────┬─────────────────────────────────────┘
                             ↓
┌──────────────────────────────────────────────────────────────────┐
│                   FERMENTATION ENGINE                             │
│                                                                    │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐          │
│  │  Triggers   │───→│ Rule Engine │───→│  Executor   │          │
│  │             │    │             │    │             │          │
│  │ Query ≥ 3×  │    │ IF freq>3   │    │ Auto-search │          │
│  │ Code reuse  │    │ → download  │    │ papers      │          │
│  │ Task done   │    │ IF reuse>3  │    │ Update graph│          │
│  │ Agent fail  │    │ → link paper│    │ Update heat │          │
│  └─────────────┘    └─────────────┘    └─────────────┘          │
│                                                                    │
└────────────────────────────┬─────────────────────────────────────┘
                             ↓
┌──────────────────────────────────────────────────────────────────┐
│                    LLM-WIKI (Knowledge Vaults)                    │
│                                                                    │
│  ┌────────────┐ ┌────────────┐ ┌────────────┐ ┌───────────────┐ │
│  │ KNOWLEDGE  │ │CONVERSATION│ │    CODE    │ │   META-GRAPH  │ │
│  │ (Chroma)   │ │ (Markdown) │ │  (Git)     │ │ (NetworkX)    │ │
│  │            │ │            │ │            │ │               │ │
│  │ papers     │ │ history    │ │ snippets   │ │ cross-vault   │ │
│  │ concepts   │ │ topics     │ │ patterns   │ │ links         │ │
│  │ summaries  │ │ ratings    │ │ benchmarks │ │ agent profiles│ │
│  │ entities   │ │ sentiment  │ │ bug modes  │ │ heat distro   │ │
│  │ vector idx │ │ tags       │ │ features   │ │ decay history │ │
│  └────────────┘ └────────────┘ └────────────┘ └───────────────┘ │
│                            ↑                                      │
│              ┌─────────────┴─────────────┐                       │
│              │     RESEARCH-SKILL        │                       │
│              │  (Data Collection Pipe)   │                       │
│              │                           │                       │
│              │  arXiv API · GitHub API   │                       │
│              │  HuggingFace · RSS/Arxiv  │                       │
│              │  Auto-download · Ingest   │                       │
│              └───────────────────────────┘                       │
│                                                                    │
└──────────────────────────────────────────────────────────────────┘
```

---

## 🔄 The Complete Loop

```
1. Research-Skill searches arXiv → finds 5 papers → downloads → extracts text
2. LLM-Wiki ingests → chunks → embeds → stores in knowledge vault
3. You query: "RAG in protein design" 
4. Agent-team routes → Claude (best for bio) → generates answer
5. Fermentation traces: topic=RAG+protein, papers used, confidence=0.85
6. Day 3: same topic queried again → hotness += 0.05
7. Day 7: topic hit threshold → trigger fires → Research-Skill searches again
8. Day 10: 3 new papers auto-downloaded, linked, notification pushed
9. Meanwhile: Agent-team notices GPT keeps failing on protein folding
   → updates agent profile → future protein tasks auto-route to Claude
```

---

## ⚡ Quick Start

```bash
# Clone
git clone https://github.com/Invovel/FermentAI.git && cd FermentAI

# Install
pip install -r requirements.txt

# Pull models (Ollama)
ollama pull nomic-embed-text    # Embedding
ollama pull gemma4:e2b          # Generation

# Initialize with your Obsidian vault
set FERMENT_VAULT_PATH=D:\Obsidian\Hub\WikiVault
python fermentai build

# Start the API server
python fermentai serve
```

```python
# Query your domain AI lab
import requests
r = requests.post("http://localhost:8000/query", json={
    "query": "Latest on diffusion models for protein design",
    "top_k": 5,
    "use_hyde": True,
    "use_rerank": True,
    "prefer_agent": "auto"    # Let Agent-team decide
})
print(r.json()["answer"])
```

---

## 📊 vs Everything Else

| | Fine-Tuning | Vanilla RAG | LangChain App | **FermentAI** |
|--|:-:|:-:|:-:|:-:|
| **Cost** | $$$$ GPU | $$ Cloud | $$ API | $ **Laptop** |
| **Auto research** | ❌ | ❌ | ❌ | ✅ **Research-Skill** |
| **Knowledge linking** | ❌ | ❌ | ❌ | ✅ **Fermentation graph** |
| **Dynamic ranking** | ❌ | ❌ | ❌ | ✅ **Heat + decay** |
| **Multi-agent** | ❌ | ❌ | ❌ | ✅ **Agent-team** |
| **Agent learning** | ❌ | ❌ | ❌ | ✅ **Experience pool** |
| **Privacy** | ⚠️ | ⚠️ | ⚠️ | ✅ **100% local** |
| **Self-evolving** | ❌ | ❌ | ❌ | ✅ **Auto-improves** |

---

## 🎯 Use Cases

### Lab AI Ecosystem
> "Our lab runs FermentAI on a single server. Research-Skill auto-ingests papers daily. The fermentation engine links them to our existing knowledge. Agent-team routes complex bio queries to Claude, simple lookups to local LLM. New members query the entire lab's knowledge history."

### Personal Research Accelerator
> "I connected my Obsidian vault. FermentAI noticed I keep asking about protein language models — it auto-downloaded 3 new papers, linked them to my existing notes, and now Agent-team recommends which agent to use per query type."

### Enterprise Knowledge Platform
> "Company docs, code repos, Slack discussions → all fed into FermentAI. The fermentation engine connects everything. Support agents query with provenance. Dev agents reuse proven code patterns. The system learns which agent is best for which task."

---

## 🗺️ Roadmap

| Phase | Status | Focus |
|-------|:------:|-------|
| **Core Engine** | ✅ Done | Knowledge graph, heat-driven retrieval, core fermentation rules |
| **Agent-team** | 🚧 Now | Capability registry, dynamic task routing, experience pool |
| **Research-Skill Integration** | 🚧 Now | Auto literature search, paper ingest pipeline, trigger-based collection |
| **Code Vault** | 📋 Next | Code-paper linking, bug pattern learning, multi-agent code review |
| **Cross-lab Federation** | 🔮 Future | Federated knowledge sharing, privacy-preserving agent collaboration |

---

## 📚 Documentation

| Document | Content |
|----------|---------|
| [Vision](docs/VISION.md) | 🌟 Why FermentAI exists — full story & philosophy |
| [Architecture](docs/architecture.md) | Full system design & data flow |
| [Fermentation](docs/fermentation.md) | Trigger-rule-executor mechanism |
| [Agent Integration](docs/agent-integration.md) | Multi-agent protocol & Agent-team |
| [Research-Skill](docs/research-skill.md) | Auto data collection pipeline |
| [API Reference](docs/api.md) | REST API endpoints |
| [Deployment](docs/deployment.md) | Lab server setup |
| [Expert Consultation](docs/expert-consultation.md) | Questions for domain experts |

---

## 💬 Seeking Expert Feedback

We are actively seeking guidance from:

- **LLM Architects** — multi-agent orchestration, capability routing, experience sharing
- **Knowledge Graph Experts** — large-scale dynamic graphs, temporal weighting
- **RAG Researchers** — advanced retrieval, domain adaptation, hallucination mitigation
- **Lab PIs & Researchers** — real knowledge management pain points, workflow integration

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
  <b>Research. Store. Ferment. Orchestrate.</b><br>
  <i>Your local AI ecosystem — by <a href="https://github.com/Invovel">Invovel</a></i>
</p>
