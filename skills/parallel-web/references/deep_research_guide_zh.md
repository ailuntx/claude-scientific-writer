# 深度研究指南

Parallel 深度研究任务 API 的综合使用指南，包括处理器选择、输出格式、结构化模式及高级模式。

---

## 概述

深度研究将自然语言研究查询转换为全面的情报报告。与简单搜索不同，它执行多步骤网络探索，遍历权威来源并综合发现，包含内联引用和置信度。

**核心特征：**
- 多步骤、多来源研究
- 自动引用和来源归属
- 结构化或文本输出格式
- 异步处理（30秒到25分钟以上）
- 带有置信度级别的研究依据

---

## 处理器选择

选择正确的处理器是最重要的决定。它决定了研究深度、速度和成本。

### 决策矩阵

| 场景 | 推荐处理器 | 原因 |
|----------|----------------------|-----|
| 论文章节的快速背景 | `pro-fast` | 快速，深度好，成本低 |
| 全面的市场研究报告 | `ultra-fast` | 深入的多来源综合 |
| 简单的事实查询或元数据 | `base-fast` | 快速，成本低 |
| 竞争格局分析 | `pro-fast` | 深度和速度的良好平衡 |
| 资助提案的背景 | `pro-fast` | 详尽且及时 |
| 主题的最前沿综述 | `ultra-fast` | 最大化的来源覆盖 |
| 写作过程中的快速问题 | `core-fast` | 2分钟以内响应 |
| 突发新闻或非常近期的事件 | `pro`（标准版） | 优先最新数据 |
| 大规模数据富化 | `base-fast` | 大规模成本效益高 |

### 处理器级别详解

**`pro-fast`**（默认，大多数任务推荐）：
- 延迟：30秒到5分钟
- 深度：探索10-20+个网络来源
- 适用于：章节级研究、背景收集、比较分析
- 成本：$0.10/查询

**`ultra-fast`**（全面研究）：
- 延迟：1到10分钟
- 深度：探索20-50+个网络来源，多个推理步骤
- 适用于：完整报告、市场分析、复杂多面问题
- 成本：$0.30/查询

**`core-fast`**（快速交叉引用答案）：
- 延迟：15秒到100秒
- 深度：交叉引用5-10个来源
- 适用于：中等复杂度问题、验证任务
- 成本：$0.025/查询

**`base-fast`**（简单富化）：
- 延迟：15到50秒
- 深度：标准网络查询，3-5个来源
- 适用于：简单事实查询、元数据富化
- 成本：$0.01/查询

### 标准版与快速版对比

- **快速处理器**（`-fast`后缀）：2-5倍速度，数据非常新鲜，适合交互式使用
- **标准处理器**（无后缀）：最高数据新鲜度，更适合后台任务

**经验法则：** 除非特别需要尽可能最新的数据（突发新闻、实时金融数据、实时事件），否则始终使用 `-fast` 变体。

---

## 输出格式

### 文本模式（Markdown报告）

返回带有内联引用的综合markdown报告。最适合人类阅读和文档集成。

```python
researcher = ParallelDeepResearch()

result = researcher.research(
    query="Comprehensive analysis of mRNA vaccine technology platforms and their applications beyond COVID-19",
    processor="pro-fast",
    description="Focus on clinical trials, approved applications, pipeline developments, and key companies. Include market size data."
)

# result["output"] 包含完整的markdown报告
# result["citations"] 包含带有摘录的来源URL
```

**何时使用文本模式：**
- 撰写科学文档（论文、综述、报告）
- 主题的背景研究
- 为人类读者创建摘要
- 需要流畅散文而非结构化数据

**使用 `description` 引导文本输出：**

`description` 参数引导报告内容：

