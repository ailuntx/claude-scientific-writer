# 元数据提取指南

从 DOI、PMID、arXiv ID 和 URL 使用各种 API 和服务提取准确引用元数据的综合指南。

## 概述

准确的元数据对于正确的引用至关重要。本指南涵盖：
- 识别论文标识符（DOI、PMID、arXiv ID）
- 查询元数据 API（CrossRef、PubMed、arXiv、DataCite）
- 按条目类型所需的 BibTeX 字段
- 处理边缘情况和特殊情况
- 验证提取的元数据

## 论文标识符

### DOI（数字对象标识符）

**格式**：`10.XXXX/suffix`

**示例**：
```
10.1038/s41586-021-03819-2    # Nature 文章
10.1126/science.aam9317       # Science 文章
10.1016/j.cell.2023.01.001    # Cell 文章
10.1371/journal.pone.0123456  # PLOS ONE 文章
```

**属性**：
- 永久标识符
- 元数据最可靠
- 解析到当前位置
- 出版商分配

**查找位置**：
- 文章首页
- 文章网页
- CrossRef、Google Scholar、PubMed
- 通常在出版商网站上显著显示

### PMID（PubMed ID）

**格式**：8位数字（通常）

**示例**：
```
34265844
28445112
35476778
```

**属性**：
- 特定于 PubMed 数据库
- 仅限于生物医学文献
- 由 NCBI 分配
- 永久标识符

**查找位置**：
- PubMed 搜索结果
- PubMed 上的文章页面
- 通常在文章 PDF 页脚
- PMC（PubMed Central）页面

### PMCID（PubMed Central ID）

**格式**：PMC 后跟数字

**示例**：
```
PMC8287551
PMC7456789
```

**属性**：
- PMC 中的免费全文文章
- PubMed 文章的子集
- 开放获取或作者手稿

### arXiv ID

**格式**：YYMM.NNNNN 或 archive/YYMMNNN

**示例**：
```
2103.14030        # 新格式（自2007年起）
2401.12345        # 2024年提交
arXiv:hep-th/9901001  # 旧格式
```

**属性**：
- 预印本（未经同行评审）
- 物理、数学、计算机科学、q-bio 等
- 版本追踪（v1、v2 等）
- 免费、开放获取

**查找位置**：
- arXiv.org
- 通常在发表前被引用
- 论文 PDF 开头

### 其他标识符

**ISBN**（书籍）：
```
978-0-12-345678-9
0-123-45678-9
```

**arXiv 类别**：
```
cs.LG    # 计算机科学 - 机器学习
q-bio.QM # 定量生物学 - 定量方法
math.ST  # 数学 - 统计学
```

## 元数据 API

### CrossRef API

**DOI 的主要来源** - 期刊文章最全面的元数据。

**基础 URL**：`https://api.crossref.org/works/`

**无需 API 密钥**，但建议使用礼貌池：
- 在 User-Agent 中添加邮箱
- 获得更好的服务
- 无速率限制

#### 基本 DOI 查询

**请求**：
```
GET https://api.crossref.org/works/10.1038/s41586-021-03819-2
```

**响应**（简化）：
```json
{
  "message": {
    "DOI": "10.1038/s41586-021-03819-2",
    "title": ["Article title here"],
    "author": [
      {"given": "John", "family": "Smith"},
      {"given": "Jane", "family": "Doe"}
    ],
    "container-title": ["Nature"],
    "volume": "595",
    "issue": "7865",
    "page": "123-128",
    "published-print": {"date-parts": [[2021, 7, 1]]},
    "publisher": "Springer Nature",
    "type": "journal-article",
    "ISSN": ["0028-0836"]
  }
}
```

#### 可用字段

**始终存在**：
- `DOI`：数字对象标识符
- `title`：文章标题（数组）
- `type`：内容类型（journal-article、book-chapter 等）

**通常存在**：
- `author`：作者对象数组
- `container-title`：期刊/书籍标题
- `published-print` 或 `published-online`：出版日期
- `volume`、`issue`、`page`：出版详情
- `publisher`：出版商名称

**有时存在**：
- `abstract`：文章摘要
- `subject`：主题类别
- `ISSN`：期刊 ISSN
- `ISBN`：书籍 ISBN
- `reference`：参考文献列表
- `is-referenced-by-count`：引用次数

#### 内容类型

