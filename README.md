# FermentAI 🧠⚡

> **Agentic Knowledge Fermentation Engine** — 让知识像酒一样发酵，越用越香

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![Ollama](https://img.shields.io/badge/Ollama-Compatible-green.svg)](https://ollama.com)
[![RAG](https://img.shields.io/badge/RAG-Advanced-orange.svg)](https://www.promptingguide.ai/techniques/rag)

<p align="center">
  <img src="docs/assets/fermentai-logo.png" alt="FermentAI Logo" width="200">
</p>

**低成本打造专属领域大模型 | 无需蒸馏 | 本地部署 | 多Agent协作**

---

## 🎯 一句话定位

**FermentAI** 是一个**Agentic 知识发酵引擎**，它让普通用户用消费级硬件就能构建**专业领域的大模型服务**——不是通过昂贵的模型训练或蒸馏，而是通过**知识关联图谱 + 热值驱动检索 + 多Agent协作**，让知识在使用过程中自动发酵、关联、进化。

---

## 🔥 为什么这是革命性的

### 传统方案的痛点

| 方案 | 成本 | 问题 |
|------|------|------|
| **微调/蒸馏** | 💰💰💰 高 | 信息损失、更新困难、需要大量算力 |
| **RAG向量库** | 💰💰 中 | 静态检索、无关联理解、知识孤岛 |
| **商用API** | 💰 持续付费 | 数据隐私、专业领域覆盖差 |

### FermentAI 的解法

```
你的专业知识库 (PDF/论文/笔记)
           ↓
    知识发酵引擎 (本地运行)
           ↓
    关联图谱 + 热值排序 + 语义检索
           ↓
    专业领域API服务 (低成本硬件可跑)
           ↓
    通用Agent (Claude/GPT/本地LLM) 生成回答
```

**核心创新：知识发酵 (Knowledge Fermentation)**

> 就像酿酒一样，知识在使用过程中产生"化学反应"——高频查询的主题自动强化关联，低频内容自然衰减，跨库链接自动建立，最终形成**越用越精准的专业知识网络**。

---

## ✨ 核心特性

### 🧠 Agentic RAG 2.0
- **不只是检索，更是理解** —— 知识图谱驱动的关联推理
- **热值动态排序** —— 实验室热点自动上浮，冷门内容自然下沉
- **多跳推理** —— 自动发现知识间的隐含关联

### 🔄 知识发酵机制
```python
# 发酵规则示例
IF 主题A在7天内被查询 >= 3次 AND 知识库无最新文献:
    THEN 自动触发文献搜索 → 下载 → 摘要 → 关联建立 → 通知用户
    
IF 代码模块M被多次复用 AND 知识库有算法论文P:
    THEN 自动建立 M↔P 关联 → 代码注释插入引用 → 生成最佳实践指南
    
IF Agent X在任务T表现优于Agent Y:
    THEN 更新能力画像 → 下次T类任务自动路由给X
```

### 🤝 多Agent协作架构
- **能力注册** —— 每个Agent声明擅长领域
- **动态路由** —— 任务自动分配给最适合的Agent
- **经验共享** —— Agent间能力互补，错误模式集体学习

### 💰 极致低成本
- **硬件要求**: 8GB RAM + 任意GPU (甚至CPU)
- **运行成本**: 本地Ollama免费 + API调用按需
- **部署成本**: 单台服务器可服务整个实验室

---

## 🚀 快速开始

### 1. 安装 (5分钟)

```bash
# 克隆仓库
git clone https://github.com/Invovel/FermentAI.git
cd FermentAI

# 安装依赖
pip install -r requirements.txt

# 安装Ollama (本地模型)
curl -fsSL https://ollama.com/install.sh | sh

# 拉取嵌入模型
ollama pull nomic-embed-text
ollama pull gemma4:e2b
```

### 2. 初始化知识库

```bash
# 配置你的Obsidian Vault路径
export FERMENT_VAULT_PATH="/path/to/your/vault"

# 构建知识关联图
python fermentai build

# 启动服务
python fermentai serve
```

### 3. 使用

```python
import requests

# 查询专业知识
response = requests.post("http://localhost:8000/query", json={
    "query": "RAG在蛋白质设计中的最新应用",
    "top_k": 5,
    "use_hyde": True,
    "use_rerank": True
})

result = response.json()
print(result["answer"])
print("参考来源:", [s["title"] for s in result["sources"]])
```

---

## 🏗️ 系统架构

```
┌─────────────────────────────────────────────────────────────────┐
│                         交互层 (Agents)                          │
│  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────────────────┐ │
│  │ Claude  │  │ ChatGPT │  │ 本地LLM │  │  实验室定制Agent    │ │
│  └────┬────┘  └────┬────┘  └────┬────┘  └──────────┬──────────┘ │
│       └─────────────┴─────────────┴─────────────────┘            │
│                         ↓ 统一API网关                            │
└─────────────────────────────────────────────────────────────────┘
                                   ↓
┌─────────────────────────────────────────────────────────────────┐
│                      发酵引擎 (Fermentation)                     │
│                                                                  │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────────┐ │
│  │  触发器     │→│  规则引擎   │→│  执行器                 │ │
│  │  (事件监听) │  │  (条件判断) │  │  (更新图谱/热值/关联)   │ │
│  └─────────────┘  └─────────────┘  └─────────────────────────┘ │
│                                                                  │
│  发酵规则: 高频查询→自动文献搜索 | 代码复用→关联论文 | 错误模式→集体学习 │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
                                   ↓
┌─────────────────────────────────────────────────────────────────┐
│                      四层知识仓库                               │
│                                                                  │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             │
│  │   知识库    │  │   对话库    │  │   代码库    │             │
│  │  (Chroma)   │  │ (Markdown)  │  │   (Git)     │             │
│  │             │  │             │  │             │             │
│  │ • 论文/概念 │  │ • 历史对话  │  │ • 代码片段  │             │
│  │ • 向量索引  │  │ • 主题标签  │  │ • 特征向量  │             │
│  │ • 关联权重  │  │ • 情感分析  │  │ • 错误模式  │             │
│  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘             │
│         └─────────────────┼─────────────────┘                   │
│                           ↓                                     │
│              ┌─────────────────────────┐                        │
│              │      元数据库            │                        │
│              │   (知识关联图谱)          │                        │
│              │  跨库关联 | Agent画像 | 热值分布 │                 │
│              └─────────────────────────┘                        │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 📊 与传统方案对比

| 维度 | 微调/蒸馏 | 传统RAG | **FermentAI** |
|------|:---------:|:-------:|:-------------:|
| **构建成本** | 💰💰💰 高 | 💰💰 中 | 💰 **极低** |
| **更新难度** | 需重新训练 | 重新索引 | **实时发酵** |
| **知识关联** | ❌ 无 | ❌ 无 | ✅ **图谱驱动** |
| **动态排序** | ❌ 静态 | ❌ 静态 | ✅ **热值驱动** |
| **多Agent协作** | ❌ 无 | ❌ 无 | ✅ **能力路由** |
| **可解释性** | ❌ 黑盒 | ⚠️ 部分 | ✅ **溯源清晰** |
| **隐私保护** | ✅ 本地 | ✅ 本地 | ✅ **本地** |

---

## 🎯 适用场景

### 1. 实验室知识中台
> "我们的生物信息学实验室有10年的论文积累，但新人入职要花3个月才能摸清脉络。FermentAI让知识活起来了——查询一个概念，自动关联到相关论文、代码、历史讨论。"

### 2. 个人知识复利
> "作为独立研究者，我用FermentAI管理Obsidian笔记。它发现我反复查询'扩散模型'，自动下载了3篇最新论文并推送给我。知识在帮我主动生长。"

### 3. 企业知识资产化
> "公司的技术文档分散在Confluence、GitHub、Slack。FermentAI把它们关联成图谱，客服Agent能精准检索，开发Agent能复用历史代码。"

---

## 🛠️ 技术栈

- **向量数据库**: Chroma (本地、轻量、可扩展)
- **知识图谱**: 自研关联图引擎 (NetworkX + 自定义权重算法)
- **嵌入模型**: Ollama (nomic-embed-text, 本地免费)
- **生成模型**: 支持Ollama/Claude/OpenAI/任意OpenAI兼容API
- **检索增强**: Hybrid Search (向量 + BM25 + RRF融合 + 交叉编码器重排序)
- **查询优化**: Multi-Query扩展 + HyDE假设文档嵌入
- **前端**: Obsidian (知识库) + 可选Web界面

---

## 📚 文档

- [快速开始指南](docs/quickstart.md)
- [架构设计文档](docs/architecture.md)
- [发酵机制详解](docs/fermentation.md)
- [Agent接入指南](docs/agent-integration.md)
- [API参考](docs/api.md)
- [部署指南](docs/deployment.md)

---

## 🤝 与相关项目的关系

```
FermentAI 站在巨人的肩膀上:

LangChain / LlamaIndex  →  提供了RAG基础组件
    ↓
FermentAI  →  增加了知识发酵层 (关联图谱 + 热值驱动 + 多Agent协作)
    ↓
你的专业领域  →  低成本拥有专属大模型服务

特别致谢:
- LangChain (RAG基础设施)
- Ollama (本地模型运行)
- Chroma (向量数据库)
- Obsidian (知识库前端)
```

---

## 🗺️ 路线图

### Phase 1: 核心引擎 (已完成 ✅)
- [x] 知识关联图构建
- [x] 热值驱动检索
- [x] 基础发酵规则

### Phase 2: 多Agent协作 (进行中 🚧)
- [ ] Agent能力注册与发现
- [ ] 动态任务路由
- [ ] 错误模式集体学习

### Phase 3: 高级发酵 (规划中 📋)
- [ ] 自动文献搜索与入库
- [ ] 代码-论文自动关联
- [ ] 跨实验室知识共享

### Phase 4: 企业级 (未来 🔮)
- [ ] 分布式部署
- [ ] 权限管理
- [ ] 审计日志

---

## 💬 社区与咨询

### 专家咨询通道
我们正在寻求以下领域的专家指导：

- **LLM架构师**: 多Agent协作、能力路由、经验共享机制
- **知识图谱专家**: 大规模关联图谱构建、动态权重更新
- **RAG研究者**: 高级检索策略、幻觉抑制、可解释性
- **实验室PI**: 科研知识管理、团队知识传承、新人培训

如果您有相关经验，欢迎通过以下方式联系：
- 📧 Email: [your-email]
- 💬 GitHub Discussions
- 🐦 Twitter/X: [@your-handle]

### 常见问题

**Q: 这和普通的RAG有什么区别？**
A: 普通RAG是静态检索，FermentAI是动态发酵。知识在使用过程中自动建立关联、调整权重、发现缺口。

**Q: 需要多少算力？**
A: 个人使用：8GB RAM的笔记本即可。实验室部署：单台16GB服务器可服务10人团队。

**Q: 数据隐私如何保障？**
A: 全部本地运行，向量数据库、知识图谱、对话记录都在你的服务器上。

---

## 📄 许可证

MIT License - 详见 [LICENSE](LICENSE)

**商业使用**: 个人使用完全免费。企业/商业使用请联系作者获取授权。

---

## 🙏 致谢

感谢以下开源项目和社区：
- [LangChain](https://github.com/langchain-ai/langchain) - RAG基础设施
- [Ollama](https://github.com/ollama/ollama) - 本地模型运行
- [Chroma](https://github.com/chroma-core/chroma) - 向量数据库
- [Obsidian](https://obsidian.md) - 知识库工具

---

<p align="center">
  <b>让知识发酵，让智慧生长</b><br>
  <i>Ferment Knowledge, Grow Intelligence</i>
</p>
