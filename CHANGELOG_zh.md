# 更新日志

科学写作项目（Scientific Writer）的所有重要变更都将记录在此文件中。

## [未发布]

---

## [2.13.0] - 2026-04-20

### 🚀 改进

- **pptx-posters**：修复了技能名称元数据，明确说明 PPTX 仅为可选加入（latex-posters 是所有研究海报的默认选项），新增 AI 视觉工作流，目标是覆盖 60-70% 的视觉区域
- **latex-posters**：添加了内容溢出预防指南——A0 最多 5-6 个章节，安全边距设置，0.85\linewidth 图形限制，300-800 字字数限制，强制要求编译检查步骤以发现溢出警告
- **parallel-web**：全面重写为统一路由技能，具备 4 个功能（网页搜索、网页提取、数据丰富、深度研究）；路由表；内置学术来源优先级；4 个新参考文件（web-search.md、web-extract.md、data-enrichment.md、deep-research.md）
- **research-lookup**：将 Perplexity/OpenRouter 后端替换为 `parallel-cli search` 作为主后端；学术查询现在使用双搜索模式及 `--include-domains` 来获取学术来源；Parallel Chat API 仅保留用于明确的深度研究；移除了所有 OPENROUTER_API_KEY 依赖
- **scientific-slides**：新增 PPT 工作流及 `--visual-only` 标志，用于生成嵌入到 PowerPoint 的图形；添加了仅视觉提示示例
- **scientific-schematics**：模型升级（Nano Banana 2、Gemini 3.1 Pro Preview）；移除了过于限制性的图形标签和元指令规则
- **scientific-writing**：添加了 `scientific_report.sty` 专业报告格式系统，包括彩色盒子环境、LaTeX 科学符号命令和文档类型路由指南

---

## [2.12.1] - 2026-03-09

### 🔄 变更

- **更新默认模型** - 在 API、CLI、文档和示例中将 claude-opus 模型引用替换为 claude-sonnet，以提升性能并降低成本

### 🔧 修复

- **版本一致性** - 修复了 pyproject.toml 和 __init__.py 之间的版本不匹配

---

## [2.11.1] - 2026-02-06

### 🔧 信息图路由修复

- **更新了 CLAUDE.md、WRITER.md（两处）和 templates/CLAUDE.scientific-writer.md**，将信息图请求正确路由到 `infographics` 技能
- 添加了明确的警告：信息图不得使用 LaTeX 或 PDF 编译
- 在所有指导文件中，将 `Infographics` 添加到特殊文档类型表中
- 从 `generate-image` 的条目列表中删除了 “infographics”，以避免错误路由

---

## [2.11.0] - 2026-02-03

### 🎨 新增信息图技能

新增全面的 AI 驱动信息图生成技能，支持智能迭代优化。

### ✨ 新增

#### 信息图技能 (`infographics/`)

- **AI 驱动生成**：使用 Nano Banana Pro 并经过 Gemini 3 Pro 质量审核
- **研究集成** - 在生成前使用 `--research` 标志通过 Perplexity Sonar Pro 收集准确数据
- **10 种信息图类型**：统计、时间线、流程、对比、列表、地理、层级、解剖、简历和社交媒体
- **8 种行业风格预设**：企业、医疗、技术、自然、教育、营销、金融和非营利
- **3 种色盲安全调色板**：Wong、IBM 和 Tol
- **智能迭代** - 仅当质量低于文档类型阈值时才重新生成
- **质量阈值** - 营销（8.5/10）、报告（8.0/10）、演示（7.5/10）、社交媒体（7.0/10）、草稿（6.5/10）

#### 新文件

- `SKILL.md` - 包含使用示例的全面文档
- `scripts/generate_infographic.py` - 主入口包装器
- `scripts/generate_infographic_ai.py` - 核心 AI 生成及迭代优化（1,290 行）
- `references/infographic_types.md` - 所有 10 种信息图类型的详细指南（907 行）
- `references/design_principles.md` - 视觉层级、布局模式、排版（636 行）
- `references/color_palettes.md` - 色盲安全和行业特定调色板（496 行）

---

## [2.10.0] - 2025-12-21

### 📝 全面的投稿风格写作指南

通过增加全面的特定投稿风格指南，显著增强了写作技能，用于撰写可发表的手稿。

### ✨ 新增

#### 投稿风格写作系统

- **主风格指南** (`venue_writing_styles.md`) - 全面概述不同出版渠道的写作风格差异
  - 从通俗易懂（Nature/Science）到专业技术（专业期刊）的风格谱系
  - 按投稿类型提供的语气、语态和摘要风格快速参考表
  - 在不同的投稿类型之间调整的指导

- **Nature/Science 风格指南** (`nature_science_style.md`) - 400+ 行全面指南
  - 广泛影响期刊的受众和语气指南
  - 流畅的段落式摘要格式及示例
  - 引言、结果、讨论的结构指导
  - 图形设计原则和引用风格
  - 常见拒稿原因和投稿前检查清单

- **Cell Press 风格指南** (`cell_press_style.md`) - Cell 系列期刊规范
  - 总结（摘要）、亮点、eTOC 概要、简要格式
  - 图形摘要要求和设计指南
  - STAR Methods 和关键资源表格式
  - 声明式子标题风格

- **医学期刊风格指南** (`medical_journal_styles.md`) - NEJM、Lancet、JAMA、BMJ
  - 结构化摘要格式（唯一要求带标签章节的投稿类型）
  - 基于研究设计的证据语言规范
  - 报告规范合规性（CONSORT、STROBE、PRISMA）
  - 各期刊的具体要求和字数限制

- **ML 会议风格指南** (`ml_conference_style.md`) - NeurIPS、ICML、ICLR、CVPR
  - 贡献要点列表格式（对 ML 论文至关重要）
  - 消融实验要求
  - 可复现性要求
  - 局限性章节指南

- **CS 会议风格指南** (`cs_conference_style.md`) - ACL、CHI、SIGKDD
  - NLP 会议要求（人工评估、错误分析）
  - HCI 论文结构（以用户为中心、设计启示）
  - 数据挖掘重点（可扩展性、行业应用）

- **审稿人期望指南** (`reviewer_expectations.md`) - 按投稿类型列出审稿人关注的要点
  - 评估标准和优先权重
  - 各投稿类型常见拒稿原因
  - 示例审稿意见和有效回复
  - 反驳策略和模板

#### 摘要格式标准

- **段落式默认** - 摘要现在默认为流畅的段落式格式
  - 更新了 `scientific-writing/SKILL.md`，明确摘要格式规则
  - 更新了 `imrad_structure.md`，添加了正确与错误的示例
  - 仅在期刊明确要求时使用结构化摘要（如医学期刊）

#### 具体示例

- **Nature 摘要示例** (`nature_abstract_examples.md`) - 5 个跨学科的完整示例
  - 分子生物学、神经科学、气候科学、物理学、生态学
  - 分析每个示例为何有效

- **NeurIPS 引言示例** (`neurips_introduction_example.md`) - 完整的 ML 论文引言
  - 逐段分解
  - 贡献要点模板
  - 常见错误避免

- **Cell 总结示例** (`cell_summary_example.md`) - 完整的 Cell Press 要素
  - 总结、亮点、eTOC 概要、简要
  - 亮点字数统计（≤85 字符）
  - 图形摘要描述

- **医学结构化摘要示例** (`medical_structured_abstract.md`)
  - NEJM、Lancet、JAMA、BMJ 示例
  - 各期刊的格式差异

### 🔧 改进

- **跨技能集成** - 所有相关技能现在引用投稿风格指南
  - 更新了 `scientific-writing/SKILL.md`
  - 更新了 `literature-review/SKILL.md`
  - 更新了 `clinical-decision-support/SKILL.md`
  - 更新了 `peer-review/SKILL.md`
  - 更新了 `treatment-plans/SKILL.md`
  - 更新了 `hypothesis-generation/SKILL.md`
  - 更新了 `research-grants/SKILL.md`
  - 更新了 `market-research-reports/SKILL.md`
  - 更新了 `venue-templates/SKILL.md`

- **同步技能** - 两个技能目录均已更新
  - `skills/` 目录（项目根目录）
  - `scientific_writer/.claude/skills/` 目录（包内）

### 📝 新增文件

