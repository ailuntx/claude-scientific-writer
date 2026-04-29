---
name: citation-management
description: 面向学术研究的综合引文管理。检索 Google Scholar 和 PubMed 中的论文，提取准确的元数据，验证引文，并生成格式正确的 BibTeX 条目。当你需要查找论文、核对引文信息、将 DOI 转换为 BibTeX，或确保科学写作中的参考文献准确无误时，应使用此技能。
allowed-tools: [Read, Write, Edit, Bash]
---

# 引文管理

## 概述

在研究和写作过程中系统地管理引文。此技能提供用于检索学术数据库（Google Scholar、PubMed）、从多个来源（CrossRef、PubMed、arXiv）提取准确元数据、验证引文信息，以及生成格式正确的 BibTeX 条目的工具和策略。

这对于保持引文准确性、避免参考文献错误以及确保研究可复现性至关重要。它与文献综述技能无缝集成，可构建完整的研究工作流。

## 何时使用此技能

在以下情况下使用此技能：
- 在 Google Scholar 或 PubMed 中检索特定论文
- 将 DOI、PMID 或 arXiv ID 转换为格式正确的 BibTeX
- 提取引文所需的完整元数据（作者、标题、期刊、年份等）
- 验证现有引文的准确性
- 清理并格式化 BibTeX 文件
- 查找某一领域中被高度引用的论文
- 核实引文信息是否与实际发表内容一致
- 为论文或学位论文构建参考文献列表
- 检查重复引文
- 确保引文格式一致

## 使用科学示意图增强视觉表达

**使用此技能创建文档时，应始终考虑添加科学图表和示意图，以增强视觉传达效果。**

如果你的文档尚未包含示意图或图表：
- 使用 **scientific-schematics** 技能生成 AI 驱动的出版级图表
- 只需用自然语言描述你想要的图表
- Nano Banana Pro 会自动生成、审阅并优化该示意图

**对于新文档：** 应默认生成科学示意图，以可视化文本中描述的关键概念、工作流、架构或关系。

**如何生成示意图：**
```bash
python scripts/generate_schematic.py "your diagram description" -o figures/output.png
```

AI 将自动：
- 创建具有正确格式的出版级图像
- 通过多轮迭代进行审阅和优化
- 确保可访问性（适合色盲、高对比度）
- 将输出保存到 figures/ 目录

**何时添加示意图：**
- 引文工作流图
- 文献检索方法流程图
- 文献管理系统架构图
- 引文样式决策树
- 数据库集成图
- 任何适合可视化的复杂概念

如需关于创建示意图的详细指导，请参阅 scientific-schematics 技能文档。

---

## 核心工作流

引文管理遵循系统化流程：

### 第 1 阶段：论文发现与检索

**目标**：使用学术搜索引擎找到相关论文。

#### Google Scholar 检索

Google Scholar 提供跨学科最全面的覆盖。

**基础检索**：
```bash
# 搜索某一主题的论文
python scripts/search_google_scholar.py "CRISPR gene editing" \
  --limit 50 \
  --output results.json

# 带年份筛选的搜索
python scripts/search_google_scholar.py "machine learning protein folding" \
  --year-start 2020 \
  --year-end 2024 \
  --limit 100 \
  --output ml_proteins.json
```

**高级检索策略**（见 `references/google_scholar_search.md`）：
- 用引号搜索精确短语：`"deep learning"`
- 按作者搜索：`author:LeCun`
- 在标题中搜索：`intitle:"neural networks"`
- 排除词项：`machine learning -survey`
- 使用排序选项查找高被引论文
- 按日期范围筛选以获取近期工作

**最佳实践**：
- 使用具体、聚焦的检索词
- 包含关键技术术语和缩写
- 对快速发展的领域筛选近几年文献
- 查看 “Cited by” 以找到奠基性论文
- 导出前几个结果进行进一步分析

#### PubMed 检索

PubMed 专注于生物医学和生命科学文献（3500 万+ 引文）。

**基础检索**：
```bash
# 搜索 PubMed
python scripts/search_pubmed.py "Alzheimer's disease treatment" \
  --limit 100 \
  --output alzheimers.json

# 使用 MeSH 术语和筛选条件搜索
python scripts/search_pubmed.py \
  --query '"Alzheimer Disease"[MeSH] AND "Drug Therapy"[MeSH]' \
  --date-start 2020 \
  --date-end 2024 \
  --publication-types "Clinical Trial,Review" \
  --output alzheimers_trials.json
```

**高级 PubMed 查询**（见 `references/pubmed_search.md`）：
- 使用 MeSH 术语：`"Diabetes Mellitus"[MeSH]`
- 字段标签：`"cancer"[Title]`, `"Smith J"[Author]`
- 布尔运算符：`AND`, `OR`, `NOT`
- 日期筛选：`2020:2024[Publication Date]`
- 出版类型：`"Review"[Publication Type]`
- 结合 E-utilities API 进行自动化

