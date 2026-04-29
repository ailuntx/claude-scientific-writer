---
name: venue-templates
description: 访问全面的 LaTeX 模板、格式要求和主要科学出版机构（Nature、Science、PLOS、IEEE、ACM）、学术会议（NeurIPS、ICML、CVPR、CHI）、研究海报和资助提案（NSF、NIH、DOE、DARPA）的投稿指南。此技能应在准备期刊投稿、会议论文、研究海报或资助提案并需要特定场馆的格式要求和模板时使用。
allowed-tools: [Read, Write, Edit, Bash]
---

# 场馆模板

## 概述

获取主要科学出版机构、学术会议、研究海报和资助提案的全面 LaTeX 模板、格式要求和投稿指南。本技能提供可直接使用的模板和详细规格，助力跨学科的学术投稿成功。

在准备期刊投稿、会议论文、研究海报或资助提案并需要特定场馆的格式要求和模板时使用此技能。

## 何时使用此技能

此技能应在以下情况下使用：
- 准备投稿到特定期刊的手稿（Nature、Science、PLOS、IEEE 等）
- 撰写具有特定格式要求的会议论文（NeurIPS、ICML、CHI 等）
- 为会议创建学术研究海报
- 起草联邦机构（NSF、NIH、DOE、DARPA）或私人基金会的资助提案
- 检查目标场馆的格式要求和页数限制
- 使用作者信息和项目详细信息自定义模板
- 验证文档是否符合场馆规格

## 使用科学示意图增强视觉效果

**使用此技能创建文档时，请始终考虑添加科学图表和示意图以增强视觉传达。**

如果您的文档尚未包含示意图或图表：
- 使用 **scientific-schematics** 技能生成由 AI 驱动的出版级质量图表
- 只需用自然语言描述您想要的图表
- Nano Banana Pro 将自动生成、审查和改进示意图

**对于新文档：** 默认应生成科学示意图，以直观呈现文本中描述的关键概念、工作流程、架构或关系。

**如何生成示意图：**
```bash
python scripts/generate_schematic.py "您的图表描述" -o figures/output.png
```

AI 将自动：
- 创建具有正确格式的出版级质量图像
- 通过多次迭代审查和改进
- 确保可访问性（色盲友好、高对比度）
- 将输出保存到 figures/ 目录

**何时添加示意图：**
- 论文的方法流程图
- 概念框架图
- 系统架构插图
- 数据流程图
- 实验设计可视化
- 研究工作流程图
- 任何受益于可视化的复杂概念

有关创建示意图的详细指南，请参阅 scientific-schematics 技能文档。

---

## 核心功能

### 1. 期刊文章模板

获取跨学科 50+ 种主要科学期刊的 LaTeX 模板和格式指南：

**Nature 系列**：
- Nature、Nature Methods、Nature Biotechnology、Nature Machine Intelligence
- Nature Communications、Nature Protocols
- Scientific Reports

**Science 系列**：
- Science、Science Advances、Science Translational Medicine
- Science Immunology、Science Robotics

**PLOS（公共科学图书馆）**：
- PLOS ONE、PLOS Biology、PLOS Computational Biology
- PLOS Medicine、PLOS Genetics

**Cell Press**：
- Cell、Neuron、Immunity、Cell Reports
- Molecular Cell、Developmental Cell

**IEEE 出版物**：
- IEEE Transactions（各学科）
- IEEE Access、IEEE Journal 模板

**ACM 出版物**：
- ACM Transactions、Communications of the ACM
- ACM 会议论文集

**其他主要出版社**：
- Springer 期刊（各学科）
- Elsevier 期刊（自定义模板）
- Wiley 期刊
- BMC 期刊
- Frontiers 期刊

### 2. 会议论文模板

具有主要学术会议正确格式的会议专用模板：

**机器学习与人工智能**：
- NeurIPS（神经信息处理系统大会）
- ICML（国际机器学习会议）
- ICLR（国际学习表征会议）
- CVPR（计算机视觉与模式识别）
- AAAI（人工智能促进协会）

**计算机科学**：
- ACM CHI（人机交互）
- SIGKDD（知识发现与数据挖掘）
- EMNLP（自然语言处理经验方法会议）
- SIGIR（信息检索）
- USENIX 会议

**生物与生物信息学**：
- ISMB（分子生物学智能系统）
- RECOMB（计算分子生物学研究）
- PSB（太平洋生物计算研讨会）

**工程**：
- IEEE 会议模板（各学科）
- ASME、AIAA 会议

### 3. 研究海报模板

会议演示的学术海报模板：