- `skills/venue-templates/references/venue_writing_styles.md`
- `skills/venue-templates/references/nature_science_style.md`
- `skills/venue-templates/references/cell_press_style.md`
- `skills/venue-templates/references/medical_journal_styles.md`
- `skills/venue-templates/references/ml_conference_style.md`
- `skills/venue-templates/references/cs_conference_style.md`
- `skills/venue-templates/references/reviewer_expectations.md`
- `skills/venue-templates/assets/examples/nature_abstract_examples.md`
- `skills/venue-templates/assets/examples/neurips_introduction_example.md`
- `skills/venue-templates/assets/examples/cell_summary_example.md`
- `skills/venue-templates/assets/examples/medical_structured_abstract.md`

### 💡 核心优势

- **可发表论文** - 论文现在与目标期刊的风格相匹配
- **正确的摘要格式** - 默认段落式，仅在需要时使用结构化格式
- **审稿人对齐** - 了解每个期刊审稿人的期望
- **跨期刊调整** - 指导如何在投稿类型之间转换
- **具体示例** - 提供可遵循的真实示例，而不仅仅是规则

---

## [2.9.5] - 2025-12-10

### 🎨 科学幻灯片技能增强

- **专业极简主义** - 增强 Nano Banana Pro 系统提示，使幻灯片更简洁
  - 最少的额外元素 - 无装饰边框、阴影或花饰
  - 通用、简单的图像 - 避免过于具体或详细的图像
  - 专业、企业/学术美感，保持克制
  - 所有演示文稿默认作者为 "K-Dense"

- **格式一致性协议** - 统一幻灯片设计的新工作流
  - 在**每个提示词中**定义格式目标（配色方案、排版、视觉风格）
  - 始终使用 `--attach` 附加上一张幻灯片，以保持视觉连续性
  - 将引用直接包含在提示词中（例如，`CITATIONS: Include at bottom: (Author et al., Year)`）
  - 从工作目录中附加结果幻灯片中已有的图形/数据

- **结果幻灯片集成** - 数据驱动型演示文稿的新指南
  - 检查 `figures/`、`results/`、`plots/`、`images/` 目录中已有的图形
  - 使用 `--attach` 将实际数据图形附加到 Nano Banana Pro
  - 支持多个图形：`--attach fig1.png --attach fig2.png`
  - 在提示词中描述如何整合附加的图形

- **简洁输出** - 每张幻灯片仅保存一个图像文件
  - 中间迭代保存到临时文件并清理
  - 不留下 `_v1`、`_v2` 或 `_review_log.json` 文件
  - 最终图像直接保存到指定的输出路径

### 🔧 技术变更

- `generate_slide_image_ai.py`：用专业极简主义更新了 FULL_SLIDE_GUIDELINES
- `generate_slide_image_ai.py`：用通用图像偏好更新了 VISUAL_ONLY_GUIDELINES
- `generate_slide_image_ai.py`：重构为使用临时文件并仅保存最终输出
- `SKILL.md`：添加了包含 5 点检查清单的格式一致性协议
- `SKILL.md`：添加了包含图形附件的示例，用于结果幻灯片
- `SKILL.md`：用新工作流更新了快速入门指南

---

## [2.9.0] - 2025-12-05

### 🚀 发布

- **版本 2.9.0** - 主要版本发布，增强了引用验证和研究工作流
  - 将 Sonar Pro 升级到 Sonar Pro Search，以提高研究查找的准确性
  - 增强了引用验证流程，集成 WebSearch 工具
  - 改进了学术引用的元数据验证
  - 改进了输出目录组织的文档

### 🔧 改进

- **引用验证** - 使用 WebSearch 进行元数据验证，增强了流程
- **研究查找** - 更新为使用 Sonar Pro Search，结果更准确
- **文档** - 在整个代码库中更新了输出目录引用

---

## [2.8.9] - 2025-12-02

### 🔒 隐私和身份保护

- **模型身份隐藏** - 科学写作工具不会透露底层模型或工具的身份
  - 在 Word 的审阅修订中，将所有作者归属从 "Claude" 改为 "Scientific-Writer"
  - 在 DOCX/PPTX 编辑中，将默认作者名从 "Claude" 改为 "Scientific-Writer"
  - 在文档编辑功能中，将默认姓名缩写从 "C" 改为 "SW"
  - 从面向用户的文档中删除了特定于模型的品牌信息
  - 包描述现在引用 "Scientific-Writer" 而非底层模型

### ✨ 增强的科学示意图生成

- **带有质量阈值的智能迭代** - 仅在质量低于文档类型阈值时才重新生成
  - 文档类型感知的质量阈值：
    * `journal`：8.5/10（Nature、Science、同行评审期刊）
    * `conference`、`thesis`、`grant`：8.0/10
    * `preprint`、`report`：7.5/10
    * `poster`：7.0/10
    * `presentation`：6.5/10
  - **Gemini 3 Pro 用于质量审核** - 用于图表评估的卓越视觉和分析能力
  - 达到质量阈值时提前停止（节省 API 调用和时间）
  - 结构化审核，包含 5 个标准：科学准确性、清晰度、标签、布局、专业外观
  - 基于阈值的自动 ACCEPTABLE/NEEDS_IMPROVEMENT 判定

- **新 `--doc-type` 标志** - 指定文档类型以应用适当的质量标准
  - `python scripts/generate_schematic.py "diagram" -o out.png --doc-type journal`
  - 审核日志现在包括 `doc_type`、`quality_threshold`、`needs_improvement`、`early_stop` 和 `early_stop_reason`

### 📝 更新的技能和文档

- **科学示意图技能** - 全面文档更新
  - 智能迭代工作流及流程图
  - 所有文档类型的质量阈值表
  - 显示 `--doc-type` 用法的更新示例
  - 解释了提前停止行为和优势

- **MarkItDown 技能** - 将模型引用更新为通用描述
  - 将 "Claude Sonnet 4.5" 引用改为 "先进的视觉模型"
  - 模型标识符保留以确保 API 兼容性

### 🔧 技术变更

- **文档编辑** - 所有技能中一致的作者身份
  - `skills/document-skills/docx/scripts/document.py`：默认作者 “Scientific-Writer” 
  - `skills/document-skills/docx/ooxml/scripts/validation/redlining.py`：更新了验证消息
  - `skills/document-skills/pptx/ooxml/scripts/validation/redlining.py`：更新了验证消息
  - 文档中所有 XML 示例均已更新

- **科学示意图生成** - 增强的 AI 审核系统
  - `scripts/generate_schematic_ai.py`：Gemini 3 Pro 审核集成
  - `scripts/generate_schematic.py`：文档类型支持
  - 生成器类中的质量阈值常量
  - 增强的审核提示词，包含结构化的 5 个标准评估

---

## [2.8.8] - 2025-12-01

### ✨ 新功能

- **实时文本流式传输** - 通过 API 实时流式传输 Scientific-Writer 的实际响应
  - 新的 `TextUpdate` 模型，用于从 Scientific-Writer 输出实时文本
  - API 现在为每个文本块产生 `{"type": "text", "content": "..."}`
  - 能够实时显示 Scientific-Writer 的推理和解释
  - 与现有的进度更新并存 - 无破坏性更改

### 📝 API 变更

- 从 `scientific_writer` 导出新的 `TextUpdate` 模型
- `generate_paper()` 现在产生三种更新类型：
  - `"text"`：Scientific-Writer 文本响应的实时流
  - `"progress"`：结构化的阶段更新（未更改）
  - `"result"`：包含所有论文详细信息的最终结果（未更改）

### 🎯 使用示例

```python
from scientific_writer import generate_paper

async for update in generate_paper("Create a paper on AI"):
    if update["type"] == "text":
        # 流式输出 Scientific-Writer 的实时输出
        print(update["content"], end="", flush=True)
    elif update["type"] == "progress":
        # 结构化的进度更新
        print(f"\n[{update['stage']}] {update['message']}")
    elif update["type"] == "result":
        print(f"\nPaper created: {update['paper_directory']}")
```

仅显示进度更新（无文本流）：

```python
async for update in generate_paper("Create a paper"):
    if update["type"] == "text":
        pass  # 跳过文本更新
    elif update["type"] == "progress":
        print(f"[{update['stage']}] {update['message']}")
```

---

## [2.8.7] - 2025-11-26

### ✨ 新功能