**最佳实践**：
- 使用 MeSH Browser 查找正确的受控词汇表
- 先在 PubMed Advanced Search Builder 中构建复杂查询
- 使用 OR 包含多个同义词
- 获取 PMID 以便轻松提取元数据
- 导出为 JSON 或直接导出为 BibTeX

### 第 2 阶段：元数据提取

**目标**：将论文标识符（DOI、PMID、arXiv ID）转换为完整、准确的元数据。

#### DOI 到 BibTeX 的快速转换

对于单个 DOI，使用快速转换工具：

```bash
# 转换单个 DOI
python scripts/doi_to_bibtex.py 10.1038/s41586-021-03819-2

# 从文件中转换多个 DOI
python scripts/doi_to_bibtex.py --input dois.txt --output references.bib

# 不同的输出格式
python scripts/doi_to_bibtex.py 10.1038/nature12345 --format json
```

#### 全面的元数据提取

适用于 DOI、PMID、arXiv ID 或 URL：

```bash
# 从 DOI 提取
python scripts/extract_metadata.py --doi 10.1038/s41586-021-03819-2

# 从 PMID 提取
python scripts/extract_metadata.py --pmid 34265844

# 从 arXiv ID 提取
python scripts/extract_metadata.py --arxiv 2103.14030

# 从 URL 提取
python scripts/extract_metadata.py --url "https://www.nature.com/articles/s41586-021-03819-2"

# 从文件批量提取（混合标识符）
python scripts/extract_metadata.py --input identifiers.txt --output citations.bib
```

**元数据来源**（见 `references/metadata_extraction.md`）：

1. **CrossRef API**：DOI 的主要来源
   - 期刊文章的完整元数据
   - 出版商提供的信息
   - 包含作者、标题、期刊、卷、页码、日期
   - 免费，无需 API key

2. **PubMed E-utilities**：生物医学文献
   - 官方 NCBI 元数据
   - 包含 MeSH 术语、摘要
   - PMID 和 PMCID 标识符
   - 免费，高频使用建议提供 API key

3. **arXiv API**：物理、数学、计算机科学、q-bio 领域的预印本
   - 预印本的完整元数据
   - 版本追踪
   - 作者单位
   - 免费，开放获取

4. **DataCite API**：研究数据集、软件及其他资源
   - 非传统学术产出的元数据
   - 数据集和代码的 DOI
   - 免费访问

**提取内容**：
- **必需字段**：author、title、year
- **期刊文章**：journal、volume、number、pages、DOI
- **图书**：publisher、ISBN、edition
- **会议论文**：booktitle、conference location、pages
- **预印本**：repository（arXiv、bioRxiv）、preprint ID
- **附加信息**：abstract、keywords、URL

### 第 2.5 阶段：通过网页搜索丰富元数据（必需）

**目标**：使用网页搜索检测并补全任何缺失的元数据字段。此阶段在提取之后、格式化之前运行，以确保每个 BibTeX 条目都完整。

**这一步至关重要的原因**：来自 API（CrossRef、PubMed、arXiv）的元数据提取有时会返回不完整记录——缺少卷、页码、期号或 DOI。在认为参考文献列表准备就绪之前，必须补齐这些缺失项。

#### 第 1 步：扫描不完整条目

提取元数据后，扫描 BibTeX 文件，查找缺少关键字段的条目：

**每种条目类型需检查的字段：**

| 条目类型 | 必需 | 应有 |
|------------|-----------|-------------|
| @article | author, title, journal, year | volume, pages, number, doi |
| @inproceedings | author, title, booktitle, year | pages, doi |
| @book | author/editor, title, publisher, year | isbn, doi |
| @misc | author, title, year | doi or url |

任何缺少 `volume`、`pages` 或 `doi` 的 `@article` 条目都被视为**不完整**，必须补全。

#### 第 2 步：通过网页搜索查找缺失元数据

对每个不完整条目，搜索缺失信息：

**选项 A — 按标题和作者搜索**（最适合查找 DOI）：
```bash
python scripts/parallel_web.py search \
  "FIRST_AUTHOR TITLE JOURNAL_NAME volume pages DOI" \
  -o sources/search_YYYYMMDD_HHMMSS_citation_CITATIONKEY.md
```

**选项 B — 从 DOI 页面提取**（已知 DOI 但缺少卷/页码时最佳）：
```bash
python scripts/parallel_web.py extract \
  "https://doi.org/10.XXXX/YYYY" \
  --objective "extract complete citation metadata: volume, issue, pages, publication date" \
  -o sources/extract_YYYYMMDD_HHMMSS_doi_CITATIONKEY.md
```

