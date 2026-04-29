---
name: market-research-reports
description: "Generate comprehensive market research reports (50+ pages) in the style of top consulting firms (McKinsey, BCG, Gartner). Features professional LaTeX formatting, extensive visual generation with scientific-schematics and generate-image, deep integration with research-lookup for data gathering, and multi-framework strategic analysis including Porter's Five Forces, PESTLE, SWOT, TAM/SAM/SOM, and BCG Matrix."
allowed-tools: [Read, Write, Edit, Bash]
---

# 市场研究报告

## 概述

市场研究报告是综合性的战略文档，用于分析行业、市场和竞争格局，以支持商业决策、投资策略和战略规划。本技能可生成**50页以上的专业级报告**，包含丰富的视觉内容，模拟麦肯锡、BCG、贝恩、Gartner和Forrester等顶级咨询公司的交付成果。

**主要特点：**
- **全面的篇幅**：报告设计为50页以上，无代币限制
- **视觉丰富的内容**：开始时生成5-6个关键图表（写作过程中根据需要添加更多）
- **数据分析驱动**：与research-lookup深度集成以获取市场数据
- **多框架方法**：波特五力模型、PESTLE分析、SWOT分析、BCG矩阵、TAM/SAM/SOM
- **专业格式**：咨询公司质量的排版、配色和布局
- **可操作的建议**：以战略为重点，包含实施路线图

**输出格式：** 带有专业样式的LaTeX，编译为PDF。使用`market_research.sty`样式包来实现一致、专业的格式。

## 何时使用此技能

在以下情况下应使用此技能：
- 为投资决策创建全面的市场分析
- 为战略规划开发行业报告
- 分析竞争格局和市场动态
- 进行市场规模计算（TAM/SAM/SOM）
- 评估市场进入机会
- 为并购活动准备尽职调查材料
- 创建行业定位的思想领导力内容
- 开发进入市场策略文档
- 分析监管和政策对市场的影响
- 为新产品发布建立商业案例

## 视觉增强要求

**关键：市场研究报告应包含关键视觉内容。**

每份报告应在开始时生成**6个核心视觉元素**，并在写作过程中根据需要添加额外的视觉元素。首先从最关键的可视化开始，以建立报告框架。

### 视觉生成工具

**使用`scientific-schematics`：**
- 市场增长轨迹图表
- TAM/SAM/SOM分解图（同心圆）
- 波特五力模型图
- 竞争定位矩阵
- 市场细分图表
- 价值链图表
- 技术路线图
- 风险热力图
- 战略优先级矩阵
- 实施时间表/甘特图
- SWOT分析图
- BCG增长-份额矩阵

```bash
# Example: Generate a TAM/SAM/SOM diagram
python skills/scientific-schematics/scripts/generate_schematic.py \
  "TAM SAM SOM concentric circle diagram showing Total Addressable Market $50B outer circle, Serviceable Addressable Market $15B middle circle, Serviceable Obtainable Market $3B inner circle, with labels and arrows pointing to each segment" \
  -o figures/tam_sam_som.png --doc-type report

# Example: Generate Porter's Five Forces
python skills/scientific-schematics/scripts/generate_schematic.py \
  "Porter's Five Forces diagram with center box 'Competitive Rivalry' connected to four surrounding boxes: 'Threat of New Entrants' (top), 'Bargaining Power of Suppliers' (left), 'Bargaining Power of Buyers' (right), 'Threat of Substitutes' (bottom). Each box should show High/Medium/Low rating" \
  -o figures/porters_five_forces.png --doc-type report
```

**使用`generate-image`：**
- 执行摘要英雄信息图表
- 行业/部门概念插图
- 抽象技术可视化
- 封面图像

```bash
# Example: Generate executive summary infographic
python skills/generate-image/scripts/generate_image.py \
  "Professional executive summary infographic for market research report, showing key metrics in modern data visualization style, blue and green color scheme, clean minimalist design with icons representing market size, growth rate, and competitive landscape" \
  --output figures/executive_summary.png
```

