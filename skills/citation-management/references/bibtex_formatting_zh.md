# BibTeX 格式指南

关于 BibTeX 条目类型、必填字段、格式约定和最佳实践的综合指南。

## 概述

BibTeX 是 LaTeX 文档的标准参考文献格式。正确的格式化可确保：
- 正确的引用显示
- 一致的格式
- 与引用样式兼容
- 无编译错误

本指南涵盖所有常见条目类型和格式规则。

## 条目类型

### @article - 期刊文章

**最常见的条目类型**，用于同行评审的期刊文章。

**必填字段**：
- `author`：作者姓名
- `title`：文章标题
- `journal`：期刊名称
- `year`：发表年份

**可选字段**：
- `volume`：卷号
- `number`：期号
- `pages`：页码范围
- `month`：发表月份
- `doi`：数字对象标识符
- `url`：URL
- `note`：附加说明

**模板**：
```bibtex
@article{CitationKey2024,
  author  = {Last1, First1 and Last2, First2},
  title   = {Article Title Here},
  journal = {Journal Name},
  year    = {2024},
  volume  = {10},
  number  = {3},
  pages   = {123--145},
  doi     = {10.1234/journal.2024.123456},
  month   = jan
}
```

**示例**：
```bibtex
@article{Jumper2021,
  author  = {Jumper, John and Evans, Richard and Pritzel, Alexander and others},
  title   = {Highly Accurate Protein Structure Prediction with {AlphaFold}},
  journal = {Nature},
  year    = {2021},
  volume  = {596},
  number  = {7873},
  pages   = {583--589},
  doi     = {10.1038/s41586-021-03819-2}
}
```

### @book - 图书

**用于整本书**。

**必填字段**：
- `author` 或 `editor`：作者或编辑
- `title`：书名
- `publisher`：出版社名称
- `year`：出版年份

**可选字段**：
- `volume`：卷号（多卷本时）
- `series`：丛书名
- `address`：出版社所在地
- `edition`：版次
- `isbn`：ISBN
- `url`：URL

**模板**：
```bibtex
@book{CitationKey2024,
  author    = {Last, First},
  title     = {Book Title},
  publisher = {Publisher Name},
  year      = {2024},
  edition   = {3},
  address   = {City, Country},
  isbn      = {978-0-123-45678-9}
}
```

**示例**：
```bibtex
@book{Kumar2021,
  author    = {Kumar, Vinay and Abbas, Abul K. and Aster, Jon C.},
  title     = {Robbins and Cotran Pathologic Basis of Disease},
  publisher = {Elsevier},
  year      = {2021},
  edition   = {10},
  address   = {Philadelphia, PA},
  isbn      = {978-0-323-53113-9}
}
```

### @inproceedings - 会议论文

**用于会议论文集中的论文**。

**必填字段**：
- `author`：作者姓名
- `title`：论文标题
- `booktitle`：会议/论文集名称
- `year`：年份

**可选字段**：
- `editor`：论文集编辑
- `volume`：卷号
- `series`：丛书名
- `pages`：页码范围
- `address`：会议地点
- `month`：会议月份
- `organization`：主办机构
- `publisher`：出版社
- `doi`：DOI

**模板**：
```bibtex
@inproceedings{CitationKey2024,
  author    = {Last, First},
  title     = {Paper Title},
  booktitle = {Proceedings of Conference Name},
  year      = {2024},
  pages     = {123--145},
  address   = {City, Country},
  month     = jun
}
```

**示例**：
```bibtex
@inproceedings{Vaswani2017,
  author    = {Vaswani, Ashish and Shazeer, Noam and Parmar, Niki and others},
  title     = {Attention is All You Need},
  booktitle = {Advances in Neural Information Processing Systems 30 (NeurIPS 2017)},
  year      = {2017},
  pages     = {5998--6008},
  address   = {Long Beach, CA}
}
```

**注**：`@conference` 是 `@inproceedings` 的别名。

### @incollection - 书籍章节

**用于编著书中的章节**。

**必填字段**：
- `author`：章节作者
- `title`：章节标题
- `booktitle`：书名
- `publisher`：出版社名称
- `year`：出版年份

**可选字段**：
- `editor`：书籍编辑
- `volume`：卷号
- `series`：丛书名
- `type`：章节类型（例如“chapter”）
- `chapter`：章节号
- `pages`：页码范围
- `address`：出版社所在地
- `edition`：版次
- `month`：月份