```python
# 聚焦特定方面
result = researcher.research(
    query="Electric vehicle battery technology landscape",
    description="Focus on: (1) solid-state battery progress, (2) charging speed improvements, (3) cost per kWh trends, (4) key patents and IP. Format as a structured report with clear sections."
)

# 控制长度和深度
result = researcher.research(
    query="AI in drug discovery",
    description="Provide a concise 500-word executive summary covering key applications, notable successes, leading companies, and market projections."
)
```

### 自动模式（结构化JSON）

让处理器自动确定最佳输出结构。返回带有每字段引用的结构化JSON。

```python
result = researcher.research_structured(
    query="Top 5 cloud computing companies: revenue, market share, key products, and recent developments",
    processor="pro-fast",
)

# result["content"] 包含结构化数据（字典）
# result["basis"] 包含带有置信度的每字段引用
```

**何时使用自动模式：**
- 数据提取和富化
- 特定字段的对比分析
- 需要编程访问单个数据点
- 与数据库或电子表格集成

### 自定义JSON模式

精确定义您希望返回的字段：

```schema = {
    "type": "object",
    "properties": {
        "market_size_2024": {
            "type": "string",
            "description": "Global market size in USD billions for 2024. Include source."
        },
        "growth_rate": {
            "type": "string",
            "description": "CAGR percentage for 2024-2030 forecast period."
        },
        "top_companies": {
            "type": "array",
            "items": {
                "type": "object",
                "properties": {
                    "name": {"type": "string", "description": "Company name"},
                    "market_share": {"type": "string", "description": "Approximate market share percentage"},
                    "revenue": {"type": "string", "description": "Most recent annual revenue"}
                },
                "required": ["name", "market_share", "revenue"]
            },
            "description": "Top 5 companies by market share"
        },
        "key_trends": {
            "type": "array",
            "items": {"type": "string"},
            "description": "Top 3-5 industry trends driving growth"
        }
    },
    "required": ["market_size_2024", "growth_rate", "top_companies", "key_trends"],
    "additionalProperties": False
}

result = researcher.research_structured(
    query="Global cybersecurity market analysis",
    output_schema=schema,
)
```

---

## 编写有效的研究查询

### 查询构建框架

将查询结构化为：**[主题] + [具体方面] + [范围/时间] + [输出期望]**

**好的查询：**
```
"Comprehensive analysis of the global lithium-ion battery recycling market,
including market size, key players, regulatory drivers, and technology
approaches. Focus on 2023-2025 developments."

"Compare the efficacy, safety profiles, and cost-effectiveness of GLP-1
receptor agonists (semaglutide, tirzepatide, liraglutide) for type 2
diabetes management based on recent clinical trial data."

"Survey of federated learning approaches for healthcare AI, covering
privacy-preserving techniques, real-world deployments, regulatory
compliance, and performance benchmarks from 2023-2025 publications."
```

**差的查询：**
```
"Tell me about batteries"          # 过于模糊
"AI"                                # 无具体方面
"What's new?"                       # 完全没有主题
"Everything about quantum computing from all time"  # 过于宽泛
```

### 获得更好结果的技巧

1. **具体说明您需要什么**："market size" vs "tell me about the market"
2. **包含时间范围**："2024-2025" 缩小到相关数据
3. **指明实体**："semaglutide vs tirzepatide" vs "diabetes drugs"
4. **指定输出期望**："Include statistics, key players, and growth projections"
5. **保持在15,000字符以内**：简洁的查询比大量提示词效果更好

---

## 使用研究依据

每个深度研究结果都包含一个 **basis** —— 每个发现的引用、推理和置信度级别。

### 文本模式依据

```python
result = researcher.research(query="...", processor="pro-fast")

# 引用已去重，包含URL和摘录
for citation in result["citations"]:
    print(f"Source: {citation['title']}")
    print(f"URL: {citation['url']}")
    if citation.get("excerpts"):
        print(f"Excerpt: {citation['excerpts'][0][:200]}")
```

### 结构化模式依据

