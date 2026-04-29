# PubMed 检索指南

在 PubMed 中搜索生物医学和生命科学文献的综合指南，包括 MeSH 词、字段标签、高级检索策略以及 E-utilities API 的使用方法。

## 概述

PubMed 是生物医学文献的首选数据库：

- **收录范围**：3500 万+ 条引文
- **学科领域**：生物医学和生命科学
- **来源**：MEDLINE、生命科学期刊、在线书籍
- **权威性**：由国家医学图书馆（NLM）/ NCBI 维护
- **访问方式**：免费，无需账户
- **更新频率**：每日更新新引文
- **编目质量**：高质量元数据、MeSH 索引

## 基本检索

### 简单关键词检索

PubMed 自动将词映射到 MeSH 并搜索多个字段：

```
diabetes
CRISPR gene editing
Alzheimer's disease treatment
cancer immunotherapy
```

**自动功能**：

- 自动 MeSH 映射
- 复数/单数变体
- 缩写展开
- 拼写检查

### 精确短语检索

使用引号进行精确短语检索：

```
"CRISPR-Cas9"
"systematic review"
"randomized controlled trial"
"machine learning"
```

## MeSH（医学主题词表）

### 什么是 MeSH？

MeSH 是用于生物医学文献标引的受控词汇词库：

- **层级结构**：按树状结构组织
- **一致的标引**：同一概念总是以相同方式标记
- **全面性**：覆盖疾病、药物、解剖学、技术等
- **专业编目**：NLM 标引员分配 MeSH 词

### 查找 MeSH 词

**MeSH 浏览器**：https://meshb.nlm.nih.gov/search

**示例**：

```
Search: "heart attack"
MeSH term: "Myocardial Infarction"
```

**在 PubMed 中**：

1. 用关键词搜索
2. 查看左侧栏中的"MeSH Terms"
3. 选择相关的 MeSH 词
4. 添加到搜索中

### 在检索中使用 MeSH

**基本 MeSH 检索**：

```
"Diabetes Mellitus"[MeSH]
"CRISPR-Cas Systems"[MeSH]
"Alzheimer Disease"[MeSH]
"Neoplasms"[MeSH]
```

**MeSH 加上副标题**：

```
"Diabetes Mellitus/drug therapy"[MeSH]
"Neoplasms/genetics"[MeSH]
"Heart Failure/prevention and control"[MeSH]
```

**常用副标题**：

- `/drug therapy`：药物治疗
- `/diagnosis`：诊断方面
- `/genetics`：遗传学方面
- `/epidemiology`：发生率和分布
- `/prevention and control`：预防方法
- `/etiology`：病因
- `/surgery`：外科治疗
- `/metabolism`：代谢方面

### MeSH 扩展

默认情况下，MeSH 搜索包含更窄的概念（扩展）：

```
"Neoplasms"[MeSH]
# Includes: Breast Neoplasms, Lung Neoplasms, etc.
```

**禁用扩展**（仅精确词）：

```
"Neoplasms"[MeSH:NoExp]
```

### MeSH 主要主题

仅在 MeSH 词是主要焦点时检索：

```
"Diabetes Mellitus"[MeSH Major Topic]
# Only papers where diabetes is main topic
```

## 字段标签

字段标签指定要搜索记录的哪个部分。

### 常用字段标签

**标题和摘要**：

```
cancer[Title]                    # In title only
treatment[Title/Abstract]        # In title or abstract
"machine learning"[Title/Abstract]
```

**作者**：

```
"Smith J"[Author]
"Doudna JA"[Author]
"Collins FS"[Author]
```

**作者 - 全名**：

```
"Smith, John"[Full Author Name]
```

**期刊**：

```
"Nature"[Journal]
"Science"[Journal]
"New England Journal of Medicine"[Journal]
"Nat Commun"[Journal]           # Abbreviated form
```

**发布日期**：

```
2023[Publication Date]
2020:2024[Publication Date]      # Date range
2023/01/01:2023/12/31[Publication Date]
```

**创建日期**：

```
2023[Date - Create]              # When added to PubMed
```

**出版类型**：

