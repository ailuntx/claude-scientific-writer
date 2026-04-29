# 完整功能指南

**Scientific Writer 是一款深度研究与写作工具**，将 AI 驱动的深度研究能力与多种形式、格式规范的书面输出相结合。在生成任何文档之前，它都会进行全面的文献检索、验证引用并综合信息——确保你的科学写作有真实、可验证的来源作为支撑。

本指南全面概述了 Scientific Writer v2.0 中可用的全部功能。

## 目录

1. [文档生成](#document-generation)
2. [AI 驱动能力](#ai-powered-capabilities)
3. [智能论文检测](#intelligent-paper-detection)
4. [数据与文件集成](#data--file-integration)
5. [文档转换](#document-conversion)
6. [开发者功能](#developer-features)

---

## 文档生成

### 科学论文

使用正确的 IMRaD 结构，以 LaTeX 生成可直接投稿的论文。

**支持的投稿 venues：**
- **Nature, Science** - 高影响力期刊，具有特定格式要求
- **NeurIPS, ICML, ICLR** - 机器学习会议
- **IEEE, ACM** - 工程与计算机科学
- **自定义 venues** - 描述任何期刊或会议

**示例请求：**
```bash
> Create a Nature paper on CRISPR gene editing
> Write a NeurIPS paper on transformer architectures
> Generate an IEEE paper on signal processing
```

**输出结构：**
```
writing_outputs/20241030_<topic>/
├── drafts/
│   ├── v1_draft.tex
│   ├── v1_draft.pdf
│   └── v2_draft.tex
├── final/
│   ├── manuscript.tex
│   └── manuscript.pdf
├── references/
│   └── references.bib
├── figures/
│   └── *.png, *.pdf
├── data/
│   └── *.csv, *.json
└── progress.md
```

### 研究海报

使用 LaTeX beamerposter、tikzposter 或 baposter 制作专业会议海报。

**功能：**
- 全页布局，边距极小
- 配色方案与视觉设计
- 无障碍与色盲安全调色板
- 标准尺寸（A0、A1、36×48"）
- 质量控制脚本

**示例：**
```bash
> Create a conference poster about my transformer paper
> Generate an A0 poster for NeurIPS with blue color scheme
```

### 资助申请书

针对美国主要资助来源提供机构特定格式。

**支持的机构：**

| Agency | 关注领域 | 关键组成部分 |
|--------|-------------|----------------|
| **NSF** | 基础研究、教育 | Intellectual Merit + Broader Impacts |
| **NIH** | 生物医学研究 | Specific Aims（1 页）、Research Strategy |
| **DOE** | 能源、物理科学 | TRLs、成本分摊、实验室合作 |
| **DARPA** | 高风险/高回报 | Heilmeier Catechism、PM 参与 |

**示例：**
```bash
> Write an NSF proposal for quantum computing research
> Generate NIH R01 Specific Aims for cancer immunotherapy
> Create a DOE proposal for renewable energy storage
```

**主要功能：**
- 预算编制与论证
- 与评审标准对齐
- 时间线与里程碑规划
- Broader impacts 策略（NSF）
- 初步数据整合（NIH）

### 文献综述

带有引文管理的系统性文献综述。

**功能：**
- 数据库检索策略（PubMed、Web of Science）
- 引用验证与格式化
- 综合与组织
- 多种引用样式（APA、IEEE、Nature 等）

**示例：**
```bash
> Create a literature review on machine learning in healthcare
> Synthesize recent papers on quantum computing from 2023-2024
```

### 临床报告

符合监管要求的全面临床文档。

**报告类型：**
- **病例报告** - 面向医学期刊、符合 CARE 标准的报告
- **诊断报告** - 放射学、病理学、实验室报告
- **临床试验报告** - SAE 报告、Clinical Study Reports（ICH-E3）
- **患者文档** - SOAP notes、H&P、出院小结

**功能：**
- 基于行业标准的 12 种专业模板
- HIPAA 合规与去标识化工具
- 监管合规（FDA、ICH-GCP）
- 医学术语验证
- 8 个自动化验证脚本

**示例：**
```bash
> Create a clinical case report for a rare disease presentation
> Generate a radiology report template for chest CT
> Write an SAE report for clinical trial adverse event
> Create a discharge summary for heart failure patient
```

### 科学示意图

适用于出版级质量的图表和可视化。

**图表类型：**
- **CONSORT 流程图** - 临床试验参与者流程
- **电路图** - 使用 CircuitikZ 的电气原理图
- **生物通路** - 信号级联、代谢网络
- **系统架构** - 方框图、数据流
- **流程图** - 方法学图、决策树

**功能：**
- 矢量图形（TikZ/LaTeX）
- 色盲安全的 Okabe-Ito 调色板
- 使用 Python 的程序化生成
- 可直接用于发表的 PDF/SVG/PNG 输出

**示例：**
```bash
> Create a CONSORT diagram for my clinical trial
> Generate a circuit diagram for an RC low-pass filter
> Design a biological pathway showing MAPK signaling
```

---

## AI 驱动能力

### 实时研究检索

由通过 OpenRouter API 的 Perplexity Sonar Pro Search 提供支持。

**功能：**
- 在论文生成过程中进行实时互联网搜索
- 最新发表的论文与预印本
- 事实核查与验证
- 最新统计数据与信息

**设置：**
```bash
# Add to .env file
echo "OPENROUTER_API_KEY=your_key" >> .env
```

**自动使用：**
在以下情况下会自动调用研究检索：
- 你请求最新研究（例如，“2024 年的论文”）
- Claude 需要核实事实或统计数据
- 需要进行文献检索
- 提到当前事件或最新进展

**示例：**
```bash
> Create a paper on recent advances in quantum computing (2024)
# Automatically searches for latest research

> What are the current success rates for CAR-T therapy?
# Looks up latest clinical data
```

### 使用 ScholarEval 进行同行评审

基于研究的系统性定量评估框架（arXiv:2510.16234）。

**8 个评估维度：**
1. **问题表述** - 清晰度、重要性、新颖性
2. **文献综述** - 覆盖范围、综合、空缺
3. **方法学** - 严谨性、有效性、可重复性
4. **数据收集** - 质量、适当性、伦理
5. **分析** - 统计严谨性、解释
6. **结果** - 清晰度、完整性、可视化
7. **写作质量** - 结构、清晰度、语法
8. **引用** - 相关性、时效性、完整性

**评分：**
- 每个维度采用 1-5 分制
- 总体分数阈值：
  - **4.5+** - 优秀（已达到顶级投稿准备状态）
  - **4.0-4.4** - 很强（仅需小幅修改）
  - **3.5-3.9** - 良好（需要较大修改）
  - **3.0-3.4** - 可接受（需要显著修改）
  - **<3.0** - 需要大幅重做

**示例：**
```bash
> Evaluate this paper using the ScholarEval framework
> Assess publication readiness for Nature Machine Intelligence
> Review the methods section for rigor and completeness
```

### 迭代式编辑

具备上下文感知的修订建议，理解你的论文结构与内容。

**功能：**
- 保持各章节之间的一致性
- 保留你的写作风格
- 跟踪不同版本之间的变化
- 根据投稿要求提出改进建议

**示例：**
```bash
> Improve the introduction to better motivate the problem
> Make the discussion more concise
> Add transition sentences between paragraphs in the results
```

---

## 智能论文检测

无需指定路径，即可自动识别你在引用现有论文。

### 工作原理

系统会分析你的输入，识别以下内容：
1. **继续关键词**："continue"、"update"、"edit"、"the paper"
2. **搜索关键词**："find"、"look for"、"show me"、"where is"
3. **主题匹配**：来自论文目录名称的关键词
4. **时间上下文**：在语义模糊时默认使用最近的论文

### 继续关键词

自动恢复对当前或最近论文的处理：

```bash
> continue
> update the paper
> edit my paper
> add a conclusion section
> fix the references
> compile the poster
> generate the PDF
```

### 搜索关键词

按主题查找特定论文：

```bash
> find the acoustics paper
> look for the quantum computing paper
> show me the CRISPR paper
> where is the transformer paper
```

### 主题匹配

根据目录名称进行匹配（格式：`YYYYMMDD_HHMMSS_topic`）：

```bash
# 找到 20241027_090109_acoustics_vinayak_agarwal/
> update the acoustics paper

# 找到 20251029_130950_transformers_ai_paper/
> continue working on the transformers paper
```

### 开始新论文

明确从头开始：

```bash
> new paper on climate change
> start fresh with a different topic
> create a new paper about quantum computing
```

---

## 数据与文件集成

### 自动数据处理

只需将文件放入项目根目录的 `data/` 文件夹。

**文件路由：**
- **图片**（png、jpg、svg 等）→ `figures/`
- **数据文件**（csv、json、txt、xlsx）→ `data/`
- **原始文件** 在复制后会自动删除

**支持的图片格式：**
`.png`、`.jpg`、`.jpeg`、`.gif`、`.bmp`、`.tiff`、`.svg`、`.webp`、`.ico`

**示例流程：**
```bash
# 1. 复制你的文件
cp experiment_results.csv ~/Documents/claude-scientific-writer/data/
cp performance_graph.png ~/Documents/claude-scientific-writer/data/

# 2. 启动 CLI
scientific-writer

# 3. 系统会自动检测并处理文件
> Create a paper analyzing the experimental results
# ✓ Files copied to paper's data/ and figures/
# ✓ Original files deleted from data/
```

### 程序化数据文件

使用 API 显式指定数据文件：

```python
async for update in generate_paper(
    query="Analyze the experimental results",
    data_files=[
        "./experiment_results.csv",
        "./figures/performance.png",
        "./supplementary_data.json"
    ]
):
    # Files are processed and included
    pass
```

**注意：** 使用 API 时，出于安全考虑，原始文件**不会**被删除。

### 文件上下文

所有包含的文件都会：
- 复制到相应目录
- 作为上下文提供给 Claude
- 可在论文中引用
- 在数据文件消息中列出

---

## 文档转换

### MarkItDown - 通用文件转换器

将 15+ 种文件格式转换为 Markdown，以便 LLM 处理。

**支持的格式：**
- **文档**：PDF、DOCX、PPTX、XLSX
- **媒体**：图片（带 AI 描述）、音频（转录）
- **Web**：HTML、YouTube（视频转录）
- **数据**：CSV、JSON、XML
- **代码**：多种编程语言

**功能：**
- 使用先进视觉模型生成 AI 增强的图片描述
- 针对扫描文档的 OCR
- 音频转文本
- 支持并行执行的批处理
- 科学文献元数据提取

**示例：**
```bash
> Convert all PDFs in the literature folder to Markdown
> Extract data from this Excel spreadsheet
> Transcribe the interview audio file
> Convert this PowerPoint to Markdown with AI descriptions
```

### 文档操作

#### DOCX（Word 文档）
- 以编程方式创建和编辑 Word 文档
- 管理批注和修订记录
- 验证文档结构
- 使用模板

#### PDF 文档
- 提取文本和元数据
- 分析 PDF 布局和边界框
- 填写 PDF 表单
- 将 PDF 转换为图片

#### PPTX（PowerPoint）
- 创建和修改演示文稿
- 将 HTML 转换为 PowerPoint
- 生成缩略图
- 管理幻灯片和布局

#### XLSX（Excel）
- 读取和写入 Excel 文件
- 重新计算公式
- 处理复杂的电子表格操作

---

## 开发者功能

### 程序化 API

完整的异步 Python API，带有全面的类型提示。

**核心函数：**
```python
from scientific_writer import generate_paper

async def generate_paper(
    query: str,
    output_dir: Optional[str] = None,
    api_key: Optional[str] = None,
    model: str = "claude-sonnet-4-6",
    data_files: Optional[List[str]] = None,
    cwd: Optional[str] = None,
) -> AsyncGenerator[Dict[str, Any], None]
```

**类型安全模型：**
```python
from scientific_writer import (
    ProgressUpdate,  # 进度信息
    PaperResult,     # 包含所有论文信息的最终结果
    PaperMetadata,   # 论文元数据（标题、日期、字数）
    PaperFiles,      # 所有文件路径（PDF、TeX、BibTeX 等）
)
```

### 进度流式输出

生成过程中的实时更新：

```python
async for update in generate_paper("Create a paper"):
    if update["type"] == "progress":
        # 进度更新
        stage = update["stage"]        # initialization|research|writing|compilation|complete
        message = update["message"]    # Human-readable message
        details = update.get("details")  # Optional: tool name, files created, etc.
        
        print(f"[{stage}] {message}")
```

### 完整结果

最终结果包括生成论文的全部信息：

```python
if update["type"] == "result":
    # 状态
    status = update["status"]  # success|partial|failed
    
    # 文件
    pdf = update["files"]["pdf_final"]
    tex = update["files"]["tex_final"]
    bib = update["files"]["bibliography"]
    figures = update["files"]["figures"]  # List of figure paths
    
    # 元数据
    title = update["metadata"]["title"]
    word_count = update["metadata"]["word_count"]
    
    # 引用
    citation_count = update["citations"]["count"]
    
    # 编译
    compiled = update["compilation_success"]
    
    # 错误（如有）
    errors = update["errors"]
```

### 错误处理

优雅的错误处理与详细信息：

```python
try:
    async for update in generate_paper(query):
        if update["type"] == "result":
            if update["status"] == "failed":
                print(f"Errors: {update['errors']}")
            elif update["status"] == "partial":
                print("TeX created but PDF compilation failed")
            else:
                print("Success!")
except ValueError as e:
    print(f"Configuration error: {e}")
```

### 自定义配置

根据你的使用场景覆盖默认设置：

```python
async for update in generate_paper(
    query="Create a paper",
    output_dir="./my_custom_directory",
    api_key="sk-ant-custom-key",
    model="claude-sonnet-4-6",
    data_files=["data.csv"],
    cwd="/path/to/project"
):
    pass
```

---

## 另见

- [API Reference](API.md) - 完整 API 文档
- [Skills Overview](SKILLS.md) - 所有可用技能与能力
- [Troubleshooting](TROUBLESHOOTING.md) - 常见问题与解决方案
- [Development Guide](DEVELOPMENT.md) - 贡献与开发
- [Changelog](../CHANGELOG.md) - 版本历史与更新