**选项 C — 直接搜索 CrossRef API**（程序化、快速）：
```bash
python scripts/parallel_web.py search \
  "crossref DOI metadata FIRST_AUTHOR TITLE" \
  -o sources/search_YYYYMMDD_HHMMSS_crossref_CITATIONKEY.md
```

**选项 D — 搜索 Google Scholar**（用于难以找到的论文的备选方案）：
```bash
python scripts/parallel_web.py search \
  "google scholar FIRST_AUTHOR TITLE YEAR complete citation" \
  -o sources/search_YYYYMMDD_HHMMSS_scholar_CITATIONKEY.md
```

#### 第 3 步：更新 BibTeX 条目

找到缺失元数据后：

1. 打开 `references.bib`
2. 将缺失字段添加到不完整条目中
3. 验证找到的元数据与现有字段一致（相同作者、标题、年份）
4. 记录每次修复：
   ```
   [HH:MM:SS] METADATA ENRICHED: [CitationKey] - added volume={X}, pages={Y--Z}, doi={10.XXX/YYY} ✅
   ```

#### 第 4 步：处理无法找到的元数据

如果经过网页搜索后仍然确实找不到元数据（非常老的论文、冷门会议等）：

1. 在 BibTeX 条目中添加 `note` 字段说明缺口：
   ```bibtex
   note = {Volume and pages not available — published online only}
   ```
2. 记录异常：
   ```
   [HH:MM:SS] METADATA INCOMPLETE: [CitationKey] - pages unavailable (online-only publication) ⚠️
   ```
3. 这些例外应当很少见——大多数现代论文都可以通过网页搜索找到完整元数据。

#### 快速参考：常见缺失字段及查找位置

| 缺失字段 | 最佳搜索策略 |
|---------------|---------------------|
| DOI | 通过 parallel_web.py 搜索 "AUTHOR TITLE DOI" |
| Volume | 从 DOI 页面提取或搜索 "JOURNAL YEAR TITLE volume" |
| Pages | 从 DOI 页面提取或搜索出版社网站 |
| Issue/Number | 从 DOI 页面提取或 CrossRef |
| Publisher | 搜索 "JOURNAL publisher" 或查看期刊网站 |

---

### 第 3 阶段：BibTeX 格式化

**目标**：生成干净、格式正确的 BibTeX 条目。

#### 理解 BibTeX 条目类型

完整指南见 `references/bibtex_formatting.md`。

**常见条目类型**：
- `@article`：期刊文章（最常见）
- `@book`：图书
- `@inproceedings`：会议论文
- `@incollection`：书籍章节
- `@phdthesis`：学位论文
- `@misc`：预印本、软件、数据集

**各类型所需字段**：

```bibtex
@article{citationkey,
  author  = {Last1, First1 and Last2, First2},
  title   = {Article Title},
  journal = {Journal Name},
  year    = {2024},
  volume  = {10},
  number  = {3},
  pages   = {123--145},
  doi     = {10.1234/example}
}

@inproceedings{citationkey,
  author    = {Last, First},
  title     = {Paper Title},
  booktitle = {Conference Name},
  year      = {2024},
  pages     = {1--10}
}

@book{citationkey,
  author    = {Last, First},
  title     = {Book Title},
  publisher = {Publisher Name},
  year      = {2024}
}
```

#### 格式化与清理

使用格式化工具标准化 BibTeX 文件：

```bash
# 格式化并清理 BibTeX 文件
python scripts/format_bibtex.py references.bib \
  --output formatted_references.bib

# 按 citation key 排序条目
python scripts/format_bibtex.py references.bib \
  --sort key \
  --output sorted_references.bib

# 按年份排序（最新在前）
python scripts/format_bibtex.py references.bib \
  --sort year \
  --descending \
  --output sorted_references.bib

# 删除重复项
python scripts/format_bibtex.py references.bib \
  --deduplicate \
  --output clean_references.bib

# 验证并报告问题
python scripts/format_bibtex.py references.bib \
  --validate \
  --report validation_report.txt
```

**格式化操作**：
- 标准化字段顺序
- 统一缩进和间距
- 标题中的正确大小写处理（用 {} 保护）
- 标准化作者姓名格式
- 统一 citation key 格式
- 删除不必要字段
- 修复常见错误（缺失逗号、括号）

### 第 4 阶段：引文验证

**目标**：验证所有引文准确且完整。

#### 全面验证

```bash
# 验证 BibTeX 文件
python scripts/validate_citations.py references.bib

# 验证并修复常见问题
python scripts/validate_citations.py references.bib \
  --auto-fix \
  --output validated_references.bib

# 生成详细验证报告
python scripts/validate_citations.py references.bib \
  --report validation_report.json \
  --verbose
```

**验证检查**（见 `references/citation_validation.md`）：