**标准格式**：
- A0（841 × 1189 mm / 33.1 × 46.8 in）
- A1（594 × 841 mm / 23.4 × 33.1 in）
- 36" × 48"（914 × 1219 mm）- 常见美国尺寸
- 42" × 56"（1067 × 1422 mm）
- 48" × 36"（横向方向）

**模板包**：
- **beamerposter**：经典学术海报模板
- **tikzposter**：现代彩色海报设计
- **baposter**：结构化多栏布局

**设计特点**：
- 远距离可读性的最佳字体大小
- 配色方案（色盲安全配色）
- 网格布局和栏目结构
- 二维码集成用于补充材料

### 4. 资助提案模板

主要资助机构的模板和格式要求：

**NSF（国家科学基金会）**：
- 完整提案模板（15 页项目描述）
- 项目摘要（1 页：概述、学术价值、更广泛影响）
- 预算和预算说明
- 个人简介（3 页限制）
- 设施、设备和其他资源
- 数据管理计划

**NIH（国立卫生研究院）**：
- R01 研究资助（多年期）
- R21 探索/发展资助
- K 奖项（职业发展）
- 具体目标页（1 页，最关键的部分）
- 研究策略（意义、创新、方法）
- 个人简介（5 页限制）

**DOE（能源部）**：
- 科学办公室提案
- ARPA-E 模板
- 技术就绪等级（TRL）描述
- 商业化和影响部分

**DARPA（国防高级研究计划局）**：
- BAA（广泛机构公告）响应
- Heilmeier 问答框架
- 技术方法和里程碑
- 过渡计划

**私人基金会**：
- 比尔及梅琳达·盖茨基金会
- 惠康信托
- 霍华德·休斯医学研究所（HHMI）
- 陈·扎克伯格倡议（CZI）

## 工作流程：查找和使用模板

### 步骤 1：确定目标场馆

确定具体的出版机构、会议或资助机构：

```
示例查询：
- "我需要投稿到 Nature"
- "NeurIPS 2025 的要求是什么？"
- "给我看看 NSF 提案格式"
- "我要为 ISMB 制作海报"
```

### 步骤 2：查询模板和要求

访问特定场馆的模板和格式指南：

**对于期刊**：
```bash
# 加载期刊格式要求
参考：references/journals_formatting.md
搜索："Nature" 或具体期刊名称

# 检索模板
模板：assets/journals/nature_article.tex
```

**对于会议**：
```bash
# 加载会议格式
参考：references/conferences_formatting.md
搜索："NeurIPS" 或具体会议

# 检索模板
模板：assets/journals/neurips_article.tex
```

**对于海报**：
```bash
# 加载海报指南
参考：references/posters_guidelines.md

# 检索模板
模板：assets/posters/beamerposter_academic.tex
```

**对于资助**：
```bash
# 加载资助要求
参考：references/grants_requirements.md
搜索："NSF" 或具体机构

# 检索模板
模板：assets/grants/nsf_proposal_template.tex
```

### 步骤 3：审查格式要求

在自定义之前检查关键规格：

**需要验证的关键要求**：
- 页数限制（因场馆而异）
- 字体大小和字体族
- 页边距规格
- 行距
- 引用样式（APA、Vancouver、Nature 等）
- 图表要求
- 文件格式（PDF、Word、LaTeX 源文件）
- 匿名化（用于双盲评审）
- 补充材料限制

### 步骤 4：自定义模板

使用辅助脚本或手动自定义：

**选项 1：辅助脚本（推荐）**：
```bash
python scripts/customize_template.py \
  --template assets/journals/nature_article.tex \
  --title "您的论文标题" \
  --authors "第一作者，第二作者" \
  --affiliations "大学名称" \
  --output my_nature_paper.tex
```

**选项 2：手动编辑**：
- 打开模板文件
- 替换占位符文本（用注释标记）
- 填写标题、作者、单位、摘要
- 将您的内容添加到每个部分

### 步骤 5：验证格式

检查是否符合场馆要求：

```bash
python scripts/validate_format.py \
  --file my_paper.pdf \
  --venue "Nature" \
  --check-all
```

**验证检查**：
- 页数在限制内
- 字体大小正确
- 页边距符合规格
- 引用格式正确
- 图表符合分辨率要求

### 步骤 6：编译和审查

编译 LaTeX 并审查输出：

```bash
# 编译 LaTeX
pdflatex my_paper.tex
bibtex my_paper
pdflatex my_paper.tex
pdflatex my_paper.tex

# 或使用 latexmk 自动编译
latexmk -pdf my_paper.tex
```

