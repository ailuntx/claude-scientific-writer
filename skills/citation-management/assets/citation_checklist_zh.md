# 引文质量检查清单

在最终提交之前，使用此清单确保你的引文准确、完整且格式正确。

## 提交前检查清单

### ✓ 元数据准确性

- [ ] 所有作者姓名都正确且格式规范
- [ ] 文章标题与实际出版物一致
- [ ] 期刊/会议名称完整（除非有要求，否则不要缩写）
- [ ] 出版年份准确
- [ ] 卷号和期号正确
- [ ] 页码范围准确

### ✓ 必需字段

- [ ] 所有 @article 条目都包含：author、title、journal、year
- [ ] 所有 @book 条目都包含：author/editor、title、publisher、year
- [ ] 所有 @inproceedings 条目都包含：author、title、booktitle、year
- [ ] 现代论文（2000 年及以后）在可用时包含 DOI
- [ ] 所有条目都具有唯一的 citation keys

### ✓ DOI 验证

- [ ] 所有 DOI 都格式正确（10.XXXX/...）
- [ ] DOI 能正确解析到对应文章
- [ ] BibTeX 字段中没有 DOI 前缀（不要使用 "doi:" 或 "https://doi.org/"）
- [ ] 来自 CrossRef 的元数据与你的 BibTeX 条目一致
- [ ] 运行：`python scripts/validate_citations.py references.bib --check-dois`

### ✓ 格式一致性

- [ ] 页码范围使用双连字符（--），不是单连字符 (-)
- [ ] pages 字段中没有 "pp." 前缀
- [ ] 作者姓名使用 "and" 分隔（不要用分号或 &）
- [ ] 标题中的大小写已被保护（{AlphaFold}、{CRISPR} 等）
- [ ] 如果包含月份名称，请使用标准缩写
- [ ] citation keys 遵循一致的格式

### ✓ 重复检测

- [ ] 参考文献中没有重复 DOI
- [ ] 没有重复的 citation keys
- [ ] 没有近似重复的标题
- [ ] 预印本在可用时已更新为已发表版本
- [ ] 运行：`python scripts/validate_citations.py references.bib`

### ✓ 特殊字符

