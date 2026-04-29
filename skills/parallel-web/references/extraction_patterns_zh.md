# 提取模式

使用 Parallel 的 Extract API 将网页转换为干净的、针对 LLM 优化内容的指南。

---

## 概述

Extract API 将任何公开 URL 转换为干净的 markdown。它可以处理简单的 HTTP 获取无法解析的 JavaScript 重页面、PDF 和复杂布局。结果针对 LLM 消费进行了优化。

**主要功能：**
- JavaScript 渲染（单页应用、动态内容）
- PDF 提取为干净文本
- 与您的目标一致的重点摘要
- 完整页面内容提取
- 多 URL 批量处理

---

## 何时使用 Extract 与 Search

| 场景 | 使用 Extract | 使用 Search |
|----------|-------------|------------|
| 您有一个特定的 URL | 是 | 否 |
| 您需要已知页面的内容 | 是 | 否 |
| 您想查找关于某个主题的页面 | 否 | 是 |
| 您需要阅读研究论文的 URL | 是 | 否 |
| 您需要验证特定网站上的信息 | 是 | 否 |
| 您正在广泛地查找信息 | 否 | 是 |
| 您从搜索中找到了 URL 并想要完整内容 | 是 | 否 |

**经验法则：** 如果您有 URL，请使用 Extract。如果您需要查找 URL，请使用 Search。

---

## 摘要模式与完整内容模式

### 摘要模式（默认）

返回与您的目标一致的重点内容。更小的 token 占用，更高的相关性。

```python
extractor = ParallelExtract()

result = extractor.extract(
    urls=["https://arxiv.org/abs/2301.12345"],
    objective="关键方法论和实验结果",
    excerpts=True,     # 默认
    full_content=False  # 默认
)
```

**最适合：**
- 从长页面中提取特定信息
- token 高效处理
- 当您知道自己在寻找什么时
- 阅读论文以获取特定声明或数据点

### 完整内容模式

将完整页面内容作为干净的 markdown 返回。

```python
result = extractor.extract(
    urls=["https://docs.example.com/api-reference"],
    objective="完整的 API 文档",
    excerpts=False,
    full_content=True,
)
```

**最适合：**
- 完整文档页面
- 需要完整文章文本进行分析
- 当您需要每个细节，而不仅仅是摘要时
- 归档或转换网页内容

### 两种模式都使用

您可以同时请求摘要和完整内容：

```python
result = extractor.extract(
    urls=["https://example.com/report"],
    objective="执行摘要和关键建议",
    excerpts=True,
    full_content=True,
)

# 使用摘要进行重点分析
# 使用完整内容作为完整参考
```

---

## 提取的目标撰写

`objective` 参数将提取重点放在相关内容上。它显著提高摘要质量。

### 好的目标

```python
# 具体且可操作
objective="提取方法论部分，包括样本量、统计方法和主要终点"

# 清楚说明您需要什么
objective="查找定价信息、功能比较表和企业计划详情"

# 针对您的任务
objective="这项临床试验的主要发现、效应量、置信区间和作者结论"
```

### 差的目标

```python
# 太模糊
objective="告诉我关于这个页面的一些信息"

# 完全没有目标（仍然有效但摘要重点不够）
extractor.extract(urls=["https://..."])
```

### 按用例分类的目标模板

**学术论文：**
```python
objective="摘要、主要发现、方法论（样本量、设计、统计检验）、带效应量和 p 值的结果以及主要结论"
```

**产品/公司页面：**
```python
objective="公司概览、主要产品/服务、定价、成立日期、领导团队和近期公告"
```

**技术文档：**
```python
objective="API 端点、认证方法、请求/响应格式、速率限制和代码示例"
```

**新闻文章：**
```python
objective="主要故事、关键引用、数据点、事件时间线和具名来源"
```

**政府/政策文件：**
```python="关键政策条款、生效日期、受影响方、合规要求和处罚"
```

---

## 批量提取

在单次调用中从多个 URL 提取：

```result = extractor.extract(
    urls=[
        "https://nature.com/articles/s12345",
        "https://science.org/doi/full/10.1234/science.xyz",
        "https://thelancet.com/journals/lancet/article/PIIS0140-6736(24)12345/fulltext"
    ],
    objective="每项研究的关键发现、样本量和统计结果",
)

# 结果按输入 URL 的相同顺序返回
for r in result["results"]:
    print(f"=== {r['title']} ===")
    print(f"URL: {r['url']}")
    for excerpt in r["excerpts"]:
        print(excerpt[:500])
```