- **Token 使用量跟踪** - 在文档生成期间跟踪输入/输出 token
  - 为 `generate_paper()` API 新增 `track_token_usage` 参数
  - 在最终结果中返回包含详细 token 细分的 `token_usage`
  - 跟踪：`input_tokens`、`output_tokens`、`total_tokens`、`cache_creation_input_tokens`、`cache_read_input_tokens`
  - 静默跟踪（无终端输出） - 仅作为数据返回，供程序化使用

### 📝 API 变更

- 从 `scientific_writer` 导出新的 `TokenUsage` 模型
- `generate_paper()` 接受可选参数 `track_token_usage: bool = False`
- 启用时，最终结果包含 `token_usage` 字段及 token 统计
- 启用跟踪时，即使出错也会在结果中包含 token 使用情况
- CLI 的 `main()` 函数现在接受 `track_token_usage` 参数并返回 `TokenUsage`

### 🎯 使用示例

```python
from scientific_writer import generate_paper

async for update in generate_paper("Create a paper", track_token_usage=True):
    if update["type"] == "result":
        if "token_usage" in update:
            usage = update["token_usage"]
            print(f"Input tokens: {usage['input_tokens']}")
            print(f"Output tokens: {usage['output_tokens']}")
            print(f"Total tokens: {usage['total_tokens']}")
```

---

## [2.8.5] - 2025-11-25

### ✨ 增强

- **更智能的上下文感知进度消息** - 进度更新现在更智能、更具体
  - 从文件路径中检测文档类型（幻灯片、海报、报告、基金申请）
  - 从文件名中提取章节名称（引言、方法、结果等）
  - 显示类似 "正在编写引言章节" 而非 "正在编写 file.tex" 的消息

- **更简洁的进度输出** - 减少进度更新中的噪音
  - 检查命令（ls、cat）不再产生进度更新
  - 基于文本的进度分析现在仅作为最小的后备方案
  - 工具使用驱动主要的进度更新

- **增强的工具分析** - 所有工具类型都有更详细的消息
  - 读取："正在分析 PDF"、"正在从 file.csv 加载数据"、"正在读取引言章节"
  - 写入："正在创建主文档结构"、"正在编写方法章节"、"正在创建带引用的参考文献列表"
  - 编辑："正在优化引言章节"、"正在更新参考文献"
  - Bash："正在运行完整的 LaTeX 编译流水线"、"正在处理参考文献引用"、"正在将最终 PDF 复制到输出"
  - 研究："搜索：[查询预览]"，"网页搜索：[查询预览]"

### 🔧 改进

- **文档类型检测** - 新的 `_detect_document_type()` 可识别：
  - 幻灯片/演示文稿（beamer）
  - 海报
  - 报告
  - 基金/提案
  - 通用文档

- **章节名称提取** - 新的 `_get_section_from_filename()` 识别：
  - 摘要、引言、方法、结果、讨论、结论
  - 背景、相关工作、实验、评估
  - 附录、补充材料

- **简化的文本分析** - `_analyze_progress()` 现在仅检测主要的阶段转换
  - 编译指示（pdflatex、latexmk）
  - 完成指示（successfully compiled、pdf generated）
  - 未检测到转换时返回 `None` 消息

---

## [2.8.4] - 2025-11-25

### 🔄 变更

- **从进度更新中移除百分比** - 进度更新现在使用基于阶段的跟踪，而不是百分比
  - 更简洁的 API 响应，没有任意百分比值
  - 进度通过阶段跟踪：`initialization` → `planning` → `research` → `writing` → `compilation` → `complete`

- **通用文档术语** - 在整个 API 中将 "paper" 替换为 "document"
  - 支持所有文档类型：论文、幻灯片、海报、报告、基金申请等。
  - 消息现在显示 "document generation" 而不是 "paper generation"
  - 更准确地反映工具的实际能力

### 📝 API 变更

- `ProgressUpdate` 模型不再包含 `percentage` 字段
- 进度更新现在仅返回：`type`、`timestamp`、`message`、`stage` 和可选的 `details`
- `_analyze_progress()` 返回 `(stage, message)` 元组，而不是 `(stage, percentage, message)`
- `_analyze_tool_use()` 返回 `(stage, message)` 元组，而不是 `(stage, percentage, message)`

### 🎯 示例输出

```python
async for update in generate_paper("Create conference slides on AI"):
    if update["type"] == "progress":
        print(f"[{update['stage']:12}] {update['message']}")
```

输出：
```
[initialization] 使用 Claude 开始文档生成
[research     ] 搜索文献数据库
[research     ] 正在研究：机器学习应用...
[writing      ] 正在编写引言章节
[writing      ] 正在编写 LaTeX 文档：main.tex
[compilation  ] 将 LaTeX 编译为 PDF
[complete     ] 文档生成完成
```

---

## [2.8.3] - 2025-11-25

### ✨ 增强

- **详细的 API 进度更新** - 显著改进了程序化 API 中的进度跟踪
  - **工具感知进度跟踪** - 检测并报告特定的工具使用（读取、写入、编辑、Bash）
  - **文件操作跟踪** - 报告正在读取、写入或编辑的文件及文件名
  - **编译检测** - 识别 pdflatex、bibtex 和 latexmk 命令，并提供具体消息
  - **研究查找跟踪** - 显示研究查询何时执行
  - **25+ 个详细的进度指示器** - 论文生成每个阶段的细粒度消息：
    - 规划：大纲创建、需求分析
    - 研究：数据库搜索、出版物收集、综合
    - 写作：摘要、引言、方法、结果、讨论、结论、参考文献
    - 编译：LaTeX 创建、pdflatex 执行次数、bibtex 处理
    - 完成：文件验证、目录组织
  - **新的 `details` 字段** - 进度更新现在包含可选的上下文：
    - `tool`：正在使用的工具名称
    - `tool_calls`：工具调用次数
    - `files_created`：写入的文件数
  - **非重复过滤** - 避免重复相同的进度消息

### 📝 API 变更

- `ProgressUpdate` 模型现在包含可选的 `details: Dict[str, Any]` 字段
- 进度阶段中新增 `planning` 阶段
- 进度百分比现在更细粒度（22%、28%、35% 等，而不是仅仅 30%、50%、80%）

### 🎯 示例输出

```python
async for update in generate_paper("Create a paper on AI"):
    if update["type"] == "progress":
        print(f"[{update['percentage']:3d}%] {update['message']}")
        if update.get('details'):
            print(f"       Tool: {update['details'].get('tool')}")
```

输出：
```
[ 10%] 使用 Claude 开始论文生成
[ 22%] 搜索文献数据库
[ 30%] 正在研究：量子计算应用...
[ 45%] 正在编写引言章节
[ 55%] 正在编写 LaTeX 文档：main.tex
[ 68%] 正在创建参考文献：references.bib
[ 78%] 将 LaTeX 编译为 PDF
[ 82%] 使用 BibTeX 处理参考文献
[ 92%] 验证输出文件
[100%] 论文生成完成
```

---

## [2.8.2] - 2025-11-24

### 🔧 修复

- **API 关键错误修复** - 修复了 `generate_paper()` 函数中的参数命名冲突
  - `query` 参数屏蔽了从 `claude_agent_sdk` 导入的 `query` 函数
  - 将 SDK 导入重命名为 `claude_query` 以避免冲突
  - API 现在可用于程序化论文生成

---

## [2.8.1] - 2025-11-24

### 🔧 变更

- **输出目录重命名** - 将默认输出目录从 `paper_outputs/` 更改为 `writing_outputs/`，以更好地反映所支持的更广泛的文档类型（论文、幻灯片、海报、报告等）
  - 更新了所有文档和模板以引用 `writing_outputs/`
  - 将 `writing_outputs/` 添加到了 `.gitignore`

---

## [2.8.0] - 2025-11-20

### 🎨 头条功能：用于科学图表的 Nano Banana Pro

此版本引入了 **Nano Banana Pro**，一个革命性的 AI 驱动系统，用于从自然语言描述生成可发表质量的科学图表。

### ✨ 新增

#### AI 驱动的科学示意图

- **Nano Banana Pro 集成** - 通过自然语言描述生成任何科学图表
  - 无需编码 - 只需描述您想要的内容
  - 无需模板 - AI 理解您的意图
  - 无需手动绘图 - 根据描述自动生成
  - 可发表质量的输出，遵循科学标准
  
- **迭代优化系统** - 通过智能审核周期自动改进质量
  - 默认 3 次迭代（可配置 1-10）
  - 每次迭代后进行 AI 质量审核（0-10 分 + 详细评审）
  - 逐步改进，解决具体问题
  - 透明的审核过程，包含详细的 JSON 日志
  
