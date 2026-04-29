# 引文验证指南

关于在 BibTeX 文件中验证引文准确性、完整性和格式的综合指南。

## 概览

引文验证可确保：
- 所有引文都准确且完整
- DOI 能正确解析
- 必需字段均已提供
- 没有重复条目
- 格式和语法正确
- 链接可访问

应在以下时机进行验证：
- 提取元数据后
- 提交稿件前
- 手动编辑 BibTeX 文件后
- 对维护中的参考文献表进行周期性检查

## 验证类别

### 1. DOI 验证

**目的**：确保 DOI 有效且可正确解析。

#### 需要检查的内容

**DOI 格式**：
```
有效:   10.1038/s41586-021-03819-2
有效:   10.1126/science.aam9317
无效:   10.1038/invalid
无效:   doi:10.1038/...（在 BibTeX 中应省略 "doi:" 前缀）
```

**DOI 解析**：
- DOI 应通过 https://doi.org/ 解析
- 应重定向到实际文章
- 不应返回 404 或错误

**元数据一致性**：
- CrossRef 元数据应与 BibTeX 匹配
- 作者姓名应一致
- 标题应一致
- 年份应一致

#### 如何验证

**手动检查**：
1. 从 BibTeX 中复制 DOI
2. 访问 https://doi.org/10.1038/nature12345
3. 验证其重定向到正确文章
4. 检查元数据是否匹配

**自动检查**（推荐）：
```bash
python scripts/validate_citations.py references.bib --check-dois
```

**流程**：
1. 从 BibTeX 文件中提取所有 DOI
2. 对每个 DOI 查询 doi.org 解析器
3. 查询 CrossRef API 获取元数据
4. 将元数据与 BibTeX 条目进行比较
5. 报告差异

#### 常见问题

**损坏的 DOI**：
- DOI 中有拼写错误
- 出版商更改了 DOI（罕见）
- 文章已撤稿
- 解决方案：从出版商网站查找正确 DOI

**元数据不匹配**：
- BibTeX 中有过时/错误信息
- 解决方案：从 CrossRef 重新提取元数据

**缺失 DOI**：
- 较早的文章可能没有 DOI
- 对 2000 年以前的出版物可接受
- 可改用 URL 或 PMID

### 2. 必需字段

**目的**：确保所有必要信息都已提供。

#### 各条目类型所需字段

**@article**：
```bibtex
author   % 必需
title    % 必需
journal  % 必需
year     % 必需
volume   % 强烈推荐
pages    % 强烈推荐
doi      % 现代论文强烈推荐
```

**@book**：
```bibtex
author OR editor  % 必需（至少一个）
title            % 必需
publisher        % 必需
year             % 必需
isbn             % 推荐
```

**@inproceedings**：
```bibtex
author     % 必需
title      % 必需
booktitle  % 必需（会议/论文集名称）
year       % 必需
pages      % 推荐
```

**@incollection**（书籍章节）：
```bibtex
author     % 必需
title      % 必需（章节标题）
booktitle  % 必需（书名）
publisher  % 必需
year       % 必需
editor     % 推荐
pages      % 推荐
```

**@phdthesis**：
```bibtex
author  % 必需
title   % 必需
school  % 必需
year    % 必需
```

**@misc**（预印本、数据集等）：
```bibtex
author  % 必需
title   % 必需
year    % 必需
howpublished  % 推荐（bioRxiv、Zenodo 等）
doi OR url    % 至少需要一个
```

#### 验证脚本

```bash
python scripts/validate_citations.py references.bib --check-required-fields
```

**输出**：
```
Error: Entry 'Smith2024' missing required field 'journal'
Error: Entry 'Doe2023' missing required field 'year'
Warning: Entry 'Jones2022' missing recommended field 'volume'
```

### 3. 作者姓名格式

**目的**：确保作者姓名格式一致且正确。

#### 正确格式

**推荐的 BibTeX 格式**：
```bibtex
author = {Last1, First1 and Last2, First2 and Last3, First3}
```