**批量限制：**
- 每次请求的 URL 数量没有硬性限制
- 每个 URL 计为一个提取单元用于计费
- 大批量可能需要更长时间处理
- 失败的 URL 会在 `errors` 字段中报告，而不会阻止成功的 URL

---

## 处理不同内容类型

### 网页 (HTML)

标准提取。JavaScript 会被渲染，因此单页应用和动态内容可以正常工作。

```python
# 标准网页
result = extractor.extract(
    urls=["https://example.com/article"],
    objective="主要文章内容",
)
```

### PDF

PDF 会自动检测并转换为文本。

```python
# PDF 提取
result = extractor.extract(
    urls=["https://example.com/whitepaper.pdf"],
    objective="执行摘要和关键建议",
)
```

### 文档网站

单页应用和文档框架（Docusaurus、GitBook、ReadTheDocs）会完全渲染。

```python
result = extractor.extract(
    urls=["https://docs.example.com/getting-started"],
    objective="安装说明和快速入门指南",
    full_content=True,
)
```

---

## 常见提取模式

### 模式 1：先搜索后提取

使用 Search 找到相关页面，然后从最佳结果中提取完整内容。

```python
from parallel_web import ParallelSearch, ParallelExtract

searcher = ParallelSearch()
extractor = ParallelExtract()

# 步骤 1：找到相关页面
search_result = searcher.search(
    objective="找到原始 Transformer 论文及其关键后续论文",
    search_queries=["attention is all you need paper", "transformer architecture paper"],
)

# 步骤 2：从最佳结果中提取详细内容
top_urls = [r["url"] for r in search_result["results"][:3]]
extract_result = extractor.extract(
    urls=top_urls,
    objective="摘要、架构描述、关键结果和消融研究",
)
```

### 模式 2：DOI 解析和论文阅读

```python
# 从 DOI URL 提取内容
result = extractor.extract(
    urls=["https://doi.org/10.1038/s41586-024-07487-w"],
    objective="研究设计、患者人群、主要终点、疗效结果和安全数据",
)
```

### 模式 3：从公司页面获取竞争情报

```python
companies = [
    "https://openai.com/about",
    "https://anthropic.com/company",
    "https://deepmind.google/about/",
]

result = extractor.extract(
    urls=companies,
    objective="公司使命、团队规模、主要产品、近期公告和融资信息",
)
```

### 模式 4：文档提取以供参考

```python
result = extractor.extract(
    urls=["https://docs.parallel.ai/search/search-quickstart"],
    objective="完整的 API 使用指南，包括请求格式、响应格式和代码示例",
    full_content=True,
)
```

### 模式 5：元数据验证

```python
# 验证特定论文的引用元数据
result = extractor.extract(
    urls=["https://doi.org/10.1234/example-doi"],
    objective="完整引用元数据：作者、标题、期刊、卷、页码、年份、DOI",
)
```

---

## 错误处理

### 常见错误

| 错误 | 原因 | 解决方案 |
|-------|-------|----------|
| URL 无法访问 | 页面需要认证、处于付费墙后或已下线 | 尝试不同的 URL 或改用 Search |
| 超时 | 页面渲染时间过长 | 重试或使用更简单的 URL |
| 内容为空 | 页面以无法渲染的方式动态加载 | 尝试 full_content 模式或改用 Search |
| 速率受限 | 请求过多 | 等待后重试，或减小批量大小 |

### 检查错误

```python
result = extractor.extract(urls=["https://example.com/page"])

if not result["success"]:
    print(f"提取失败: {result['error']}")
elif result.get("errors"):
    print(f"某些 URL 失败: {result['errors']}")
else:
    print(f"成功提取了 {len(result['results'])} 个页面")
```

---

## 技巧和最佳实践

1. **始终提供目标**：即使是一般性的目标也会显著提高摘要质量
2. **默认使用摘要**：只有当您真正需要所有内容时才使用完整内容
3. **批量相关 URL**：一次调用 5 个 URL 比 5 次单独调用更好
4. **检查错误**：并非所有 URL 都可以提取（付费墙、认证等）
5. **与 Search 结合**：Search 找到 URL，Extract 详细读取它们
6. **用于 DOI 解析**：Extract 自动处理 DOI 重定向
7. **优先使用 Extract 而非手动获取**：处理 JavaScript、PDF 和复杂布局

---

## 另请参阅

- [API 参考](api_reference.md) - 完整 API 参数参考
- [Search 最佳实践](search_best_practices.md) - 用于查找要提取的 URL
- [深度研究指南](deep_research_guide.md) - 用于综合研究任务
- [工作流配方](workflow_recipes.md) - 常见多步骤模式