- **全面输出** - 多个版本加上质量评估
  - 三个图像版本（v1、v2、v3），展示改进过程
  - 最终完善图像，即可用于发表
  - 详细的审核日志，包含评分和评审意见
  - 质量指标：清晰度、标签、准确性、可访问性
  
- **内置科学标准** - 自动遵循最佳实践
  - 干净的白色/浅色背景
  - 高对比度，确保可读性（符合 WCAG 2.1 标准）
  - 专业的排版（最小 10pt 字体，无衬线体）
  - 色盲友好的调色板（Okabe-Ito 方案）
  - 适当的间距、比例尺、图例和坐标轴
  - 标准的科学符号和标记

#### 通用图表支持

- **临床与医学** - CONSORT 流程图、临床试验、诊断算法、患者路径
- **计算与 AI** - 神经网络（CNN、Transformer、RNN）、算法、系统架构
- **生物与化学** - 信号通路（MAPK、PI3K/AKT）、代谢通路、蛋白质结构
- **工程与物理** - 电路图、框图、实验装置、信号处理
- **及更多** - 研究设计、概念框架、流程图、时间线、组织架构图

#### 全面文档

- **README.md** - 快速入门指南，包含安装、使用、示例（340+ 行）
- **QUICK_REFERENCE.md** - 常用任务的一页速查表（209 行）
- **SKILL.md** - 包含大量示例的完整文档（737 行）
- **IMPLEMENTATION_SUMMARY.md** - 技术细节和架构（372 行）
- **示例脚本** - `example_usage.sh`，包含实际的演示
- **测试套件** - `test_ai_generation.py`，包含 6 个全面的测试

### 🔧 改进

#### 提示词工程系统

- **有效的提示词指南** - 获得高质量结果的最佳实践
  - 指定布局和结构（垂直/水平流向、定位）
  - 包含定量细节（数字、尺寸、参数）
  - 描述视觉风格（极简、详细、技术性）
  - 请求具体的标签和注释
  - 提及颜色和可访问性要求
  
- **质量评估框架** - 七个维度的评估系统
  - 科学准确性 - 表示的正确性
  - 元素清晰度 - 易于理解
  - 标签可读性 - 字体、大小、位置
  - 布局与构图 - 视觉层级
  - 可访问性 - 色盲友好、高对比度
  - 专业质量 - 可发表的外观
  - 完整性 - 所有必需元素都存在

#### 开发者体验

- **Python API** - 程序化访问 Nano Banana Pro
  ```python
  from scripts.generate_schematic_ai import ScientificSchematicGenerator
  
  generator = ScientificSchematicGenerator(api_key="your_key", verbose=True)
  results = generator.generate_iterative(
      user_prompt="CONSORT 流程图",
      output_path="figures/consort.png",
      iterations=3
  )
  print(f"最终评分: {results['final_score']}/10")
  ```

- **命令行界面** - 简单、直观的使用方式
  ```bash
  python scripts/generate_schematic.py "diagram description" -o output.png
  ```

- **灵活配置** - 多种自定义选项
  - `--iterations N` - 控制优化周期（1-10）
  - `--method ai|code` - 选择生成方法
  - `-v, --verbose` - 详细的进度输出
  - `--api-key KEY` - 覆盖环境变量

### 🎯 使用示例

#### CONSORT 流程图
```bash
python scripts/generate_schematic.py \
  "CONSORT 参与者流程：筛选 n=500，排除 n=150，随机分组 n=350" \
  -o consort.png
```

#### 神经网络架构
```bash
python scripts/generate_schematic.py \
  "包含编码器和解码器的 Transformer 架构，展示注意力机制" \
  -o transformer.png
```

#### 生物通路
```bash
python scripts/generate_schematic.py \
  "MAPK 信号通路：EGFR → RAS → RAF → MEK → ERK → 细胞核" \
  -o mapk.png
```

### 💡 核心优势

- **快速**：1-2 分钟即可获得结果（3 次迭代）
- **简便**：仅需自然语言描述
- **高质量**：自动审核和优化
- **通用**：适用于所有图表类型
- **可发表就绪**：立即输出高质量图像
- **经济**：每张图表 $0.10-0.50
- **易于访问**：色盲友好，高对比度
- **文档完备**：全面的指南和示例

### 📦 新文件

- `skills/scientific-schematics/`
  - `scripts/generate_schematic_ai.py` - AI 生成引擎及迭代优化
  - `scripts/generate_schematic.py` - 统一入口（AI + 代码方法）
  - `README.md` - 快速入门和全面指南
  - `QUICK_REFERENCE.md` - 一页速查表
  - `IMPLEMENTATION_SUMMARY.md` - 技术细节
  - `test_ai_generation.py` - 验证测试套件
  - `example_usage.sh` - 使用演示

### 🔄 向后兼容性

- ✅ 所有现有的基于代码的生成仍可通过 `--method code` 使用
- ✅ Graphviz、TikZ、schemdraw 以及其他工具未更改
- ✅ 所有现有的模板和脚本都保留
- ✅ 对于喜欢经典工作流的用户仍可访问

### 🧪 测试

运行验证测试：
```bash
python skills/scientific-schematics/test_ai_generation.py
# 预期："6/6 tests passed"
```

### 📊 性能表现

- **生成时间**：3 次迭代 1-2 分钟
- **成本**：每张图表 $0.10-0.50（3 次迭代）
- **质量评分**：通常最终迭代为 7-9.5/10
- **成功率**：对多种图表类型均能高质量生成

### 🌟 输出示例

参见 `figures/` 目录中的实际示例：
- `google_gemini_architecture.png` - 复杂的 AI 系统架构
- `gemini_moe_architecture.png` - 专家混合图
- `test_nano_banana.png` - 测试图
- `*_review_log.json` - 质量评估日志

---

## [2.7.0] - 2025-01-22

### 🎯 Claude Code 插件焦点

此版本强调将 Scientific Writer 用作 **Claude Code (Cursor) 插件**，使得在 IDE 中直接获取科学写作功能比以往更容易。

### ✨ 新增

#### 增强的插件体验

- **简化的插件安装** - 改进的文档和 Claude Code 插件设置流程
  - 清晰的分步安装指南
  - 市场集成说明
  - 本地开发和测试指南
  - 常见插件问题的故障排除

- **优化的插件结构** - 更好地组织插件使用
  - 安装插件后，所有 19+ 个技能自动可用
  - `/scientific-writer:init` 命令创建全面的 `CLAUDE.md` 配置
  - 无需额外设置即可在 IDE 中直接访问技能
  - 为插件上下文优化的模板文件

- **插件优先文档** - 增强的 README，突出插件部分
  - 插件安装被突出显示在顶部
  - 在 Claude Code 中使用技能的清晰示例
  - 面向开发人员的插件测试指南
  - 针对插件特定问题的故障排除部分

### 🔧 改进

#### 更好的 IDE 集成

- **无缝技能访问** - 所有技能在 Claude Code 中原生工作
  - 无需在 CLI 和 IDE 之间切换
  - 技能可通过 `@skill-name` 语法自动发现
  - 上下文感知的技能建议
  - 在 IDE 中直接编辑和创建文件

- **改进的初始化命令** - 增强的 `/scientific-writer:init` 体验
  - 更好地处理现有的 `CLAUDE.md` 文件
  - 对现有配置的备份和合并选项
  - 清晰反馈已安装的内容
  - 可用的技能和功能摘要

- **插件优化的工作流** - 为 IDE 使用设计的工作流
  - 文件操作直接在项目目录中进行
  - 不需要单独的数据文件夹 - 使用项目结构
  - 技能与 IDE 的文件系统集成
  - 在 IDE 上下文中提供更好的进度反馈

### 📝 文档更新

- **插件快速入门** - 面向插件用户的新快速入门指南
- **插件示例** - 在 Claude Code 中使用技能的实际示例
- **技能参考** - 所有 19+ 个可用技能的完整列表
- **故障排除** - 常见的插件安装和使用问题

### 🎯 使用示例

#### 插件安装

```bash
# 添加市场
/plugin marketplace add https://github.com/K-Dense-AI/claude-scientific-writer

# 安装插件
/plugin install claude-scientific-writer

# 在您的项目中初始化
/scientific-writer:init
```

#### 在 Claude Code 中使用技能