**模板**：
```bibtex
@incollection{CitationKey2024,
  author    = {Last, First},
  title     = {Chapter Title},
  booktitle = {Book Title},
  editor    = {Editor, Last and Editor2, Last},
  publisher = {Publisher Name},
  year      = {2024},
  pages     = {123--145},
  chapter   = {5}
}
```

**示例**：
```bibtex
@incollection{Brown2020,
  author    = {Brown, Peter O. and Botstein, David},
  title     = {Exploring the New World of the Genome with {DNA} Microarrays},
  booktitle = {DNA Microarrays: A Molecular Cloning Manual},
  editor    = {Eisen, Michael B. and Brown, Patrick O.},
  publisher = {Cold Spring Harbor Laboratory Press},
  year      = {2020},
  pages     = {1--45},
  address   = {Cold Spring Harbor, NY}
}
```

### @phdthesis - 博士论文

**用于博士论文和学位论文**。

**必填字段**：
- `author`：作者姓名
- `title`：论文标题
- `school`：机构
- `year`：年份

**可选字段**：
- `type`：类型（例如“PhD dissertation”，“PhD thesis”）
- `address`：机构所在地
- `month`：月份
- `url`：URL
- `note`：附加说明

**模板**：
```bibtex
@phdthesis{CitationKey2024,
  author = {Last, First},
  title  = {Dissertation Title},
  school = {University Name},
  year   = {2024},
  type   = {{PhD} dissertation},
  address = {City, State}
}
```

**示例**：
```bibtex
@phdthesis{Johnson2023,
  author  = {Johnson, Mary L.},
  title   = {Novel Approaches to Cancer Immunotherapy Using {CRISPR} Technology},
  school  = {Stanford University},
  year    = {2023},
  type    = {{PhD} dissertation},
  address = {Stanford, CA}
}
```

**注**：`@mastersthesis` 类似，但用于硕士论文。

### @mastersthesis - 硕士论文

**用于硕士论文**。

**必填字段**：
- `author`：作者姓名
- `title`：论文标题
- `school`：机构
- `year`：年份

**模板**：
```bibtex
@mastersthesis{CitationKey2024,
  author = {Last, First},
  title  = {Thesis Title},
  school = {University Name},
  year   = {2024}
}
```

### @misc - 其他

**用于不属于其他类别的条目**（预印本、数据集、软件、网站等）。

**必填字段**：
- `author`（如果已知）
- `title`
- `year`

**可选字段**：
- `howpublished`：仓库、网站、格式
- `url`：URL
- `doi`：DOI
- `note`：附加信息
- `month`：月份

**预印本模板**：
```bibtex
@misc{CitationKey2024,
  author       = {Last, First},
  title        = {Preprint Title},
  year         = {2024},
  howpublished = {bioRxiv},
  doi          = {10.1101/2024.01.01.123456},
  note         = {Preprint}
}
```

**数据集模板**：
```bibtex
@misc{DatasetName2024,
  author       = {Last, First},
  title        = {Dataset Title},
  year         = {2024},
  howpublished = {Zenodo},
  doi          = {10.5281/zenodo.123456},
  note         = {Version 1.2}
}
```

**软件模板**：
```bibtex
@misc{SoftwareName2024,
  author       = {Last, First},
  title        = {Software Name},
  year         = {2024},
  howpublished = {GitHub},
  url          = {https://github.com/user/repo},
  note         = {Version 2.0}
}
```

### @techreport - 技术报告

**用于技术报告**。

**必填字段**：
- `author`：作者姓名
- `title`：报告标题
- `institution`：机构
- `year`：年份

**可选字段**：
- `type`：报告类型
- `number`：报告编号
- `address`：机构所在地
- `month`：月份

**模板**：
```bibtex
@techreport{CitationKey2024,
  author      = {Last, First},
  title       = {Report Title},
  institution = {Institution Name},
  year        = {2024},
  type        = {Technical Report},
  number      = {TR-2024-01}
}
```

### @unpublished - 未发表作品

**用于未发表作品**（不是预印本——预印本请使用 @misc）。

**必填字段**：
- `author`：作者姓名
- `title`：作品标题
- `note`：描述

**可选字段**：
- `month`：月份
- `year`：年份