审查清单：
- [ ] 所有部分都存在且格式正确
- [ ] 引用正确呈现
- [ ] 图表带有正确的标题
- [ ] 页数在限制内
- [ ] 遵循作者指南
- [ ] 已准备好补充材料（如需要）

## 与其他技能的集成

此技能可与其他科学技能无缝协作：

### 科学写作
- 使用 **scientific-writing** 技能获取内容指导（IMRaD 结构、清晰度、精确性）
- 使用本技能的应用特定模板进行格式设置
- 结合使用以完成完整的手稿准备

### 文献综述
- 使用 **literature-review** 技能进行系统文献检索和综合
- 应用场馆要求的适当引用样式
- 根据模板规格格式化参考文献

### 同行评审
- 使用 **peer-review** 技能评估手稿质量
- 使用本技能验证格式合规性
- 确保遵守报告指南（CONSORT、STROBE 等）

### 研究资助
- 与 **research-grants** 技能交叉参考内容策略
- 使用本技能获取机构特定的模板和格式
- 结合使用以进行全面的资助提案准备

### LaTeX 海报
- 此技能提供与场馆无关的海报模板
- 用于会议特定的海报要求
- 与可视化技能集成以创建图表

## 模板分类

### 按文档类型

| 类别 | 模板数量 | 常见场馆 |
|----------|---------------|---------------|
| **期刊文章** | 30+ | Nature、Science、PLOS、IEEE、ACM、Cell Press |
| **会议论文** | 20+ | NeurIPS、ICML、CVPR、CHI、ISMB |
| **研究海报** | 10+ | A0、A1、36×48、各种模板包 |
| **资助提案** | 15+ | NSF、NIH、DARPA、基金会 |

### 按学科

| 学科 | 支持的场馆 |
|------------|------------------|
| **生命科学** | Nature、Cell Press、PLOS、ISMB、RECOMB |
| **物理科学** | Science、Physical Review、ACS、APS |
| **工程** | IEEE、ASME、AIAA、ACM |
| **计算机科学** | ACM、IEEE、NeurIPS、ICML、ICLR |
| **医学** | NEJM、Lancet、JAMA、BMJ |
| **跨学科** | PNAS、Nature Communications、Science Advances |

## 辅助脚本

### query_template.py

按场馆名称、类型或关键词搜索和检索模板：

```bash
# 查找特定期刊的模板
python scripts/query_template.py --venue "Nature" --type "article"

# 按关键词搜索
python scripts/query_template.py --keyword "machine learning"

# 列出所有可用模板
python scripts/query_template.py --list-all

# 获取场馆的要求
python scripts/query_template.py --venue "NeurIPS" --requirements
```

### customize_template.py

使用作者和项目信息自定义模板：

```bash
# 基本自定义
python scripts/customize_template.py \
  --template assets/journals/nature_article.tex \
  --output my_paper.tex

# 包含作者信息
python scripts/customize_template.py \
  --template assets/journals/nature_article.tex \
  --title "蛋白质折叠的新方法" \
  --authors "Jane Doe, John Smith, Alice Johnson" \
  --affiliations "MIT, Stanford, Harvard" \
  --email "[email protected]" \
  --output my_paper.tex

# 交互模式
python scripts/customize_template.py --interactive
```

### validate_format.py

检查文档是否符合场馆要求：

```bash
# 验证编译后的 PDF
python scripts/validate_format.py \
  --file my_paper.pdf \
  --venue "Nature" \
  --check-all

# 检查特定方面
python scripts/validate_format.py \
  --file my_paper.pdf \
  --venue "NeurIPS" \
  --check page-count,margins,fonts

# 生成验证报告
python scripts/validate_format.py \
  --file my_paper.pdf \
  --venue "Science" \
  --report validation_report.txt
```

## 最佳实践

### 模板选择
1. **验证时效性**：检查模板日期并与最新的作者指南比较
2. **检查官方来源**：许多期刊提供官方 LaTeX 类
3. **测试编译**：在添加内容之前先编译模板
4. **阅读注释**：模板包含有用的内联注释

### 自定义
1. **保留结构**：不要删除必需的部分或包
2. **遵循占位符**：系统地替换标记的占位符文本
3. **保持格式**：不要覆盖场馆特定的格式
4. **保留备份**：自定义前保存原始模板

### 合规性
1. **检查页数限制**：最终投稿前验证
2. **验证引用**：使用场馆的正确引用样式
3. **测试图表**：确保图表符合分辨率要求
4. **审查匿名化**：如需要，删除身份信息