CrossRef `type` 字段值：
- `journal-article`：期刊文章
- `book-chapter`：书籍章节
- `book`：书籍
- `proceedings-article`：会议论文
- `posted-content`：预印本
- `dataset`：研究数据集
- `report`：技术报告
- `dissertation`：学位论文

### PubMed E-utilities API

**专为生物医学文献设计** - 包含 MeSH 词的精选元数据。

**基础 URL**：`https://eutils.ncbi.nlm.nih.gov/entrez/eutils/`

**建议使用 API 密钥**（免费）：
- 更高的速率限制
- 更好的性能

#### PMID 到元数据

**步骤 1：EFetch 获取完整记录**

```
GET https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?
  db=pubmed&
  id=34265844&
  retmode=xml&
  api_key=YOUR_KEY
```

**响应**：包含全面元数据的 XML

**步骤 2：解析 XML**

关键字段：
```xml
<PubmedArticle>
  <MedlineCitation>
    <PMID>34265844</PMID>
    <Article>
      <ArticleTitle>Title here</ArticleTitle>
      <AuthorList>
        <Author><LastName>Smith</LastName><ForeName>John</ForeName></Author>
      </AuthorList>
      <Journal>
        <Title>Nature</Title>
        <JournalIssue>
          <Volume>595</Volume>
          <Issue>7865</Issue>
          <PubDate><Year>2021</Year></PubDate>
        </JournalIssue>
      </Journal>
      <Pagination><MedlinePgn>123-128</MedlinePgn></Pagination>
      <Abstract><AbstractText>Abstract text here</AbstractText></Abstract>
    </Article>
  </MedlineCitation>
  <PubmedData>
    <ArticleIdList>
      <ArticleId IdType="doi">10.1038/s41586-021-03819-2</ArticleId>
      <ArticleId IdType="pmc">PMC8287551</ArticleId>
    </ArticleIdList>
  </PubmedData>
</PubmedArticle>
```

#### PubMed 独有字段

**MeSH 词**：受控词汇
```xml
<MeshHeadingList>
  <MeshHeading>
    <DescriptorName UI="D003920">Diabetes Mellitus</DescriptorName>
  </MeshHeading>
</MeshHeadingList>
```

**出版类型**：
```xml
<PublicationTypeList>
  <PublicationType UI="D016428">Journal Article</PublicationType>
  <PublicationType UI="D016449">Randomized Controlled Trial</PublicationType>
</PublicationTypeList>
```

**资助信息**：
```xml
<GrantList>
  <Grant>
    <GrantID>R01-123456</GrantID>
    <Agency>NIAID NIH HHS</Agency>
    <Country>United States</Country>
  </Grant>
</GrantList>
```

### arXiv API

**物理、数学、计算机科学、q-bio 的预印本** - 免费、开放获取。

**基础 URL**：`http://export.arxiv.org/api/query`

**无需 API 密钥**

#### arXiv ID 到元数据

**请求**：
```
GET http://export.arxiv.org/api/query?id_list=2103.14030
```

**响应**：Atom XML

```xml
<entry>
  <id>http://arxiv.org/abs/2103.14030v2</id>
  <title>Highly accurate protein structure prediction with AlphaFold</title>
  <author><name>John Jumper</name></author>
  <author><name>Richard Evans</name></author>
  <published>2021-03-26T17:47:17Z</published>
  <updated>2021-07-01T16:51:46Z</updated>
  <summary>Abstract text here...</summary>
  <arxiv:doi>10.1038/s41586-021-03819-2</arxiv:doi>
  <category term="q-bio.BM" scheme="http://arxiv.org/schemas/atom"/>
  <category term="cs.LG" scheme="http://arxiv.org/schemas/atom"/>
</entry>
```

#### 关键字段

- `id`：arXiv URL
- `title`：预印本标题
- `author`：作者列表
- `published`：第一版本日期
- `updated`：最新版本日期
- `summary`：摘要
- `arxiv:doi`：如果已发表则为 DOI
- `arxiv:journal_ref`：如果已发表则为期刊引用
- `category`：arXiv 类别

#### 版本追踪

arXiv 追踪版本：
- `v1`：初始提交
- `v2`、`v3` 等：修订版本

**始终检查**预印本是否已在期刊上发表（如有 DOI 请使用 DOI）。

### DataCite API

**研究数据集、软件和其他产出** - 为非传统学术作品分配 DOI。

**基础 URL**：`https://api.datacite.org/dois/`