```bash
# 创建一篇论文（技能会自动使用）
> Create a Nature paper on CRISPR gene editing

# 使用特定的技能
> @research-lookup Find recent papers on mRNA vaccines
> @peer-review Evaluate this manuscript
> @clinical-reports Create a case report for this patient

# 生成文档
> Create an NSF grant proposal for quantum computing
> Generate conference slides from my paper
> Create a research poster for NeurIPS
```

### 💡 插件用户的核心优势

- **无需 CLI** - 一切都在 Claude Code 中直接操作
- **即时访问** - 安装后所有 19+ 个技能立即可用
- **IDE 集成** - 直接在您的项目中创建和编辑文件
- **上下文感知** - 技能了解您的项目结构
- **无缝工作流** - 无需在工具之间切换

### 🚀 从 CLI 迁移到插件

对于现有的 CLI 用户：
- 插件提供相同的功能，并具有更好的 IDE 集成
- 技能在 CLI 和插件模式下工作方式相同
- 可以在同一个项目中同时使用 CLI 和插件
- 对于基于 IDE 的工作流，推荐使用插件

### 📦 插件结构

```
claude-scientific-writer/
├── .claude-plugin/          # 插件元数据（如果存在）
├── commands/                 # 插件命令
│   └── scientific-writer-init.md
├── skills/                   # 所有 19+ 个技能
│   ├── research-lookup/
│   ├── peer-review/
│   ├── clinical-reports/
│   └── ... (还有 16 个)
├── templates/                # CLAUDE.md 模板
│   └── CLAUDE.scientific-writer.md
└── ... (Python 包文件)
```

### 🎨 插件功能

- **19+ 个专业技能** - 研究、写作、审稿等
- **一键设置** - `/scientific-writer:init` 配置一切
- **技能发现** - 询问 "What skills are available?" 即可查看完整列表
- **直接集成** - 技能与 IDE 的文件操作一起工作
- **模板系统** - 所有文档类型的专业模板

---

## [2.6.1] - 2025-11-17

### ⚡ 性能

#### 并行研究查找系统

- **显著节省时间** - 研究查询的并行执行可将查找时间最多减少 10 倍
  - 顺序工作流：每个查询约需 N × ~12 秒
  - 并行工作流：无论 N 是多少，约需 15-20 秒（达到工作线程上限）
  - 示例：20 个查询现在大约需要 20 秒，而不是 4 分钟
  
- **AI 驱动的主题识别** - 从文本中自动提取研究主题
  - 智能识别关键研究问题
  - 节省手动提取主题的时间
  - 主题保存为可审核/编辑的文件格式
  
- **灵活的工作流模式** - 适用于不同场景的三种使用模式：
  1. **快速与自动化** - 一个命令即可获得即时结果
  2. **审核与优化** - 包含人工审核主题的两步过程
  3. **手动控制** - 自带主题列表
  
- **智能查询复杂度评估** - 自动选择模型
  - 简单查询 → 快速的 'pro' 模型
  - 复杂查询（对比、分析）→ 'reasoning' 模型
  - 在速度和质量的平衡上进行优化

### 🔧 改进

#### 增强的研究查找功能

- **并行执行引擎** - 使用 ThreadPoolExecutor 的并发 API 调用
  - 可配置的工作线程数（默认：5，最大：10）
  - 智能速率限制和错误处理
  - 批处理的进度跟踪
  
- **主题管理** - 基于文件的主题处理
  - `save_topics_to_file()` - 保存识别出的主题以供审核
  - `load_topics_from_file()` - 加载并处理主题列表
  - 易于编辑的人类可读格式
  
- **新的研究方法**：
  - `identify_research_topics()` - AI 驱动的主题提取
  - `parallel_lookup()` - 并发研究执行
  - `identify_and_research()` - 组合工作流（识别 + 研究）
  - `batch_lookup()` - 增强并添加了 `parallel` 和 `max_workers` 参数

### 🎯 使用示例

#### CLI - 快速并行研究

```bash
# 自动工作流（一个命令）
python research_lookup.py --identify input.txt \
    --topics-file topics.txt \
    --parallel --max-workers 10 \
    --output results.json

# ✅ 不到 1 分钟即可获得完整结果（无论主题数量多少）
```

#### CLI - 审核与优化工作流

```bash
# 步骤 1：识别主题
python research_lookup.py --identify input.txt \
    --topics-file topics.txt

# 步骤 2：手动审核/编辑 topics.txt

# 步骤 3：并行研究
python research_lookup.py --topics-file topics.txt \
    --parallel --max-workers 10 \
    --output results.json
```

#### 程序化 API - 并行查找

```python
from research_lookup import ResearchLookup

research = ResearchLookup()

# 通过一次调用实现识别和研究
results = research.identify_and_research(
    text_file="research_proposal.txt",
    parallel=True,
    max_workers=10,
    output_file="results.json"
)

# 手动主题并进行并行执行
topics = ["CRISPR gene editing", "mRNA vaccines", "AI in medicine"]
results = research.parallel_lookup(
    topics, 
    max_workers=10,
    show_progress=True
)
```

### 💡 核心优势

- **10 倍加速** - 并行执行显著减少研究时间
- **智能** - AI 驱动的主题识别和复杂度评估
- **灵活** - 多种工作流模式适用于不同用例
- **可扩展** - 高效处理大型研究项目
- **可靠** - 内置错误处理和速率限制
- **人在回路** - 在开始研究之前审核/编辑主题

### 📝 增强的文件

- `skills/research-lookup/research_lookup.py` - 添加了并行执行引擎
- `skills/research-lookup/WORKFLOW_GUIDE.md` - 包含可视化图表的全面 381 行工作流指南
- `skills/research-lookup/test_parallel.py` - 并行功能的测试套件
- `skills/research-lookup/UPGRADE_SUMMARY.md` - 新功能的迁移指南

### 🚀 性能影响

**之前（顺序执行）：**
- 5 个查询：约 60 秒
- 10 个查询：约 120 秒
- 20 个查询：约 240 秒

**之后（10 个工作线程的并行执行）：**
- 5 个查询：约 15 秒 ⚡ 快了 4 倍
- 10 个查询：约 18 秒 ⚡ 快了 6.6 倍
- 20 个查询：约 20 秒 ⚡ 快了 12 倍

---

## [2.6.0] - 2025-11-17

### ✨ 新增

#### 专业的假设生成报告

- **科学假设生成技能** - 用于开发可测试科学假设的全面框架
  - 从观察结果到可测试预测的系统性工作流
  - 基于文献综合的证据驱动方法
  - 生成 3-5 个相互竞争的机制性假设
  - 带有美观彩色盒子的专业 LaTeX 报告
  - 结构为简洁正文（8-14 页）和全面的附录

- **假设报告功能**
  - **彩色盒子系统** - 使用自定义 LaTeX 环境的视觉组织：
    - 5 个不同的假设盒子（蓝色、绿色、紫色、青色、橙色）
    - 预测盒子（琥珀色）
    - 对比盒子（钢青色）
    - 证据盒子（浅蓝色）
    - 总结盒子，提供执行概览
  - **专业结构**：
    - 执行摘要 - 一页高度总结
    - 相互竞争的假设 - 每个假设都有专用的彩色盒子，包含机制、证据和假设
    - 可测试的预测 - 针对每个假设的具体、可测量的预测
    - 关键对比 - 如何通过实验区分这些假设
  - **全面的附录**：
    - 附录 A：文献综述（40-60+ 引用）
    - 附录 B：详细的实验设计
    - 附录 C：质量评估表
    - 附录 D：补充证据和类比系统

- **严格的质量框架** - 七个维度的评估系统：
  - **可测试性** - 能用当前方法进行实证检验
  - **可证伪性** - 明确否证假设的条件
  - **简洁性** - 符合证据的最简单解释（奥卡姆剃刀）
  - **解释力** - 解释大部分观察结果
  - **范围** - 涵盖的现象和情境
  - **一致性** - 与现有知识的对齐
  - **新颖性** - 超越重述已知事实的新见解

- **全面的资源**
  - `hypothesis_generation.sty` - 带有彩色盒子的专业 LaTeX 样式包
  - `hypothesis_report_template.tex` - 包含正文和附录的完整模板
  - `hypothesis_quality_criteria.md` - 详细的评估框架（200+ 行）
  - `experimental_design_patterns.md` - 跨领域的常见方法
  - `literature_search_strategies.md` - 有效的搜索技巧
  - `FORMATTING_GUIDE.md` - 所有格式化功能的快速参考