### 按部分推荐的可视化元素（根据需要生成）

| 部分 | 优先级可视化 | 可选可视化 |
|---------|-----------------|------------------|
| 执行摘要 | 执行摘要信息图表（开始） | - |
| 市场规模与增长 | 增长轨迹（开始），TAM/SAM/SOM（开始） | 区域分解，增长细分 |
| 竞争格局 | 波特五力（开始），定位矩阵（开始） | 市场份额图表，战略群体 |
| 风险分析 | 风险热力图（开始） | 缓解矩阵 |
| 战略建议 | 机会矩阵 | 优先级框架 |
| 实施路线图 | 时间表/甘特图 | 里程碑追踪 |
| 投资论题 | 财务预测 | 情景分析 |

**从6个优先级可视化开始**（如上标记为开始），然后在撰写特定部分需要视觉支持时生成额外的可视化。

---

## 报告结构（50+页）

### 前面部分（约5页）

#### 封面页（1页）
- 报告标题和副标题
- 英雄可视化（已生成）
- 日期和分类
- 准备对象/准备人

#### 目录（1-2页）
- 从LaTeX自动生成
- 图表目录
- 表格目录

#### 执行摘要（2-3页）
- **市场概览框**：关键指标一览
- **投资论题**：3-5点摘要
- **主要发现**：重大发现和见解
- **战略建议**：前3-5个可操作建议
- **执行摘要信息图表**：报告亮点的视觉综合

---

### 核心分析（约35页）

#### 第1章：市场概述与定义（4-5页）

**内容要求：**
- 市场定义和范围
- 行业生态系统映射
- 主要利益相关者及其角色
- 市场边界和相邻领域
- 历史背景和演变

**必需可视化（2）：**
1. 市场生态系统/价值链图
2. 行业结构图

**关键数据点：**
- 市场定义标准
- 包含/排除的细分
- 地理范围
- 分析时间范围

---

#### 第2章：市场规模与增长分析（6-8页）

**内容要求：**
- 可寻址市场总量（TAM）计算
- 可服务市场（SAM）定义
- 可服务可获得市场（SOM）估算
- 历史增长分析（5-10年）
- 增长预测（未来5-10年）
- 增长驱动因素和抑制因素
- 区域市场分解
- 细分层面分析

**必需可视化（4）：**
1. 市场增长轨迹图表（历史+预测）
2. TAM/SAM/SOM同心圆图
3. 区域市场分解（饼图或树图）
4. 细分增长比较（柱状图）

**关键数据点：**
- 当前市场规模（含来源）
- CAGR（历史和预测）
- 按地区市场规模
- 按细分市场规模
- 预测的关键假设

**数据来源：**
使用`research-lookup`查找：
- 市场研究报告（Gartner、Forrester、IDC等）
- 行业协会数据
- 政府统计
- 公司财务报告
- 学术研究

---

#### 第3章：行业驱动因素与趋势（5-6页）

**内容要求：**
- 宏观经济因素
- 技术趋势
- 监管驱动因素
- 社会和人口变化
- 环境因素
- 行业特定趋势

**分析框架：**
- **PESTLE分析**：政治、经济、社会、技术、法律、环境
- **趋势影响评估**：可能性与影响矩阵

**必需可视化（3）：**
1. 行业趋势时间表或雷达图
2. 驱动因素影响矩阵
3. PESTLE分析图

**关键数据点：**
- 前5-10个增长驱动因素及量化影响
- 新兴趋势及时间线
- 颠覆性因素

---

#### 第4章：竞争格局（6-8页）

**内容要求：**
- 市场结构分析
- 主要参与者档案
- 市场份额分析
- 竞争定位
- 进入壁垒
- 竞争动态

**分析框架：**
- **波特五力模型**：全面的行业分析
- **竞争定位矩阵**：关键维度的2x2矩阵
- **战略群体映射**：按策略对竞争对手进行聚类

