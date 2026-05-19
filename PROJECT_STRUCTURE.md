# FermentAI 项目结构

```
FermentAI/
├── README.md                          # 项目主页，吸引眼球的入口
├── LICENSE                            # MIT License
├── requirements.txt                   # Python依赖
├── setup.py                          # 安装脚本
├── .gitignore                        # Git忽略规则
│
├── fermentai/                        # 核心代码包
│   ├── __init__.py
│   ├── core/                         # 核心引擎
│   │   ├── __init__.py
│   │   ├── knowledge_graph.py        # 知识关联图引擎
│   │   ├── fermentation.py           # 发酵引擎
│   │   ├── retrieval.py              # 检索引擎 (RAG)
│   │   └── agent_router.py           # Agent路由
│   │
│   ├── vaults/                       # 四层仓库
│   │   ├── __init__.py
│   │   ├── knowledge_vault.py        # 知识库管理
│   │   ├── conversation_vault.py     # 对话库管理
│   │   ├── code_vault.py             # 代码库管理
│   │   └── meta_vault.py             # 元数据库
│   │
│   ├── agents/                       # Agent接口
│   │   ├── __init__.py
│   │   ├── base.py                   # Agent基类
│   │   ├── claude_agent.py           # Claude接口
│   │   ├── openai_agent.py           # OpenAI接口
│   │   ├── ollama_agent.py           # Ollama本地模型
│   │   └── registry.py               # Agent注册中心
│   │
│   ├── api/                          # API服务
│   │   ├── __init__.py
│   │   ├── server.py                 # FastAPI服务
│   │   ├── routes/                   # API路由
│   │   │   ├── query.py
│   │   │   ├── ingest.py
│   │   │   ├── recommend.py
│   │   │   └── admin.py
│   │   └── middleware/               # 中间件
│   │       ├── auth.py
│   │       └── logging.py
│   │
│   ├── cli/                          # 命令行工具
│   │   ├── __init__.py
│   │   └── commands.py               # CLI命令
│   │
│   └── utils/                        # 工具函数
│       ├── __init__.py
│       ├── embedding.py              # 嵌入模型封装
│       ├── text_splitter.py          # 文本分割
│       └── logger.py                 # 日志工具
│
├── docs/                             # 文档
│   ├── README.md                     # 文档首页
│   ├── architecture.md               # 架构设计
│   ├── fermentation.md               # 发酵机制详解
│   ├── agent-integration.md          # Agent接入指南
│   ├── api.md                        # API参考
│   ├── deployment.md                 # 部署指南
│   ├── expert-consultation.md        # 专家咨询问题
│   └── assets/                       # 图片资源
│       └── fermentai-logo.png
│
├── examples/                         # 示例
│   ├── basic_usage.py                # 基础使用
│   ├── custom_fermentation_rule.py   # 自定义发酵规则
│   ├── multi_agent_collaboration.py  # 多Agent协作
│   └── obsidian_integration.md       # Obsidian集成
│
├── tests/                            # 测试
│   ├── __init__.py
│   ├── test_knowledge_graph.py
│   ├── test_fermentation.py
│   ├── test_retrieval.py
│   └── test_agents.py
│
├── scripts/                          # 辅助脚本
│   ├── setup_ollama.sh               # Ollama安装
│   ├── build_graph.py                # 构建知识图
│   └── backup_vault.py               # 备份脚本
│
└── docker/                           # Docker部署
    ├── Dockerfile
    └── docker-compose.yml
```

## 关键文件说明

### 核心引擎

| 文件 | 职责 |
|------|------|
| `knowledge_graph.py` | 构建和维护知识关联图，支持节点查询、路径查找、聚类分析 |
| `fermentation.py` | 发酵引擎，包含触发器、规则引擎、执行器 |
| `retrieval.py` | RAG检索引擎，向量+BM25+图谱融合 |
| `agent_router.py` | Agent能力画像和动态路由 |

### 仓库层

| 文件 | 职责 |
|------|------|
| `knowledge_vault.py` | 知识库管理，Chroma向量库封装 |
| `conversation_vault.py` | 对话库管理，主题提取，反馈记录 |
| `code_vault.py` | 代码库管理，特征提取，错误模式 |
| `meta_vault.py` | 元数据库，跨库关联，Agent画像 |

### API服务

| 文件 | 职责 |
|------|------|
| `server.py` | FastAPI主服务 |
| `query.py` | 查询接口 POST /query |
| `ingest.py` | 入库接口 POST /ingest |
| `recommend.py` | 推荐接口 GET /recommend |

## 快速导航

- **想快速了解项目**: 看 [README.md](README.md)
- **想深入架构**: 看 [docs/architecture.md](docs/architecture.md)
- **想接入Agent**: 看 [docs/agent-integration.md](docs/agent-integration.md)
- **想咨询专家**: 看 [docs/expert-consultation.md](docs/expert-consultation.md)
- **想部署使用**: 看 [docs/deployment.md](docs/deployment.md)