### 🔧 改进

#### 增强的科学工作流

- **文献集成** - 双重搜索策略：
  - PubMed 适用于生物医学主题
  - 普通网页搜索适用于更广泛的科学领域
  - 每份报告综合 50+ 参考文献（正文 15-20，附录 40-60+）
  - 基于证据的假设开发

- **机制性关注** - 强调解释性机制：
  - 每个假设都解释“如何”和“为什么”（而不仅仅是“是什么”）
  - 多层次解释（分子、细胞、系统、群体）
  - 己有机制的新颖组合
  - 挑战现有解释中的假设

- **实验设计** - 实用的测试策略：
  - 实验室实验（体外、体内、计算）
  - 观测性研究（横断面、纵向、病例对照）
  - 临床试验（如适用）
  - 自然实验和准实验设计

### 🎯 使用示例

#### CLI - 生成假设报告

```bash
scientific-writer
> Generate competing hypotheses for why NAD+ levels decline with aging

# 系统将：
# ✓ 通过 PubMed 和网页搜索生物医学文献
# ✓ 综合当前理解
# ✓ 生成 3-5 个机制性假设
# ✓ 评估每个假设在 7 个质量维度上的表现
# ✓ 设计检验预测的实验
# ✓ 创建带有彩色盒子的专业 LaTeX 报告
# ✓ 编译为精美的 PDF
```

#### API - 程序化假设生成

```python
import asyncio
from scientific_writer import generate_paper

async def main():
    async for update in generate_paper(
        "What mechanisms could explain the obesity paradox in heart failure patients?"
    ):
        if update["type"] == "progress":
            print(f"[{update['percentage']}%] {update['message']}")
        else:
            print(f"Report: {update['files']['pdf_final']}")

asyncio.run(main())
```

#### 研究应用

```bash
# 癌症生物学
> Why do some tumors respond to immunotherapy while others don't?

# 神经科学
> What mechanisms could explain the therapeutic effect of ketamine in depression?

# 气候科学
> Generate hypotheses for accelerated ice sheet melting in Greenland

# 材料科学
> Why does this novel catalyst show unexpected selectivity?
```

### 💡 核心功能

- **基于证据** - 所有假设均有坚实的文献支持，引用广泛
- **机制性** - 侧重解释机制，而不仅仅是描述性模式
- **可测试** - 每个假设都有具体、可测量的预测
- **全面** - 系统评估多个相互竞争的解释
- **美观** - 带有彩色视觉组织的专业 LaTeX 格式
- **严谨** - 七个维度的质量评估框架
- **实用** - 详细的实验设计，可直接实施

### 📝 新增文件

- `skills/hypothesis-generation/` - 完整的假设生成技能
  - `SKILL.md` - 全面的工作流文档（200+ 行）
  - `assets/hypothesis_generation.sty` - 带有彩色盒子的 LaTeX 样式包
  - `assets/hypothesis_report_template.tex` - 专业报告模板
  - `assets/FORMATTING_GUIDE.md` - 格式化快速参考
  - `references/hypothesis_quality_criteria.md` - 评估框架
  - `references/experimental_design_patterns.md` - 设计策略
  - `references/literature_search_strategies.md` - 搜索技巧

### 🎨 报告结构

假设生成系统创建格式精美的报告：

**正文（简洁）：**
- 执行摘要（1 页）
- 相互竞争的假设（3-5 个假设，用彩色盒子呈现）
- 可测试的预测（琥珀色盒子）
- 关键对比（灰色盒子）

**附录（全面）：**
- 文献综述（40-60+ 引用）
- 实验设计（详细方案）
- 质量评估（系统评估）
- 补充证据（支持性数据）

### 🔬 科学严谨性

系统通过以下方式确保高质量的假设：

1. **系统文献搜索** - 对现有证据的全面回顾
2. **多个假设** - 3-5 个相互竞争的解释，而不仅仅是一个
3. **质量评估** - 七维评估框架
4. **实验检验** - 区分假设的详细设计
5. **清晰的预测** - 具体、定量、可证伪的预测
6. **专业呈现** - 可发表的 LaTeX 报告

---

## [2.5.0] - 2025-11-11

### ✨ 新增

#### 科学幻灯片和演示系统

- **专业演示文稿生成** - 直接从研究论文或主题创建高质量的科学幻灯片
  - 支持学术会议、研究研讨会和机构演示
  - 美观的 LaTeX Beamer 模板，现代专业设计
  - 自动内容结构化，针对科学传播进行了优化
  - 与现有的论文工作流集成

- **全面的演示文稿技能** - 新的 `scientific-slides` 技能，资源丰富
  - **设计指南** - 663 行全面指南涵盖：
    - 视觉层级和布局原则
    - 色彩理论和可访问性（符合 WCAG 2.1 标准）
    - 演示文稿的排版最佳实践
    - 数据可视化指南
    - 动画和过渡建议
    - 特定投稿的格式（会议尺寸、宽高比）
  - **LaTeX Beamer 模板** - 多个可立即使用的专业主题
  - **演示文稿资源** - 图标、图表和视觉元素
  - **示例脚本** - 用于演示文稿创建的 Python 自动化
  - **参考资料** - 科学演示的最佳实践

- **PowerPoint 转换支持** - 生成 LaTeX 和 PowerPoint 格式
  - 使用 `python-pptx` 的基于 Python 的转换脚本
  - 保留布局、格式和设计元素
  - 支持复杂的幻灯片结构和动画
  - 导出为多种格式（PDF、PPTX）

### 🔧 改进

#### 增强的文档生成工作流

- **智能演示文稿识别** - 自动识别演示文稿请求
  - 检测诸如“演示文稿”、“幻灯片”、“PowerPoint”、“deck”等关键词
  - 路由到适当的模板和格式
  - 优化内容结构以适应视觉传达

- **更好的模板组织** - 改进的技能系统架构
  - 清晰区分的文档类型（论文、海报、幻灯片、基金、报告）
  - 更容易访问特定投稿的模板
  - 增强元数据和标签，便于模板发现

#### 输出组织

- **特定演示文稿的目录** - 有组织的输出结构
  - `drafts/` - LaTeX 源文件和初始版本
  - `final/` - 编译后的 PDF 和 PowerPoint 文件
  - `figures/` - 演示文稿图形和图表
  - `references/` - 参考文献文件
  - `slide_images/` - 单个幻灯片导出

### 🎯 使用示例

#### CLI - 生成科学演示文稿

```bash
scientific-writer
> Create a conference presentation on The AI Scientist framework by Sakana AI

# 系统将：
# ✓ 生成专业的 Beamer 幻灯片
# ✓ 为视觉传达构建内容
# ✓ 包含图表和图形
# ✓ 编译为 PDF
# ✓ （可选）转换为 PowerPoint
```

#### API - 程序化演示文稿生成

```python
import asyncio
from scientific_writer import generate_paper

async def main():
    async for update in generate_paper(
        "Create a research seminar presentation on CRISPR applications in agriculture"
    ):
        if update["type"] == "progress":
            print(f"[{update['percentage']}%] {update['message']}")
        else:
            print(f"Presentation: {update['files']['pdf_final']}")

asyncio.run(main())
```

#### 将论文转换为幻灯片

```bash
# 将您的论文放在数据文件夹中
cp my_paper.pdf data/

scientific-writer
> Convert this paper into a 20-minute conference presentation

# 系统将：
# ✓ 从论文中提取关键发现
# ✓ 为时间限制构建幻灯片
# ✓ 创建可视化表示
# ✓ 生成演讲者注释
```

### 💡 核心功能

- **专业质量** - 遵循最佳实践的可发表幻灯片
- **科学准确性** - 在优化视觉沟通的同时保持严谨性
- **灵活格式** - LaTeX Beamer、PDF 和 PowerPoint 输出
- **可访问性** - 符合 WCAG 2.1 标准的配色和布局
- **时间优化** - 针对不同演示时长自动调整内容节奏
- **视觉设计** - 适合学术环境的现代、简洁美学

### 📝 新增/修改的文件

- `scientific_writer/.claude/skills/scientific-slides/` - 完整的演示文稿技能目录
  - `assets/powerpoint_design_guide.md` - 全面的 663 行设计指南
  - 额外模板、脚本和参考资料
- 文档更新以反映新的演示文稿功能

### 🎨 设计哲学