**必需可视化（4）：**
1. 波特五力模型图
2. 市场份额饼图或柱状图
3. 竞争定位矩阵（2x2）
4. 战略群体图

**关键数据点：**
- 按公司市场份额（前10名）
- 竞争强度评级
- 进入壁垒评估
- 供应商/买家议价能力评估

---

#### 第5章：客户分析与细分（4-5页）

**内容要求：**
- 客户细分定义
- 细分规模与增长
- 购买行为分析
- 客户需求和痛点
- 决策过程
- 按细分的价值驱动因素

**分析框架：**
- **客户细分矩阵**：规模与增长
- **价值主张画布**：工作、痛点、收益
- **客户旅程映射**：认知到倡导

**必需可视化（3）：**
1. 客户细分分解（饼图/树图）
2. 细分吸引力矩阵
3. 客户旅程或价值主张图

**关键数据点：**
- 细分规模和百分比
- 按细分增长率
- 平均交易规模/每位客户收入
- 按细分的客户获取成本

---

#### 第6章：技术与创新格局（4-5页）

**内容要求：**
- 当前技术栈
- 新兴技术
- 创新趋势
- 技术采用曲线
- 研发投资分析
- 专利格局

**分析框架：**
- **技术就绪评估**：TRL级别
- **技术成熟度周期定位**：技术所处的位置
- **技术路线图**：随时间的演变

**必需可视化（2）：**
1. 技术路线图
2. 创新/采用曲线或技术成熟度周期

**关键数据点：**
- 行业研发支出
- 关键技术里程碑
- 专利申请趋势
- 技术采用率

---

#### 第7章：监管与政策环境（3-4页）

**内容要求：**
- 当前监管框架
- 主要监管机构
- 合规要求
- 即将到来的监管变化
- 政策趋势
- 影响评估

**必需可视化（1）：**
1. 监管时间表或框架图

**关键数据点：**
- 关键法规及生效日期
- 合规成本
- 监管风险
- 政策变化可能性

---

#### 第8章：风险分析（3-4页）

**内容要求：**
- 市场风险
- 竞争风险
- 监管风险
- 技术风险
- 运营风险
- 财务风险
- 风险缓解策略

**分析框架：**
- **风险热力图**：可能性与影响
- **风险登记册**：全面的风险清单
- **缓解矩阵**：风险与缓解策略

**必需可视化（2）：**
1. 风险热力图（可能性与影响）
2. 风险缓解矩阵

**关键数据点：**
- 前10个风险及评级
- 风险可能性得分
- 影响严重程度得分
- 缓解成本估算

---

### 战略建议（约10页）

#### 第9章：战略机会与建议（4-5页）

**内容要求：**
- 机会识别
- 机会规模
- 战略选项分析
- 优先级框架
- 详细建议
- 成功因素

**分析框架：**
- **机会吸引力矩阵**：吸引力与获胜能力
- **战略选项框架**：构建、购买、合作伙伴、忽视
- **优先级矩阵**：影响与努力

**必需可视化（3）：**
1. 机会矩阵
2. 战略选项框架
3. 优先级/建议矩阵

**关键数据点：**
- 机会规模
- 投资需求
- 预期回报
- 价值实现时间

---

#### 第10章：实施路线图（3-4页）

**内容要求：**
- 分阶段实施计划
- 关键里程碑和交付物
- 资源需求
- 时间和顺序
- 依赖关系和关键路径
- 治理结构

**必需可视化（2）：**
1. 实施时间表/甘特图
2. 里程碑追踪或阶段图

**关键数据点：**
- 阶段持续时间
- 资源需求
- 关键里程碑及日期
- 按阶段预算分配

---

#### 第11章：投资论题与财务预测（3-4页）

**内容要求：**
- 投资摘要
- 财务预测
- 情景分析
- 回报预期
- 关键假设
- 敏感性分析

**必需可视化（2）：**
1. 财务预测图表（收入、增长）
2. 情景分析比较

**关键数据点：**
- 收入预测（3-5年）
- CAGR预测
- ROI/IRR预期
- 关键财务假设

