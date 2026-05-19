# FermentAI 架构设计文档

## 设计哲学

> **"知识不是静态的库存，而是动态的过程。"**

传统知识管理系统把知识当作**货物**——存进去，取出来，用完放回。

FermentAI 把知识当作**生命体**——在使用过程中生长、关联、进化、衰减。

---

## 核心概念：知识发酵

### 什么是知识发酵？

```
传统系统:
知识 → 存储 → 查询 → 结束 (知识不变)

发酵系统:
知识 → 存储 → 使用 → 产生痕迹 → 痕迹积累 → 触发规则 → 生成新关联 → 知识进化
         ↑___________________________________________________________|
```

**发酵的本质**: 让数据在使用过程中产生"化学反应"，生成新的关联和价值。

### 发酵的三要素

| 要素 | 说明 | 类比酿酒 |
|------|------|----------|
| **原料** | 原始知识 (论文/代码/对话) | 粮食 |
| **酵母** | 使用痕迹 (查询/引用/复用) | 酒曲 |
| **时间** | 积累与衰减 | 发酵时间 |
| **产物** | 关联图谱 + 热值分布 | 美酒 |

---

## 系统架构详解

### 整体架构

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                           第一层：交互层 (Presentation)                       │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   用户/Agent ──→ 统一API网关 ──→ 路由分发                                    │
│                      ↓                                                       │
│              ┌───────────────┐                                               │
│              │  查询接口      │  POST /query                                  │
│              │  入库接口      │  POST /ingest                                 │
│              │  推荐接口      │  GET /recommend                               │
│              │  管理接口      │  GET /stats, POST /admin                      │
│              └───────────────┘                                               │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
                                      ↓
┌─────────────────────────────────────────────────────────────────────────────┐
│                           第二层：发酵层 (Fermentation)                       │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │                        触发器 (Triggers)                             │   │
│   │                                                                      │   │
│   │   对话结束 ──→ 提取主题 ──→ 匹配知识库 ──→ 更新热值                   │   │
│   │   代码生成 ──→ 特征提取 ──→ 关联论文 ──→ 建立链接                     │   │
│   │   高频查询 ──→ 自动下载 ──→ 知识入库 ──→ 标签对话                     │   │
│   │   任务完成 ──→ 能力评估 ──→ 更新画像 ──→ 优化分配                     │   │
│   │                                                                      │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                      ↓                                       │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │                        规则引擎 (Rules)                              │   │
│   │                                                                      │   │
│   │   IF 主题A在30天内被查询 >= 3次 AND 知识库无最新文献                   │   │
│   │   THEN Research-Skill搜索 → 自动下载 → 入库 → 打标签 → 通知用户       │   │
│   │                                                                      │   │
│   │   IF 代码模块M被多次复用 AND 知识库有算法论文P                         │   │
│   │   THEN 建立M↔P关联 → 代码注释插入引用 → 生成使用指南                   │   │
│   │                                                                      │   │
│   │   IF Agent X在任务T表现优于Agent Y                                    │   │
│   │   THEN X.ability[T] += 0.1 → 下次T优先分配X                           │   │
│   │                                                                      │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                      ↓                                       │
│   ┌─────────────────────────────────────────────────────────────────────┐   │
│   │                        执行器 (Actions)                              │   │
│   │                                                                      │   │
│   │   • 写入四层仓库 (知识/对话/代码/元数据)                               │   │
│   │   • 更新关联图谱                                                       │   │
│   │   • 生成洞察报告 (供Agent消费)                                         │   │
│   │   • 触发通知 (新文献/新关联/能力更新)                                   │   │
│   │                                                                      │   │
│   └─────────────────────────────────────────────────────────────────────┘   │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
                                      ↓
┌─────────────────────────────────────────────────────────────────────────────┐
│                           第三层：仓库层 (Storage)                            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│   ┌─────────────┐    ┌─────────────┐    ┌─────────────┐                    │
│   │   知识库     │    │   对话库     │    │   代码库     │                    │
│   │             │    │             │    │             │                    │
│   │ • 论文/概念  │    │ • 历史对话   │    │ • 代码片段   │                    │
│   │ • 向量索引   │    │ • 主题标签   │    │ • 特征向量   │                    │
│   │ • 关联权重   │    │ • 情感/意图  │    │ • 错误模式   │                    │
│   │ • 热值/置信度│    │ • 解决状态   │    │ • 性能指标   │                    │
│   └──────┬──────┘    └──────┬──────┘    └──────┬──────┘                    │
│          │                  │                  │                            │
│          └──────────────────┼──────────────────┘                            │
│                             ↓                                               │
│              ┌─────────────────────────┐                                    │
│              │        元数据库          │                                    │
│              │     (Meta-Graph)        │                                    │
│              │                         │                                    │
│              │ • 跨库关联图谱           │                                    │
│              │ • Agent能力画像          │                                    │
│              │ • 发酵历史记录           │                                    │
│              │ • 全局热值分布           │                                    │
│              └─────────────────────────┘                                    │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 核心组件详解