1. **DOI 验证**：
   - DOI 可通过 doi.org 正确解析
   - BibTeX 与 CrossRef 之间的元数据一致
   - 不存在损坏或无效 DOI

2. **必需字段**：
   - 条目类型所需字段齐全
   - 不存在空白或缺失的关键信息
   - 作者姓名格式正确

3. **数据一致性**：
   - 年份有效（4 位数字，范围合理）
   - 卷/期为数字
   - 页码格式正确（例如 123--145）
   - URL 可访问

4. **重复检测**：
   - 同一 DOI 被多次使用
   - 相似标题（可能重复）
   - 相同作者/年份/标题组合

5. **格式合规**：
   - BibTeX 语法有效
   - 括号和引号使用正确
   - citation key 唯一
   - 特殊字符处理正确

**验证输出**：
```json
{
  "total_entries": 150,
  "valid_entries": 145,
  "errors": [
    {
      "citation_key": "Smith2023",
      "error_type": "missing_field",
      "field": "journal",
      "severity": "high"
    },
    {
      "citation_key": "Jones2022",
      "error_type": "invalid_doi",
      "doi": "10.1234/broken",
      "severity": "high"
    }
  ],
  "warnings": [
    {
      "citation_key": "Brown2021",
      "warning_type": "possible_duplicate",
      "duplicate_of": "Brown2021a",
      "severity": "medium"
    }
  ]
}
```

### 第 5 阶段：与写作工作流集成

#### 为论文构建参考文献

创建参考文献列表的完整工作流：

```bash
# 1. 检索你主题相关的论文
python scripts/search_pubmed.py \
  '"CRISPR-Cas Systems"[MeSH] AND "Gene Editing"[MeSH]' \
  --date-start 2020 \
  --limit 200 \
  --output crispr_papers.json

# 2. 从检索结果中提取 DOI 并转换为 BibTeX
python scripts/extract_metadata.py \
  --input crispr_papers.json \
  --output crispr_refs.bib

# 3. 通过 DOI 添加特定论文
python scripts/doi_to_bibtex.py 10.1038/nature12345 >> crispr_refs.bib
python scripts/doi_to_bibtex.py 10.1126/science.abcd1234 >> crispr_refs.bib

# 4. 格式化并清理 BibTeX 文件
python scripts/format_bibtex.py crispr_refs.bib \
  --deduplicate \
  --sort year \
  --descending \
  --output references.bib

# 5. 验证所有引文
python scripts/validate_citations.py references.bib \
  --auto-fix \
  --report validation.json \
  --output final_references.bib

# 6. 查看验证报告并修复任何剩余问题
cat validation.json

# 7. 在你的 LaTeX 文档中使用
# \bibliography{final_references}
```

#### 与文献综述技能集成

此技能与 `literature-review` 技能相辅相成：

**文献综述技能** → 系统检索与综合
**引文管理技能** → 技术性引文处理

**组合工作流**：
1. 使用 `literature-review` 进行跨数据库的全面检索
2. 使用 `citation-management` 提取并验证所有引文
3. 使用 `literature-review` 按主题综合研究发现
4. 使用 `citation-management` 核实最终参考文献的准确性

```bash
# 完成文献综述后
# 验证综述文档中的所有引文
python scripts/validate_citations.py my_review_references.bib --report review_validation.json

# 如有需要，按特定引文样式格式化
python scripts/format_bibtex.py my_review_references.bib \
  --style nature \
  --output formatted_refs.bib
```

## 检索策略

### Google Scholar 最佳实践

**查找奠基性和高影响力论文**（关键）：

始终优先考虑基于被引次数、发表平台质量和作者声誉的论文：

**被引次数阈值：**
| 论文年龄 | 引用次数 | 分类 |
|-----------|-----------|----------------|
| 0-3 年 | 20+ | 值得关注 |
| 0-3 年 | 100+ | 影响很大 |
| 3-7 年 | 100+ | 重要 |
| 3-7 年 | 500+ | 里程碑论文 |
| 7+ 年 | 500+ | 奠基性工作 |
| 7+ 年 | 1000+ | 基础性工作 |

**期刊/会议质量层级：**
- **第 1 层（优先）：** Nature、Science、Cell、NEJM、Lancet、JAMA、PNAS
- **第 2 层（高优先级）：** 影响因子 >10，顶级会议（NeurIPS、ICML、ICLR）
- **第 3 层（良好）：** 专业期刊（IF 5-10）
- **第 4 层（谨慎使用）：** 较低影响力的同行评审平台

**作者声誉指标：**
- h-index >40 的资深研究者
- 在第 1 层平台上有多篇论文发表
- 在知名机构担任领导角色
- 获奖情况和编委/编辑职位

