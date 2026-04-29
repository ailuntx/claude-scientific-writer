# 搜索 API 最佳实践

Parallel 搜索 API 获取最佳结果的综合指南。

---

## 核心概念

搜索 API 基于自然语言目标返回经过排序的、针对 LLM 优化的网络资源摘录。结果直接可用作模型输入，从而实现更快的推理和更高质量的完成。

### 相比传统搜索的主要优势

- **针对令牌效率的上下文工程**：结果按推理效用而非参与度排序
- **单跳解析**：复杂的多主题查询一次请求即可解决
- **多跳效率**：深度研究工作流可在更少的工具调用中完成

---

## 制作有效的搜索查询

### 同时提供 `objective` 和 `search_queries`

`objective` 描述你的更广泛目标；`search_queries` 确保特定关键词被优先处理。同时使用两者可获得明显更好的结果。

**好的：**
```python
searcher.search(
    objective="I'm writing a literature review on Alzheimer's treatments. Find peer-reviewed research papers and clinical trial results from the past 2 years on amyloid-beta targeted therapies.",
    search_queries=[
        "amyloid beta clinical trials 2024-2025",
        "Alzheimer's monoclonal antibody treatment results",
        "lecanemab donanemab trial outcomes"
    ],
)
```

**差的：**
```python
# Too vague - no context about intent
searcher.search(objective="Alzheimer's treatment")

# Missing objective - no context for ranking
searcher.search(search_queries=["Alzheimer's drugs"])
```

### 目标编写技巧

1. **陈述你的更广泛任务**："I'm writing a research paper on...", "I'm analyzing the market for...", "I'm preparing a presentation about..."
2. **对来源偏好具体说明**："Prefer official government websites", "Focus on peer-reviewed journals", "From major news outlets"
3. **包含时效性要求**："From the past 6 months", "Published in 2024-2025", "Most recent data available"
4. **指定内容类型**："Technical documentation", "Clinical trial results", "Market analysis reports", "Product announcements"

### 按用例分类的目标示例

**学术研究：**
```
"I'm writing a literature review on CRISPR gene editing applications in cancer therapy.
Find peer-reviewed papers from Nature, Science, Cell, and other high-impact journals
published in 2023-2025. Prefer clinical trial results and systematic reviews."
```

**市场情报：**
```
"I'm preparing Q1 2025 investor materials for a fintech startup.
Find recent announcements from the Federal Reserve and SEC about digital asset
regulations and banking partnerships with crypto firms. Past 3 months only."
```

**技术文档：**
```
"I'm designing a machine learning course. Find technical documentation and API guides
that explain how transformer attention mechanisms work, preferably from official
framework documentation like PyTorch or Hugging Face."
```

**时事：**
```
"I'm tracking AI regulation developments. Find official policy announcements,
legislative actions, and regulatory guidance from the EU, US, and UK governments
from the past month."
```

---

## 搜索模式

使用 `mode` 参数优化你的工作流：

| 模式 | 最佳用途 | 摘录风格 | 延迟 |
|------|----------|---------------|---------|
| `one-shot`（默认） | 直接查询、单次请求工作流 | 全面、较长 | 较低 |
| `agentic` | 多步推理循环、智能体工作流 | 简洁、令牌高效 | 稍高 |
| `fast` | 实时应用、UI 自动完成 | 极简、速度优化 | 约 1 秒 |

### 何时使用各模式

**`one-shot`**（默认）：
- 需要全面答案的单个研究问题
- 撰写论文某部分需要完整上下文
- 开始文档前的背景研究
- 只需进行一次搜索调用的任何情况

**`agentic`**：
- 多步研究工作流（搜索 → 分析 → 再次搜索）
- 令牌效率很重要的智能体循环
- 研究查询的迭代优化
- 与其他工具集成时（搜索 → 提取 → 综合）

**`fast`**：
- 实时自动完成或建议系统
- 写作过程中的快速事实核查
- 实时元数据查找
- 任何延迟敏感型应用

---

## 来源策略

控制从结果中包含或排除哪些域：

```python
searcher.search(
    objective="Find clinical trial results for new cancer immunotherapy drugs",
    search_queries=["checkpoint inhibitor clinical trials 2025"],
    source_policy={
        "allow_domains": ["clinicaltrials.gov", "nejm.org", "thelancet.com", "nature.com"],
        "deny_domains": ["reddit.com", "quora.com"],
        "after_date": "2024-01-01"
    },
)
```

### 来源策略参数