```python
result = researcher.research_structured(query="...", processor="pro-fast")

for basis_entry in result["basis"]:
    print(f"Field: {basis_entry['field']}")
    print(f"Confidence: {basis_entry['confidence']}")
    print(f"Reasoning: {basis_entry['reasoning']}")
    for cit in basis_entry["citations"]:
        print(f"  Source: {cit['url']}")
```

### 置信度级别

| 级别 | 含义 | 操作 |
|-------|---------|--------|
| `high` | 多个权威来源一致 | 直接使用 |
| `medium` | 部分支持证据，轻微不确定性 | 带警告使用 |
| `low` | 证据有限，显著不确定性 | 独立验证 |

---

## 高级模式

### 多阶段研究

按顺序使用不同的处理器进行渐进式深入研究：

```python
# 第一阶段：使用base-fast快速概览
overview = researcher.research(
    query="What are the main approaches to quantum error correction?",
    processor="base-fast",
)

# 第二阶段：深入研究最有前途的方法
deep_dive = researcher.research(
    query=f"Detailed analysis of surface code quantum error correction: "
          f"recent breakthroughs, implementation challenges, and leading research groups. "
          f"Context: {overview['output'][:500]}",
    processor="pro-fast",
)
```

### 对比研究

```python
result = researcher.research(
    query="Compare and contrast three leading large language model architectures: "
          "GPT-4, Claude, and Gemini. Cover architecture differences, benchmark performance, "
          "pricing, context window, and unique capabilities. Include specific benchmark scores.",
    processor="pro-fast",
    description="Create a structured comparison with a summary table. Include specific numbers and benchmarks."
)
```

### 带后续提取的研究

```python
# 第一步：研究以找到相关来源
research_result = researcher.research(
    query="Most influential papers on attention mechanisms in 2024",
    processor="pro-fast",
)

# 第二步：从最相关的来源提取完整内容
from parallel_web import ParallelExtract
extractor = ParallelExtract()

key_urls = [c["url"] for c in research_result["citations"][:5]]
for url in key_urls:
    extracted = extractor.extract(
        urls=[url],
        objective="Key methodology, results, and conclusions",
    )
```

---

## 性能优化

### 降低延迟

1. **使用 `-fast` 处理器**：比标准版快2-5倍
2. **对中等查询使用 `core-fast`**：大多数问题2分钟以内响应
3. **查询要具体**：模糊的查询需要更多探索
4. **设置适当的超时**：不要过度等待

### 降低成本

1. **从 `base-fast` 开始**：仅在深度不足时升级
2. **对中等复杂度使用 `core-fast`**：$0.025 vs $0.10（pro版）
3. **批量相关查询**：一个精心构建的查询优于多个简单查询
4. **缓存结果**：存储研究输出以便跨部分重用

### 最大化质量

1. **使用 `pro-fast` 或 `ultra-fast`**：更多来源=更好的综合
2. **提供上下文**："I'm writing a paper for Nature Medicine about..."
3. **使用 `description` 参数**：引导输出结构和重点
4. **验证关键发现**：用搜索API或提取进行交叉检查

---

## 常见错误

| 错误 | 影响 | 修复 |
|---------|--------|-----|
| 查询太模糊 | 结果分散、无焦点 | 添加具体方面和时间范围 |
| 查询太长（>15K字符） | API拒绝或结果质量下降 | 总结上下文，聚焦关键问题 |
| 处理器错误 | 太慢或太浅 | 使用上面的决策矩阵 |
| 不使用 `description` | 报告结构与需求不符 | 添加description引导输出 |
| 忽略置信度级别 | 将低置信度数据当作事实使用 | 引用前检查basis置信度 |
| 不验证引用 | 存在过时或归属错误数据的风险 | 用提取交叉检查关键引用 |

---

## 另请参阅

- [API参考](api_reference.md) - 完整的API参数参考
- [搜索最佳实践](search_best_practices.md) - 快速网络搜索
- [提取模式](extraction_patterns.md) - 读取特定URL
- [工作流方案](workflow_recipes.md) - 常见多步骤模式