**高影响力论文检索策略：**
- 按引用次数排序（最常被引用的优先）
- 查找第 1 层期刊的综述文章以获取概览
- 查看 “Cited by” 评估影响力和后续工作
- 使用引用提醒跟踪关键论文的新引用
- 使用 `source:Nature` 或 `source:Science` 按顶级期刊筛选
- 使用 `author:LastName` 搜索已知领域领军人物的论文

**高级运算符**（完整列表见 `references/google_scholar_search.md`）：
```
"exact phrase"           # 精确短语匹配
author:lastname          # 按作者搜索
intitle:keyword          # 仅在标题中搜索
source:journal           # 搜索特定期刊
-exclude                 # 排除词项
OR                       # 备选词项
2020..2024              # 年份范围
```

**示例检索**：
```
# 查找某主题近期综述
"CRISPR" intitle:review 2023..2024

# 查找某位作者在该主题上的论文
author:Church "synthetic biology"

# 查找高被引的基础性工作
"deep learning" 2012..2015 sort:citations

# 排除综述并聚焦方法论文
"protein folding" -survey -review intitle:method
```

### PubMed 最佳实践

**使用 MeSH 术语**：
MeSH（Medical Subject Headings）提供受控词汇表，用于精确检索。

1. **查找 MeSH 术语**：https://meshb.nlm.nih.gov/search
2. **在查询中使用**：`"Diabetes Mellitus, Type 2"[MeSH]`
3. **结合关键词**以获得全面覆盖

**字段标签**：
```
[Title]              # 仅在标题中搜索
[Title/Abstract]     # 在标题或摘要中搜索
[Author]             # 按作者姓名搜索
[Journal]            # 搜索特定期刊
[Publication Date]   # 日期范围
[Publication Type]   # 文章类型
[MeSH]              # MeSH 术语
```

**构建复杂查询**：
```bash
# 近期发表的糖尿病治疗临床试验
"Diabetes Mellitus, Type 2"[MeSH] AND "Drug Therapy"[MeSH] 
AND "Clinical Trial"[Publication Type] AND 2020:2024[Publication Date]

# 某特定期刊中关于 CRISPR 的综述
"CRISPR-Cas Systems"[MeSH] AND "Nature"[Journal] AND "Review"[Publication Type]

# 某位作者的近期工作
"Smith AB"[Author] AND cancer[Title/Abstract] AND 2022:2024[Publication Date]
```

**用于自动化的 E-utilities**：
这些脚本使用 NCBI E-utilities API 进行程序化访问：
- **ESearch**：搜索并检索 PMID
- **EFetch**：检索完整元数据
- **ESummary**：获取摘要信息
- **ELink**：查找相关文章

完整 API 文档见 `references/pubmed_search.md`。

## 工具与脚本

### search_google_scholar.py

检索 Google Scholar 并导出结果。

**功能**：
- 带速率限制的自动化搜索
- 支持分页
- 年份范围筛选
- 导出为 JSON 或 BibTeX
- 引用次数信息

**用法**：
```bash
# 基础搜索
python scripts/search_google_scholar.py "quantum computing"

# 带筛选条件的高级搜索
python scripts/search_google_scholar.py "quantum computing" \
  --year-start 2020 \
  --year-end 2024 \
  --limit 100 \
  --sort-by citations \
  --output quantum_papers.json

# 直接导出为 BibTeX
python scripts/search_google_scholar.py "machine learning" \
  --limit 50 \
  --format bibtex \
  --output ml_papers.bib
```

### search_pubmed.py

使用 E-utilities API 检索 PubMed。

**功能**：
- 支持复杂查询（MeSH、字段标签、布尔运算）
- 日期范围筛选
- 出版类型筛选
- 带元数据的批量检索
- 导出为 JSON 或 BibTeX

**用法**：
```bash
# 简单关键词搜索
python scripts/search_pubmed.py "CRISPR gene editing"

# 带筛选条件的复杂查询
python scripts/search_pubmed.py \
  --query '"CRISPR-Cas Systems"[MeSH] AND "therapeutic"[Title/Abstract]' \
  --date-start 2020-01-01 \
  --date-end 2024-12-31 \
  --publication-types "Clinical Trial,Review" \
  --limit 200 \
  --output crispr_therapeutic.json

# 导出为 BibTeX
python scripts/search_pubmed.py "Alzheimer's disease" \
  --limit 100 \
  --format bibtex \
  --output alzheimers.bib
```

### extract_metadata.py

从论文标识符中提取完整元数据。

**功能**：
- 支持 DOI、PMID、arXiv ID、URL
- 查询 CrossRef、PubMed、arXiv API
- 处理多种标识符类型
- 批量处理
- 多种输出格式