- [ ] 带重音字符格式正确（例如，ü 写作 {\"u}）
- [ ] 数学符号使用 LaTeX 命令
- [ ] 化学式格式正确
- [ ] 没有未转义的特殊字符（%、&、$、# 等）

### ✓ BibTeX 语法

- [ ] 所有条目的花括号 {} 配对平衡
- [ ] 字段之间用逗号分隔
- [ ] 每个条目的最后一个字段后没有逗号
- [ ] 条目类型有效（@article、@book 等）
- [ ] 运行：`python scripts/validate_citations.py references.bib`

### ✓ 文件组织

- [ ] 参考文献按合理顺序排序（按年份、作者或键）
- [ ] 全文格式一致
- [ ] 条目之间没有格式不一致
- [ ] 运行：`python scripts/format_bibtex.py references.bib --sort year`

## 自动化验证

### 第 1 步：格式化并清理

```bash
python scripts/format_bibtex.py references.bib \
  --deduplicate \
  --sort year \
  --descending \
  --output clean_references.bib
```

**此操作会做什么**：
- 删除重复项
- 标准化格式
- 修复常见问题（页码范围、DOI 格式等）
- 按年份排序（最新在前）

### 第 2 步：验证

```bash
python scripts/validate_citations.py clean_references.bib \
  --check-dois \
  --report validation_report.json \
  --verbose
```

**此操作会做什么**：
- 检查必需字段
- 验证 DOI 是否可解析
- 检测重复项
- 验证语法
- 生成详细报告

### 第 3 步：查看报告

```bash
cat validation_report.json
```

**需要处理任何**：
- **错误**：必须修复（缺失字段、损坏的 DOI、语法错误）
- **警告**：应当修复（缺失推荐字段、格式问题）
- **重复项**：删除或合并

### 第 4 步：最终检查

```bash
python scripts/validate_citations.py clean_references.bib --verbose
```

**目标**：零错误，尽量少的警告

## 人工审查清单

### 关键引文（最重要的前 10-20 条）

对于最重要的引文，请手动核对：

- [ ] 打开 DOI 链接并确认它是正确的文章
- [ ] 将作者姓名与实际出版物对照检查
- [ ] 验证年份与发表日期一致
- [ ] 确认期刊/会议名称正确
- [ ] 检查卷号/页码是否匹配

### 需要注意的常见问题

**缺失信息**：
- [ ] 2000 年后发表的论文没有 DOI
- [ ] 期刊文章缺少卷号或页码
- [ ] 图书缺少出版社
- [ ] 会议论文集缺少会议地点

**格式错误**：
- [ ] 页码范围使用单连字符（123-145 → 123--145）
- [ ] 作者列表中使用 &（Smith & Jones → Smith and Jones）
- [ ] 标题中的缩写未受保护（DNA → {DNA}）
- [ ] DOI 包含 URL 前缀（https://doi.org/10.xxx → 10.xxx）

**元数据不匹配**：
- [ ] 作者姓名与出版物不一致
- [ ] 年份是在线首发时间而不是印刷出版时间
- [ ] 期刊名被缩写而本应使用全称
- [ ] 卷号/期号被颠倒

**重复项**：
- [ ] 同一论文使用不同 citation keys 引用
- [ ] 同时引用了预印本和已发表版本
- [ ] 同时引用了会议论文和期刊版本

## 按领域的检查

### 生物医学科学

- [ ] 如可用，包含 PubMed Central ID（PMCID）
- [ ] 使用时 MeSH 术语恰当
- [ ] 如适用，包含临床试验注册号
- [ ] 与治疗/药物相关的所有参考都已准确引用

### 计算机科学

- [ ] 预印本包含 arXiv ID
- [ ] 会议论文集引用完整（不只是 "NeurIPS"）
- [ ] 软件/数据集引用包含版本号
- [ ] GitHub 链接稳定且永久

### 一般科学

- [ ] 数据可用性声明已正确引用
- [ ] 已识别并移除撤稿论文
- [ ] 检查预印本是否已有发表版本
- [ ] 如有关键内容，引用补充材料

## 最终提交前步骤

### 提交前 1 周

- [ ] 运行包含 DOI 检查的完整验证
- [ ] 修复所有错误和关键警告
- [ ] 手动核对前 10-20 条最重要的引文
- [ ] 检查是否存在任何撤稿论文

### 提交前 3 天

- [ ] 在任何手动编辑后重新运行验证
- [ ] 确保所有文内引文都有对应的参考文献条目
- [ ] 确保所有参考文献条目都在正文中被引用
- [ ] 检查 citation style 是否符合期刊要求

### 提交前 1 天

- [ ] 最终验证检查
- [ ] LaTeX 编译成功且无警告
- [ ] PDF 中所有引文显示正确
- [ ] 参考文献格式正确
- [ ] 没有占位引文（Smith et al. XXXX）

### 提交当天

- [ ] 最后一次验证运行
- [ ] 未经重新验证不要进行临时修改
- [ ] 参考文献文件已包含在提交包中
- [ ] 文中提到的图/表与参考文献一致

## 质量指标

### 优秀的参考文献

- ✓ 100% 的条目都有 DOI（针对现代论文）
- ✓ 零验证错误
- ✓ 零缺失必需字段
- ✓ 零损坏 DOI
- ✓ 零重复项
- ✓ 全文格式一致
- ✓ 所有引文都已人工抽查

### 可接受的参考文献

- ✓ 90%+ 的现代条目有 DOI
- ✓ 零高严重性错误
- ✓ 仅有轻微警告（例如缺失推荐字段）
- ✓ 关键引文已人工核对
- ✓ 编译无错误

### 需要改进

- ✗ 近期论文缺少 DOI
- ✗ 高严重性验证错误
- ✗ 损坏或错误的 DOI
- ✗ 重复条目
- ✗ 格式不一致
- ✗ 编译警告或错误

## 紧急修复

如果你在最后一刻发现问题：

### 损坏的 DOI

```bash
# 查找正确的 DOI
# 选项 1：在 CrossRef 搜索
# https://www.crossref.org/

# 选项 2：在出版社网站搜索
# 选项 3：Google Scholar

# 重新提取元数据
python scripts/extract_metadata.py --doi CORRECT_DOI
```

### 缺失信息

```bash
# 从 DOI 提取
python scripts/extract_metadata.py --doi 10.xxxx/yyyy

# 或从 PMID 提取（生物医学）
python scripts/extract_metadata.py --pmid 12345678

# 或从 arXiv 提取
python scripts/extract_metadata.py --arxiv 2103.12345
```

### 重复条目

```bash
# 自动删除重复项
python scripts/format_bibtex.py references.bib \
  --deduplicate \
  --output fixed_references.bib
```

### 格式错误

```bash
# 自动修复常见问题
python scripts/format_bibtex.py references.bib \
  --output fixed_references.bib

# 然后验证
python scripts/validate_citations.py fixed_references.bib
```

## 长期最佳实践

### 在研究期间

- [ ] 在找到引文后立即将其添加到参考文献文件中
- [ ] 使用 DOI 立即提取元数据
- [ ] 每添加 10-20 条后进行验证
- [ ] 将参考文献文件纳入版本控制

### 在写作期间

- [ ] 边写边引用
- [ ] 使用一致的 citation keys
- [ ] 不要拖延添加参考文献
- [ ] 每周验证一次

### 提交前

- [ ] 预留 2-3 天用于引文清理
- [ ] 不要等到最后一天
- [ ] 尽可能自动化
- [ ] 手动核对关键引文

## 工具速查

### 提取元数据

```bash
# 从 DOI
python scripts/doi_to_bibtex.py 10.1038/nature12345

# 从多个来源
python scripts/extract_metadata.py \
  --doi 10.1038/nature12345 \
  --pmid 12345678 \
  --arxiv 2103.12345 \
  --output references.bib
```

### 验证

```bash
# 基本验证
python scripts/validate_citations.py references.bib

# 带 DOI 检查（较慢但更全面）
python scripts/validate_citations.py references.bib --check-dois

# 生成报告
python scripts/validate_citations.py references.bib \
  --report validation.json \
  --verbose
```

### 格式化并清理

```bash
# 格式化并修复问题
python scripts/format_bibtex.py references.bib

# 删除重复项并排序
python scripts/format_bibtex.py references.bib \
  --deduplicate \
  --sort year \
  --descending \
  --output clean_refs.bib
```

## 总结

**最低要求**：
1. 运行 `format_bibtex.py --deduplicate`
2. 运行 `validate_citations.py`
3. 修复所有错误
4. 成功编译

**推荐做法**：
1. 格式化、去重并排序
2. 使用 `--check-dois` 验证
3. 修复所有错误和警告
4. 手动核对最重要的引文
5. 修复后重新验证

**最佳实践**：
1. 在整个研究过程中持续验证
2. 持续使用自动化工具
3. 保持参考文献整洁有序
4. 记录任何特殊情况
5. 在提交前 1-3 天进行最终验证

**记住**：引文错误会对你的学术工作造成负面影响。花时间确保准确性是值得的！
