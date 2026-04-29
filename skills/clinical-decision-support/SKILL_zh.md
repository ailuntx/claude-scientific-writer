---
name: clinical-decision-support
description: "Generate professional clinical decision support (CDS) documents for pharmaceutical and clinical research settings, including patient cohort analyses (biomarker-stratified with outcomes) and treatment recommendation reports (evidence-based guidelines with decision algorithms). Supports GRADE evidence grading, statistical analysis (hazard ratios, survival curves, waterfall plots), biomarker integration, and regulatory compliance. Outputs publication-ready LaTeX/PDF format optimized for drug development, clinical research, and evidence synthesis."
allowed-tools: [Read, Write, Edit, Bash]
---

# 临床决策支持文档

## 描述

为制药公司、临床研究人员和医学决策者生成专业的临床决策支持（CDS）文件。此技能专注于分析性、循证文件，为治疗策略和药物开发提供信息：

1. **患者队列分析** - 按生物标志物分层的组分析，包含统计学结果比较
2. **治疗建议报告** - 循证临床指南，包含GRADE分级和决策算法

所有文件均生成为可发表的LaTeX/PDF文件，针对制药研究、监管提交和临床指南开发进行了优化。

**注意：** 对于床边的个体患者治疗计划，请使用 `treatment-plans` 技能。此技能专注于组级别分析和制药/研究环境的循证综合。

**写作风格：** 对于针对医学期刊的可发表文件，请参阅 **venue-templates** 技能的 `medical_journal_styles.md`，获取结构化摘要、循证语言和CONSORT/STROBE合规性指南。

## 功能

### 文档类型

**患者队列分析**
- 基于生物标志物的患者分层（分子亚型、基因表达、免疫组化）
- 分子亚型分类（例如，GBM间充质-免疫活性型vs成神经细胞型，乳腺癌亚型）
- 包含统计分析的结果指标（OS、PFS、ORR、DOR、DCR）
- 亚组间统计学比较（风险比、p值、95% CI）
- 生存分析，含Kaplan-Meier曲线和对数秩检验
- 疗效表和瀑布图
- 比较效果分析
- 制药队列报告（试验亚组、真实世界证据）

**治疗建议报告**
- 针对特定疾病状态的循证治疗指南
- 推荐强度分级（GRADE系统：1A、1B、2A、2B、2C）
- 证据质量评估（高、中、低、极低）
- 含TikZ图的治疗算法流程图
- 基于生物标志物的治疗线序贯
- 包含临床和分子标准的决策路径
- 制药战略文件
- 医学学会临床指南开发

### 临床特征

- **生物标志物整合**：基因组改变（突变、CNV、融合）、基因表达特征、免疫组化标记、PD-L1评分
- **统计分析**：风险比、p值、可信区间、生存曲线、Cox回归、对数秩检验
- **证据分级**：GRADE系统（1A/1B/2A/2B/2C）、Oxford CEBM水平、证据质量评估
- **临床术语**：SNOMED-CT、LOINC、正确的医学命名法、试验命名法
- **监管合规**：HIPAA去标识化、保密头文件、ICH-GCP对齐
- **专业格式**：紧凑的0.5英寸边距、颜色编码的建议、可发表、适合监管提交

## 制药和研究用例

此技能专为制药和临床研究应用设计：

**药物开发**
- **2/3期试验分析**：生物标志物分层的疗效和安全性分析
- **亚组分析**：显示跨患者亚组治疗效果的森林图
- **伴随诊断开发**：将生物标志物与药物反应关联
- **监管提交**：带证据摘要的IND/NDA文档

**医学事务**
- **KOL教育材料**：针对意见领袖的循证治疗算法
- **医学战略文件**：竞争格局和定位策略
- **顾问委员会材料**：队列分析和治疗建议框架
- **发表规划**：同行评审期刊的稿件分析

**临床指南**
- **指南开发**：针对专业学会的GRADE方法循证综合
- **共识建议**：多利益相关方治疗算法开发
- **实践标准**：基于生物标志物的治疗选择标准
- **质量指标**：循证绩效指标