**类似于 CrossRef** 但用于数据集、软件、代码等。

**请求**：
```
GET https://api.datacite.org/dois/10.5281/zenodo.1234567
```

**响应**：包含数据集/软件元数据的 JSON

## 必需的 BibTeX 字段

### @article（期刊文章）

**必需**：
- `author`：作者姓名
- `title`：文章标题
- `journal`：期刊名称
- `year`：出版年份

**可选但建议使用**：
- `volume`：卷号
- `number`：期号
- `pages`：页码范围（如 123--145）
- `doi`：数字对象标识符
- `url`：如果没有 DOI 则使用 URL
- `month`：出版月份

**示例**：
```bibtex
@article{Smith2024,
  author  = {Smith, John and Doe, Jane},
  title   = {Novel Approach to Protein Folding},
  journal = {Nature},
  year    = {2024},
  volume  = {625},
  number  = {8001},
  pages   = {123--145},
  doi     = {10.1038/nature12345}
}
```

### @book（书籍）

**必需**：
- `author` 或 `editor`：作者或编辑
- `title`：书名
- `publisher`：出版商名称
- `year`：出版年份

**可选但建议使用**：
- `edition`：版次（如果不是第一版）
- `address`：出版商所在地
- `isbn`：ISBN
- `url`：URL
- `series`：系列名称

**示例**：
```bibtex
@book{Kumar2021,
  author    = {Kumar, Vinay and Abbas, Abul K. and Aster, Jon C.},
  title     = {Robbins and Cotran Pathologic Basis of Disease},
  publisher = {Elsevier},
  year      = {2021},
  edition   = {10},
  isbn      = {978-0-323-53113-9}
}
```

### @inproceedings（会议论文）

**必需**：
- `author`：作者姓名
- `title`：论文标题
- `booktitle`：会议/论文集名称
- `year`：年份

**可选但建议使用**：
- `pages`：页码范围
- `organization`：组织机构
- `publisher`：出版商
- `address`：会议地点
- `month`：会议月份
- `doi`：如有则使用 DOI

**示例**：
```bibtex
@inproceedings{Vaswani2017,
  author    = {Vaswani, Ashish and Shazeer, Noam and others},
  title     = {Attention is All You Need},
  booktitle = {Advances in Neural Information Processing Systems},
  year      = {2017},
  pages     = {5998--6008},
  volume    = {30}
}
```

### @incollection（书籍章节）

**必需**：
- `author`：章节作者
- `title`：章节标题
- `booktitle`：书名
- `publisher`：出版商名称
- `year`：出版年份

**可选但建议使用**：
- `editor`：书籍编辑
- `pages`：章节页码范围
- `chapter`：章节编号
- `edition`：版次
- `address`：出版商所在地

**示例**：
```bibtex
@incollection{Brown2020,
  author    = {Brown, Peter O. and Botstein, David},
  title     = {Exploring the New World of the Genome with {DNA} Microarrays},
  booktitle = {DNA Microarrays: A Molecular Cloning Manual},
  editor    = {Eisen, Michael B. and Brown, Patrick O.},
  publisher = {Cold Spring Harbor Laboratory Press},
  year      = {2020},
  pages     = {1--45}
}
```

### @phdthesis（学位论文）

**必需**：
- `author`：作者姓名
- `title`：论文标题
- `school`：机构
- `year`：年份

**可选**：
- `type`：类型（如"PhD dissertation"）
- `address`：机构所在地
- `month`：月份
- `url`：URL

**示例**：
```bibtex
@phdthesis{Johnson2023,
  author = {Johnson, Mary L.},
  title  = {Novel Approaches to Cancer Immunotherapy},
  school = {Stanford University},
  year   = {2023},
  type   = {{PhD} dissertation}
}
```

### @misc（预印本、软件、数据集）

**必需**：
- `author`：作者
- `title`：标题
- `year`：年份

**对于预印本，另加**：
- `howpublished`：仓库（如"bioRxiv"）
- `doi`：预印本 DOI
- `note`：预印本 ID

**示例（预印本）**：
```bibtex
@misc{Zhang2024,
  author       = {Zhang, Yi and Chen, Li and Wang, Hui},
  title        = {Novel Therapeutic Targets in Alzheimer's Disease},
  year         = {2024},
  howpublished = {bioRxiv},
  doi          = {10.1101/2024.01.001},
  note         = {Preprint}
}
```