---

### 后面部分（约5页）

#### 附录A：方法论与数据来源（1-2页）
- 研究方法论
- 数据收集方法
- 数据来源和引用
- 局限性和假设

#### 附录B：详细市场数据表（2-3页）
- 综合市场数据表
- 区域分解
- 细分详情
- 历史数据序列

#### 附录C：公司档案（1-2页）
- 主要竞争对手简介
- 财务亮点
- 战略重点领域

#### 参考文献/参考书目
- 所有引用的来源
- LaTeX的BibTeX格式

---

## 工作流程

### 阶段1：研究与数据收集

**步骤1：定义范围**
- 明确市场定义
- 设定地理边界
- 确定时间范围
- 识别需要回答的关键问题

**步骤2：进行深入研究**

广泛使用`research-lookup`收集市场数据：

```bash
# Market size and growth data
python skills/research-lookup/scripts/research_lookup.py \
  "What is the current market size and projected growth rate for [MARKET] industry? Include TAM, SAM, SOM estimates and CAGR projections"

# Competitive landscape
python skills/research-lookup/scripts/research_lookup.py \
  "Who are the top 10 competitors in the [MARKET] market? What is their market share and competitive positioning?"

# Industry trends
python skills/research-lookup/scripts/research_lookup.py \
  "What are the major trends and growth drivers in the [MARKET] industry for 2024-2030?"

# Regulatory environment
python skills/research-lookup/scripts/research_lookup.py \
  "What are the key regulations and policy changes affecting the [MARKET] industry?"
```

**步骤3：数据组织**
- 创建包含研究笔记的`sources/`文件夹
- 按部分组织数据
- 识别数据缺口
- 根据需要进行后续研究

### 阶段2：分析与框架应用

**步骤4：应用分析框架**

对每个框架进行结构化分析：

- **市场规模化**：TAM → SAM → SOM，清晰假设
- **波特五力模型**：为每个力量评级高/中/低并说明理由
- **PESTLE**：分析每个维度的趋势和影响
- **SWOT**：内部优势/劣势，外部机会/威胁
- **竞争定位**：定义轴，绘制竞争对手

**步骤5：形成见解**
- 将发现综合成关键见解
- 识别战略含义
- 制定建议
- 确定机会优先级

### 阶段3：视觉生成

**步骤6：生成所有可视化**

在写报告之前生成可视化。使用批量生成脚本：

```bash
# Generate all standard market report visuals
python skills/market-research-reports/scripts/generate_market_visuals.py \
  --topic "[MARKET NAME]" \
  --output-dir figures/
```

或单独生成：

```bash
# 1. Market growth trajectory
python skills/scientific-schematics/scripts/generate_schematic.py \
  "Bar chart showing market growth from 2020 to 2034, with historical bars in dark blue (2020-2024) and projected bars in light blue (2025-2034). Y-axis shows market size in billions USD. Include CAGR annotation" \
  -o figures/01_market_growth.png --doc-type report

# 2. TAM/SAM/SOM breakdown
python skills/scientific-schematics/scripts/generate_schematic.py \
  "TAM SAM SOM concentric circles diagram. Outer circle TAM Total Addressable Market, middle circle SAM Serviceable Addressable Market, inner circle SOM Serviceable Obtainable Market. Each labeled with acronym and description. Blue gradient" \
  -o figures/02_tam_sam_som.png --doc-type report

# 3. Porter's Five Forces
python skills/scientific-schematics/scripts/generate_schematic.py \
  "Porter's Five Forces diagram with center box 'Competitive Rivalry' connected to four surrounding boxes: Threat of New Entrants (top), Bargaining Power of Suppliers (left), Bargaining Power of Buyers (right), Threat of Substitutes (bottom). Color code by rating: High=red, Medium=yellow, Low=green" \
  -o figures/03_porters_five_forces.png --doc-type report

# 4. Competitive positioning matrix
python skills/scientific-schematics/scripts/generate_schematic.py \
  "2x2 competitive positioning matrix with X-axis 'Market Focus (Niche to Broad)' and Y-axis 'Solution Approach (Product to Platform)'. Plot 8-10 competitors as labeled circles of varying sizes. Include quadrant labels" \
  -o figures/04_competitive_positioning.png --doc-type report

# 5. Risk heatmap
python skills/scientific-schematics/scripts/generate_schematic.py \
  "Risk heatmap matrix. X-axis Impact (Low to Critical), Y-axis Probability (Unlikely to Very Likely). Color gradient: Green (low risk) to Red (critical risk). Plot 10-12 risks as labeled points" \
  -o figures/05_risk_heatmap.png --doc-type report

# 6. (Optional) Executive summary infographic
python skills/generate-image/scripts/generate_image.py \
  "Professional executive summary infographic for market research report, modern data visualization style, blue and green color scheme, clean minimalist design" \
  --output figures/06_exec_summary.png
```

