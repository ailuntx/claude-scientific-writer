---
name: research-lookup
description: 使用 parallel-cli search（主要、快速网页搜索）或 Parallel Chat API（深度研究）查找当前研究信息。自动将查询路由到最佳后端。用于查找论文、收集研究数据和验证科学信息。
allowed-tools: Read Write Edit Bash
license: MIT license
compatibility: 需要 parallel-cli（主要）；可选 PARALLEL_API_KEY 用于通过 Parallel Chat API 进行深度研究
metadata:
    skill-author: K-Dense Inc.
---

# 研究信息查找

## 概览

此技能提供实时研究信息查找，并具备**智能后端路由**：

- **parallel-cli search**（parallel-web 技能）：**所有研究查询的主要和默认后端**。快速、经济高效的网页搜索，优先考虑学术来源。使用 `parallel-cli search` 配合 `--include-domains` 来筛选学术来源。
- **Parallel Chat API**（`core` 模型）：用于复杂、多来源的深度研究（延迟 60 秒 - 5 分钟）的辅助后端，仅在明确需要时使用。
此技能自动检测查询类型并路由到最佳后端。

## 何时使用此技能

在以下情况下使用此技能：

- **当前研究信息**：最新研究、论文和发现
- **文献验证**：根据当前研究核查事实、统计数据或声明
- **背景研究**：为科学写作收集背景和支持性证据
- **引用来源**：找到相关论文和研究以进行引用
- **技术文档**：查找规范、协议或方法学
- **市场/行业数据**：当前统计数据、趋势、竞争情报
- **近期发展**：新兴趋势、突破、公告

## 使用科学示意图增强可视化

**在使用此技能创建文档时，始终考虑添加科学图表和示意图来增强视觉传达。**

如果你的文档尚未包含示意图或图表：
- 使用 **scientific-schematics** 技能生成 AI 驱动的出版级图表
- 只需用自然语言描述你想要的图表即可

```bash
python scripts/generate_schematic.py "你的图表描述" -o figures/output.png
```

---

## 自动后端选择

此技能根据内容自动将查询路由到最佳后端：

### 路由逻辑

```
查询到达
    |
    +-- 需要深度多来源综合？（用户提到"深度研究"、"穷尽式"）
    |       是 --> Parallel Chat API（core 模型，60秒-5分钟）
    |
    +-- 其他所有情况（一般研究、学术查询、市场数据、技术信息）
            --> parallel-cli search（快速、默认）
```

### 默认：parallel-cli search（parallel-web 技能）

**所有标准研究查询的主要后端。** 快速、经济高效，并支持学术来源优先。

对于科学/技术查询，执行两次搜索以确保学术覆盖：

```bash
# 1. 学术聚焦搜索
parallel-cli search "你的研究查询" -q "关键词1" -q "关键词2" \
  --json --max-results 10 --excerpt-max-chars-total 27000 \
  --include-domains "scholar.google.com,arxiv.org,pubmed.ncbi.nlm.nih.gov,semanticscholar.org,biorxiv.org,medrxiv.org,ncbi.nlm.nih.gov,nature.com,science.org,ieee.org,acm.org,springer.com,wiley.com,cell.com,pnas.org,nih.gov" \
  -o sources/research_<主题>-academic.json

# 2. 一般搜索（捕捉非学术来源）
parallel-cli search "你的研究查询" -q "关键词1" -q "关键词2" \
  --json --max-results 10 --excerpt-max-chars-total 27000 \
  -o sources/research_<主题>-general.json
```

选项：
- `--after-date YYYY-MM-DD` 用于时间敏感的查询
- `--include-domains domain1.com,domain2.com` 限制特定来源

合并结果，优先排列学术来源。对于非科学查询，一次一般搜索就足够了。

默认情况下，所有其他查询都路由到此，包括：

- 一般研究问题
- 市场和行业分析
- 技术信息和文档
- 当前事件和近期发展
- 比较分析
- 统计数据检索
- 事实核查与验证

### 学术关键词（路由到带有学术域名的 parallel-cli）

包含以下术语的查询会触发两次搜索模式，并优先选择学术域名：

- 查找论文：`find papers`、`find articles`、`research papers on`、`published studies`
- 引用：`cite`、`citation`、`doi`、`pubmed`、`pmid`
- 学术来源：`peer-reviewed`、`journal article`、`scholarly`、`arxiv`、`preprint`
- 综述类型：`systematic review`、`meta-analysis`、`literature search`
- 论文质量：`foundational papers`、`seminal papers`、`landmark papers`、`highly cited`