**真实世界证据**
- **RWE队列研究**：来自电子病历数据的患者队列回顾性分析
- **比较效果**：真实世界环境中头对头治疗比较
- **结局研究**：临床实践中的长期生存和安全性
- **健康经济学**：按生物标志物亚组的成本效果分析

## 使用时机

在需要以下情况时使用此技能：

- **分析按生物标志物、分子亚型或临床特征分层的患者队列**
- **生成包含临床指南或制药策略证据分级的治疗建议报告**
- **比较患者亚组间的结果，进行统计分析（生存、反应率、风险比）**
- **为药物开发、临床试验或监管提交生成制药研究文件**
- **使用GRADE证据分级和决策算法开发临床实践指南**
- **记录人群水平的生物标志物指导治疗选择（非个体患者）**
- **综合多个试验或真实世界数据来源的证据**
- **创建治疗序贯流程图以生成临床决策算法**

**不要将此技能用于：**
- 个体患者治疗计划（使用 `treatment-plans` 技能）
- 床旁临床护理文档（使用 `treatment-plans` 技能）
- 简单的患者特异性治疗方案（使用 `treatment-plans` 技能）

## 科学图表视觉增强

**⚠️强制要求：每个临床决策支持文档必须包含至少1-2个使用scientific-schematics技能生成的AI生成图表。**

这不是可选的。临床决策文件需要清晰的视觉算法。在完成任何文档之前：
1. 至少生成一张图表或图示（例如，临床决策算法、治疗路径或生物标志物分层树）
2. 对于队列分析：包含患者流程图
3. 对于治疗建议：包含决策流程图

**如何生成图表：**
- 使用 **scientific-schematics** 技能生成AI驱动的可发表质量图表
- 只需用自然语言描述您想要的图表
- Nano Banana Pro将自动生成、审查和改进图示

**如何生成图示：**
```bash
python scripts/generate_schematic.py "your diagram description" -o figures/output.png
```

AI将自动：
- 创建具有正确格式的可发表质量图像
- 通过多次迭代审查和改进
- 确保可访问性（色盲友好、高对比度）
- 将输出保存在figures/目录中

**何时添加图示：**
- 临床决策算法流程图
- 治疗路径图
- 生物标志物分层树
- 患者队列流程图（CONSORT风格）
- 生存曲线可视化
- 分子机制图
- 任何受益于可视化的复杂概念

有关创建图示的详细指南，请参阅scientific-schematics技能文档。

---

## 文档结构

**关键要求：所有临床决策支持文档必须在第1页以完整执行摘要开头，该摘要应占满第一页，然后才出现目录或详细部分。**

### 第1页执行摘要结构

每个CDS文档的第一页应仅包含执行摘要，包含以下部分：

**必需元素（均在第1页）：**
1. **文档标题和类型**
   - 主标题（例如，"生物标志物分层队列分析"或"循证治疗建议"）
   - 副标题包含疾病状态和重点

2. **报告信息框**（使用彩色tcolorbox）
   - 文档类型和目的
   - 分析/报告日期
   - 疾病状态和患者人群
   - 作者/机构（如适用）
   - 分析框架或方法学

3. **关键发现框**（3-5个彩色框，使用tcolorbox）
   - **主要结果**（蓝色框）：主要疗效/结局发现
   - **生物标志物见解**（绿色框）：关键分子亚型发现
   - **临床意义**（黄色/橙色框）：可操作的治疗意义
   - **统计摘要**（灰色框）：风险比、p值、关键统计数据
   - **安全性要点**（红色框，如适用）：关键不良事件或警告

**视觉要求：**
- 使用 `\thispagestyle{empty}` 去除第1页的页码
- 所有内容必须在第1页（之前`\newpage`）
- 使用不同颜色的彩色tcolorbox环境以实现视觉层次
- 框应可扫描并突出最关键的信息
- 使用项目符号，而非叙述性段落
- 第1页以`\newpage`结束，然后是目录或详细部分