### 阶段4：报告撰写

**步骤7：初始化项目结构**

创建标准项目结构：

```
writing_outputs/YYYYMMDD_HHMMSS_market_report_[topic]/
├── progress.md
├── drafts/
│   └── v1_market_report.tex
├── references/
│   └── references.bib
├── figures/
│   └── [all generated visuals]
├── sources/
│   └── [research notes]
└── final/
```

**步骤8：使用模板撰写报告**

使用`market_report_template.tex`作为起点。按照结构指南撰写每个部分，确保：

- **全面覆盖**：每个小节都有涉及
- **数据驱动的内容**：声明有研究支持
- **视觉整合**：引用所有生成的图表
- **专业的语气**：咨询风格的写作
- **无代币限制**：完整撰写，不要缩写

**写作指南：**
- 尽可能使用主动语态
- 以见解开头，数据支持
- 建议使用编号列表
- 所有统计数据都包含数据来源
- 部分之间过渡流畅

### 阶段5：编译与审查

**步骤9：编译LaTeX**

```bash
cd writing_outputs/[project_folder]/drafts/
xelatex v1_market_report.tex
bibtex v1_market_report
xelatex v1_market_report.tex
xelatex v1_market_report.tex
```

**步骤10：质量审查**

验证报告是否符合质量标准：

- [ ] 总页数达到50页以上
- [ ] 所有必要的可视化（5-6个核心+任何额外的）都已包含并正确渲染
- [ ] 执行摘要捕捉了关键发现
- [ ] 所有数据点都有引用的来源
- [ ] 分析框架应用正确
- [ ] 建议是可操作的且已确定优先级
- [ ] 没有孤立的图表或表格
- [ ] 目录、图表目录、表格目录准确
- [ ] 参考文献完整
- [ ] PDF渲染无错误

**步骤11：同行评审**

使用同行评审技能评估报告：
- 评估全面性
- 验证数据准确性
- 检查逻辑流程
- 评估建议质量

---

## 质量标准

### 页数目标

| 部分 | 最少页数 | 目标页数 |
|---------|---------------|--------------|
| 前面部分 | 4 | 5 |
| 市场概述 | 4 | 5 |
| 市场规模与增长 | 5 | 7 |
| 行业驱动因素 | 4 | 6 |
| 竞争格局 | 5 | 7 |
| 客户分析 | 3 | 5 |
| 技术格局 | 3 | 5 |
| 监管环境 | 2 | 4 |
| 风险分析 | 2 | 4 |
| 战略建议 | 3 | 5 |
| 实施路线图 | 2 | 4 |
| 投资论题 | 2 | 4 |
| 后面部分 | 4 | 5 |
| **总计** | **43** | **66** |

### 视觉质量要求

- **分辨率**：所有图像最低300 DPI
- **格式**：栅格图像用PNG，矢量图用PDF
- **无障碍**：色盲友好的调色板
- **一致性**：整个报告使用相同的配色方案
- **标注**：所有轴、图例和数据点都有标注
- **来源归属**：图表说明中标明来源