### 1. 知识库 (Knowledge Vault)

**职责**: 存储结构化知识，支持语义检索和关联查询

**数据模型**:

```python
class KnowledgeNode:
    id: str                    # 唯一标识 (如 "wiki/concepts/RAG.md")
    title: str                 # 显示标题
    node_type: str             # concept | summary | entity | synthesis
    content: str               # Markdown内容
    embedding: List[float]     # 向量嵌入
    
    # 元数据
    tags: List[str]
    hotness: float            # 热值 0-1
    confidence: float         # 置信度 0-1
    sources: List[str]        # 引用的源文件
    parent_concepts: List[str]
    related_concepts: List[str]
    
    # 关联
    out_links: List[str]      # 出链 (wikilinks)
    in_links: List[str]       # 入链 (反向引用)
    
    # 时间
    created: datetime
    updated: datetime
```

**存储结构**:
```
vault/
├── wiki/
│   ├── concepts/          # 概念定义页
│   │   └── [概念名].md    # frontmatter: hotness, confidence, sources...
│   ├── summaries/         # 论文摘要
│   │   └── source-[名].md # wikilinks指向concepts
│   ├── entities/          # 实体 (人/机构/工具)
│   └── synthesis/         # 综合页面 (由发酵引擎生成)
├── raw/
│   └── 收件箱/            # 原始论文/资料
└── .fermentai/
    ├── chroma_db/         # 向量数据库
    ├── graph.json         # 关联图谱
    └── heatmap.json       # 热值分布
```

**检索策略**:
1. **向量检索**: 语义相似度 (Chroma)
2. **BM25检索**: 关键词匹配 (whoosh)
3. **关联检索**: 图谱扩展 (NetworkX)
4. **融合排序**: RRF + 热值偏置

---

### 2. 对话库 (Conversation Vault)

**职责**: 记录对话历史，提取主题，反馈Agent表现

**数据模型**:

```python
class Conversation:
    id: str
    timestamp: datetime
    agent: str                 # 使用的Agent
    query: str
    answer: str
    
    # 提取信息
    topics: List[str]         # 主题标签
    knowledge_used: List[str] # 使用的知识条目
    code_generated: str       # 生成的代码ID
    
    # 反馈
    user_rating: int          # 用户评分 1-5
    modification_count: int   # 用户修改次数
    follow_up_questions: int  # 追问次数
    
    # 性能
    latency_ms: int
    tokens_in: int
    tokens_out: int
```

**发酵价值**:
- 高频主题 → 提升相关知识热值
- 用户反馈 → 更新Agent能力画像
- 主题关联 → 建立对话↔知识链接

---

### 3. 代码库 (Code Vault)

**职责**: 存储代码片段，提取特征，建立与知识的关联

**数据模型**:

```python
class CodeSnippet:
    id: str
    code: str
    language: str
    
    # 特征
    algorithm_type: str       # 算法类型 (attention, cnn, etc.)
    complexity: str           # 时间复杂度
    dependencies: List[str]   # 依赖库
    
    # 关联
    source_paper: str         # 实现的论文
    related_concepts: List[str]
    
    # 质量
    test_coverage: float
    performance_benchmark: Dict
    error_patterns: List[str]
    
    # 使用
    reuse_count: int
    last_used: datetime
```

**发酵价值**:
- 代码复用 → 提升关联知识热值
- 错误模式 → 提取规则，前置检查
- 性能数据 → 推荐最佳实践

---

### 4. 元数据库 (Meta-Graph)

**职责**: 连接前三层，记录跨库关联和Agent能力

**核心图谱**:

```python
class KnowledgeGraph:
    # 节点: 知识/对话/代码的统一标识
    nodes: Dict[str, Node]
    
    # 边: 跨库关联
    edges: List[Edge]
    # Edge类型:
    # - wikilink: 页面间链接
    # - source_ref: 知识引用源文件
    # - concept_usage: 对话使用知识
    # - code_implementation: 代码实现算法
    # - co_occurrence: 共现关联
    # - shared_tag: 共享标签
    
    # Agent能力画像
    agent_profiles: Dict[str, AgentProfile]
    
    # 热值分布
    heat_distribution: Dict[str, float]
```

---

## 发酵机制详解

### 触发器设计

```python
class FermentationTrigger:
    """监听事件，触发发酵"""
    
    def on_conversation_end(self, conversation: Conversation):
        """对话结束触发"""
        topics = extract_topics(conversation)
        for topic in topics:
            related_knowledge = search_knowledge(topic)
            for knowledge in related_knowledge:
                knowledge.hotness += 0.05
                create_link(conversation, knowledge, type="concept_usage")
    
    def on_code_generated(self, code: CodeSnippet):
        """代码生成触发"""
        features = extract_code_features(code)
        related_papers = match_papers_by_algorithm(features.algorithm_type)
        for paper in related_papers:
            create_link(code, paper, type="code_implementation")
            paper.hotness += 0.03
    
    def on_high_frequency_query(self, query: str, count: int):
        """高频查询触发"""
        if count >= 3:
            # 触发自动文献搜索
            new_papers = research_skill_search(query)
            for paper in new_papers:
                ingest_paper(paper)
                notify_user(f"发现新文献: {paper.title}")
```

### 规则引擎设计

```python
class FermentationRule:
    condition: Callable
    action: Callable
    priority: int

# 规则1: 对话→知识发酵
Rule(
    condition=lambda ctx: (
        ctx.event == "conversation_end" and
        ctx.topic_frequency >= 3 and
        ctx.knowledge_coverage < 0.5
    ),
    action=lambda ctx: (
        research_skill_search(ctx.topic),
        auto_download_papers(),
        generate_summary_pages(),
        tag_related_conversations()
    ),
    priority=1
)

# 规则2: 代码→知识发酵
Rule(
    condition=lambda ctx: (
        ctx.event == "code_generated" and
        ctx.code_reuse_count >= 3 and
        ctx.paper_link is None
    ),
    action=lambda ctx: (
        match_paper_by_algorithm(ctx.code_features),
        create_code_paper_link(),
        insert_paper_reference_in_comment(),
        generate_usage_guide()
    ),
    priority=2
)

# 规则3: Agent能力发酵
Rule(
    condition=lambda ctx: (
        ctx.event == "task_completed" and
        ctx.sample_count >= 10
    ),
    action=lambda ctx: (
        rank_agents_by_performance(ctx.task_type),
        update_agent_profiles(),
        optimize_task_routing()
    ),
    priority=3
)
```

---

## 检索流程详解

### 完整检索流程

```
用户查询: "RAG在蛋白质设计中的应用"
    ↓
┌─────────────────────────────────────────┐
│ 1. 查询理解与扩展                        │
│    • 提取关键词: [RAG, 蛋白质设计]        │
│    • Multi-Query扩展:                     │
│      - "检索增强生成用于蛋白质结构预测"    │
│      - "RAG技术如何辅助蛋白质工程"        │
│    • HyDE生成假设文档                     │
└─────────────────────────────────────────┘
    ↓
┌─────────────────────────────────────────┐
│ 2. 多路检索                              │
│    • 向量检索 (语义相似度)                │
│    • BM25检索 (关键词匹配)                │
│    • 关联图谱扩展 (相关节点)              │
└─────────────────────────────────────────┘
    ↓
┌─────────────────────────────────────────┐
│ 3. 融合与排序                            │
│    • RRF融合 (向量 + BM25)               │
│    • 热值偏置 (hotness × 0.3)            │
│    • 关联权重加成                         │
└─────────────────────────────────────────┘
    ↓
┌─────────────────────────────────────────┐
│ 4. 重排序                                │
│    • 交叉编码器精排                       │
│    • 上下文相关性评估                     │
└─────────────────────────────────────────┘
    ↓
┌─────────────────────────────────────────┐
│ 5. 上下文构建                            │
│    • 拼接Top-K文档                        │
│    • 标注来源和关联强度                   │
└─────────────────────────────────────────┘
    ↓
┌─────────────────────────────────────────┐
│ 6. Agent生成                             │
│    • 检索结果 + 用户查询 → LLM           │
│    • 生成带引用的回答                     │
└─────────────────────────────────────────┘
    ↓
┌─────────────────────────────────────────┐
│ 7. 痕迹记录 (发酵原料)                    │
│    • 记录查询主题                         │
│    • 记录使用的知识                       │
│    • 触发发酵规则                         │
└─────────────────────────────────────────┘
```