| 参数 | 类型 | 描述 |
|-----------|------|-------------|
| `allow_domains` | list[str] | 仅包含来自这些域的结果 |
| `deny_domains` | list[str] | 排除来自这些域的结果 |
| `after_date` | str (YYYY-MM-DD) | 仅包含在此日期之后发布的内容 |

### 按用例分类的域列表

**学术研究：**
```python
allow_domains = [
    "nature.com", "science.org", "cell.com", "thelancet.com",
    "nejm.org", "bmj.com", "pnas.org", "arxiv.org",
    "pubmed.ncbi.nlm.nih.gov", "scholar.google.com"
]
```

**技术/AI：**
```python
allow_domains = [
    "arxiv.org", "openai.com", "anthropic.com", "deepmind.google",
    "huggingface.co", "pytorch.org", "tensorflow.org",
    "proceedings.neurips.cc", "proceedings.mlr.press"
]
```

**市场情报：**
```python
deny_domains = [
    "reddit.com", "quora.com", "medium.com",
    "wikipedia.org"  # Good for facts, not for market data
]
```

**政府/政策：**
```python
allow_domains = [
    "gov", "europa.eu", "who.int", "worldbank.org",
    "imf.org", "oecd.org", "un.org"
]
```

---

## 控制结果数量

### `max_results` 参数

- 范围：1-20（默认：10）
- 更多结果 = 更广泛覆盖但需要处理更多令牌
- 更少结果 = 更聚焦但可能遗漏相关来源

**建议：**
- 快速事实核查：`max_results=3`
- 标准研究：`max_results=10`（默认）
- 综合调查：`max_results=20`

### 摘录长度控制

```python
searcher.search(
    objective="...",
    max_chars_per_result=10000,  # Default: 10000
)
```

- **短摘录（1000-3000）**：快速摘要、元数据提取
- **中等摘录（5000-10000）**：标准研究、平衡深度
- **长摘录（10000-50000）**：完整文章内容、深度分析

---

## 常见模式

### 模式 1：写作前研究

```python
# Before writing each section, search for relevant information
result = searcher.search(
    objective="Find recent advances in transformer attention mechanisms for a NeurIPS paper introduction",
    search_queries=["attention mechanism innovations 2024", "efficient transformers"],
    max_results=10,
)

# Extract key findings for the section
for r in result["results"]:
    print(f"Source: {r['title']} ({r['url']})")
    # Use excerpts to inform writing
```

### 模式 2：事实验证

```python
# Quick verification of a specific claim
result = searcher.search(
    objective="Verify: Did GPT-4 achieve 86.4% on MMLU benchmark?",
    search_queries=["GPT-4 MMLU benchmark score"],
    max_results=5,
)
```

### 模式 3：竞争情报

```python
result = searcher.search(
    objective="Find recent product launches and funding announcements for AI coding assistants in 2025",
    search_queries=[
        "AI coding assistant funding 2025",
        "code generation tool launch",
        "AI developer tools new product"
    ],
    source_policy={"after_date": "2025-01-01"},
    max_results=15,
)
```

### 模式 4：多语言研究

```python
# Search includes multilingual results automatically
result = searcher.search(
    objective="Find global perspectives on AI regulation, including EU, China, and US approaches",
    search_queries=[
        "EU AI Act implementation 2025",
        "China AI regulation policy",
        "US AI executive order updates"
    ],
)
```

---

## 故障排除

### 结果很少或没有结果

- **扩大你的目标**：移除过于具体的约束
- **添加更多搜索查询**：同一概念的不同表述
- **移除来源策略**：域限制可能过于狭窄
- **检查日期过滤器**：`after_date` 可能太近期

### 结果不相关

- **使目标更具体**：添加关于任务的上下文
- **使用来源策略**：仅允许权威域
- **添加负面上下文**："Not about [unrelated topic]"
- **优化搜索查询**：使用更精确的关键词

### 结果中令牌过多

- **减少 `max_results`**：从 10 降至 5 或 3
- **减少摘录长度**：降低 `max_chars_per_result`
- **使用 `agentic` 模式**：更简洁的摘录
- **使用 `fast` 模式**：极简摘录

---

## 另请参阅

- [API 参考](api_reference.md) - 完整 API 参数参考
- [深度研究指南](deep_research_guide.md) - 用于综合研究任务
- [提取模式](extraction_patterns.md) - 用于读取特定 URL
- [工作流配方](workflow_recipes.md) - 常见多步模式