```
"Review"[Publication Type]
"Clinical Trial"[Publication Type]
"Meta-Analysis"[Publication Type]
"Randomized Controlled Trial"[Publication Type]
```

**语言**：

```
English[Language]
French[Language]
```

**DOI**：

```
10.1038/nature12345[DOI]
```

**PMID（PubMed ID）**：

```
12345678[PMID]
```

**文章 ID**：

```
PMC1234567[PMC]                  # PubMed Central ID
```

### 不太常用但有用的标签

```
humans[MeSH Terms]               # Only human studies
animals[MeSH Terms]              # Only animal studies
"United States"[Place of Publication]
nih[Grant Number]                # NIH-funded research
"Female"[Sex]                    # Female subjects
"Aged, 80 and over"[Age]        # Elderly subjects
```

## 布尔运算符

用布尔逻辑组合搜索词。

### AND

两个词都必须出现（默认行为）：

```
diabetes AND treatment
"CRISPR-Cas9" AND "gene editing"
cancer AND immunotherapy AND "clinical trial"[Publication Type]
```

### OR

任一词出现即可：

```
"heart attack" OR "myocardial infarction"
diabetes OR "diabetes mellitus"
CRISPR OR Cas9 OR "gene editing"
```

**使用场景**：同义词和相关词

### NOT

排除词：

```
cancer NOT review
diabetes NOT animal
"machine learning" NOT "deep learning"
```

**注意**：可能会排除同时提到两个词的相关论文。

### 组合运算符

使用括号进行复杂逻辑：

```
(diabetes OR "diabetes mellitus") AND (treatment OR therapy)

("CRISPR" OR "gene editing") AND ("therapeutic" OR "therapy") 
  AND 2020:2024[Publication Date]

(cancer OR neoplasm) AND (immunotherapy OR "immune checkpoint inhibitor") 
  AND ("clinical Trial"[Publication Type] OR "randomized controlled trial"[Publication Type])
```

## 高级搜索构建器

**访问地址**：https://pubmed.ncbi.nlm.nih.gov/advanced/

**功能**：

- 可视化查询构建器
- 添加多个查询框
- 从下拉菜单中选择字段标签
- 用 AND/OR/NOT 组合
- 预览结果
- 显示最终查询字符串
- 保存查询

**工作流程**：

1. 在单独的框中添加搜索词
2. 选择字段标签
3. 选择布尔运算符
4. 预览结果
5. 根据需要优化
6. 复制最终查询字符串
7. 在脚本中使用或保存

**构建的查询示例**：

```
#1: "Diabetes Mellitus, Type 2"[MeSH]
#2: "Metformin"[MeSH]
#3: "Clinical Trial"[Publication Type]
#4: 2020:2024[Publication Date]
#5: #1 AND #2 AND #3 AND #4
```

## 筛选条件和限制

### 文章类型

```
"Review"[Publication Type]
"Systematic Review"[Publication Type]
"Meta-Analysis"[Publication Type]
"Clinical Trial"[Publication Type]
"Randomized Controlled Trial"[Publication Type]
"Case Reports"[Publication Type]
"Comparative Study"[Publication Type]
```

### 物种

```
humans[MeSH Terms]
mice[MeSH Terms]
rats[MeSH Terms]
```

### 性别

```
"Female"[MeSH Terms]
"Male"[MeSH Terms]
```

### 年龄组

```
"Infant"[MeSH Terms]
"Child"[MeSH Terms]
"Adolescent"[MeSH Terms]
"Adult"[MeSH Terms]
"Aged"[MeSH Terms]
"Aged, 80 and over"[MeSH Terms]
```

### 文本可获取性

```
free full text[Filter]           # Free full-text available
```

### 期刊类别

```
"Journal Article"[Publication Type]
```

## E-utilities API

NCBI 通过 E-utilities（Entrez 编程工具）提供程序化访问。

### 概述

**基础 URL**：`https://eutils.ncbi.nlm.nih.gov/entrez/eutils/`

**主要工具**：

- **ESearch**：搜索并检索 PMID
- **EFetch**：检索完整记录
- **ESummary**：检索文档摘要
- **ELink**：查找相关文章
- **EInfo**：数据库统计

**无需 API 密钥**，但建议使用以：