---

## Agent协作机制

### 能力注册

```python
class AgentRegistry:
    def register(self, agent: Agent):
        self.agents[agent.name] = {
            "capabilities": agent.capabilities,
            "cost_level": agent.cost_level,
            "latency": agent.latency,
            "context_window": agent.context_window,
            "performance_history": {}
        }
```

### 动态路由

```python
def route_task(task: Task) -> Agent:
    candidates = []
    for name, profile in agent_registry.items():
        if task.type in profile["capabilities"]:
            score = calculate_match_score(task, profile)
            candidates.append((name, score))
    
    # 排序: 能力匹配度 × 历史表现 × 成本效率
    candidates.sort(key=lambda x: x[1], reverse=True)
    return agent_registry[candidates[0][0]]
```

### 经验共享

```python
def share_experience(agent: Agent, task: Task, result: Result):
    """Agent完成任务后，经验写入共享库"""
    experience = {
        "task_type": task.type,
        "difficulty": task.difficulty,
        "approach": result.approach,
        "pitfalls": result.pitfalls,
        "best_practices": result.best_practices
    }
    shared_experience_library.add(experience)
```

---

## 性能优化

### 索引优化

| 策略 | 效果 |
|------|------|
| 增量索引 | 只更新变更文件，速度提升10x |
| 批量嵌入 | 一次处理多个文档，减少API调用 |
| 分层索引 | 父文档+子文档，平衡召回与精度 |
| 热值缓存 | 热门查询结果缓存1小时 |

### 查询优化

| 策略 | 效果 |
|------|------|
| 查询缓存 | 相同查询直接返回缓存 |
| 并行检索 | 向量+BM25并行执行 |
| 近似最近邻 | HNSW算法，毫秒级搜索 |
| 结果预取 | 预测用户可能感兴趣的关联内容 |

---

## 部署架构

### 个人使用

```
笔记本 (8GB RAM)
├── Ollama (本地模型)
├── Chroma (向量数据库)
└── FermentAI (Python服务)
    └── 监听 localhost:8000
```

### 实验室部署

```
服务器 (16GB RAM, 可选GPU)
├── FermentAI API服务
│   ├── 多用户认证
│   ├── 并发查询处理
│   └── 定时发酵任务
├── Chroma (向量数据库)
├── 共享Obsidian Vault
└── 备份与同步
```

### 扩展部署

```
Kubernetes集群
├── API Gateway (负载均衡)
├── FermentAI Pods (水平扩展)
├── Chroma Cluster (分布式向量库)
└── 对象存储 (备份/归档)
```

---

## 安全与隐私

### 数据安全

- **本地优先**: 所有数据默认本地存储
- **加密传输**: API通信使用HTTPS
- **访问控制**: 基于角色的权限管理
- **审计日志**: 所有操作可追溯

### 隐私保护

- **数据隔离**: 用户数据逻辑隔离
- **敏感信息过滤**: 自动检测并脱敏
- **合规支持**: GDPR/CCPA兼容

---

## 扩展性设计

### 插件系统

```python
class FermentPlugin:
    """插件接口"""
    
    def on_ingest(self, document: Document):
        """文档入库时触发"""
        pass
    
    def on_query(self, query: str, results: List[Result]):
        """查询完成时触发"""
        pass
    
    def on_ferment(self, event: FermentationEvent):
        """发酵事件触发"""
        pass
```

### 自定义规则

```python
# 用户自定义发酵规则
@fermentation_rule(priority=1)
def my_custom_rule(ctx: FermentationContext):
    if ctx.topic == "我的专业领域":
        ctx.boost_hotness(multiplier=2.0)
        ctx.notify_user(priority="high")
```

---

## 总结

FermentAI 的架构设计围绕一个核心思想：**知识是活的**。

通过四层仓库的分离与关联、发酵引擎的持续运转、多Agent的协作学习，我们构建了一个**自我进化的知识生态系统**。

它不是替代LLM，而是让LLM拥有**专业领域的长期记忆和关联推理能力**——就像一个经验丰富的研究员，不仅记得所有读过的论文，还知道它们之间的关联，哪些是最新的热点，哪些是经典必读。

这就是**低成本专属大模型**的真正含义：**不是训练一个模型，而是构建一个让通用模型变专业的系统**。