**示例（软件）**：
```bibtex
@misc{AlphaFold2021,
  author       = {DeepMind},
  title        = {{AlphaFold} Protein Structure Database},
  year         = {2021},
  howpublished = {Software},
  url          = {https://alphafold.ebi.ac.uk/},
  doi          = {10.5281/zenodo.5123456}
}
```

## 提取工作流

### 从 DOI 提取

**最佳实践** - 最可靠的来源：

```bash
# 单一 DOI
python scripts/extract_metadata.py --doi 10.1038/s41586-021-03819-2

# 多个 DOI
python scripts/extract_metadata.py \
  --doi 10.1038/nature12345 \
  --doi 10.1126/science.abc1234 \
  --output refs.bib
```

**流程**：
1. 使用 DOI 查询 CrossRef API
2. 解析 JSON 响应
3. 提取所需字段
4. 确定条目类型（@article、@book 等）
5. 格式化为 BibTeX
6. 验证完整性

### 从 PMID 提取

**适用于生物医学文献**：

```bash
# 单一 PMID
python scripts/extract_metadata.py --pmid 34265844

# 多个 PMID
python scripts/extract_metadata.py \
  --pmid 34265844 \
  --pmid 28445112 \
  --output refs.bib
```

**流程**：
1. 使用 PMID 查询 PubMed EFetch
2. 解析 XML 响应
3. 提取元数据包括 MeSH 词
4. 检查响应中是否有 DOI
5. 如有 DOI，可选择查询 CrossRef 获取额外元数据
6. 格式化为 BibTeX

### 从 arXiv ID 提取

**适用于预印本**：

```bash
python scripts/extract_metadata.py --arxiv 2103.14030
```

**流程**：
1. 使用 ID 查询 arXiv API
2. 解析 Atom XML 响应
3. 检查已发表版本（响应中的 DOI）
4. 如已发表：使用 DOI 和 CrossRef
5. 如未发表：使用预印本元数据
6. 格式化为带预印本注释的 @misc

**重要**：始终检查预印本是否已在期刊上发表！

### 从 URL 提取

**当只有 URL 时**：

```bash
python scripts/extract_metadata.py \
  --url "https://www.nature.com/articles/s41586-021-03819-2"
```

**流程**：
1. 解析 URL 以提取标识符
2. 识别类型（DOI、PMID、arXiv）
3. 从 URL 中提取标识符
4. 查询相应的 API
5. 格式化为 BibTeX

**URL 模式**：
```
# DOI URL
https://doi.org/10.1038/nature12345
https://dx.doi.org/10.1126/science.abc123
https://www.nature.com/articles/s41586-021-03819-2

# PubMed URL
https://pubmed.ncbi.nlm.nih.gov/34265844/
https://www.ncbi.nlm.nih.gov/pubmed/34265844

# arXiv URL
https://arxiv.org/abs/2103.14030
https://arxiv.org/pdf/2103.14030.pdf
```

### 批量处理

**从包含混合标识符的文件**：

```bash
# 创建每行一个标识符的文件
# identifiers.txt:
#   10.1038/nature12345
#   34265844
#   2103.14030
#   https://doi.org/10.1126/science.abc123

python scripts/extract_metadata.py \
  --input identifiers.txt \
  --output references.bib
```

**流程**：
- 脚本自动检测标识符类型
- 查询相应的 API
- 合并为单个 BibTeX 文件
- 优雅处理错误

## 特殊情况与边缘情况

### 后已发表的预印本

**问题**：引用了预印本，但期刊版本现已可用。

**解决方案**：
1. 检查 arXiv 元数据中的 DOI 字段
2. 如有 DOI，使用已发表版本
3. 更新引用为期刊文章
4. 如需要可在注释中注明预印本版本

**示例**：
```bibtex
% 原始：arXiv:2103.14030
% 已发表为：
@article{Jumper2021,
  author  = {Jumper, John and Evans, Richard and others},
  title   = {Highly Accurate Protein Structure Prediction with {AlphaFold}},
  journal = {Nature},
  year    = {2021},
  volume  = {596},
  pages   = {583--589},
  doi     = {10.1038/s41586-021-03819-2}
}
```

### 多位作者（et al.）

**问题**：作者众多（10+ 位）。

**BibTeX 实践**：
- 如少于 10 位则包含所有作者
- 10 位及以上使用"and others"
- 或列出全部（期刊要求不同）