### 深度研究（路由到 Parallel Chat API）

仅在用户明确要求深度、穷尽或全面研究时使用。比 parallel-cli search 慢得多且成本更高。

### 手动覆盖

你可以强制使用特定后端：

```bash
# 强制使用 parallel-cli search（快速网页搜索）
parallel-cli search "你的查询" -q "关键词" --json --max-results 10 -o sources/research_<主题>.json

# 强制使用 Parallel Chat API（深度研究，慢）
python research_lookup.py "你的查询" --force-backend parallel-chat

# 显式强制使用 parallel-cli
python research_lookup.py "你的查询" --force-backend parallel-cli
```

---

## 核心能力

### 1. 一般研究查询（parallel-cli search — 默认）

**主要后端。** 通过 parallel-web 技能实现快速、经济高效的网页搜索，并优先考虑学术来源。

```
查询示例：
- "Recent advances in CRISPR gene editing 2025"
- "Compare mRNA vaccines vs traditional vaccines for cancer treatment"
- "AI adoption in healthcare industry statistics"
- "Global renewable energy market trends and projections"
- "Explain the mechanism underlying gut microbiome and depression"
```

```bash
# 示例：CRISPR 进展研究
parallel-cli search "Recent advances in CRISPR gene editing 2025" \
  -q "CRISPR" -q "gene editing" -q "2025" \
  --json --max-results 10 --excerpt-max-chars-total 27000 \
  --include-domains "scholar.google.com,arxiv.org,pubmed.ncbi.nlm.nih.gov,nature.com,science.org,cell.com,pnas.org,nih.gov" \
  -o sources/research_crispr_advances-academic.json

parallel-cli search "Recent advances in CRISPR gene editing 2025" \
  -q "CRISPR" -q "gene editing" \
  --json --max-results 10 --excerpt-max-chars-total 27000 \
  -o sources/research_crispr_advances-general.json
```

**回复包含：**
- 带有来自搜索结果的内联引用的综合发现
- 优先考虑学术来源（同行评审、预印本）
- 具体的事实、数字和日期
- 按类型分组列出所有引用 URL 的来源部分

### 2. 学术论文搜索（带有学术域名的 parallel-cli）

**在检测到学术关键词时**使用两次搜索模式。通过 `--include-domains` 优先选择学术数据库。

```
查询示例：
- "Find papers on transformer attention mechanisms in NeurIPS 2024"
- "Foundational papers on quantum error correction"
- "Systematic review of immunotherapy in non-small cell lung cancer"
- "Cite the original BERT paper and its most influential follow-ups"
- "Published studies on CRISPR off-target effects in clinical trials"
```

**回复包含：**
- 来自学术域名（arxiv、pubmed、nature 等）和一般网络的结果
- 每个来源的标题、URL、发布日期和内容摘录
- 同行评审期刊、预印本和机构网站的来源

### 3. 深度研究（Parallel Chat API — 仅在请求时使用）

**仅在用户明确请求深度/穷尽研究时使用。** 通过 Chat API（`core` 模型）提供全面、多来源的综合。延迟 60 秒至 5 分钟。

```
查询示例：
- "Deep research on the current state of quantum computing error correction"
- "Exhaustive analysis of mRNA vaccine platforms for cancer immunotherapy"
```

### 4. 技术和方法学信息

使用 parallel-cli search（默认）进行快速查找：

```bash
parallel-cli search "Western blot protocol for protein detection" \
  -q "western blot" -q "protocol" \
  --json --max-results 10 --excerpt-max-chars-total 27000 \
  -o sources/research_western_blot.json
```

### 5. 统计和市场数据

使用 parallel-cli search（默认）获取当前数据：

```bash
parallel-cli search "Global AI market size and growth projections 2025" \
  -q "AI market" -q "statistics" -q "growth" \
  --json --max-results 10 --excerpt-max-chars-total 27000 \
  --after-date 2024-01-01 \
  -o sources/research_ai_market.json
```

---

## 论文质量和流行度优先级

**关键**：在查找论文时，始终优先选择高质量、有影响力的论文。

### 基于引用的排名

| 论文年龄 | 引用阈值 | 分类 |
|-----------|-------------------|----------------|
| 0-3 年 | 20+ 引用 | 值得关注 |
| 0-3 年 | 100+ 引用 | 高度有影响力 |
| 3-7 年 | 100+ 引用 | 重要 |
| 3-7 年 | 500+ 引用 | 里程碑论文 |
| 7+ 年 | 500+ 引用 | 开创性工作 |
| 7+ 年 | 1000+ 引用 | 基础性 |