**模板**：
```bibtex
@unpublished{CitationKey2024,
  author = {Last, First},
  title  = {Work Title},
  note   = {Unpublished manuscript},
  year   = {2024}
}
```

### @online/@electronic - 在线资源

**用于网页和仅在线内容**。

**注**：这不是标准 BibTeX，但许多文献包（biblatex）都支持。

**必填字段**：
- `author` 或 `organization`
- `title`
- `url`
- `year`

**模板**：
```bibtex
@online{CitationKey2024,
  author = {{Organization Name}},
  title  = {Page Title},
  url    = {https://example.com/page},
  year   = {2024},
  note   = {Accessed: 2024-01-15}
}
```

## 格式规则

### 引用键

**约定**：`FirstAuthorYEARkeyword`

**示例**：
```bibtex
Smith2024protein
Doe2023machine
JohnsonWilliams2024cancer  % Multiple authors, no space
NatureEditorial2024        % No author, use publication
WHO2024guidelines          % Organization author
```

**规则**：
- 仅使用字母数字加：`-`、`_`、`.`、`:`
- 不要有空格
- 区分大小写
- 文件内唯一
- 具有描述性

**避免**：
- 特殊字符：`@`、`#`、`&`、`%`、`$`
- 空格：使用 CamelCase 或下划线
- 以数字开头：`2024Smith`（某些系统不允许）

### 作者姓名

**推荐格式**：`Last, First Middle`

**单个作者**：
```bibtex
author = {Smith, John}
author = {Smith, John A.}
author = {Smith, John Andrew}
```

**多个作者** - 用 `and` 分隔：
```bibtex
author = {Smith, John and Doe, Jane}
author = {Smith, John A. and Doe, Jane M. and Johnson, Mary L.}
```

**多个作者**（10 个以上）：
```bibtex
author = {Smith, John and Doe, Jane and Johnson, Mary and others}
```

**特殊情况**：
```bibtex
% 后缀（Jr., III 等）
author = {King, Jr., Martin Luther}

% 机构作为作者
author = {{World Health Organization}}
% 注：双层花括号将其视为单一实体

% 多重姓氏
author = {Garc{\'i}a-Mart{\'i}nez, Jos{\'e}}

% 姓氏前缀（van, von, de, 等）
author = {van der Waals, Johannes}
author = {de Broglie, Louis}
```

**错误格式**（不要使用）：
```bibtex
author = {Smith, J.; Doe, J.}  % Semicolons (wrong)
author = {Smith, J., Doe, J.}  % Commas (wrong)
author = {Smith, J. & Doe, J.} % Ampersand (wrong)
author = {Smith J}             % No comma
```

### 标题大小写

**使用花括号保护大小写**：

```bibtex
% 专有名词、缩写、公式
title = {{AlphaFold}: Protein Structure Prediction}
title = {Machine Learning for {DNA} Sequencing}
title = {The {Ising} Model in Statistical Physics}
title = {{CRISPR-Cas9} Gene Editing Technology}
```

**原因**：引用样式可能会更改大小写。花括号可保护其不被修改。

**示例**：
```bibtex
% Good
title = {Advances in {COVID-19} Treatment}
title = {Using {Python} for Data Analysis}
title = {The {AlphaFold} Protein Structure Database}

% Will be lowercase in title case styles
title = {Advances in COVID-19 Treatment}  % covid-19
title = {Using Python for Data Analysis}  % python
```

**整个标题保护**（很少需要）：
```bibtex
title = {{This Entire Title Keeps Its Capitalization}}
```

### 页码范围

**使用 en-dash**（双连字符 `--`）：

```bibtex
pages = {123--145}     % 正确
pages = {1234--1256}   % 正确
pages = {e0123456}     % Article ID (PLOS, etc.)
pages = {123}          % 单页
```

**错误**：
```bibtex
pages = {123-145}      % 单连字符（不要使用）
pages = {pp. 123-145}  % 不需要 "pp."
pages = {123–145}      % Unicode en-dash（可能导致问题）
```

### 月份名称

**使用三字母缩写**（不加引号）：

```bibtex
month = jan
month = feb
month = mar
month = apr
month = may
month = jun
month = jul
month = aug
month = sep
month = oct
month = nov
month = dec
```

**或使用数字**：
```bibtex
month = {1}   % 一月
month = {12}  % 十二月
```

**或使用花括号中的全称**：
```bibtex
month = {January}
```