**用法**：
```bash
# 单个 DOI
python scripts/extract_metadata.py --doi 10.1038/s41586-021-03819-2

# 单个 PMID
python scripts/extract_metadata.py --pmid 34265844

# 单个 arXiv ID
python scripts/extract_metadata.py --arxiv 2103.14030

# 从 URL
python scripts/extract_metadata.py \
  --url "https://www.nature.com/articles/s41586-021-03819-2"

# 批量处理（每行一个标识符的文件）
python scripts/extract_metadata.py \
  --input paper_ids.txt \
  --output references.bib

# 不同的输出格式
python scripts/extract_metadata.py \
  --doi 10.1038/nature12345 \
  --format json  # 或 bibtex、yaml
```

### validate_citations.py

验证 BibTeX 条目的准确性和完整性。

**功能**：
- 通过 doi.org 和 CrossRef 验证 DOI
- 检查必需字段
- 检测重复项
- 格式验证
- 自动修复常见问题
- 详细报告

**用法**：
```bash
# 基础验证
python scripts/validate_citations.py references.bib

# 带自动修复
python scripts/validate_citations.py references.bib \
  --auto-fix \
  --output fixed_references.bib

# 详细验证报告
python scripts/validate_citations.py references.bib \
  --report validation_report.json \
  --verbose

# 仅检查 DOI
python scripts/validate_citations.py references.bib \
  --check-dois-only
```

### format_bibtex.py

格式化并清理 BibTeX 文件。

**功能**：
- 标准化格式
- 排序条目（按 key、年份、作者）
- 删除重复项
- 验证语法
- 修复常见错误
- 强制执行 citation key 规范

**用法**：
```bash
# 基础格式化
python scripts/format_bibtex.py references.bib

# 按年份排序（最新在前）
python scripts/format_bibtex.py references.bib \
  --sort year \
  --descending \
  --output sorted_refs.bib

# 删除重复项
python scripts/format_bibtex.py references.bib \
  --deduplicate \
  --output clean_refs.bib

# 完整清理
python scripts/format_bibtex.py references.bib \
  --deduplicate \
  --sort year \
  --validate \
  --auto-fix \
  --output final_refs.bib
```

### doi_to_bibtex.py

快速将 DOI 转换为 BibTeX。

**功能**：
- 快速转换单个 DOI
- 批量处理
- 多种输出格式
- 剪贴板支持

**用法**：
```bash
# 单个 DOI
python scripts/doi_to_bibtex.py 10.1038/s41586-021-03819-2

# 多个 DOI
python scripts/doi_to_bibtex.py \
  10.1038/nature12345 \
  10.1126/science.abc1234 \
  10.1016/j.cell.2023.01.001

# 从文件读取（每行一个 DOI）
python scripts/doi_to_bibtex.py --input dois.txt --output references.bib

# 复制到剪贴板
python scripts/doi_to_bibtex.py 10.1038/nature12345 --clipboard
```

## 最佳实践

### 检索策略

1. **先广后窄**：
   - 先用通用术语了解领域
   - 再用更具体的关键词和筛选条件收窄
   - 使用同义词和相关术语

2. **使用多个来源**：
   - Google Scholar 提供全面覆盖
   - PubMed 侧重生物医学
   - arXiv 提供预印本
   - 结合结果以确保完整性

3. **利用引用关系**：
   - 查看 “Cited by” 以寻找奠基性论文
   - 阅读关键论文的参考文献
   - 使用引文网络发现相关工作

4. **记录你的检索**：
   - 保存检索查询和日期
   - 记录结果数量
   - 备注应用的筛选条件或限制

### 元数据提取

1. **始终优先使用 DOI（如果可用）**：
   - 最可靠的标识符
   - 指向出版物的永久链接
   - 通过 CrossRef 获取最佳元数据来源

2. **验证提取的元数据**：
   - 检查作者姓名是否正确
   - 核实期刊/会议名称
   - 确认出版年份
   - 验证页码和卷号

3. **处理特殊情况**：
   - 预印本：包含 repository 和 ID
   - 后来发表的预印本：使用正式发表版本
   - 会议论文：包含会议名称和地点
   - 书籍章节：包含书名和编辑

4. **保持一致性**：
   - 使用一致的作者姓名格式
   - 标准化期刊缩写
   - DOI 采用统一格式（优先 URL 形式）

### BibTeX 质量

1. **遵循规范**：
   - 使用有意义的 citation key（FirstAuthor2024keyword）
   - 用 {} 保护标题中的大小写
   - 页码范围使用 --（不是单个连字符）
   - 所有现代出版物都应包含 DOI 字段

2. **保持整洁**：
   - 删除不必要字段
   - 不保留冗余信息
   - 保持格式一致
   - 定期验证语法

3. **系统化组织**：
   - 按年份或主题排序
   - 将相关论文分组
   - 不同项目使用单独文件
   - 合并时谨慎，避免重复