### 发表场所质量等级

**一级 - 顶级场所**（始终优先）：
- **通用科学**：Nature、Science、Cell、PNAS
- **医学**：NEJM、Lancet、JAMA、BMJ
- **领域特定**：Nature Medicine、Nature Biotechnology、Nature Methods
- **顶级 CS/AI**：NeurIPS、ICML、ICLR、ACL、CVPR

**二级 - 高影响力专业场所**（强烈偏好）：
- 影响因子 > 10 的期刊
- 子领域顶级会议（EMNLP、NAACL、ECCV、MICCAI）

**三级 - 受尊重的专业场所**（相关时包括）：
- 影响因子 5-10 的期刊

---

## 技术集成

### 先决条件

```bash
# 主要后端 (parallel-cli) - 必需
# 如果尚未安装 parallel-cli，请安装：
curl -fsSL https://parallel.ai/install.sh | bash
# 或：uv tool install "parallel-web-tools[cli]"

# 验证：
parallel-cli auth
# 或：export PARALLEL_API_KEY="你的 parallel_api_key"
```

### 环境变量

```bash
# 验证 parallel-cli（主要后端）
parallel-cli auth
# 或直接设置 API 密钥：
export PARALLEL_API_KEY="你的 parallel_api_key"

# 深度研究后端 (Parallel Chat API) - 可选，使用相同密钥
# 使用 PARALLEL_API_KEY
```

### API 规格

**parallel-cli search（主要）：**
- 命令：带有 `--json` 输出的 `parallel-cli search`
- 延迟：2-10 秒（快速）
- 输出：包含 title、URL、publish_date、摘要的 JSON
- 学术域名：使用 `--include-domains` 获取学术来源
- 保存结果：`-o 文件名.json` 以便后续使用和再现性

**Parallel Chat API（仅深度研究）：**
- 端点：`https://api.parallel.ai`（兼容 OpenAI SDK）
- 模型：`core`（延迟 60 秒 - 5 分钟，复杂多来源综合）
- 输出：带有内联引用的 Markdown 文本
- 引用：带有 URL、推理和置信度的研究基础
- 速率限制：300 请求/分钟
- Python 包：`openai`

### 命令行使用

```bash
# 通过 parallel-cli 快速网页搜索（默认 — 推荐） — 始终保存到 sources/
parallel-cli search "你的查询" -q "关键词1" -q "关键词2" \
  --json --max-results 10 --excerpt-max-chars-total 27000 \
  -o sources/research_<主题>.json

# 通过 parallel-cli 进行学术聚焦搜索 — 始终保存到 sources/
parallel-cli search "你的查询" -q "关键词1" \
  --json --max-results 10 --excerpt-max-chars-total 27000 \
  --include-domains "scholar.google.com,arxiv.org,pubmed.ncbi.nlm.nih.gov,semanticscholar.org,biorxiv.org,medrxiv.org,nature.com,science.org,cell.com,pnas.org,nih.gov" \
  -o sources/research_<主题>-academic.json

# 通过 parallel-cli 进行时间敏感搜索
parallel-cli search "你的查询" -q "关键词" \
  --json --max-results 10 --after-date 2024-01-01 \
  -o sources/research_<主题>.json

# 提取特定 URL 的完整内容（使用 parallel-web extract）
parallel-cli extract "https://example.com/paper" --json

# 强制 Parallel Deep Research（慢速、穷尽） — 通过 research_lookup.py
python research_lookup.py "你的查询" --force-backend parallel -o sources/research_<主题>.md

# 通过 research_lookup.py 自动路由 — 始终保存到 sources/
python research_lookup.py "你的查询" -o sources/research_YYYYMMDD_HHMMSS_<主题>.md

# 通过 research_lookup.py 批量查询 — 始终保存到 sources/
python research_lookup.py --batch "查询 1" "查询 2" "查询 3" -o sources/batch_research_<主题>.md
```

---

## 强制：将所有结果保存到 Sources 文件夹

**每个 research-lookup 结果都必须保存到项目的 `sources/` 文件夹中。**

这是不可协商的。研究结果的获取成本高昂，并且对可再现性至关重要。

### 保存规则

| 后端 | `-o` 标志目标 | 文件名模式 |
|---------|-----------------|------------------|
| parallel-cli search（默认） | `sources/research_<简短主题>.json` | `research_<简短主题>.json` 或 `research_<简短主题>-academic.json` |
| Parallel Chat API（深度研究） | `sources/research_<主题>.md` | `research_YYYYMMDD_HHMMSS_<简短主题>.md` |
| 批量查询 | `sources/batch_<主题>.md` | `batch_research_YYYYMMDD_HHMMSS_<简短主题>.md` |