标准缩写无需引号即可使用，因为它们已在 BibTeX 中定义。

### 期刊名称

**使用全称**（不要缩写）：

```bibtex
journal = {Nature}
journal = {Science}
journal = {Cell}
journal = {Proceedings of the National Academy of Sciences}
journal = {Journal of the American Chemical Society}
```

**如有需要，参考文献样式会处理缩写。**

**避免手动缩写**：
```bibtex
% Don't do this in BibTeX file
journal = {Proc. Natl. Acad. Sci. U.S.A.}

% Do this instead
journal = {Proceedings of the National Academy of Sciences}
```

**例外**：如果样式要求缩写，请使用完整的缩写形式：
```bibtex
journal = {Proc. Natl. Acad. Sci. U.S.A.}  % If required by style
```

### DOI 格式

**URL 格式**（推荐）：

```bibtex
doi = {10.1038/s41586-021-03819-2}
```

**不要**：
```bibtex
doi = {https://doi.org/10.1038/s41586-021-03819-2}  % 不要包含 URL
doi = {doi:10.1038/s41586-021-03819-2}              % 不要包含前缀
```

**LaTeX** 会自动将其格式化为 URL。

**注**：DOI 字段后不要加句点！

### URL 格式

```bibtex
url = {https://www.example.com/article}
```

**在以下情况下使用**：
- DOI 不可用时
- 网页
- 补充材料

**不要重复**：
```bibtex
% Don't include both if DOI URL is same as url
doi = {10.1038/nature12345}
url = {https://doi.org/10.1038/nature12345}  % Redundant!
```

### 特殊字符

**重音符号和变音符**：
```bibtex
author = {M{\"u}ller, Hans}        % ü
author = {Garc{\'i}a, Jos{\'e}}    % í, é
author = {Erd{\H{o}}s, Paul}       % ő
author = {Schr{\"o}dinger, Erwin}  % ö
```

**或使用 UTF-8**（配合正确的 LaTeX 设置）：
```bibtex
author = {Müller, Hans}
author = {García, José}
```

**数学符号**：
```bibtex
title = {The $\alpha$-helix Structure}
title = {$\beta$-sheet Prediction}
```

**化学式**：
```bibtex
title = {H$_2$O Molecular Dynamics}
% 或使用 chemformula 宏包：
title = {\ce{H2O} Molecular Dynamics}
```

### 字段顺序

**推荐顺序**（便于阅读）：

```bibtex
@article{Key,
  author  = {},
  title   = {},
  journal = {},
  year    = {},
  volume  = {},
  number  = {},
  pages   = {},
  doi     = {},
  url     = {},
  note    = {}
}
```

**规则**：
- 最重要的字段放前面
- 条目之间保持一致
- 使用格式化工具标准化

## 最佳实践

### 1. 保持格式一致

全篇使用相同格式：
- 作者姓名格式
- 标题大小写
- 期刊名称
- 引用键风格

### 2. 必填字段

始终包含：
- 对应条目类型的所有必填字段
- 现代论文（2000 年以后）的 DOI
- 文章的卷号和页码
- 图书的出版社

### 3. 保护大小写

对以下内容使用花括号：
- 专有名词：`{AlphaFold}`
- 缩写：`{DNA}`、`{CRISPR}`
- 公式：`{H2O}`
- 名称：`{Python}`、`{R}`

### 4. 完整作者列表

尽可能包含所有作者：
- 少于 10 位作者时列出全部
- 10 位以上使用 "and others"
- 不要手动缩写为 "et al."

### 5. 使用标准条目类型

选择正确的条目类型：
- 期刊文章 → `@article`
- 图书 → `@book`
- 会议论文 → `@inproceedings`
- 预印本 → `@misc`

### 6. 验证语法

检查：
- 花括号是否配对
- 字段后是否有逗号
- 引用键是否唯一
- 条目类型是否有效

### 7. 使用格式化工具

使用自动化工具：
```bash
python scripts/format_bibtex.py references.bib
```

优点：
- 格式一致
- 捕获语法错误
- 标准化字段顺序
- 修正常见问题

## 常见错误

### 1. 作者分隔符错误

**错误**：
```bibtex
author = {Smith, J.; Doe, J.}    % 分号
author = {Smith, J., Doe, J.}    % 逗号
author = {Smith, J. & Doe, J.}   % 与号
```