**第一页LaTeX结构示例：**
```latex
\maketitle
\thispagestyle{empty}

% Report Information Box
\begin{tcolorbox}[colback=blue!5!white, colframe=blue!75!black, title=Report Information]
\textbf{Document Type:} Patient Cohort Analysis\\
\textbf{Disease State:} HER2-Positive Metastatic Breast Cancer\\
\textbf{Analysis Date:} \today\\
\textbf{Population:} 60 patients, biomarker-stratified by HR status
\end{tcolorbox}

\vspace{0.3cm}

% Key Finding #1: Primary Results
\begin{tcolorbox}[colback=blue!5!white, colframe=blue!75!black, title=Primary Efficacy Results]
\begin{itemize}
    \item Overall ORR: 72\% (95\% CI: 59-83\%)
    \item Median PFS: 18.5 months (95\% CI: 14.2-22.8)
    \item Median OS: 35.2 months (95\% CI: 28.1-NR)
\end{itemize}
\end{tcolorbox}

\vspace{0.3cm}

% Key Finding #2: Biomarker Insights
\begin{tcolorbox}[colback=green!5!white, colframe=green!75!black, title=Biomarker Stratification Findings]
\begin{itemize}
    \item HR+/HER2+: ORR 68\%, median PFS 16.2 months
    \item HR-/HER2+: ORR 78\%, median PFS 22.1 months
    \item HR status significantly associated with outcomes (p=0.041)
\end{itemize}
\end{tcolorbox}

\vspace{0.3cm}

% Key Finding #3: Clinical Implications
\begin{tcolorbox}[colback=orange!5!white, colframe=orange!75!black, title=Clinical Recommendations]
\begin{itemize}
    \item Strong efficacy observed regardless of HR status (Grade 1A)
    \item HR-/HER2+ patients showed numerically superior outcomes
    \item Treatment recommended for all HER2+ MBC patients
\end{itemize}
\end{tcolorbox}

\newpage
\tableofcontents  % TOC on page 2
\newpage  % Detailed content starts page 3
```

### 患者队列分析（详细部分-第3页+）
- **队列特征**：人口统计学、基线特征、患者选择标准
- **生物标志物分层**：分子亚型、基因组改变、免疫组化特征
- **治疗暴露**：接受的治疗、剂量、各亚组治疗持续时间
- **结局分析**：反应率（ORR、DCR）、生存数据（OS、PFS）、DOR
- **统计方法**：Kaplan-Meier生存曲线、风险比、对数秩检验、Cox回归
- **亚组比较**：生物标志物分层的疗效、森林图、统计学显著性
- **安全性特征**：各亚组不良事件、剂量调整、停药
- **临床建议**：基于生物标志物特征的治疗意义
- **图表**：瀑布图、泳图、生存曲线、森林图
- **表格**：人口统计学表、生物标志物频率、各亚组结果

### 治疗建议报告（详细部分-第3页+）

**治疗建议第1页执行摘要应包括：**
1. **报告信息框**：疾病状态、指南版本/日期、目标人群
2. **关键建议框**（绿色）：按治疗线的前3-5个GRADE分级建议
3. **生物标志物决策标准框**（蓝色）：影响治疗选择的关键分子标记
4. **证据摘要框**（灰色）：支持建议的主要试验（例如，KEYNOTE-189、FLAURA）
5. **关键监测框**（橙色/红色）：必要的安全性监测要求

**详细部分（第3页+）：**
- **临床背景**：疾病状态、流行病学、当前治疗前景
- **目标人群**：患者特征、生物标志物标准、分期
- **证据审查**：系统文献综合、指南摘要、试验数据
- **治疗选择**：可用治疗及其作用机制
- **证据分级**：每项建议的GRADE评估（1A、1B、2A、2B、2C）
- **按治疗线的建议**：一线、二线、后续治疗
- **生物标志物指导的选择**：基于分子概况的决策标准
- **治疗算法**：显示决策路径的TikZ流程图
- **监测方案**：安全性评估、疗效监测、剂量调整
- **特殊人群**：老年人、肾/肝损伤、合并症
- **参考文献**：包含试验名称和引用的完整参考文献