**示例**：
```bibtex
% 正确
author = {Smith, John}
author = {Smith, John A.}
author = {Smith, John Andrew}
author = {Smith, John and Doe, Jane}
author = {Smith, John and Doe, Jane and Johnson, Mary}

% 对于很多作者
author = {Smith, John and Doe, Jane and others}

% 错误
author = {John Smith}  % First Last 格式（不推荐）
author = {Smith, J.; Doe, J.}  % 分号分隔（错误）
author = {Smith J, Doe J}  % 缺少逗号
```

#### 特殊情况

**后缀（Jr.、III 等）**：
```bibtex
author = {King, Jr., Martin Luther}
```

**复姓（连字符）**：
```bibtex
author = {Smith-Jones, Mary}
```

**Van、von、de 等**：
```bibtex
author = {van der Waals, Johannes}
author = {de Broglie, Louis}
```

**机构作为作者**：
```bibtex
author = {{World Health Organization}}
% 双重花括号将其视为单个作者
```

#### 验证检查

**自动验证**：
```bash
python scripts/validate_citations.py references.bib --check-authors
```

**检查内容**：
- 正确的分隔符（and，而不是 &、;、, 等）
- 逗号位置
- 空作者字段
- 格式错误的姓名

### 4. 数据一致性

**目的**：确保所有字段都包含有效且合理的值。

#### 年份验证

**有效年份**：
```bibtex
year = {2024}    % 当前/近期
year = {1953}    % Watson & Crick DNA 结构（历史）
year = {1665}    % Hooke 的 Micrographia（非常早）
```

**无效年份**：
```bibtex
year = {24}      % 两位数（有歧义）
year = {202}     % 拼写错误
year = {2025}    % 未来（除非已接受/在线优先发表）
year = {0}       % 明显错误
```

**检查**：
- 四位数字
- 合理范围（1600-当前+1）
- 不能全为 0

#### 卷/期号验证

```bibtex
volume = {123}      % 数值
volume = {12}       % 有效
number = {3}        % 有效
number = {S1}       % 增刊期（有效）
```

**无效**：
```bibtex
volume = {Vol. 123}  % 应仅为数字
number = {Issue 3}   % 应仅为数字
```

#### 页码范围验证

**正确格式**：
```bibtex
pages = {123--145}    % 连字符（两个短横）
pages = {e0123456}    % PLOS 风格文章 ID
pages = {123}         % 单页
```

**错误格式**：
```bibtex
pages = {123-145}     % 单个连字符（应使用 --）
pages = {pp. 123-145} % 去掉 "pp."
pages = {123–145}     % Unicode 长横（可能导致问题）
```

#### URL 验证

**检查**：
- URL 可访问（返回 200 状态）
- 如可用则使用 HTTPS
- 无明显拼写错误
- 使用永久链接（而非临时链接）

**有效**：
```bibtex
url = {https://www.nature.com/articles/nature12345}
url = {https://arxiv.org/abs/2103.14030}
```

**可疑**：
```bibtex
url = {http://...}  % 使用 HTTP 而非 HTTPS
url = {file:///...} % 本地文件路径
url = {bit.ly/...}  % URL 缩短器（非永久）
```

### 5. 重复检测

**目的**：查找并删除重复条目。

#### 重复类型

**完全重复**（相同 DOI）：
```bibtex
@article{Smith2024a,
  doi = {10.1038/nature12345},
  ...
}

@article{Smith2024b,
  doi = {10.1038/nature12345},  % 相同 DOI！
  ...
}
```

**近似重复**（相似标题/作者）：
```bibtex
@article{Smith2024,
  title = {Machine Learning for Drug Discovery},
  ...
}

@article{Smith2024method,
  title = {Machine learning for drug discovery},  % 相同，仅大小写不同
  ...
}
```

**预印本 + 已发表版本**：
```bibtex
@misc{Smith2023arxiv,
  title = {AlphaFold Results},
  howpublished = {arXiv},
  ...
}

@article{Smith2024,
  title = {AlphaFold Results},  % 同一论文，现在已发表
  journal = {Nature},
  ...
}
% 只保留已发表版本
```