### 数据质量要求

- **时效性**：数据不超过2年（最好使用今年）
- **来源**：所有统计数据归因于特定来源
- **验证**：可能时交叉核对多个来源
- **假设**：所有预测说明底层假设
- **局限性**：承认数据局限性和差距

### 写作质量要求

- **客观性**：呈现平衡的分析，承认不确定性
- **清晰性**：避免行话，定义技术术语
- **精确性**：使用具体数字而非模糊的限定词
- **结构**：清晰的标题，逻辑流畅，过渡顺畅
- **可操作性**：建议具体且可实施

---

## LaTeX格式

### 使用样式包

`market_research.sty`包提供专业格式。在文档中包含它：

```latex
\documentclass[11pt,letterpaper]{report}
\usepackage{market_research}
```

### 盒子环境

使用彩色盒子突出关键内容：

```latex
% Key insight box (blue)
\begin{keyinsightbox}[Key Finding]
The market is projected to grow at 15.3% CAGR through 2030.
\end{keyinsightbox}

% Market data box (green)
\begin{marketdatabox}[Market Snapshot]
\begin{itemize}
    \item Market Size (2024): \$45.2B
    \item Projected Size (2030): \$98.7B
    \item CAGR: 15.3%
\end{itemize}
\end{marketdatabox}

% Risk box (orange/warning)
\begin{riskbox}[Critical Risk]
Regulatory changes could impact 40% of market participants.
\end{riskbox}

% Recommendation box (purple)
\begin{recommendationbox}[Strategic Recommendation]
Prioritize market entry in the Asia-Pacific region.
\end{recommendationbox}

% Callout box (gray)
\begin{calloutbox}[Definition]
TAM (Total Addressable Market) represents the total revenue opportunity.
\end{calloutbox}
```

### 图表格式

```latex
\begin{figure}[htbp]
centering
includegraphics[width=0.9\textwidth]{../figures/market_growth.png}
caption{Market Growth Trajectory (2020-2030). Source: Industry analysis, company data.}
\label{fig:market_growth}
\end{figure}
```

### 表格格式

```latex
begin{table}[htbp]
centering
caption{Market Size by Region (2024)}
begin{tabular}{@{}lrrr@{}}
toprule
textbf{Region} & textbf{Size (USD)} & textbf{Share} & textbf{CAGR} \
midrule
North America & $18.2B & 40.3% & 12.5% \
rowcolor{tablealt} Europe & $12.1B & 26.8% & 14.2% \
Asia-Pacific & $10.5B & 23.2% & 18.7% \
rowcolor{tablealt} Rest of World & $4.4B & 9.7% & 11.3% \
midrule
textbf{Total} & textbf{$45.2B} & textbf{100%} & textbf{15.3%} \
bottomrule
end{tabular}
label{tab:market_by_region}
end{table}
```

有关完整格式参考，请参阅`assets/FORMATTING_GUIDE.md`。

---

## 与其他技能的集成

此技能与以下技能协同工作：

- **research-lookup**：对于收集市场数据、统计信息和竞争情报至关重要
- **scientific-schematics**：生成所有图表、图表和可视化
- **venue-templates**：在研究发表时提供学术出版写作风格指导

**出版写作风格：** 当市场研究成果在学术期刊发表时，请参阅**venue-templates**技能获取涵盖Nature/Science、Cell Press、医学期刊和ML/CS会议的写作风格指南。
- **generate-image**：创建信息图表和概念插图
- **peer-review**：评估报告质量和完整性
- **citation-management**：管理BibTeX参考文献

---

## 示例提示

### 市场概述部分

```
Write a comprehensive market overview section for the [Electric Vehicle Charging Infrastructure] market. Include:
- Clear market definition and scope
- Industry ecosystem with key stakeholders
- Value chain analysis
- Historical evolution of the market
- Current market dynamics

Generate 2 supporting visuals using scientific-schematics.
```

### 竞争格局部分