## 输出格式

**强制第一页要求：**
- **第1页**：完整执行摘要，包含3-5个彩色tcolorbox元素
- **第2页**：目录（可选）
- **第3页+**：包含方法、结果、图表、表格的详细部分

**文档规格：**
- **主要格式**：LaTeX/PDF，0.5英寸边距，紧凑、数据密集的呈现
- **长度**：通常5-15页（1页执行摘要+4-14页详细内容）
- **风格**：可发表的、制药级的、适合监管提交
- **第一页**：始终是完整的执行摘要，占满第1页（见文档结构部分）

**视觉元素：**
- **颜色**：
  - 第1页框：蓝色=数据/信息，绿色=生物标志物/建议，黄色/橙色=临床意义，红色=警告
  - 建议框（绿色=强建议，黄色=有条件，蓝色=需要研究）
  - 生物标志物分层（颜色编码的分子亚型）
  - 统计学显著性（颜色编码的p值、风险比）
- **表格**：
  - 基线特征的人口统计学
  - 亚组生物标志物频率
  - 结果表（按分子亚型的ORR、PFS、OS、DOR）
  - 各队列不良事件
  - 带GRADE评级的证据摘要表
- **图表**：
  - 带对数秩p值和风险人数表的Kaplan-Meier生存曲线
  - 显示患者最佳反应的瀑布图
  - 亚组分析的森林图（含可信区间）
  - TikZ决策算法流程图
  - 个体患者时间线的泳图
- **统计学**：带95% CI的风险比、p值、中位生存时间、里程碑生存率
- **合规性**：按HIPAA Safe Harbor去标识化、专有数据保密声明

## 集成

此技能与以下技能集成：
- **scientific-writing**：引文管理、统计分析报告、循证综合
- **clinical-reports**：医学术语、HIPAA合规、监管文档
- **scientific-schematics**：用于决策算法和治疗路径的TikZ流程图
- **treatment-plans**：队列衍生见解的个体患者应用（双向）

## 与Treatment-Plans技能的关键区别

**临床决策支持（此技能）：**
- **受众**：制药公司、临床研究工作人员、指南委员会、医学事务
- **Scope**：人群水平分析、循证综合、指南开发
- **Focus**：生物标志物分层、统计学比较、证据分级
- **Output**：多页分析文件（通常5-15页），包含大量图表和表格
- **Use Cases**：药物开发、监管提交、临床实践指南、医学战略
- **Example**："分析60名HER2+乳腺癌患者按激素受体状态的生存结果"

**Treatment-Plans技能：**
- **受众**：临床医生、患者、护理团队
- **Scope**：个体患者护理计划
- **Focus**：SMART目标、患者特异性干预、监测计划
- **Output**：简明的1-4页可操作护理计划
- **Use Cases**：床旁临床护理、电子病历文档、以患者为中心的规划
- **Example**："为新诊断的2型糖尿病患者创建治疗方案"

**何时使用：**
- 使用 **clinical-decision-support**：队列分析、生物标志物分层研究、治疗指南开发、制药战略文件
- **treatment-plans**：个体患者护理计划、特定患者的治疗方案、床旁临床文档

## 示例用法

### 患者队列分析

**示例1：NSCLC生物标志物分层**
```
> 分析45名NSCLC患者队列，按PD-L1表达（<1%、1-49%、≥50%）分层
> 接受帕博利珠单抗治疗。包含结果：ORR、中位PFS、中位OS及
> 比较PD-L1≥50% vs <50%的风险比。生成Kaplan-Meier曲线和瀑布图。
```