#### 检测方法

**按 DOI**（最可靠）：
- 相同 DOI = 完全重复
- 保留一个，删除另一个

**按标题相似度**：
- 规范化：转为小写，去除标点
- 计算相似度（例如 Levenshtein 距离）
- 若相似度 >90% 则标记

**按作者-年份-标题**：
- 第一作者 + 年份 + 相似标题相同
- 很可能是重复

**自动检测**：
```bash
python scripts/validate_citations.py references.bib --check-duplicates
```

**输出**：
```
Warning: Possible duplicate entries:
  - Smith2024a (DOI: 10.1038/nature12345)
  - Smith2024b (DOI: 10.1038/nature12345)
  Recommendation: Keep one entry, remove the other.
```

### 6. 格式与语法

**目的**：确保 BibTeX 语法有效。

#### 常见语法错误

**缺少逗号**：
```bibtex
@article{Smith2024,
  author = {Smith, John}   % 缺少逗号！
  title = {Title}
}
% 应为：
  author = {Smith, John},  % 每个字段后都要有逗号
```

**花括号不匹配**：
```bibtex
title = {Title with {Protected} Text  % 缺少右花括号
% 应为：
title = {Title with {Protected} Text}
```

**条目缺少右花括号**：
```bibtex
@article{Smith2024,
  author = {Smith, John},
  title = {Title}
  % 缺少右花括号！
% 应以以下内容结尾：
}
```

**键中的非法字符**：
```bibtex
@article{Smith&Doe2024,  % 键中不允许 &
  ...
}
% 应使用：
@article{SmithDoe2024,
  ...
}
```

#### BibTeX 语法规则

**条目结构**：
```bibtex
@TYPE{citationkey,
  field1 = {value1},
  field2 = {value2},
  ...
  fieldN = {valueN}
}
```

**引用键**：
- 字母数字及部分标点（-、_、.、:）
- 不含空格
- 区分大小写
- 在文件内唯一

**字段值**：
- 用 {braces} 或 "quotes" 包围
- 复杂文本优先使用 braces
- 数字可不加引号：`year = 2024`