### 投稿
1. **遵循说明**：阅读完整的作者指南
2. **包含所有文件**：LaTeX 源文件、图表、参考文献
3. **正确生成**：使用推荐的编译方法
4. **检查输出**：验证 PDF 符合预期

## 常见格式要求

### 页数限制（典型）

| 场馆类型 | 典型限制 | 备注 |
|------------|---------------|-------|
| **Nature 文章** | 5 页 | 约 3000 词，不含参考文献 |
| **Science 报告** | 5 页 | 图表计入限制 |
| **PLOS ONE** | 无限制 | 长度不限 |
| **NeurIPS** | 8 页 | + 无限参考文献/附录 |
| **ICML** | 8 页 | + 无限参考文献/附录 |
| **NSF 提案** | 15 页 | 仅项目描述 |
| **NIH R01** | 12 页 | 研究策略 |

### 按场馆的引用样式

| 场馆 | 引用样式 | 格式 |
|-------|---------------|-------|
| **Nature** | 编号（上标） | Nature 格式 |
| **Science** | 编号（上标） | Science 格式 |
| **PLOS** | 编号（括号） | Vancouver |
| **Cell Press** | 作者-年份 | Cell 格式 |
| **ACM** | 编号 | ACM 格式 |
| **IEEE** | 编号（括号） | IEEE 格式 |
| **APA 期刊** | 作者-年份 | APA 第 7 版 |

### 图表要求

| 场馆 | 分辨率 | 格式 | 颜色 |
|-------|-----------|--------|-------|
| **Nature** | 300+ dpi | TIFF、EPS、PDF | RGB 或 CMYK |
| **Science** | 300+ dpi | TIFF、PDF | RGB |
| **PLOS** | 300-600 dpi | TIFF、EPS | RGB |
| **IEEE** | 300+ dpi | EPS、PDF | RGB 或灰度 |

## 写作风格指南

除了格式之外，本技能还提供全面的**写作风格指南**，捕捉论文在不同场馆的*阅读方式*——不仅仅是它们的外观。

### 为什么风格重要

为 Nature 撰写的同一研究与为 NeurIPS 撰写的内容会有很大不同：
- **Nature/Science**：非专业人员可读，故事驱动，广泛意义
- **Cell Press**：机制深度，全面数据，需要图形摘要
- **医学期刊**：以患者为中心，证据分级，结构化摘要
- **ML 会议**：贡献要点，消融研究，可重复性重点
- **CS 会议**：领域特定约定，评估标准各异

### 可用的风格指南

| 指南 | 涵盖内容 | 关键主题 |
|-------|-----------|------------|
| `venue_writing_styles.md` | 总览 | 风格频谱、快速参考 |
| `nature_science_style.md` | Nature、Science、PNAS | 可访问性、故事讲述、广泛影响 |
| `cell_press_style.md` | Cell、Neuron、Immunity | 图形摘要、eTOC、亮点 |
| `medical_journal_styles.md` | NEJM、Lancet、JAMA、BMJ | 结构化摘要、证据语言 |
| `ml_conference_style.md` | NeurIPS、ICML、ICLR、CVPR | 贡献要点、消融 |
| `cs_conference_style.md` | ACL、EMNLP、CHI、SIGKDD | 领域特定约定 |
| `reviewer_expectations.md` | 所有场馆 | 评审者关注点、反驳技巧 |

### 写作示例

具体示例可在 `assets/examples/` 中找到：
- `nature_abstract_examples.md`：高影响力期刊的流畅段落摘要
- `neurips_introduction_example.md`：带贡献要点的 ML 会议引言
- `cell_summary_example.md`：Cell Press 摘要、亮点、eTOC 格式
- `medical_structured_abstract.md`：NEJM、Lancet、JAMA 结构化格式

### 适应场馆的工作流程

1. **确定目标场馆**并加载相应的风格指南
2. **审查写作约定**：语气、风格、摘要格式、结构
3. **检查示例**以获取部分具体指导
4. **审查预期**：该场馆的评审者优先关注什么？
5. **应用格式**：使用 `assets/` 中的 LaTeX 模板

---

## 资源

### 捆绑资源

**写作风格指南**（位于 `references/`）：
- `venue_writing_styles.md`：总风格概述和比较
- `nature_science_style.md`：Nature/Science 写作约定
- `cell_press_style.md`：Cell Press 期刊风格
- `medical_journal_styles.md`：医学期刊写作指南
- `ml_conference_style.md`：ML 会议写作约定
- `cs_conference_style.md`：CS 会议写作指南
- `reviewer_expectations.md`：各场馆评审者关注点