**示例2：GBM分子亚型分析**
```
> 为30名GBM患者生成队列分析，分为簇1（间充质-免疫活性型）
> 和簇2（成神经细胞型）分子亚型。比较包括中位OS、6个月PFS率、
> 以及TMZ+贝伐单抗的反应。包含生物标志物特征表和统计比较。
```

**示例3：乳腺癌HER2队列**
```
> 分析60名HER2阳性转移性乳腺癌患者接受德喜曲妥珠单抗治疗，
> 按既往曲妥珠单抗暴露（是/否）分层。包含ORR、DOR、中位PFS，
> 按激素受体状态、脑转移和既往治疗线数显示亚组分析的森林图。
```

### 治疗建议报告

**示例1：HER2+转移性乳腺癌指南**
```
> 为HER2阳性转移性乳腺癌创建循证治疗建议，包括
> 生物标志物指导的治疗选择。使用GRADE系统为一线
> （曲妥珠单抗+帕妥珠单抗+紫杉醇）、二线（德喜曲妥珠单抗）
> 和三线选项分级建议。包含基于脑转移、激素受体状态和
> 既往治疗的决策算法流程图。
```

**示例2：晚期NSCLC治疗算法**
```
> 生成基于PD-L1表达、EGFR突变、ALK重排和体力状况的
> 晚期NSCLC治疗建议报告。为每个分子亚型包含GRADE分级建议，
> 用于生物标志物指导治疗选择的TikZ流程图，以及来自KEYNOTE-189、
> FLAURA和CheckMate-227试验的证据表。
```

**示例3：多发性骨髓瘤治疗线序贯**
```
> 为新诊断的多发性骨髓瘤至复发/难治设置创建治疗算法。
> 包含对适合移植vs不适合移植、高危细胞遗传学考虑的GRADE建议，
> 以及达雷妥尤单抗、卡菲佐米和CAR-T治疗的序贯。提供显示每个
> 治疗线决策点的流程图。
```

## 关键特征

### 生物标志物分类
- 基因组：突变、CNV、基因融合
- 表达：RNA-seq、免疫组化评分
- 分子亚型：疾病特异性分类
- 临床可操作性：治疗选择指导

### 结果指标
- 生存：OS（总生存）、PFS（无进展生存）
- 反应：ORR（客观反应率）、DOR（反应持续时间）、DCR（疾病控制率）
- 质量：ECOG体能状态、症状负担
- 安全性：不良事件、剂量调整

### 统计方法
- 生存分析：Kaplan-Meier曲线、对数秩检验
- 组比较：t检验、卡方、Fisher精确检验
- 效应量：带95% CI的风险比、比值比
- 显著性：p值、多重比较校正

### 证据分级

**GRADE系统**
- **1A**：强建议，高质量证据
- **1B**：强建议，中等质量证据
- **2A**：弱建议，高质量证据
- **2B**：弱建议，中等质量证据
- **2C**：弱建议，低质量证据

**建议强度**
- **强**：获益明显超过风险
- **Conditional**：存在权衡，患者价值观很重要
- **Research**：证据不足，需要临床试验

## 最佳实践

### 对于队列分析

1. **患者选择透明度**：清晰记录纳入/排除标准、患者流程和排除原因
2. **生物标志物清晰度**：指定检测方法、平台（例如，FoundationOne、Caris）、截断点和验证状态
3. **统计严谨性**：
   - 报告带95%可信区间的风险比，而不仅仅是p值
   - 包含生存分析的中位随访时间
   - 指定使用的统计检验（对数秩、Cox回归、Fisher精确检验）
   - 适当校正多重比较
4. **结局定义**：使用标准标准：
   - 反应：RECIST 1.1，iRECIST用于免疫治疗
   - 不良事件：CTCAE 5.0版
   - 体能状态：ECOG或Karnofsky
5. **生存数据呈现**：
   - 带95% CI的OS/PFS中位值
   - 里程碑生存率（6个月、12个月、24个月）
   - Kaplan-Meier曲线下方的人数风险表
   - 清晰标注删失