- 获得更高的速率限制（10 次/秒 vs 3 次/秒）
- 获得更好的性能
- 识别您的项目

**获取 API 密钥**：https://www.ncbi.nlm.nih.gov/account/

### ESearch - 搜索 PubMed

获取查询的 PMID。

**端点**：`/esearch.fcgi`

**参数**：

- `db`：数据库（pubmed）
- `term`：搜索查询
- `retmax`：最大结果数（默认 20，最大 10000）
- `retstart`：起始位置（用于分页）
- `sort`：排序顺序（relevance、pub_date、author）
- `api_key`：您的 API 密钥（可选但建议使用）

**示例 URL**：

```
https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi?
  db=pubmed&
  term=diabetes+AND+treatment&
  retmax=100&
  retmode=json&
  api_key=YOUR_API_KEY
```

**响应**：

```json
{
  "esearchresult": {
    "count": "250000",
    "retmax": "100",
    "idlist": ["12345678", "12345679", ...]
  }
}
```

### EFetch - 检索记录

获取 PMID 的完整元数据。

**端点**：`/efetch.fcgi`

**参数**：

- `db`：（pubmed）
- `id`：逗号分隔的 PMID
- `retmode`：格式（xml、json、text）
- `rettype`：类型（abstract、medline、full）
- `api_key`：您的 API 密钥

**示例 URL**：

```
https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?
  db=pubmed&
  id=12345678,12345679&
  retmode=xml&
  api_key=YOUR_API_KEY
```

**响应**：包含完整元数据的 XML，包括：

- 标题
- 作者（及其单位）
- 摘要
- 期刊
- 发布日期
- DOI
- PMID、PMCID
- MeSH 词
- 关键词

### ESummary - 获取摘要

比 EFetch 更轻量的替代方案。

**示例**：

```
https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esummary.fcgi?
  db=pubmed&
  id=12345678&
  retmode=json&
  api_key=YOUR_API_KEY
```

**返回**：关键元数据，不包括完整摘要和详细信息。

### ELink - 查找相关文章

查找相关文章或到其他数据库的链接。

**示例**：

```
https://eutils.ncbi.nlm.nih.gov/entrez/eutils/elink.fcgi?
  dbfrom=pubmed&
  db=pubmed&
  id=12345678&
  linkname=pubmed_pubmed_citedin
```

**链接类型**：

- `pubmed_pubmed`：相关文章
- `pubmed_pubmed_citedin`：引用本文的论文
- `pubmed_pmc`：PMC 全文版本
- `pubmed_protein`：相关蛋白质记录

### 速率限制

**无 API 密钥**：

- 每秒 3 个请求
- 超出则被阻止

**有 API 密钥**：

- 每秒 10 个请求
- 更适合程序化访问

**最佳实践**：

```python
import time
time.sleep(0.34)  # ~3 requests/second
# or
time.sleep(0.11)  # ~10 requests/second with API key
```

### API 密钥使用方法

**获取 API 密钥**：

1. 创建 NCBI 账户：https://www.ncbi.nlm.nih.gov/account/
2. 设置 → API 密钥管理
3. 创建新 API 密钥
4. 复制密钥

**在请求中使用**：

```
&api_key=YOUR_API_KEY_HERE
```

**安全存储**：

```bash
# In environment variable
export NCBI_API_KEY="your_key_here"

# In script
import os
api_key = os.getenv('NCBI_API_KEY')
```

## 检索策略

### 综合系统检索

用于系统综述和荟萃分析：

```
# 1. Identify key concepts
Concept 1: Diabetes
Concept 2: Treatment
Concept 3: Outcomes

# 2. Find MeSH terms and synonyms
Concept 1: "Diabetes Mellitus"[MeSH] OR diabetes OR diabetic
Concept 2: "Drug Therapy"[MeSH] OR treatment OR therapy OR medication
Concept 3: "Treatment Outcome"[MeSH] OR outcome OR efficacy OR effectiveness

# 3. Combine with AND
("Diabetes Mellitus"[MeSH] OR diabetes OR diabetic) 
  AND ("Drug Therapy"[MeSH] OR treatment OR therapy OR medication)
  AND ("Treatment Outcome"[MeSH] OR outcome OR efficacy OR effectiveness)

# 4. Add filters
AND 2015:2024[Publication Date]
AND ("Clinical Trial"[Publication Type] OR "Randomized Controlled Trial"[Publication Type])
AND English[Language]
AND humans[MeSH Terms]
```