```
Analyze the competitive landscape for the [Cloud Computing] market. Include:
- Porter's Five Forces analysis with High/Medium/Low ratings
- Top 10 competitors with market share
- Competitive positioning matrix
- Strategic group mapping
- Barriers to entry analysis

Generate 4 supporting visuals including Porter's Five Forces diagram and positioning matrix.
```

### 战略建议部分

```
Develop strategic recommendations for entering the [Renewable Energy Storage] market. Include:
- 5-7 prioritized recommendations
- Opportunity sizing for each
- Implementation considerations
- Risk factors and mitigations
- Success criteria

Generate 3 supporting visuals including opportunity matrix and priority framework.
```

---

## 验证清单：50+页验证

在最终确定报告之前，验证：

### 结构完整性
- [ ] 带英雄视觉的封面页
- [ ] 目录（自动生成）
- [ ] 图表目录（自动生成）
- [ ] 表格目录（自动生成）
- [ ] 执行摘要（2-3页）
- [ ] 所有11个核心章节都存在
- [ ] 附录A：方法论
- [ ] 附录B：数据表
- [ ] 附录C：公司档案
- [ ] 参考文献/参考书目

### 视觉完整性（核心5-6）
- [ ] 市场增长轨迹图表（优先级1）
- [ ] TAM/SAM/SOM图（优先级2）
- [ ] 波特五力（优先级3）
- [ ] 竞争定位矩阵（优先级4）
- [ ] 风险热力图（优先级5）
- [ ] 执行摘要信息图表（优先级6，可选）

### 额外可视化（根据需要生成）
- [ ] 市场生态系统图
- [ ] 区域分解图表
- [ ] 细分增长图表
- [ ] 行业趋势/PESTLE图
- [ ] 市场份额图表
- [ ] 客户细分图表
- [ ] 技术路线图
- [ ] 监管时间表
- [ ] 机会矩阵
- [ ] 实施时间表
- [ ] 财务预测图表
- [ ] 其他部分特定的可视化

### 内容质量
- [ ] 所有统计数据都有来源
- [ ] 预测包含假设
- [ ] 框架正确应用
- [ ] 建议可操作
- [ ] 写作质量专业
- [ ] 无占位符或不完整部分

### 技术质量
- [ ] PDF编译无错误
- [ ] 所有图表正确渲染
- [ ] 交叉引用有效
- [ ] 参考文献完整
- [ ] 页数超过50

---

## 资源

### 参考文件

加载这些文件以获取详细指导：

- **`references/report_structure_guide.md`**：详细的逐部分内容要求
- **`references/visual_generation_guide.md`**：生成所有可视化类型的完整提示
- **`references/data_analysis_patterns.md`**：波特、PESTLE、SWOT等的模板

### 资产

- **`assets/market_research.sty`**：LaTeX样式包
- **`assets/market_report_template.tex`**：完整的LaTeX模板
- **`assets/FORMATTING_GUIDE.md`**：盒子环境和样式的快速参考

### 脚本

- **`scripts/generate_market_visuals.py`**：批量生成所有报告可视化

---

## 故障排除

### 常见问题

**问题**：报告不足50页
- **解决方案**：扩展附录中的数据表，添加更详细的公司档案，包含额外的区域分解

**问题**：可视化不渲染
- **解决方案**：检查LaTeX中的文件路径，确保图像在figures/文件夹中，验证文件扩展名

**问题**：参考文献缺少条目
- **解决方案**：在第一次xelatex后运行bibtex，检查.bib文件的语法错误

**问题**：表格/图表溢出
- **解决方案**：使用`\resizebox`或`adjustbox`包，减少图像宽度百分比

**问题**：生成的可视化质量差
- **解决方案**：使用`--doc-type report`标志，使用`--iterations 5`增加迭代次数

---

使用此技能创建全面的、视觉丰富的市场研究报告，其质量可与顶级咨询公司的交付成果相媲美。深度研究、结构化框架和广泛可视化的结合将产生能够为战略决策提供信息并展示分析严谨性的文档。