**正确**：
```bibtex
author = {Smith, John and Doe, Jane}
```

### 2. 缺少逗号

**错误**：
```bibtex
@article{Smith2024,
  author = {Smith, John}    % 缺少逗号！
  title = {Title}
}
```

**正确**：
```bibtex
@article{Smith2024,
  author = {Smith, John},   % 每个字段后加逗号
  title = {Title}
}
```

### 3. 未保护的大小写

**错误**：
```bibtex
title = {Machine Learning with Python}
% "Python" will become "python" in title case
```

**正确**：
```bibtex
title = {Machine Learning with {Python}}
```

### 4. 页码中使用单连字符

**错误**：
```bibtex
pages = {123-145}   % 单连字符
```

**正确**：
```bibtex
pages = {123--145}  % 双连字符（en-dash）
```

### 5. 页码中多余的 "pp."

**错误**：
```bibtex
pages = {pp. 123--145}
```

**正确**：
```bibtex
pages = {123--145}
```

### 6. 带 URL 前缀的 DOI

**错误**：
```bibtex
doi = {https://doi.org/10.1038/nature12345}
doi = {doi:10.1038/nature12345}
```

**正确**：
```bibtex
doi = {10.1038/nature12345}
```

## 完整参考文献示例

```bibtex
% 期刊文章
@article{Jumper2021,
  author  = {Jumper, John and Evans, Richard and Pritzel, Alexander and others},
  title   = {Highly Accurate Protein Structure Prediction with {AlphaFold}},
  journal = {Nature},
  year    = {2021},
  volume  = {596},
  number  = {7873},
  pages   = {583--589},
  doi     = {10.1038/s41586-021-03819-2}
}

% 图书
@book{Kumar2021,
  author    = {Kumar, Vinay and Abbas, Abul K. and Aster, Jon C.},
  title     = {Robbins and Cotran Pathologic Basis of Disease},
  publisher = {Elsevier},
  year      = {2021},
  edition   = {10},
  address   = {Philadelphia, PA},
  isbn      = {978-0-323-53113-9}
}

% 会议论文
@inproceedings{Vaswani2017,
  author    = {Vaswani, Ashish and Shazeer, Noam and Parmar, Niki and others},
  title     = {Attention is All You Need},
  booktitle = {Advances in Neural Information Processing Systems 30 (NeurIPS 2017)},
  year      = {2017},
  pages     = {5998--6008}
}

% 书籍章节
@incollection{Brown2020,
  author    = {Brown, Peter O. and Botstein, David},
  title     = {Exploring the New World of the Genome with {DNA} Microarrays},
  booktitle = {DNA Microarrays: A Molecular Cloning Manual},
  editor    = {Eisen, Michael B. and Brown, Patrick O.},
  publisher = {Cold Spring Harbor Laboratory Press},
  year      = {2020},
  pages     = {1--45}
}

% 博士论文
@phdthesis{Johnson2023,
  author  = {Johnson, Mary L.},
  title   = {Novel Approaches to Cancer Immunotherapy},
  school  = {Stanford University},
  year    = {2023},
  type    = {{PhD} dissertation}
}

% 预印本
@misc{Zhang2024,
  author       = {Zhang, Yi and Chen, Li and Wang, Hui},
  title        = {Novel Therapeutic Targets in {Alzheimer}'s Disease},
  year         = {2024},
  howpublished = {bioRxiv},
  doi          = {10.1101/2024.01.001},
  note         = {Preprint}
}

% 数据集
@misc{AlphaFoldDB2021,
  author       = {{DeepMind} and {EMBL-EBI}},
  title        = {{AlphaFold} Protein Structure Database},
  year         = {2021},
  howpublished = {Database},
  url          = {https://alphafold.ebi.ac.uk/},
  doi          = {10.1093/nar/gkab1061}
}
```

## 总结

BibTeX 格式化要点：

✓ **选择正确的条目类型**（@article、@book 等）  
✓ **包含所有必填字段**  
✓ **多个作者使用 `and`**  
✓ **使用花括号保护大小写**  
✓ **页码范围使用 `--`**  
✓ **现代论文包含 DOI**  
✓ **编译前验证语法**  

使用格式化工具确保一致性：
```bash
python scripts/format_bibtex.py references.bib
```

格式正确的 BibTeX 可确保在所有参考文献样式中都获得准确、一致的引用！