### 查找临床试验

```
# Specific disease + clinical trials
"Alzheimer Disease"[MeSH] 
  AND ("Clinical Trial"[Publication Type] 
       OR "Randomized Controlled Trial"[Publication Type])
  AND 2020:2024[Publication Date]

# Specific drug trials
"Metformin"[MeSH] 
  AND "Diabetes Mellitus, Type 2"[MeSH]
  AND "Randomized Controlled Trial"[Publication Type]
```

### 查找综述

```
# Systematic reviews on topic
"CRISPR-Cas Systems"[MeSH] 
  AND ("Systematic Review"[Publication Type] OR "Meta-Analysis"[Publication Type])

# Reviews in high-impact journals
cancer immunotherapy 
  AND "Review"[Publication Type]
  AND ("Nature"[Journal] OR "Science"[Journal] OR "Cell"[Journal])
```

### 查找近期论文

```
# Papers from last year
"machine learning"[Title/Abstract] 
  AND "drug discovery"[Title/Abstract]
  AND 2024[Publication Date]

# Recent papers in specific journal
"CRISPR"[Title/Abstract] 
  AND "Nature"[Journal]
  AND 2023:2024[Publication Date]
```

### 作者追踪

```
# Specific author's recent work
"Doudna JA"[Author] AND 2020:2024[Publication Date]

# Author + topic
"Church GM"[Author] AND "synthetic biology"[Title/Abstract]
```

### 高质量证据

```
# Meta-analyses and systematic reviews
(diabetes OR "diabetes mellitus") 
  AND (treatment OR therapy)
  AND ("Meta-Analysis"[Publication Type] OR "Systematic Review"[Publication Type])

# RCTs only
cancer immunotherapy 
  AND "Randomized Controlled Trial"[Publication Type]
  AND 2020:2024[Publication Date]
```

## 脚本集成

### search_pubmed.py 使用方法

**基本搜索**：

```bash
python scripts/search_pubmed.py "diabetes treatment"
```

**使用 MeSH 词**：

```bash
python scripts/search_pubmed.py \
  --query '"Diabetes Mellitus"[MeSH] AND "Drug Therapy"[MeSH]'
```

**日期范围筛选**：

```bash
python scripts/search_pubmed.py "CRISPR" \
  --date-start 2020-01-01 \
  --date-end 2024-12-31 \
  --limit 200
```

**出版类型筛选**：

```bash
python scripts/search_pubmed.py "cancer immunotherapy" \
  --publication-types "Clinical Trial,Randomized Controlled Trial" \
  --limit 100
```

**导出为 BibTeX**：

```bash
python scripts/search_pubmed.py "Alzheimer's disease" \
  --limit 100 \
  --format bibtex \
  --output alzheimers.bib
```

**从文件加载复杂查询**：

```bash
# Save complex query in query.txt
cat > query.txt << 'EOF'
("Diabetes Mellitus, Type 2"[MeSH] OR "diabetes"[Title/Abstract])
AND ("Metformin"[MeSH] OR "metformin"[Title/Abstract])
AND "Randomized Controlled Trial"[Publication Type]
AND 2015:2024[Publication Date]
AND English[Language]
EOF

# Run search
python scripts/search_pubmed.py --query-file query.txt --limit 500
```

### 批量搜索

```bash
# Search multiple topics
TOPICS=("diabetes treatment" "cancer immunotherapy" "CRISPR gene editing")

for topic in "${TOPICS[@]}"; do
  python scripts/search_pubmed.py "$topic" \
    --limit 100 \
    --output "${topic// /_}.json"
  sleep 1
done
```

### 提取元数据

```bash
# Search returns PMIDs
python scripts/search_pubmed.py "topic" --output results.json

# Extract full metadata
python scripts/extract_metadata.py \
  --input results.json \
  --output references.bib
```

## 技巧和最佳实践

### 检索构建