**示例**：
```bibtex
@article{LargeCollaboration2024,
  author = {First, Author and Second, Author and Third, Author and others},
  ...
}
```

### 作者姓名变体

**问题**：作者使用不同的姓名格式发表。

**标准化**：
```
# 常见变体
John Smith
John A. Smith
John Andrew Smith
J. A. Smith
Smith, J.
Smith, J. A.

# BibTeX 格式（推荐）
author = {Smith, John A.}
```

**提取偏好**：
1. 如有全名则使用全名
2. 如有中间名首字母则包含
3. 格式：姓, 名 中间名

### 无可用 DOI

**问题**：较旧的论文或书籍没有 DOI。

**解决方案**：
1. 如有则使用 PMID（生物医学）
2. 书籍使用 ISBN
3. 使用稳定来源的 URL
4. 包含完整的出版详情

**示例**：
```bibtex
@article{OldPaper1995,
  author  = {Author, Name},
  title   = {Title Here},
  journal = {Journal Name},
  year    = {1995},
  volume  = {123},
  pages   = {45--67},
  url     = {https://stable-url-here},
  note    = {PMID: 12345678}
}
```

### 会议论文与期刊文章

**问题**：同一作品在两者中都有发表。

**最佳实践**：
- 如两者都可用则引用期刊版本
- 期刊版本更具档案价值
- 会议版本用于时效性

**如引用会议**：
```bibtex
@inproceedings{Smith2024conf,
  author    = {Smith, John},
  title     = {Title},
  booktitle = {Proceedings of NeurIPS 2024},
  year      = {2024}
}
```

**如引用期刊**：
```bibtex
@article{Smith2024journal,
  author  = {Smith, John},
  title   = {Title},
  journal = {Journal of Machine Learning Research},
  year    = {2024}
}
```

### 书籍章节与编辑文集

**正确提取**：
- 章节：使用 `@incollection`
- 整本书：使用 `@book`
- 书籍编辑：列在 `editor` 字段
- 章节作者：列在 `author` 字段

### 数据集和软件

**使用 @misc** 并填充相应字段：

```bibtex
@misc{DatasetName2024,
  author       = {Author, Name},
  title        = {Dataset Title},
  year         = {2024},
  howpublished = {Zenodo},
  doi          = {10.5281/zenodo.123456},
  note         = {Version 1.2}
}
```

## 提取后验证

始终验证提取的元数据：

```bash
python scripts/validate_citations.py extracted_refs.bib
```

**检查**：
- 所有必需字段都已填写
- DOI 能正确解析
- 作者姓名格式一致
- 年份合理（4位数字）
- 期刊/出版商名称正确
- 页码范围使用 -- 而非 -
- 特殊字符处理得当

## 最佳实践

### 1. 优先使用 DOI（如果有）

DOI 提供：
- 永久标识符
- 最佳元数据来源
- 出版商验证的信息
- 可解析的链接

### 2. 验证自动提取的元数据

抽查：
- 作者姓名与出版物匹配
- 标题匹配（包括大小写）
- 年份正确
- 期刊名称完整

### 3. 处理特殊字符

**LaTeX 特殊字符**：
- 保护大小写：{AlphaFold}
- 处理重音：M{"u}ller 或使用 Unicode
- 化学式：H$_2$O 或 \ce{H2O}

### 4. 使用一致的引用键

**约定**：`FirstAuthorYEARkeyword`
```
Smith2024protein
Doe2023machine
Johnson2024cancer
```

### 5. 为现代论文包含 DOI

~2000 年后发表的所有论文都应有 DOI：
```bibtex
doi = {10.1038/nature12345}
```

### 6. 记录来源

对于非标准来源，添加注释：
```bibtex
note = {Preprint, not peer-reviewed}
note = {Technical report}
note = {Dataset accompanying [citation]}
```

## 摘要

元数据提取工作流：

1. **识别**：确定标识符类型（DOI、PMID、arXiv、URL）
2. **查询**：使用相应的 API（CrossRef、PubMed、arXiv）
3. **提取**：解析响应以获取所需字段
4. **格式化**：创建格式正确的 BibTeX 条目
5. **验证**：检查完整性和准确性
6. **核实**：抽查关键引用

**使用脚本**实现自动化：
- `extract_metadata.py`：通用提取器
- `doi_to_bibtex.py`：快速 DOI 转换
- `validate_citations.py`：验证准确性

**在最终提交前始终验证**提取的元数据！
