# FermentAI 🧠⚡

> **Agentic 知识发酵引擎** — 让数据像酒一样发酵，越用越香

[English](README.md) | [📖 **中文文档**](README.zh.md)

[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![Ollama](https://img.shields.io/badge/Ollama-Compatible-green.svg)](https://ollama.com)
[![RAG](https://img.shields.io/badge/RAG-Agentic%20RAG%202.0-orange.svg)](docs/architecture.md)

---

**消费级硬件跑专属领域大模型。无需训练，无需GPU集群，无需厂商绑定。**

---

## 🎯 解决什么问题

| 痛点 | FermentAI 的答案 |
|------|-----------------|
| 微调成本高昂 $$$ | **零训练成本** — 检索增强替代权重更新 |
| 向量库是死的 | **活的知识图谱** — 关联自动建立、自然衰减 |
| Agent 各自为战 | **多Agent协同** — Claude/GPT/本地LLM共享一个大脑 |
| 数据隐私噩梦 | **100%本地部署** — 数据绝不离开你的服务器 |
| 知识腐烂 | **热值驱动策展** — 热点上浮，过时下沉 |

---

## 🔬 核心创新：知识发酵

> 如同酿酒 — 原料（数据）+ 酒曲（使用痕迹）+ 时间 = 价值

```
传统系统:  存储 → 查询 → 结束（数据是死的）
FermentAI: 存储 → 查询 → 留痕 → 积累 → 触发 → 进化 → 更聪明的查询
            ↑_________________________________________________↓
```

**三条发酵回路：**

| 回路 | 触发条件 | 执行动作 |
|------|---------|---------|
| **对话 → 知识** | 某主题30天内被查≥3次 | 自动下载最新论文，与对话关联 |
| **代码 → 知识** | 某模块被复用≥3次 | 关联算法论文，插入引用，生成最佳实践 |
| **Agent → Agent** | 某类任务积累≥10个样本 | 排名Agent能力，下次自动路由到最佳Agent |

---

## 🏗️ 系统架构

```
┌──────────────────────────────────────────────────────────────┐
│                    交互层 (Claude / GPT / 本地LLM)            │
│     统一API网关  →  Agent注册中心  →  动态路由器              │
└────────────────────────────┬─────────────────────────────────┘
                             ↓
┌──────────────────────────────────────────────────────────────┐
│                     发酵引擎                                  │
│  触发器 → 规则引擎 → 执行器 → 洞察生成器                      │
│  (高频查询→自动搜文献)  (代码复用→关联论文)                    │
└────────────────────────────┬─────────────────────────────────┘
                             ↓
┌──────────────────────────────────────────────────────────────┐
│                    四层知识仓库                                │
│   知识库(Chroma)  │  对话库  │  代码库  │  元数据库(关联图谱)   │
│   论文 · 概念     │ 历史·标签 │ 片段·模式 │ 跨库关联·Agent画像  │
└──────────────────────────────────────────────────────────────┘
```

---

## ⚡ 快速开始

```bash
# 克隆仓库
git clone https://github.com/Invovel/FermentAI.git && cd FermentAI

# 安装依赖
pip install -r requirements.txt

# 拉取嵌入模型 (Ollama)
ollama pull nomic-embed-text

# 从你的 Obsidian 知识库构建关联图
set FERMENT_VAULT_PATH=D:\你的\知识库\路径
python fermentai build

# 启动 API 服务
python fermentai serve
```

```python
# 查询你的专属领域知识
import requests
r = requests.post("http://localhost:8000/query", json={
    "query": "RAG在蛋白质设计中的最新应用",
    "top_k": 5,
    "use_hyde": True,     # HyDE假设文档增强
    "use_rerank": True    # 交叉编码器重排序
})
print(r.json()["answer"])
```

---

## 📊 与传统方案对比

| | 微调蒸馏 | 传统RAG | **FermentAI** |
|--|:-:|:-:|:-:|
| **构建成本** | $$$$ GPU集群 | $$ 中等 | $ **家用笔记本** |
| **更新成本** | 重新训练 | 重新索引 | **自动进化** |
| **知识关联** | ❌ 无 | ❌ 无 | ✅ **图谱驱动** |
| **动态排序** | ❌ 静态 | ❌ 静态 | ✅ **热值加权** |
| **多Agent协同** | ❌ | ❌ | ✅ **能力路由** |
| **可解释性** | ❌ 黑盒 | ⚠️ 部分 | ✅ **完全溯源** |
| **隐私保护** | ⚠️ 云端 | ⚠️ 云端 | ✅ **100%本地** |

---

## 🎯 使用场景

### 实验室知识中台
> "我们生物信息学实验室积累了10年的论文，FermentAI把它们连接成活的知识图谱——新人入职几天就能上手，而不是几个月。"

### 个人知识复利
> "我反复查询'扩散模型'，FermentAI检测到了，自动下载了3篇最新论文并推送通知。我的知识在主动帮我生长。"

### 企业知识资产化
> "公司文档散落在Confluence、GitHub、Slack中。FermentAI将它们统一成图谱。客服Agent精准检索，开发Agent复用验证过的代码。"

---

## 🛠️ 技术栈

| 组件 | 技术 |
|------|------|
| 向量数据库 | Chroma（本地、轻量） |
| 知识图谱 | 自研图引擎（NetworkX + 加权边） |
| 嵌入模型 | Ollama `nomic-embed-text`（免费、本地） |
| 生成模型 | Ollama / Claude / OpenAI / 任意兼容API |
| 检索策略 | 混合：向量 + BM25 + RRF融合 + 交叉编码器重排序 |
| 查询优化 | Multi-Query多头扩展 + HyDE（假设文档嵌入） |
| 前端 | Obsidian（知识库浏览） + FastAPI（REST API） |

---

## 🗺️ 路线图

- [x] 知识关联图构建
- [x] 热值驱动检索
- [x] 核心发酵规则
- [ ] 多Agent能力注册与动态路由
- [ ] 自动文献搜索与入库
- [ ] 代码-论文自动关联
- [ ] 跨实验室知识联邦
- [ ] Web可视化面板

---

## 📚 文档

| 文档 | 内容 |
|------|------|
| [架构设计](docs/architecture.md) | 完整系统设计与数据流 |
| [发酵机制](docs/fermentation.md) | 触发器-规则-执行器详解 |
| [Agent接入](docs/agent-integration.md) | 多Agent协作协议 |
| [API参考](docs/api.md) | REST API接口文档 |
| [部署指南](docs/deployment.md) | 实验室服务器部署 |
| [专家咨询](docs/expert-consultation.md) | 面向领域专家的问题清单 |

---

## 💬 寻求专家指导

我们积极寻求以下领域专家的建议：

- **LLM架构师** — 多Agent协同、幻觉抑制
- **知识图谱专家** — 大规模图构建、时序知识图谱
- **RAG研究者** — 高级检索策略、领域自适应、评估体系
- **实验室PI/研究员** — 真实的知识管理需求和工作流

📧 **联系方式**: indegceyuan@outlook.com

详见 [专家咨询问题清单](docs/expert-consultation.md)

---

## 📄 许可证

MIT License — 详见 [LICENSE](LICENSE)。个人及学术使用完全免费。商业使用请联系作者授权。

---

## 🙏 致谢

站在巨人的肩膀上：
- [LangChain](https://github.com/langchain-ai/langchain) — RAG基础设施
- [Ollama](https://github.com/ollama/ollama) — 本地模型运行
- [Chroma](https://github.com/chroma-core/chroma) — 向量数据库
- [Obsidian](https://obsidian.md) — 知识库前端

---

<p align="center">
  <b>让知识发酵，让智慧生长</b><br>
  <i>由 <a href="https://github.com/Invovel">Invovel</a> 用 ❤️ 构建</i>
</p>