### 如何保存

**关键：每次搜索都必须使用 `-o` 标志将结果保存到 `sources/` 文件夹。**

**关键：保存的文件必须保留所有引用、来源 URL 和 DOI。**

```bash
# parallel-cli search（默认） — 将 JSON 保存到 sources/
parallel-cli search "Recent advances in CRISPR gene editing 2025" \
  -q "CRISPR" -q "gene editing" \
  --json --max-results 10 --excerpt-max-chars-total 27000 \
  --include-domains "scholar.google.com,arxiv.org,pubmed.ncbi.nlm.nih.gov,nature.com,science.org,cell.com,pnas.org,nih.gov" \
  -o sources/research_crispr_advances-academic.json

parallel-cli search "Recent advances in CRISPR gene editing 2025" \
  -q "CRISPR" -q "gene editing" \
  --json --max-results 10 --excerpt-max-chars-total 27000 \
  -o sources/research_crispr_advances-general.json

# 通过 Parallel Chat API 进行深度研究 — 保存到 sources/
python research_lookup.py "AI regulation landscape" --force-backend parallel-chat \
  -o sources/research_20250217_144000_ai_regulation.md

# 批量查询 — 保存到 sources/
python research_lookup.py --batch "mRNA vaccines efficacy" "mRNA vaccines safety" \
  -o sources/batch_research_20250217_144500_mrna_vaccines.md
```

### 保存文件中的引用保存

每种输出格式保留引用的方式不同：

| 格式 | 包含的引用 | 何时使用 |
|--------|-------------------|-------------|
| parallel-cli JSON（默认） | 完整结果对象：`title`、`url`、`publish_date`、`excerpts` | 标准使用 — 结构化、可解析、快速 |
| 文本 (research_lookup.py) | `Sources (N):` 部分，包含 `[标题] (日期) + URL` + `Additional References (N):` 及 DOI 和学术 URL | 深度研究（Parallel Chat API）— 人类可读 |
| JSON（`--json` 通过 research_lookup.py） | 完整引用对象：`url`、`title`、`date`、`snippet`、`doi`、`type` | 当需要从深度研究中获取最大引用元数据时 |

**对于 parallel-cli search**，保存的 JSON 文件包括：每个结果的完整搜索结果，包括标题、URL、发布日期和内容摘要。
**对于 Parallel Chat API 后端**，保存的文件包括：研究报告 + 来源列表（标题、URL） + 附加参考文献（DOI、学术 URL）。

**在以下情况下使用 `--json`：**
- 以编程方式解析引用元数据
- 保留完整的 DOI 和 URL 数据以生成 BibTeX
- 维护结构化的引用对象以进行交叉引用

### 为什么全部保存

1.  **可再现性**：每个引用和声明都可以追溯到其原始研究来源
2.  **上下文窗口恢复**：如果上下文被压缩，可以重新读取保存的结果而无需重新查询
3.  **审计跟踪**：`sources/` 文件夹准确记录了所有研究信息的收集方式
4.  **跨部分重用**：多个部分可以引用相同保存的研究，而无需重复查询
5.  **成本效率**：在进行新的 API 调用之前，检查 `sources/` 中是否已有现有结果
6.  **同行评审支持**：审阅者可以验证每个引用背后的研究

### 进行新查询前，首先检查 Sources

在调用 `research_lookup.py` 之前，检查是否已有相关结果：

```bash
ls sources/  # 检查现有保存的结果
```

如果之前的查找覆盖了同一主题，则重新读取保存的文件，而不是进行新的 API 调用。

### 日志记录

保存研究结果时，始终记录：

```
[HH:MM:SS] SAVED: Research lookup to sources/research_20250217_143000_crispr_advances.md (3,800 words, 8 citations)
[HH:MM:SS] SAVED: Paper search to sources/papers_20250217_143500_transformer_attention.md (6 papers found)
```

---

## 与科学写作集成

此技能通过以下方式增强科学写作：

1.  **文献综述支持**：为引言和讨论收集当前研究 — **保存到 `sources/`**
2.  **方法验证**：根据当前标准验证协议 — **保存到 `sources/`**
3.  **结果背景化**：将发现与最近的类似研究进行比较 — **保存到 `sources/`**
4.  **讨论增强**：用最新证据支持论点 — **保存到 `sources/`**
5.  **引用管理**：提供格式正确的引用 — **保存到 `sources/`**