**特殊字符**：
- `{` 和 `}` 用于分组
- `\` 用于 LaTeX 命令
- 保留大小写：`{AlphaFold}`
- 重音：`{\"u}`、`{\'e}`、`{\aa}`

#### 验证

```bash
python scripts/validate_citations.py references.bib --check-syntax
```

**检查**：
- 有效的 BibTeX 结构
- 花括号配对
- 正确的逗号
- 有效的条目类型
- 唯一的引用键

## 验证工作流

### 第 1 步：基础验证

运行全面验证：

```bash
python scripts/validate_citations.py references.bib
```

**检查全部内容**：
- DOI 解析
- 必需字段
- 作者格式
- 数据一致性
- 重复项
- 语法

### 第 2 步：审查报告

查看验证报告：

```json
{
  "total_entries": 150,
  "valid_entries": 140,
  "errors": [
    {
      "entry": "Smith2024",
      "error": "missing_required_field",
      "field": "journal",
      "severity": "high"
    },
    {
      "entry": "Doe2023",
      "error": "invalid_doi",
      "doi": "10.1038/broken",
      "severity": "high"
    }
  ],
  "warnings": [
    {
      "entry": "Jones2022",
      "warning": "missing_recommended_field",
      "field": "volume",
      "severity": "medium"
    }
  ],
  "duplicates": [
    {
      "entries": ["Smith2024a", "Smith2024b"],
      "reason": "same_doi",
      "doi": "10.1038/nature12345"
    }
  ]
}
```

### 第 3 步：修复问题

**高优先级**（错误）：
1. 添加缺失的必需字段
2. 修复损坏的 DOI
3. 删除重复项
4. 更正语法错误

**中优先级**（警告）：
1. 添加推荐字段
2. 改进作者格式
3. 修复页码范围

**低优先级**：
1. 统一格式
2. 添加 URL 以提高可访问性

### 第 4 步：自动修复

使用自动修复进行安全更正：

```bash
python scripts/validate_citations.py references.bib \
  --auto-fix \
  --output fixed_references.bib
```

**自动修复可**：
- 修复页码范围格式（- 改为 --）
- 从 pages 中移除 "pp."
- 统一作者分隔符
- 修复常见语法错误
- 标准化字段顺序

**自动修复不能**：
- 添加缺失信息
- 查找正确 DOI
- 判断保留哪个重复项
- 修复语义错误

### 第 5 步：人工审查

审查自动修复后的文件：
```bash
# 查看发生了什么变化
diff references.bib fixed_references.bib

# 审查出现错误的特定条目
grep -A 10 "Smith2024" fixed_references.bib
```

### 第 6 步：重新验证

修复后再次验证：

```bash
python scripts/validate_citations.py fixed_references.bib --verbose
```

应显示：
```
✓ 所有 DOI 均有效
✓ 所有必需字段均已提供
✓ 未发现重复项
✓ 语法有效
✓ 150/150 条目有效
```

## 验证清单

在最终提交前使用此清单：

### DOI 验证
- [ ] 所有 DOI 都能正确解析
- [ ] BibTeX 与 CrossRef 之间的元数据一致
- [ ] 没有损坏或无效的 DOI

### 完整性
- [ ] 所有条目都包含必需字段
- [ ] 现代论文（2000 年以后）都有 DOI
- [ ] 作者格式正确
- [ ] 期刊/会议名称正确

### 一致性
- [ ] 年份为四位数字
- [ ] 页码范围使用 -- 而不是 -
- [ ] 卷号/期号为数字
- [ ] URL 可访问

### 重复项
- [ ] 没有相同 DOI 的条目
- [ ] 没有近似重复的标题
- [ ] 预印本已更新为已发表版本

### 格式
- [ ] BibTeX 语法有效
- [ ] 花括号配对
- [ ] 逗号正确
- [ ] 引用键唯一

### 最终检查
- [ ] 参考文献表编译无错误
- [ ] 文中所有引文都出现在参考文献表中
- [ ] 参考文献表中的所有条目都被文中引用
- [ ] 引文样式符合期刊要求

## 最佳实践

### 1. 尽早且经常验证

```bash
# 提取后
python scripts/extract_metadata.py --doi ... --output refs.bib
python scripts/validate_citations.py refs.bib

# 手动编辑后
python scripts/validate_citations.py refs.bib

# 提交前
python scripts/validate_citations.py refs.bib --strict
```

### 2. 使用自动化工具

不要手动验证——使用脚本：
- 更快
- 更全面
- 能发现人类容易忽略的错误
- 可生成报告

### 3. 保留备份

```bash
# 自动修复前
cp references.bib references_backup.bib

# 运行自动修复
python scripts/validate_citations.py references.bib \
  --auto-fix \
  --output references_fixed.bib

# 审查更改
diff references.bib references_fixed.bib

# 如满意，则替换
mv references_fixed.bib references.bib
```

### 4. 先修复高优先级问题

**优先顺序**：
1. 语法错误（会阻止编译）
2. 缺失的必需字段（引文不完整）
3. 损坏的 DOI（链接失效）
4. 重复项（混淆、浪费空间）
5. 缺失的推荐字段
6. 格式不一致

### 5. 记录例外情况

对于无法修复的条目：

```bibtex
@article{Old1950,
  author = {Smith, John},
  title = {Title},
  journal = {Obscure Journal},
  year = {1950},
  volume = {12},
  pages = {34--56},
  note = {2000 年之前的出版物无 DOI 可用}
}
```

### 6. 按期刊要求验证

不同期刊有不同要求：
- 引文样式（编号制、作者-年份制）
- 缩写（期刊名）
- 最大参考文献数量
- 格式（BibTeX、EndNote、手动）

请检查期刊作者指南！

## 常见验证问题

### 问题 1：元数据不匹配

**问题**：BibTeX 显示 2023，CrossRef 显示 2024。

**原因**：
- 先在线发表，后印刷发表
- 勘误/更新
- 提取错误

**解决方案**：
1. 检查实际文章
2. 使用更新/更准确的日期
3. 更新 BibTeX 条目
4. 重新验证

### 问题 2：特殊字符

**问题**：LaTeX 编译在特殊字符处失败。

**原因**：
- 重音字符（é、ü、ñ）
- 化学式（H₂O）
- 数学符号（α、β、±）

**解决方案**：
```bibtex
% 使用 LaTeX 命令
author = {M{\"u}ller, Hans}  % Müller
title = {Study of H\textsubscript{2}O}  % H₂O
% 或使用 UTF-8 并配合合适的 LaTeX 宏包
```

### 问题 3：提取不完整（需要网页搜索）

**问题**：提取的元数据缺少字段（volume、pages、DOI、issue number）。

**原因**：
- 源 API 未提供全部元数据
- 提取错误
- 数据库记录不完整
- 先在线发表，尚未获得最终页码

**解决方案 — 必须使用网页搜索补全缺失项**：

1. **通过扫描 BibTeX 条目识别缺失字段**，查找空缺或缺失的 `volume`、`pages`、`number`、`doi` 字段。

2. **使用网页搜索查找缺失元数据**：
   ```bash
   # 通过作者 + 标题搜索完整引文信息
   python scripts/parallel_web.py search \
     "AUTHOR_NAME PAPER_TITLE JOURNAL volume pages DOI" \
     -o sources/search_YYYYMMDD_HHMMSS_citation_CITATIONKEY.md
   ```

3. **如果 DOI 已知，从 DOI 解析页提取**：
   ```bash
   python scripts/parallel_web.py extract \
     "https://doi.org/DOI_HERE" \
     --objective "extract volume, issue number, page range, publication date" \
     -o sources/extract_YYYYMMDD_HHMMSS_doi_CITATIONKEY.md
   ```

4. **如果 DOI 未知，先搜索它**：
   ```bash
   python scripts/parallel_web.py search \
     "AUTHOR_NAME PAPER_TITLE JOURNAL_NAME DOI" \
     -o sources/search_YYYYMMDD_HHMMSS_find_doi_CITATIONKEY.md
   ```

5. **尝试其他元数据来源**：
   - CrossRef API（通过 DOI）：对 volume/pages 最可靠
   - PubMed（通过 PMID）：适用于生物医学论文
   - Google Scholar：作为难查论文的备选
   - 出版商网站：最后手段

6. **用找到的元数据更新 BibTeX 条目并记录日志**：
   ```
   [HH:MM:SS] METADATA ENRICHED: [CitationKey] - added volume, pages, doi ✅
   ```

7. **如果确实找不到**（罕见），添加 note 字段：
   ```bibtex
   note = {完整页码尚未分配 — 先在线发表}
   ```

**关键**：除非已穷尽所有搜索选项并记录原因，否则不要让 `@article` 条目缺少 `volume`、`pages` 和 `doi`。

### 问题 4：找不到重复项

**问题**：同一篇论文出现两次，但未被检测出来。

**原因**：
- 不同 DOI（应较少见）
- 不同标题（缩写、拼写错误）
- 不同引用键

**解决方案**：
- 手动按作者 + 年份搜索
- 检查相似标题
- 手动删除

## 总结

验证可确保引文质量：

✓ **准确性**：DOI 可解析，元数据正确  
✓ **完整性**：所有必需字段均已提供  
✓ **一致性**：全篇格式正确  
✓ **无重复**：每篇论文只引用一次  
✓ **语法有效**：BibTeX 可无错误编译  

**在最终提交前务必验证！**

使用自动化工具：
```bash
python scripts/validate_citations.py references.bib
```

遵循工作流：
1. 提取元数据
2. 验证
3. 修复错误
4. 重新验证
5. 提交
