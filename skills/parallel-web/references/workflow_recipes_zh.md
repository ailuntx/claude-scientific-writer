# 工作流配方

常见的多步模式，结合 Parallel 的 Search、Extract 和 Deep Research API，用于科学写作任务。

---

## 配方索引

| 配方 | 使用的 API | 时间 | 使用场景 |
|--------|-----------|------|----------|
| [Section Research Pipeline](#recipe-1-section-research-pipeline) | Research + Search | 2-5 分钟 | 撰写论文章节 |
| [Citation Verification](#recipe-2-citation-verification) | Search + Extract | 1-2 分钟 | 验证论文元数据 |
| [Literature Survey](#recipe-3-literature-survey) | Research + Search + Extract | 5-15 分钟 | 综合文献综述 |
| [Market Intelligence Report](#recipe-4-market-intelligence-report) | Research（多阶段）| 10-30 分钟 | 市场/行业分析 |
| [Competitive Analysis](#recipe-5-competitive-analysis) | Search + Extract + Research | 5-10 分钟 | 比较公司/产品 |
| [Fact-Check Pipeline](#recipe-6-fact-check-pipeline) | Search + Extract | 1-3 分钟 | 验证声明 |
| [Current Events Briefing](#recipe-7-current-events-briefing) | Search + Research | 3-5 分钟 | 新闻综合 |
| [Technical Documentation Gathering](#recipe-8-technical-documentation-gathering) | Search + Extract | 2-5 分钟 | API/框架文档 |
| [Grant Background Research](#recipe-9-grant-background-research) | Research + Search | 5-10 分钟 | 资助申请背景研究 |

---

## 配方 1：章节研究流程

**目标：** 为科学论文的单个章节收集研究和引用。

**API：** Deep Research（pro-fast）+ Search

```bash
# 步骤 1：深度研究以获取全面背景
python scripts/parallel_web.py research \
  "Recent advances in federated learning for healthcare AI, focusing on privacy-preserving training methods, real-world deployments, and regulatory considerations (2023-2025)" \
  --processor pro-fast -o sources/section_background.md

# 步骤 2：针对性搜索特定引用
python scripts/parallel_web.py search \
  "Find peer-reviewed papers on federated learning in hospitals" \
  --queries "federated learning clinical deployment" "privacy preserving ML healthcare" \
  --max-results 10 -o sources/section_citations.txt
```

**Python 版本：**
```python
from parallel_web import ParallelDeepResearch, ParallelSearch

researcher = ParallelDeepResearch()
searcher = ParallelSearch()

# 步骤 1：深度背景研究
background = researcher.research(
    query="Recent advances in federated learning for healthcare AI (2023-2025): "
          "privacy-preserving methods, real-world deployments, regulatory landscape",
    processor="pro-fast",
    description="Structure as: (1) Key approaches, (2) Clinical deployments, "
                "(3) Regulatory considerations, (4) Open challenges. Include statistics."
)

# 步骤 2：查找特定论文以供引用
papers = searcher.search(
    objective="Find recent peer-reviewed papers on federated learning deployed in hospital settings",
    search_queries=[
        "federated learning hospital clinical study 2024",
        "privacy preserving machine learning healthcare deployment"
    ],
    source_policy={"allow_domains": ["nature.com", "thelancet.com", "arxiv.org", "pubmed.ncbi.nlm.nih.gov"]},
)

# 组合：使用 background 撰写，使用 papers 引用
```

**何时使用：** 在撰写研究论文、文献综述或资助申请的每个主要章节之前。

---

## 配方 2：引用验证

**目标：** 验证引用是否真实并获取完整的元数据（DOI、卷、页码、年份）。

**API：** Search + Extract

```bash
# 选项 A：搜索论文
python scripts/parallel_web.py search \
  "Vaswani et al 2017 Attention is All You Need paper NeurIPS" \
  --queries "Attention is All You Need DOI" --max-results 5

# 选项 B：从 DOI 提取元数据
python scripts/parallel_web.py extract \
  "https://doi.org/10.48550/arXiv.1706.03762" \
  --objective "Complete citation: authors, title, venue, year, pages, DOI"
```

**Python 版本：**
```python
from parallel_web import ParallelSearch, ParallelExtract

searcher = ParallelSearch()
extractor = ParallelExtract()

# 步骤 1：查找论文
result = searcher.search(
    objective="Find the exact citation details for the Attention Is All You Need paper by Vaswani et al.",
    search_queries=["Attention is All You Need Vaswani 2017 NeurIPS DOI"],
    max_results=5,
)

# 步骤 2：从论文页面提取完整元数据
paper_url = result["results"][0]["url"]
metadata = extractor.extract(
    urls=[paper_url],
    objective="Complete BibTeX citation: all authors, title, conference/journal, year, pages, DOI, volume",
)
```

**何时使用：** 撰写章节后，验证 references.bib 中的每个引用都具有正确和完整的元数据。

---

## 配方 3：文献综述

**目标：** 对研究领域进行全面调查，识别关键论文、主题和研究空白。

**API：** Deep Research + Search + Extract

```python
from parallel_web import ParallelDeepResearch, ParallelSearch, ParallelExtract

researcher = ParallelDeepResearch()
searcher = ParallelSearch()
extractor = ParallelExtract()

topic = "CRISPR-based diagnostics for infectious diseases"

# 阶段 1：广泛研究概述
overview = researcher.research(
    query=f"Comprehensive review of {topic}: key developments, clinical applications, "
          f"regulatory status, commercial products, and future directions (2020-2025)",
    processor="ultra-fast",
    description="Structure as a literature review: (1) Historical development, "
                "(2) Current technologies, (3) Clinical applications, "
                "(4) Regulatory landscape, (5) Commercial products, "
                "(6) Limitations and future directions. Include key statistics and milestones."
)

# 阶段 2：查找特定的里程碑论文
key_papers = searcher.search(
    objective=f"Find the most cited and influential papers on {topic} from Nature, Science, Cell, NEJM",
    search_queries=[
        "CRISPR diagnostics SHERLOCK DETECTR Nature",
        "CRISPR point-of-care testing clinical study",
        "nucleic acid detection CRISPR review"
    ],
    source_policy={
        "allow_domains": ["nature.com", "science.org", "cell.com", "nejm.org", "thelancet.com"],
    },
    max_results=15,
)

# 阶段 3：从排名前 5 的论文中提取详细内容
top_urls = [r["url"] for r in key_papers["results"][:5]]
detailed = extractor.extract(
    urls=top_urls,
    objective="Study design, key results, sensitivity/specificity data, and clinical implications",
)
```

**何时使用：** 开始文献综述、系统综述或综合背景章节时。

---

## 配方 4：市场情报报告

**目标：** 生成关于某个行业或产品类别的综合市场研究报告。

**API：** Deep Research（多阶段）

```python
researcher = ParallelDeepResearch()

industry = "AI-powered drug discovery"

# 阶段 1：市场概述（使用 ultra-fast 以获得最大深度）
market_overview = researcher.research(
    query=f"Comprehensive market analysis of {industry}: market size, growth rate, "
          f"key segments, geographic distribution, and forecast through 2030",
    processor="ultra-fast",
    description="Include specific dollar figures, CAGR percentages, and data sources. "
                "Break down by segment and geography."
)

# 阶段 2：竞争格局
competitors = researcher.research_structured(
    query=f"Top 10 companies in {industry}: revenue, funding, key products, partnerships, and market position",
    processor="pro-fast",
)

# 阶段 3：技术和创新趋势
tech_trends = researcher.research(
    query=f"Technology trends and innovation landscape in {industry}: "
          f"emerging approaches, breakthrough technologies, patent landscape, and R&D investment",
    processor="pro-fast",
    description="Focus on specific technologies, quantify R&D spending, and identify emerging leaders."
)

# 阶段 4：监管和风险分析
regulatory = researcher.research(
    query=f"Regulatory landscape and risk factors for {industry}: "
          f"FDA guidance, EMA requirements, compliance challenges, and market risks",
    processor="pro-fast",
)
```

**何时使用：** 创建市场研究报告、投资者演示或战略分析文档时。

---

## 配方 5：竞争分析

**目标：** 并排比较多个公司、产品或技术。

**API：** Search + Extract + Research

```python
searcher = ParallelSearch()
extractor = ParallelExtract()
researcher = ParallelDeepResearch()

companies = ["OpenAI", "Anthropic", "Google DeepMind"]

# 步骤 1：搜索每个公司的最新数据
for company in companies:
    result = searcher.search(
        objective=f"Latest product launches, funding, team size, and strategy for {company} in 2025",
        search_queries=[f"{company} product launch 2025", f"{company} funding valuation"],
        source_policy={"after_date": "2024-06-01"},
    )

# 步骤 2：从公司页面提取信息
company_pages = [
    "https://openai.com/about",
    "https://anthropic.com/company",
    "https://deepmind.google/about/",
]
company_data = extractor.extract(
    urls=company_pages,
    objective="Mission, key products, team size, founding date, and recent milestones",
)

# 步骤 3：深度研究以进行综合
comparison = researcher.research(
    query=f"Detailed comparison of {', '.join(companies)}: "
          f"products, pricing, technology approach, market position, strengths, weaknesses",
    processor="pro-fast",
    description="Create a structured comparison covering: "
                "(1) Product portfolio, (2) Technology approach, (3) Pricing, "
                "(4) Market position, (5) Strengths/weaknesses, (6) Future outlook. "
                "Include a summary comparison table."
)
```

---

## 配方 6：事实核查流程

**目标：** 在将特定声明或统计数据包含在文档中之前进行验证。

**API：** Search + Extract

```python
searcher = ParallelSearch()
extractor = ParallelExtract()

claim = "The global AI market is expected to reach $1.8 trillion by 2030"

# 步骤 1：搜索 corroborating 来源
result = searcher.search(
    objective=f"Verify this claim: '{claim}'. Find authoritative sources that confirm or contradict this figure.",
    search_queries=["global AI market size 2030 forecast", "artificial intelligence market projection trillion"],
    max_results=8,
)

# 步骤 2：从主要来源提取具体数字
source_urls = [r["url"] for r in result["results"][:3]]
details = extractor.extract(
    urls=source_urls,
    objective="Specific market size figures, forecast years, CAGR, and methodology of the projection",
)

# 分析：多个权威来源是否一致？
```

**何时使用：** 在论文或报告中包含任何特定统计数据、市场数字或事实性声明之前。

---

## 配方 7：时事简报

**目标：** 获取关于某个主题的最新发展的最新综合信息。

**API：** Search + Research

```python
searcher = ParallelSearch()
researcher = ParallelDeepResearch()

topic = "EU AI Act implementation"

# 步骤 1：查找最新新闻
latest = searcher.search(
    objective=f"Latest news and developments on {topic} from the past month",
    search_queries=[f"{topic} 2025", f"{topic} latest updates"],
    source_policy={"after_date": "2025-01-15"},
    max_results=15,
)

# 步骤 2：综合成简报
briefing = researcher.research(
    query=f"Summarize the latest developments in {topic} as of February 2025: "
          f"key milestones, compliance deadlines, industry reactions, and implications",
    processor="pro-fast",
    description="Write a concise 500-word executive briefing with timeline of key events."
)
```

---

## 配方 8：技术文档收集

**目标：** 为框架或 API 收集和综合技术文档。

**API：** Search + Extract

```python
searcher = ParallelSearch()
extractor = ParallelExtract()

# 步骤 1：查找文档页面
docs = searcher.search(
    objective="Find official PyTorch documentation for implementing custom attention mechanisms",
    search_queries=["PyTorch attention mechanism tutorial", "PyTorch MultiheadAttention documentation"],
    source_policy={"allow_domains": ["pytorch.org", "github.com/pytorch"]},
)

# 步骤 2：从文档页面提取完整内容
doc_urls = [r["url"] for r in docs["results"][:3]]
full_docs = extractor.extract(
    urls=doc_urls,
    objective="Complete API reference, parameters, usage examples, and code snippets",
    full_content=True,
)
```

---

## 配方 9：资助背景研究

**目标：** 为资助提案构建具有验证统计数据的综合背景章节。

**API：** Deep Research + Search

```python
researcher = ParallelDeepResearch()
searcher = ParallelSearch()

research_area = "AI-guided antibiotic discovery to combat antimicrobial resistance"

# 步骤 1：意义和疾病负担
significance = researcher.research(
    query=f"Burden of antimicrobial resistance: mortality statistics, economic impact, "
          f"WHO priority pathogens, and projections. Include specific numbers.",
    processor="pro-fast",
    description="Focus on statistics suitable for NIH Significance section: "
                "deaths per year, economic cost, resistance trends, and urgency."
)

# 步骤 2：创新格局
innovation = researcher.research(
    query=f"Current approaches to {research_area}: successes (halicin, etc.), "
          f"limitations of current methods, and what makes our approach novel",
    processor="pro-fast",
    description="Focus on Innovation section: what has been tried, what gaps remain, "
                "and what new approaches are emerging."
)

# 步骤 3：查找特定论文以了解初步数据背景
papers = searcher.search(
    objective="Find landmark papers on AI-discovered antibiotics and ML approaches to drug discovery",
    search_queries=[
        "halicin AI antibiotic discovery Nature",
        "machine learning antibiotic resistance prediction",
        "deep learning drug discovery antibiotics"
    ],
    source_policy={"allow_domains": ["nature.com", "science.org", "cell.com", "pnas.org"]},
)
```

**何时使用：** 为 NIH、NSF 或其他资助提案撰写 Significance、Innovation 或 Background 章节时。

---

## 与其他技能结合使用

### 与 `research-lookup`（学术论文）

```python
# 使用 parallel-web 进行一般研究
researcher.research("Current state of quantum computing applications")

# 使用 research-lookup 进行学术论文搜索（自动路由到 Perplexity）
# python research_lookup.py "find papers on quantum error correction in Nature and Science"
```

### 与 `citation-management`（BibTeX）

```python
# 步骤 1：使用 parallel search 查找论文
result = searcher.search(objective="Vaswani et al Attention Is All You Need paper")

# 步骤 2：从结果获取 DOI
doi = "10.48550/arXiv.1706.03762"

# 步骤 3：使用 citation-management 技能转换为 BibTeX
# python scripts/doi_to_bibtex.py 10.48550/arXiv.1706.03762
```

### 与 `scientific-schematics`（图表）

```python
# 步骤 1：研究一个过程
result = researcher.research("How does the CRISPR-Cas9 gene editing mechanism work step by step")

# 步骤 2：使用研究结果为图表提供信息
# python scripts/generate_schematic.py "CRISPR-Cas9 gene editing workflow: guide RNA design -> Cas9 binding -> DNA cleavage -> repair pathway" -o figures/crispr_mechanism.png
```

---

## 性能速查表

| 任务 | 处理器 | 预期时间 | 近似成本 |
|------|-----------|---------------|------------------|
| 快速事实查询 | `base-fast` | 15-50秒 | $0.01 |
| 章节背景 | `pro-fast` | 30秒-5分钟 | $0.10 |
| 综合报告 | `ultra-fast` | 1-10分钟 | $0.30 |
| 网页搜索（10 条结果）| Search API | 1-3秒 | $0.005 |
| URL 提取（1 个 URL）| Extract API | 1-20秒 | $0.001 |
| URL 提取（5 个 URL）| Extract API | 5-30秒 | $0.005 |

---

## 另请参阅

- [API 参考](api_reference.md) - 完整 API 参数参考
- [搜索最佳实践](search_best_practices.md) - 有效的搜索查询
- [深度研究指南](deep_research_guide.md) - 处理器选择和输出格式
- [提取模式](extraction_patterns.md) - URL 内容提取