### 验证

1. **尽早且经常验证**：
   - 添加引文时就进行检查
   - 提交前验证完整参考文献
   - 任何手动编辑后重新验证

2. **及时修复问题**：
   - 损坏的 DOI：查找正确标识符
   - 缺失字段：从原始来源提取
   - 重复项：选择最佳版本，删除其他版本
   - 格式错误：在安全时使用自动修复

3. **对关键引文进行人工复核**：
   - 确认关键论文引用正确
   - 检查作者姓名与出版物一致
   - 核实页码和卷号
   - 确保 URL 仍然有效

## 常见陷阱与规避方法

1. **单一来源偏差**：只使用 Google Scholar 或 PubMed
   - **解决方案**：使用多个数据库进行全面检索

2. **盲目信任元数据**：不核实提取信息
   - **解决方案**：将提取的元数据与原始来源抽样核对

3. **忽略 DOI 错误**：参考文献中的 DOI 损坏或错误
   - **解决方案**：在最终提交前运行验证

4. **格式不一致**：citation key 风格混杂、格式不统一
   - **解决方案**：使用 format_bibtex.py 标准化

5. **重复条目**：同一论文用不同 key 重复引用
   - **解决方案**：在验证中使用重复检测

6. **缺少必需字段**：BibTeX 条目不完整（缺少 volume、pages、DOI）
   - **解决方案**：运行第 2.5 阶段的元数据丰富——在继续之前为每个缺失字段进行网页搜索。绝不要留下没有 volume、pages 和 DOI 的 @article 条目。

7. **过时预印本**：已发表正式版本却仍引用预印本
   - **解决方案**：检查预印本是否已正式发表，并更新为期刊版本

8. **特殊字符问题**：字符导致 LaTeX 编译失败
   - **解决方案**：在 BibTeX 中使用正确转义或 Unicode

9. **提交前未验证**：带着引文错误提交
   - **解决方案**：始终将验证作为最后一步

10. **手动编写 BibTeX 条目**：手工输入条目
    - **解决方案**：始终使用脚本从元数据来源提取

## 示例工作流

### 示例 1：为论文构建参考文献

```bash
# 第 1 步：查找与你主题相关的关键论文
python scripts/search_google_scholar.py "transformer neural networks" \
  --year-start 2017 \
  --limit 50 \
  --output transformers_gs.json

python scripts/search_pubmed.py "deep learning medical imaging" \
  --date-start 2020 \
  --limit 50 \
  --output medical_dl_pm.json

# 第 2 步：从检索结果中提取元数据
python scripts/extract_metadata.py \
  --input transformers_gs.json \
  --output transformers.bib

python scripts/extract_metadata.py \
  --input medical_dl_pm.json \
  --output medical.bib

# 第 3 步：添加你已经知道的特定论文
python scripts/doi_to_bibtex.py 10.1038/s41586-021-03819-2 >> specific.bib
python scripts/doi_to_bibtex.py 10.1126/science.aam9317 >> specific.bib

# 第 4 步：合并所有 BibTeX 文件
cat transformers.bib medical.bib specific.bib > combined.bib

# 第 5 步：格式化并去重
python scripts/format_bibtex.py combined.bib \
  --deduplicate \
  --sort year \
  --descending \
  --output formatted.bib

# 第 6 步：验证
python scripts/validate_citations.py formatted.bib \
  --auto-fix \
  --report validation.json \
  --output final_references.bib

# 第 7 步：查看任何问题
cat validation.json | grep -A 3 '"errors"'

# 第 8 步：在 LaTeX 中使用
# \bibliography{final_references}
```

### 示例 2：转换 DOI 列表

```bash
# 你有一个包含 DOI 的文本文件（每行一个）
# dois.txt 内容如下：
# 10.1038/s41586-021-03819-2
# 10.1126/science.aam9317
# 10.1016/j.cell.2023.01.001

# 全部转换为 BibTeX
python scripts/doi_to_bibtex.py --input dois.txt --output references.bib

# 验证结果
python scripts/validate_citations.py references.bib --verbose
```

### 示例 3：清理现有 BibTeX 文件

```bash
# 你有一个来自不同来源的杂乱 BibTeX 文件
# 按系统化方式清理它

# 第 1 步：格式化并标准化
python scripts/format_bibtex.py messy_references.bib \
  --output step1_formatted.bib

# 第 2 步：删除重复项
python scripts/format_bibtex.py step1_formatted.bib \
  --deduplicate \
  --output step2_deduplicated.bib

# 第 3 步：验证并自动修复
python scripts/validate_citations.py step2_deduplicated.bib \
  --auto-fix \
  --output step3_validated.bib

# 第 4 步：按年份排序
python scripts/format_bibtex.py step3_validated.bib \
  --sort year \
  --descending \
  --output clean_references.bib

# 第 5 步：最终验证报告
python scripts/validate_citations.py clean_references.bib \
  --report final_validation.json \
  --verbose

# 查看报告
cat final_validation.json
```