**格式要求**（位于 `references/`）：
- `journals_formatting.md`：全面的期刊格式要求
- `conferences_formatting.md`：会议论文规格
- `posters_guidelines.md`：研究海报设计和尺寸
- `grants_requirements.md`：各机构的资助提案要求

**写作示例**（位于 `assets/examples/`）：
- `nature_abstract_examples.md`：高影响力期刊摘要示例
- `neurips_introduction_example.md`：ML 会议引言格式
- `cell_summary_example.md`：Cell Press 摘要/亮点/eTOC
- `medical_structured_abstract.md`：NEJM/Lancet/JAMA 摘要格式

**模板**（位于 `assets/`）：
- `journals/`：期刊文章 LaTeX 模板
- `posters/`：研究海报模板
- `grants/`：资助提案模板

**脚本**（位于 `scripts/`）：
- `query_template.py`：搜索和检索模板
- `customize_template.py`：自定义作者信息
- `validate_format.py`：检查要求合规性

### 外部资源

**期刊作者指南**：
- Nature: https://www.nature.com/nature/for-authors
- Science: https://www.science.org/content/page/instructions-authors
- PLOS: https://plos.org/resources/for-authors/
- Cell Press: https://www.cell.com/author-guidelines

**会议格式**：
- NeurIPS: https://neurips.cc/Conferences/2024/CallForPapers
- ICML: https://icml.cc/Conferences/2024/StyleAuthorInstructions
- CVPR: https://cvpr.thecvf.com/Conferences/2024/AuthorGuidelines

**资助资源**：
- NSF PAPPG: https://www.nsf.gov/publications/pub_summ.jsp?ods_key=pappg
- NIH 表单: https://grants.nih.gov/grants/how-to-apply-application-guide.html
- DOE 资助: https://science.osti.gov/grants

## 使用示例

### 示例 1：Nature 文章投稿

```markdown
用户："我需要准备一篇投稿到 Nature 的手稿"

响应：
1. 加载 Nature 格式要求（references/journals_formatting.md）
2. 检索 Nature 模板（assets/journals/nature_article.tex）
3. 关键要求：
   - 长度：约 3000 词，约 5 页
   - 格式：单栏，12pt 字体
   - 引用：编号上标（Nature 风格）
   - 图表：300+ dpi，RGB 颜色
4. 使用您的标题、作者、单位自定义模板
5. 编译并根据要求验证
```

### 示例 2：NeurIPS 会议论文

```markdown
用户："NeurIPS 的格式要求是什么？"

响应：
来自 references/conferences_formatting.md：
- 页数限制：8 页正文 + 无限参考文献/附录
- 格式：双栏，10pt 字体
- 模板：neurips_2024.sty（官方样式文件）
- 匿名化：初始投稿需要
- 引用：编号（括号）
- 图表：高分辨率，建议色盲安全
```

### 示例 3：NSF 提案

```markdown
用户："帮我格式化 NSF 提案"

响应：
NSF 要求（来自 references/grants_requirements.md）：
- 项目描述：最多 15 页
- 项目摘要：1 页（概述、学术价值、更广泛影响）
- 预算说明：3-5 页
- 个人简介：每位高级人员 3 页
- 字体：最小 10pt，Times Roman 或类似
- 页边距：四周 1 英寸
模板：assets/grants/nsf_proposal_template.tex
```

### 示例 4：会议海报

```markdown
用户："我需要为 ISMB 创建海报"

响应：
ISMB 海报规格：
- 尺寸：通常 A0 竖版（33.1 × 46.8 英寸）
- 推荐模板：beamerposter 或 tikzposter
- 字体大小：标题 60-85pt，标题 36-48pt，正文 24-32pt
- 包含：二维码用于论文/补充材料
可用模板：
- assets/posters/beamerposter_academic.tex
- assets/posters/tikzposter_research.tex
```

## 更新和维护

**模板时效性**：
- 模板每年更新或在机构发布新指南时更新
- 最后更新：2024
- 检查官方场馆站点以获取最新要求

**报告问题**：
- 模板编译错误
- 过时的格式要求
- 缺失的场馆模板
- 规格不正确

## 总结

venue-templates 技能提供全面的访问权限：

1. **50+ 个跨学科出版场馆模板**
2. **期刊、会议、海报、资助的详细格式要求**
3. **捕捉每种场馆类型的语气、风格和约定的写作风格指南**
4. **各场馆的摘要、引言和其他部分的具体示例**
5. **评审者预期解释评审者在不同场馆关注的内容**
6. **用于模板发现、自定义和验证的辅助脚本**
7. **与其他科学写作技能的集成**

每当您需要特定场馆的格式指导、写作风格约定或学术出版模板时，请使用此技能。