1. **从 MeSH 词开始**：

   - 使用 MeSH 浏览器查找正确的词
   - 比关键词检索更精确
   - 无论使用什么术语，都能捕获所有相关论文

2. **包含文本词变体**：

   ```
   # Better coverage
   ("Diabetes Mellitus"[MeSH] OR diabetes OR diabetic)
   ```

3. **适当使用字段标签**：

   - `[MeSH]` 用于标准化概念
   - `[Title/Abstract]` 用于特定术语
   - `[Author]` 用于已知作者
   - `[Journal]` 用于特定出版物

4. **逐步构建**：

   ```
   # Step 1: Basic search
   diabetes
   
   # Step 2: Add specificity
   "Diabetes Mellitus, Type 2"[MeSH]
   
   # Step 3: Add treatment
   "Diabetes Mellitus, Type 2"[MeSH] AND "Metformin"[MeSH]
   
   # Step 4: Add study type
   "Diabetes Mellitus, Type 2"[MeSH] AND "Metformin"[MeSH] 
     AND "Clinical Trial"[Publication Type]
   
   # Step 5: Add date range
   ... AND 2020:2024[Publication Date]
   ```

### 优化结果

1. **结果过多**：添加筛选条件

   - 限制出版类型
   - 缩小日期范围
   - 添加更具体的 MeSH 词
   - 使用主要主题：`[MeSH Major Topic]`

2. **结果过少**：扩大搜索范围

   - 移除限制性筛选条件
   - 使用 OR 连接同义词
   - 扩大日期范围
   - 使用 MeSH 扩展（默认）

3. **结果不相关**：优化术语

   - 使用更具体的 MeSH 词
   - 用 NOT 添加排除条件
   - 使用标题字段而非所有字段
   - 添加 MeSH 副标题

### 质量控制

1. **记录检索策略**：

   - 保存精确的查询字符串
   - 记录搜索日期
   - 记录结果数量
   - 保存使用的筛选条件

2. **系统化导出**：

   - 使用一致的文件命名
   - 导出为 JSON 以保持灵活性
   - 根据需要转换为 BibTeX
   - 保留原始搜索结果

3. **验证检索到的引文**：

   ```bash
   python scripts/validate_citations.py pubmed_results.bib
   ```

### 保持最新

1. **设置搜索提醒**：

   - PubMed → 保存搜索
   - 接收电子邮件更新
   - 每日、每周或每月

2. **追踪特定期刊**：

   ```
   "Nature"[Journal] AND CRISPR[Title]
   ```

3. **关注关键作者**：

   ```
   "Church GM"[Author]
   ```

## 常见问题及解决方案

### 问题：未找到 MeSH 词

**解决方案**：

- 检查拼写
- 使用 MeSH 浏览器
- 尝试相关术语
- 使用文本词搜索作为后备方案

### 问题：无结果

**解决方案**：

- 移除筛选条件
- 检查查询语法
- 使用 OR 进行更广泛搜索
- 尝试同义词

### 问题：结果质量差

**解决方案**：

- 添加出版类型筛选
- 限制在近几年
- 使用 MeSH 主要主题
- 按期刊质量筛选

### 问题：来自不同来源的重复

**解决方案**：

```bash
python scripts/format_bibtex.py results.bib \
  --deduplicate \
  --output clean.bib
```

### 问题：API 速率限制

**解决方案**：

- 获取 API 密钥（将限制提高到 10 次/秒）
- 在脚本中添加延迟
- 批量处理
- 在非高峰时段使用

## 总结

PubMed 提供权威的生物医学文献检索：

✓ **经过审核的内容**：MeSH 索引、质量控制  
✓ **精确的检索**：字段标签、MeSH 词、筛选条件  
✓ **程序化访问**：E-utilities API  
✓ **免费访问**：无需订阅  
✓ **全面性**：3500 万+ 条引文，每日更新  

关键策略：

- 使用 MeSH 词进行精确检索
- 与文本词结合以获得全面覆盖
- 适当应用字段标签
- 按出版类型和日期筛选
- 使用 E-utilities API 实现自动化
- 记录检索策略以保证可重复性

为了获得更广泛的跨学科覆盖，可以使用 Google Scholar 作为补充。