科学的幻灯片系统遵循基于证据的设计原则：
- **认知负荷理论** - 最小化无关信息
- **双重编码理论** - 结合语言和视觉信息
- **循证医学演示** - CONSORT/PRISMA 图表标准
- **学术交流最佳实践** - Nature、Science、Cell 的演示指南

---

## [2.4.0] - 2025-11-07

### ✨ 新增

#### 智能文件路由系统

- **智能文件分类** - 根据文件类型和目的自动路由文件
  - **手稿文件**（仅 .tex）→ `drafts/` 文件夹 [触发编辑模式]
  - **源文件/上下文文件**（.md, .docx, .pdf）→ `sources/` 文件夹 [参考资料]
  - **图像文件**（.png, .jpg, .svg 等）→ `figures/` 文件夹
  - **数据文件**（.csv, .json, .xlsx, .txt 等）→ `data/` 文件夹
  - **其他文件** → `sources/` 文件夹 [上下文]

- **新的源目录** - 专门用于参考和上下文材料的文件夹
  - 将用作参考的 .md、.docx、.pdf 文件分开存放
  - 清楚区分可编辑手稿和支持材料
  - 更好地组织项目资源

### 🔧 改进

#### 增强的手稿编辑工作流

- **优化的编辑模式检测** - 仅当 `drafts/` 中的 .tex 文件才触发编辑模式
  - 之前行为：.tex、.md、.docx、.pdf 均触发编辑模式
  - 新行为：仅 .tex 文件被视为可编辑手稿
  - .md、.docx、.pdf 文件现在作为 `sources/` 中的参考资料
  - 更清晰的用户体验，行为更可预测

- **改进的文件处理** - 更好的错误处理和用户反馈
  - 文件复制操作期间增强的进度报告
  - 分开计数手稿、源文件、数据和图像
  - 清晰指示每种文件类型被复制到哪里
  - 整个文件处理工作流中更详细的 CLI 输出

- **更新的文档** - 系统指导的全面更新
  - 在 WRITER.md 中明确了文件路由规则
  - 更新了 CLI 帮助文本，包含新的文件分类
  - 增强的欢迎消息，解释文件处理
  - 更好的示例演示工作流

### 🗑️ 移除

- **CLAUDE.md** - 整合了系统指导
  - 从项目根目录移除了冗余的 CLAUDE.md 文件
  - 所有系统指导现在集中在 `.claude/WRITER.md` 和 `scientific_writer/.claude/WRITER.md`
  - 减少混淆和维护开销

### 📝 修改的文件

- `scientific_writer/cli.py` - 增强的文件路由和用户反馈
- `scientific_writer/core.py` - 新的文件分类函数和处理逻辑
- `scientific_writer/utils.py` - 添加了 sources/ 目录扫描
- `.claude/WRITER.md` - 更新了文件路由文档
- `scientific_writer/.claude/WRITER.md` - 更新了文件路由规则

### 🎯 使用示例

```bash
# 将各种文件放在数据文件夹中
cp my_paper.tex data/           # → drafts/ (编辑模式)
cp background.pdf data/          # → sources/ (参考资料)
cp dataset.csv data/             # → data/
cp figure1.png data/             # → figures/

# 运行科学写作工具
scientific-writer

# 系统将：
# ✓ 将 .tex 路由到 drafts/ 并激活编辑模式
# ✓ 将 .pdf 复制到 sources/ 作为参考资料
# ✓ 将 .csv 复制到 data/ 文件夹
# ✓ 将 .png 复制到 figures/ 文件夹
# ✓ 为每个操作提供清晰的反馈

> "使用背景资料改进引言"
```

### 💡 核心优势

- **更佳组织** - 清楚分离手稿、源文件、数据和图像
- **可预测的行为** - 基于文件类型的一致性文件路由
- **增强的清晰性** - 用户确切知道他们的文件将去往何处
- **改进的工作流** - 更容易管理包含多种文件类型的复杂项目
- **更好的上下文** - 参考资料与可编辑内容清楚分离

---

## [2.3.2] - 2025-11-06

### 🔧 改进

- 包维护和版本更新

---

## [2.3.1] - 2025-11-05

### 🔧 改进

- 包维护和版本更新

---

## [2.3.0] - 2025-11-04

### ✨ 新增

#### 手稿编辑工作流

- **自动编辑模式检测** - 基于文件类型的智能文件路由
  - 手稿文件（`.tex`、`.md`、`.docx`、`.pdf`）自动复制到 `drafts/` 文件夹
  - 图像文件路由到 `figures/` 文件夹
  - 数据文件路由到 `data/` 文件夹
  - 系统将 drafts/ 中的手稿视为编辑任务，而不是从头创建
  
- **编辑模式上下文** - 清晰的反馈和说明
  - 当检测到手稿时，显示突出的 `⚠️ 编辑模式` 警告
  - 助手收到明确的指示以编辑现有手稿
  - CLI 输出中包含 `[编辑模式]` 视觉指示器
  - 进度消息单独显示手稿文件计数
  
- **增强的文件处理** - 改进的数据文件处理
  - `core.py` 中新增 `get_manuscript_extensions()` 函数
  - 更新了 `process_data_files()` 以处理三种文件类别
  - 更新了 `create_data_context_message()`，包含编辑模式检测
  - 在 processed_info 字典中单独跟踪手稿文件

### 🔧 改进

- **系统指导（WRITER.md）** - 添加了全面的手稿编辑工作流部分
  - 清晰的指示，处理来自数据文件夹的手稿文件
  - 按文件类型定义的文件路由规则
  - 为助手提供了详细的编辑工作流
  - 演示工作流的示例场景
  
- **CLI 用户体验** - 更好地了解文件处理
  - 欢迎消息解释了手稿文件的路由
  - 文件处理显示手稿、数据和图像的单独计数
  - 帮助文本更新，包含手稿编辑信息
  - 整个过程中保持一致的 `[编辑模式]` 指示器
  
- **API 进度更新** - 增强程序化模式下的反馈
  - 进度消息单独报告手稿文件
  - 当手稿复制到 drafts/ 时提供清晰指示
  - 更好地跟踪文件处理阶段

### 📝 修改的文件

- `scientific_writer/.claude/WRITER.md` - 添加了“关键：手稿编辑工作流”部分
- `scientific_writer/core.py` - 添加了手稿检测和路由逻辑
- `scientific_writer/cli.py` - 更新了 UI 以显示编辑模式指示器
- `scientific_writer/api.py` - 增强了手稿文件的进度报告

### 🎯 使用示例

```bash
# 将手稿文件放在数据文件夹中
cp my_paper.tex data/

# 运行科学写作工具
scientific-writer

# 系统将：
# ✓ 检测 my_paper.tex 为手稿文件
# ✓ 将其复制到 drafts/ 文件夹（而不是 data/）
# ✓ 显示 [编辑模式] 指示器
# ✓ 将任务视为编辑，而不是创建

> "改进引言并增加 5 条引用"
```

---

## [2.2.1] - 2025-11-04

### 🔧 改进

- 小错误修复和稳定性改进
- 文档更新
- 增强的错误处理

---

## [2.2.0] - 2025-11-04

### ✨ 新增

#### 新技能和功能

- **临床报告技能** - 全面的临床文档系统
  - 四种主要报告类型：病例报告、诊断报告、临床试验报告、患者记录
  - 符合 CARE 标准的病例报告，用于期刊发表
  - 诊断报告（影像学/ACR、病理学/CAP、实验室/CLSI）
  - 临床试验文档（SAE 报告、遵循 ICH-E3 的 CSR）
  - 患者临床记录（SOAP、H&P、出院小结、会诊记录）
  - 基于行业标准的 12 个专业模板
  - 8 个全面参考指南（每篇 570-745 行）
  - 8 个验证和自动化 Python 脚本
  - HIPAA 合规性和去标识化工具
  - 法规合规性（FDA 21 CFR Part 11、ICH-GCP）
  - 医学术语标准（SNOMED-CT、LOINC、ICD-10、CPT）
  - 质量保证检查清单
  - 与科学写作和同行评审技能的集成

### 🔧 改进

- 增强的医学和临床文档能力
- 文档生成从学术论文扩展到临床环境
- 添加了医疗法规合规性功能
- 改进的模板库，包含行业标准医学格式

### 📝 文档

- 更新了 README.md，将临床报告纳入文档生成
- 更新了 docs/SKILLS.md，包含全面的临床报告技能文档
- 更新了 docs/FEATURES.md，包含临床报告示例
- 添加了 clinical-reports/README.md 快速入门指南