### 示例 4：查找并引用奠基性论文

```bash
# 查找某一主题的高被引论文
python scripts/search_google_scholar.py "AlphaFold protein structure" \
  --year-start 2020 \
  --year-end 2024 \
  --sort-by citations \
  --limit 20 \
  --output alphafold_seminal.json

# 按被引次数提取前 10 篇
# （脚本会在 JSON 中包含引用次数）

# 转换为 BibTeX
python scripts/extract_metadata.py \
  --input alphafold_seminal.json \
  --output alphafold_refs.bib

# 现在 BibTeX 文件包含最具影响力的论文
```

## 与其他技能的集成

### 文献综述技能

**引文管理** 为 **文献综述** 提供技术基础设施：

- **文献综述**：跨数据库系统检索与综合
- **引文管理**：元数据提取与验证

**组合工作流**：
1. 使用 literature-review 进行系统化检索方法
2. 使用 citation-management 提取并验证引文
3. 使用 literature-review 综合研究发现
4. 使用 citation-management 确保参考文献准确性

### 科学写作技能

**引文管理** 确保 **科学写作** 中参考文献准确：

- 将已验证的 BibTeX 导出用于 LaTeX 论文
- 核实引文符合出版标准
- 按期刊要求格式化参考文献

### 期刊模板技能

**引文管理** 与 **Venue Templates** 协作，用于投稿就绪的稿件：

- 不同期刊/会议需要不同引文样式
- 生成格式正确的参考文献
- 验证引文是否符合期刊/会议要求

## 资源

### 内置资源

**参考文档**（位于 `references/`）：
- `google_scholar_search.md`：完整的 Google Scholar 检索指南
- `pubmed_search.md`：PubMed 和 E-utilities API 文档
- `metadata_extraction.md`：元数据来源和字段要求
- `citation_validation.md`：验证标准与质量检查
- `bibtex_formatting.md`：BibTeX 条目类型和格式规则

**脚本**（位于 `scripts/`）：
- `search_google_scholar.py`：Google Scholar 检索自动化
- `search_pubmed.py`：PubMed E-utilities API 客户端
- `extract_metadata.py`：通用元数据提取器
- `validate_citations.py`：引文验证与核查
- `format_bibtex.py`：BibTeX 格式化与清理
- `doi_to_bibtex.py`：快速 DOI 到 BibTeX 转换器

**资源文件**（位于 `assets/`）：
- `bibtex_template.bib`：各种类型的 BibTeX 示例条目
- `citation_checklist.md`：质量保证检查清单

### 外部资源

**搜索引擎**：
- Google Scholar: https://scholar.google.com/
- PubMed: https://pubmed.ncbi.nlm.nih.gov/
- PubMed Advanced Search: https://pubmed.ncbi.nlm.nih.gov/advanced/

**元数据 API**：
- CrossRef API: https://api.crossref.org/
- PubMed E-utilities: https://www.ncbi.nlm.nih.gov/books/NBK25501/
- arXiv API: https://arxiv.org/help/api/
- DataCite API: https://api.datacite.org/

**工具与验证器**：
- MeSH Browser: https://meshb.nlm.nih.gov/search
- DOI Resolver: https://doi.org/
- BibTeX Format: http://www.bibtex.org/Format/

**引文样式**：
- BibTeX documentation: http://www.bibtex.org/
- LaTeX bibliography management: https://www.overleaf.com/learn/latex/Bibliography_management

## 依赖项

### 必需的 Python 包

```bash
# 核心依赖
pip install requests  # 用于 API 的 HTTP 请求
pip install bibtexparser  # BibTeX 解析与格式化
pip install biopython  # 访问 PubMed E-utilities

# 可选（用于 Google Scholar）
pip install scholarly  # Google Scholar API 封装
# 或
pip install selenium  # 更稳健的 Scholar 抓取
```

### 可选工具

```bash
# 用于高级验证
pip install crossref-commons  # 增强的 CrossRef API 访问
pip install pylatexenc  # LaTeX 特殊字符处理
```

## 总结

citation-management 技能提供：

1. **全面检索能力**，适用于 Google Scholar 和 PubMed
2. **自动化元数据提取**，支持 DOI、PMID、arXiv ID、URL
3. **引文验证**，包括 DOI 核验和完整性检查
4. **BibTeX 格式化**，配有标准化与清理工具
5. **质量保证**，通过验证和报告实现
6. **与科学写作工作流的集成**
7. **通过文档化的检索与提取方法实现可复现性**

使用此技能可在研究全过程中保持引文准确、完整，并确保参考文献达到可发表标准。