## 补充工具

| 任务 | 工具 |
|------|------|
| 一般网页搜索（快速） | `parallel-cli search`（内置于此技能中） |
| 学术聚焦网页搜索 | `parallel-cli search --include-domains`（内置于此技能中） |
| URL 内容提取 | `parallel-cli extract`（parallel-web 技能） |
| 深度研究（穷尽） | `research-lookup` 通过 Parallel Chat API 或 `parallel-web` deep research |
| 学术论文搜索 | `research-lookup`（通过带有学术域名的 parallel-cli 自动路由） |
| Google 学术搜索 | `citation-management` 技能 |
| PubMed 搜索 | `citation-management` 技能 |
| DOI 转 BibTeX | `citation-management` 技能 |
| 元数据验证 | `parallel-cli extract`（parallel-web 技能） |

---

## 错误处理与限制

**已知限制：**
- parallel-cli search：需要安装并验证 `parallel-cli`
- Parallel Chat API（core 模型）：复杂查询可能需要多达 5 分钟
- 所有后端：无法访问专有或受限数据库
- parallel-cli：需要安装和验证
- Parallel Chat API：复杂查询可能需要多达 5 分钟

**回退行为：**
- 如果未找到 `parallel-cli`，使用 `curl -fsSL https://parallel.ai/install.sh | bash` 或 `uv tool install "parallel-web-tools[cli]"` 安装
- 如果 parallel-cli 搜索返回的结果不足，回退到 Parallel Chat API
- 如果所选后端的 API 密钥缺失，尝试另一个后端
- 如果所有后端都失败，返回结构化的错误响应
- 如果初始响应不足，重新措辞查询以获得更好的结果

---

## 使用示例

### 示例 1：一般研究（路由到 parallel-cli search）

**查询**："Recent advances in transformer attention mechanisms 2025"

**后端**：parallel-cli search（默认、快速）

**命令**：
```bash
parallel-cli search "Recent advances in transformer attention mechanisms 2025" \
  -q "transformer" -q "attention" -q "2025" \
  --json --max-results 10 --excerpt-max-chars-total 27000 \
  --include-domains "arxiv.org,semanticscholar.org,nature.com,science.org,ieee.org,acm.org" \
  -o sources/research_transformer_attention-academic.json

parallel-cli search "Recent advances in transformer attention mechanisms 2025" \
  -q "transformer" -q "attention" \
  --json --max-results 10 --excerpt-max-chars-total 27000 \
  -o sources/research_transformer_attention-general.json
```

**回复**：带有来自学术和一般来源的内联引用的综合发现，涵盖最新论文、关键创新和性能基准。

### 示例 2：学术论文搜索（路由到带有学术域名的 parallel-cli）

**查询**："Find papers on CRISPR off-target effects in clinical trials"

**后端**：带有 `--include-domains` 的 parallel-cli search，目标学术来源

**回复**：来自 arxiv、pubmed、nature、science 和其他学术来源的，带有标题、URL、日期和内容摘要的结果。

### 示例 3：比较分析（路由到 parallel-cli search）

**查询**："Compare and contrast mRNA vaccines vs traditional vaccines for cancer treatment"

**后端**：parallel-cli search（默认、快速）

**回复**：来自多个网页来源的综合比较，带有内联引用、结构化分析和证据质量注释。

### 示例 4：市场数据（路由到 parallel-cli search）

**查询**："Global AI adoption in healthcare statistics 2025"

**后端**：parallel-cli search（默认、快速）

```bash
parallel-cli search "Global AI adoption in healthcare statistics 2025" \
  -q "AI healthcare" -q "adoption statistics" \
  --json --max-results 10 --excerpt-max-chars-total 27000 \
  --after-date 2024-01-01 \
  -o sources/research_ai_healthcare_adoption.json
```

**回复**：当前市场数据、采用率、增长预测和带有来源引用的区域分析。

---

## 总结

此技能作为主要研究界面，具有智能三后端路由：

- **parallel-cli search**（默认）：通过 parallel-web 技能实现快速、经济高效的网页搜索，并优先考虑学术来源
- **Parallel Chat API**（`core` 模型）：深度、穷尽的多来源综合（仅在明确请求时使用）
- **自动路由**：检测查询类型并路由到最佳后端
- **手动覆盖**：在需要时强制使用任何后端
- **学术优先级**：两次搜索模式确保科学查询中学术来源的出现