---

## [2.1.0] - 2025-11-01

### ✨ 新增

#### 新技能

- **引文管理技能** - 高级的引文质量控制体系
  - 验证所有引文元数据的完整性和准确性
  - 检查正确的作者姓名、标题、期刊、DOI 和 URL
  - 减少 AI 生成参考文献时的幻觉
  - 确保引文符合发表标准
  - 帮助避免因引文问题被直接退稿

- **投稿模板技能** - 全面的学术投稿模板
  - 期刊模板（Nature、Science、Cell、PNAS 等）
  - 会议模板（NeurIPS、ICML、CVPR、ACL 等）
  - 带有特定投稿尺寸和样式的海报模板
  - 基金申请书模板（NSF、NIH、DOE、DARPA）
  - 特定投稿的格式指南和要求
  - 包含投稿最佳实践的参考文档
  - 常见投稿渠道的示例使用脚本

### 🔧 改进

- 通过自动元数据验证提高了引文准确性
- 通过即用型模板简化了学术投稿工作流
- 更好地支持多种出版渠道和格式

### 📝 文档

- 添加了引文管理工作流的全面文档
- 包含了投稿模板示例和使用指南
- 更新了技能文档，反映新功能

---

## [2.0.1] - 2025-10-30

### 📝 文档更新

#### 新增
- **[FEATURES.md](docs/FEATURES.md)** - 全面的功能指南，涵盖：
  - 文档生成（论文、海报、基金、综述、示意图）
  - AI 驱动的功能（研究查找、同行评审、迭代编辑）
  - 智能论文检测系统
  - 数据和文件集成工作流
  - 使用 MarkItDown 进行文档转换
  - 开发者功能和 API 模式

#### 增强
- **README.md** - 重新组织并改进了功能亮点：
  - 分类功能（文档生成、AI 能力、开发者工具）
  - 扩展了 CLI 和 API 使用示例
  - 添加了常见用例的工作流示例
  - 使用表情符号和章节更好地视觉组织
  
- **API.md** - 添加了高级文档：
  - 研究查找的设置和使用
  - 数据文件处理细节
  - 智能论文检测说明
  - 自定义输出组织模式
  - 元数据提取示例
  - 进度监控模式（进度条、基于阶段、日志）
  - 多论文生成（顺序和并行）
  
- **文档组织** - 重构为：
  - 用户指南（功能、API、技能、故障排除）
  - 开发者资源（开发、发布、变更日志、系统指导）

### 关键亮点

此更新显著提升了以下方面的文档覆盖：
- ✨ **研究查找** - 使用 Perplexity Sonar Pro 实时文献搜索
- ✨ **智能论文检测** - CLI 中的自动上下文跟踪
- ✨ **基金申请书** - NSF、NIH、DOE、DARPA 及其特定机构指导
- ✨ **科学示意图** - CONSORT 图表、电路、通路
- ✨ **文档转换** - 使用 MarkItDown 转换 15+ 种格式
- ✨ **ScholarEval 框架** - 八维论文定量评估

---

## [2.0.0] - 2025-10-28

### 🎉 重要发布：程序化 API

此版本将 Scientific Writer 从纯 CLI 工具转变为一个完整的 Python 包，同时具备程序化 API 和 CLI 接口。

### ✨ 新增

#### 程序化 API
- **新的 `generate_paper()` 异步函数** - 在您自己的 Python 代码中以程序化方式生成论文
- **实时进度更新** - 异步生成器在执行期间产生进度信息
- **全面的 JSON 结果** - 完整的论文元数据、文件路径、引用等
- **全面的类型提示** - 全类型注释，提供更好的 IDE 支持和开发体验
- **灵活配置** - 覆盖 API 密钥、输出目录、模型等

#### 包结构
- **模块化架构** - 清晰地分成 `api.py`、`cli.py`、`core.py`、`models.py`、`utils.py`
- **适当的 Python 包** - 可通过 pip/uv 安装，带有入口点
- **数据模型** - `ProgressUpdate`、`PaperResult`、`PaperMetadata`、`PaperFiles` 数据类

#### 文档
- **[API_REFERENCE.md](API_REFERENCE.md)** - 完整的 API 文档及示例
- **[MIGRATION_GUIDE.md](MIGRATION_GUIDE.md)** - 从 v1.x 升级的指南
- **[example_api_usage.py](example_api_usage.py)** - 实用代码示例
- **更新的 README** - API 和 CLI 使用的全面文档

### 🔄 变更

- **包名**：`claude-scientific-writer` → `scientific-writer`（在 pyproject.toml 中）
- **版本**：`1.1.1` → `2.0.0`
- **CLI 入口点**：现在调用 `scientific_writer.cli:cli_main` 而非独立脚本
- **文件结构**：从单个 `scientific_writer.py` 移动到包目录

### ✅ 向后兼容性

- **100% CLI 兼容** - 所有现有 CLI 命令工作方式完全相同
- **相同的输出结构** - 论文目录和文件组织方式相同
- **相同的功能** - 所有技能、工具和能力均保留
- **相同的配置** - `.env` 文件、系统指导和技能未更改

### 🗑️ 移除

- `scientific_writer.py` - 被 `scientific_writer/` 包目录取代

### 📦 包详情

**新文件结构：**
```
scientific_writer/
├── __init__.py      # 包导出和版本
├── api.py           # 异步 API 实现
├── cli.py           # CLI 界面（重构）
├── core.py          # 核心实用程序（API 密钥、指导等）
├── models.py        # API 响应的数据模型
└── utils.py         # 辅助函数（论文检测、文件扫描）
```

**公开 API 导出：**
```python
from scientific_writer import (
    generate_paper,    # 主 API 函数
    ProgressUpdate,    # 进度更新模型
    PaperResult,       # 最终结果模型
    PaperMetadata,     # 论文元数据模型
    PaperFiles,        # 论文文件模型
)
```

### 🔧 技术细节

#### API 响应格式

**进度更新：**
```json
{
  "type": "progress",
  "timestamp": "2024-10-28T14:30:22Z",
  "message": "正在编写论文章节",
  "stage": "writing",
  "percentage": 50
}
```

**最终结果：**
```json
{
  "type": "result",
  "status": "success",
  "paper_directory": "/path/to/paper_outputs/20241028_topic/",
  "paper_name": "20241028_topic",
  "metadata": {...},
  "files": {...},
  "citations": {...},
  "figures_count": 5,
  "compilation_success": true,
  "errors": []
}
```

#### 进度阶段
- `initialization` - 设置论文生成
- `research` - 进行文献研究
- `writing` - 编写论文章节
- `compilation` - 将 LaTeX 编译为 PDF
- `complete` - 完成并扫描结果

### 📝 使用示例

#### CLI（未更改）
```bash
scientific-writer
> Create a Nature paper on CRISPR gene editing
```

#### 程序化 API（新）
```python
import asyncio
from scientific_writer import generate_paper

async def main():
    async for update in generate_paper("Create a Nature paper on CRISPR"):
        if update["type"] == "progress":
            print(f"[{update['percentage']}%] {update['message']}")
        else:
            print(f"PDF: {update['files']['pdf_final']}")

asyncio.run(main())
```

### 🧪 测试

- ✅ 包导入正常工作
- ✅ API 签名验证通过
- ✅ 数据模型正确实例化
- ✅ CLI 入口点正常运作
- ✅ 所有必需文件存在
- ✅ 版本信息正确

### 📊 迁移路径

对于从 v1.x 升级的用户：
1. 拉取最新更改：`git pull origin main`
2. 重新安装：`uv sync`
3. 继续像以前一样使用 CLI，或开始使用新的 API

有关详细的迁移说明，请参阅 [MIGRATION_GUIDE.md](MIGRATION_GUIDE.md)。

### 🙏 致谢

此版本保留了 v1.x 的所有出色功能，同时为程序化使用添加了强大的新功能。现有用户的 CLI 体验保持不变。

---

## [1.1.1] - 2024-10-27

### 之前的版本
- 仅 CLI 界面
- 单个 `scientific_writer.py` 文件
- 手动会话管理
- 所有功能均按文档运行

---

**图例：**
- ✨ 新增 - 新功能
- 🔄 变更 - 现有功能的变更
- 🗑️ 移除 - 移除的功能
- 🔧 修复 - 错误修复
- 📝 文档 - 文档更改