6. **亚组分析**：预先指定亚组；清晰标注探索性vs计划内分析
7. **数据完整性**：报告缺失数据及其处理方式

### 对于治疗建议报告

1. **证据分级透明度**： 
   - 一致使用GRADE系统（1A、1B、2A、2B、2C）
   - 记录每个分级的理由
   - 清晰说明证据质量（高、中、低、极低）
2. **综合证据审查**： 
   - 将3期随机试验作为主要证据
   - 用2期数据补充新兴治疗
   - 注意真实世界证据和Meta分析
   - 引用试验名称（例如，KEYNOTE-189、CheckMate-227）
3. **生物标志物指导的建议**：
   - 将特定生物标志物与治疗建议关联
   - 指定检测方法和经验证的检测
   - 包含伴随诊断的FDA/EMA批准状态
4. **临床可操作性**：每项建议应有明确的实施指导
5. **决策算法清晰度**：TikZ流程图应有明确的决策点，是/否清晰
6. **特殊人群**：解决老年人、肾/肝损伤、怀孕、药物相互作用问题
7. **监测指导**：指定安全性实验室、影像学和频率
8. **更新频率**：标注建议日期并计划周期性更新

### 一般最佳实践

1. **第一页执行摘要（强制）**： 
   - 始终在第1页创建完整执行摘要，占满第一页
   - 使用3-5个彩色tcolorbox元素突出关键发现
   - 第1页不含目录或详细部分
   - 使用`\thispagestyle{empty}`并以`\newpage`结束
   - 这是最重要的一页——应在60秒内可扫描
2. **去标识化**：在文档生成前移除所有18个HIPAA标识符（Safe Harbor方法）
3. **监管合规**：为专有制药数据包含保密声明
4. **可发表格式**：使用0.5英寸边距、专业字体、颜色编码部分
5. **可重复性**：记录所有统计方法以实现复制
6. **利益冲突**：在适用时披露制药资金或关系
7. **视觉层次**：一致使用彩色框（蓝色=数据，绿色=生物标志物，黄色/橙色=建议，红色=警告）

## 参考文献

有关详细指南，请参阅 `references/` 目录：
- 患者队列分析和分层方法
- 治疗建议开发
- 临床决策算法
- 生物标志物分类和解释
- 结局分析和统计方法
- 循证综合和分级系统

## 模板

有关LaTeX模板，请参阅 `assets/` 目录：
- `cohort_analysis_template.tex` - 带统计比较的生物标志物分层患者队列分析
- `treatment_recommendation_template.tex` - 带GRADE分级的循证临床实践指南
- `clinical_pathway_template.tex` - 用于治疗序贯的TikZ决策算法流程图
- `biomarker_report_template.tex` - 分子亚型分类和基因组特征报告
- `evidence_synthesis_template.tex` - 系统证据审查和Meta分析摘要

**模板特征：**
- 紧凑呈现的0.5英寸边距
- 颜色编码的建议框
- 人口统计学、生物标志物、结果的专业表格
- 内置支持Kaplan-Meier曲线、瀑布图、森林图
- GRADE证据分级表
- 制药文档的保密头文件

## 脚本

有关分析和可视化工具，请参阅 `scripts/` 目录：
- `generate_survival_analysis.py` - 带对数秩检验、风险比、95% CI的Kaplan-Meier曲线生成
- `create_waterfall_plot.py` - 队列分析最佳反应可视化
- `create_forest_plot.py` - 带可信区间的亚组分析可视化
- `create_cohort_tables.py` - 人口统计学、生物标志物频率和结果表
- `build_decision_tree.py` - 治疗算法TikZ流程图生成
- `biomarker_classifier.py` - 患者分子亚型分层算法
- `calculate_statistics.py` - 风险比、Cox回归、对数秩检验、Fisher精确检验
- `validate_cds_document.py` - 质量和合规检查（HIPAA、统计分析报告标准）
- `grade_evidence.py` - 治疗建议自动GRADE评估辅助
