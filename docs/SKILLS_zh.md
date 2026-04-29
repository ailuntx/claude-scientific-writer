# 可用技能

**Scientific Writer 是一个深度研究和写作工具**，它将 AI 驱动的深度研究与格式良好的书面输出相结合。下面的技能共同支撑这一能力——从进行文献检索和核实引文，到生成可直接发表、并支持多种格式的文档。

本文档概述了 Scientific Writer CLI 中可用的全部技能。

## 写作技能

### 1. Scientific Writing
**位置**：`.claude/skills/scientific-writing/`

**功能**：
- IMRaD 结构指导（Introduction、Methods、Results 和 Discussion）
- 引文格式（APA、MLA、Chicago、Nature、Science 等）
- 图表格式化最佳实践
- 各类研究类型的报告规范
- 追求清晰、精确与科学严谨的写作原则

**参考资料**：
- `citation_styles.md`：主要引文格式的综合指南
- `figures_tables.md`：数据呈现最佳实践
- `imrad_structure.md`：各部分的详细指导
- `reporting_guidelines.md`：临床试验、观察性研究等标准
- `writing_principles.md`：科学传播的核心原则

---

### 2. Literature Review
**位置**：`.claude/skills/literature-review/`

**功能**：
- 开展系统性文献检索
- 数据库检索策略（PubMed、Web of Science 等）
- 引文管理与核实
- 综述综合与组织
- 为文献总结生成 PDF

**参考资料**：
- `citation_styles.md`：引文格式指南
- `database_strategies.md`：有效的检索策略

**脚本**：
- `search_databases.py`：自动化数据库检索
- `verify_citations.py`：引文核实工具
- `generate_pdf.py`：用于综述的 PDF 生成

**资源**：
- `review_template.md`：文献综述文档模板

---

### 3. Peer Review
**位置**：`.claude/skills/peer-review/`

**功能**：
- 识别科学稿件中的常见问题
- 评估报告规范符合性
- 提供建设性反馈
- 评估方法学与统计分析
- 检查对期刊指南的遵循情况

**参考资料**：
- `common_issues.md`：稿件中常见问题
- `reporting_standards.md`：不同研究类型所需元素

---

### 4. Scholar Evaluation
**位置**：`.claude/skills/scholar-evaluation/`

**功能**：
- 使用 ScholarEval 框架从 8 个维度进行系统化定量评估
- 对研究论文、提案和文献综述进行评分（1-5 分制）
- 评估面向目标刊物/场景的发表准备度
- 提供按优先级排序、可执行的反馈与基于证据的建议
- 识别问题表述、文献综述、方法学、数据收集、分析、结果、写作质量和引文方面的优势与不足
- 生成包含各维度得分的综合评估报告

**参考资料**：
- `evaluation_framework.md`：全部 8 个评估维度的详细评分量表与质量指标

**脚本**：
- `calculate_scores.py`：根据维度评分计算总分，并生成评估报告

**特性**：
- 基于研究的框架（来自 arXiv:2510.16234 的 ScholarEval 方法学）
- 定量评分（每个维度 1-5 分）与加权平均
- 面向各维度的评分量表，确保评估一致性
- 发表准备度评估
- 优势/不足识别
- 按影响程度排序的建议
- 根据工作阶段、刊物和学科进行上下文调整

**适用场景**：
- 作为同行评审的补充，用于定量评估
- 在投稿前评估发表准备度
- 跟踪多轮修订中的改进情况
- 将研究质量与既定标准进行基准比较
- 为学术工作提供结构化反馈

**关键指导**：
- 与 peer-review 技能互补，采用系统化定量方法
- 从 8 个维度进行评估：Problem Formulation、Literature Review、Methodology、Data Collection、Analysis、Results、Writing Quality、Citations
- 分数范围从 1（差）到 5（优秀）
- 总体评估阈值：4.5+（卓越/顶尖）、4.0-4.4（强/小修）、3.5-3.9（良好/大修）、3.0-3.4（可接受/显著修改）、<3.0（需要大幅重做）

---

### 5. Research Grants
**位置**：`.claude/skills/research-grants/`

**功能**：
- 为 NSF、NIH、DOE 和 DARPA 撰写有竞争力的研究提案
- 机构特定的格式与要求
- 评审标准理解（Intellectual Merit、Broader Impacts、Significance、Innovation）
- 预算编制与说明
- Specific Aims 页（NIH）
- Project Summaries（NSF）
- Broader Impacts 策略
- 技术转化规划（DOE、DARPA）
- 重新提交策略

**重点机构**：
- **NSF**：National Science Foundation（Intellectual Merit + Broader Impacts）
- **NIH**：National Institutes of Health（R01、R21、K 奖项等）
- **DOE**：Department of Energy（Office of Science、ARPA-E、EERE）
- **DARPA**：Defense Advanced Research Projects Agency（BAA、SBIR）

**参考资料**：
- `nsf_guidelines.md`：NSF 提案结构、Broader Impacts、评审标准
- `nih_guidelines.md`：NIH 机制、Specific Aims、研究策略
- `doe_guidelines.md`：DOE 项目、TRL、成本分摊、实验室合作
- `darpa_guidelines.md`：DARPA 结构、Heilmeier Catechism、PM 互动
- `broader_impacts.md`：NSF Broader Impacts 综合策略
- `specific_aims_guide.md`：NIH Specific Aims 页完整指南

**资源/模板**：
- `nsf_project_summary_template.md`：包含 Overview、Intellectual Merit、Broader Impacts 的 NSF Project Summary
- `nih_specific_aims_template.md`：NIH Specific Aims 页模板
- `budget_justification_template.md`：包含机构特定示例的预算说明模板

**特性**：
- 机构特定的评审标准与评分体系
- 各机构的成功率与资助趋势
- 时间线规划与里程碑制定
- 包括人员、设备、差旅、耗材的预算编制
- 具有可衡量结果的 Broader Impacts（NSF）
- 初步数据整合（NIH）
- 国家实验室合作（DOE）
- 技术转化与商业化（DOE、DARPA）
- 重新提交与审稿意见回应策略

**关键指导**：
- NSF：Intellectual Merit 与 Broader Impacts 同等权重（且都必须有实质内容）
- NIH：Specific Aims 页是最关键部分（1 页）
- DOE：能源相关性、TRL、成本分摊、商业化路径
- DARPA：高风险/高回报、Heilmeier Catechism、PM 互动至关重要

---

### 6. Clinical Reports
**位置**：`.claude/skills/clinical-reports/`

**功能**：
- 按照 CARE（CAse REport）指南撰写用于期刊发表的临床病例报告
- 创建诊断报告（放射学、病理学、实验室）并符合专业标准
- 记录临床试验数据（SAE 报告、按 ICH-E3 的 Clinical Study Reports）
- 患者临床文档（SOAP 记录、H&P、出院小结）
- HIPAA 合规与去标识化验证
- 监管合规（FDA 21 CFR Part 11、ICH-GCP）
- 医学术语与编码标准（SNOMED-CT、LOINC、ICD-10、CPT）
- 质量保证与验证

**四类主要报告**：
1. **Clinical Case Reports** - 符合 CARE 的医学期刊病例报告
2. **Diagnostic Reports** - 放射学（ACR）、病理学（CAP）、实验室报告
3. **Clinical Trial Reports** - SAE 报告、CSR、方案偏离、DSMB 报告
4. **Patient Documentation** - SOAP 记录、H&P、出院小结、会诊记录

**参考资料**：
- `case_report_guidelines.md`：CARE 指南、期刊要求、去标识化
- `diagnostic_reports_standards.md`：ACR/CAP/CLSI 标准、结构化报告
- `clinical_trial_reporting.md`：ICH-E3、CONSORT、SAE 报告、MedDRA 编码
- `patient_documentation.md`：SOAP、H&P、出院小结标准
- `regulatory_compliance.md`：HIPAA、21 CFR Part 11、ICH-GCP、FDA 要求
- `medical_terminology.md`：SNOMED-CT、LOINC、ICD-10、CPT、缩写
- `data_presentation.md`：临床表格、图形、Kaplan-Meier 曲线、forest plots
- `peer_review_standards.md`：临床稿件的审稿标准

**模板（12 个综合模板）**：
- `case_report_template.md`：符合 CARE 的病例报告结构
- `soap_note_template.md`：SOAP 进展记录格式
- `history_physical_template.md`：完整 H&P 模板
- `discharge_summary_template.md`：医院出院小结
- `consult_note_template.md`：会诊记录格式
- `radiology_report_template.md`：结构化放射学报告
- `pathology_report_template.md`：带 synoptic reporting 的外科病理报告
- `lab_report_template.md`：临床实验室报告
- `clinical_trial_sae_template.md`：严重不良事件报告
- `clinical_trial_csr_template.md`：临床研究报告（ICH-E3）
- `quality_checklist.md`：所有报告类型的 QA 清单
- `hipaa_compliance_checklist.md`：隐私合规核查

**脚本（8 个验证与自动化工具）**：
- `validate_case_report.py`：检查 CARE 指南符合性
- `check_deidentification.py`：扫描 18 项 HIPAA 标识符
- `validate_trial_report.py`：验证 ICH-E3 结构
- `format_adverse_events.py`：生成 AE 汇总表
- `generate_report_template.py`：交互式模板生成器
- `extract_clinical_data.py`：解析结构化临床数据
- `compliance_checker.py`：监管合规验证
- `terminology_validator.py`：医学术语与编码验证

**特性**：
- 全面覆盖所有临床报告类型
- 内置监管合规（HIPAA、FDA、ICH-GCP）
- 基于行业标准的专业模板
- 自动化验证与质量检查
- 隐私保护与去标识化工具
- 与 scientific-writing 和 peer-review 技能集成

**关键指导**：
- 病例报告务必先获得知情同意
- 在发表前删除全部 18 项 HIPAA 标识符
- 病例报告遵循 CARE 指南
- 诊断报告使用结构化报告（BI-RADS、Lung-RADS 等）
- 满足 SAE 报告的监管时限（7 天、15 天）
- 记录医学必要性以支持计费
- 临床试验数据应遵循 ALCOA-CCEA 原则

**适用场景**：
- 在医学期刊发表临床病例报告
- 撰写放射学、病理学或实验室报告
- 在临床试验中记录不良事件
- 准备监管提交材料（CSR、IND 安全报告）
- 创建患者病程记录与总结
- 确保临床文档符合 HIPAA

**示例用法**：

### 撰写临床病例报告
```
> 为一位表现为急性阑尾炎但症状不典型的患者创建一份临床病例报告
```
Claude 将使用 clinical-reports 技能创建符合 CARE 的病例报告，并进行适当的去标识化。

### 生成诊断报告
```
> 为胸部 CT 扫描生成放射学报告模板
> 为乳腺活检标本创建病理学报告
```
Claude 将使用结构化报告模板（ACR、CAP）并配合适当的医学术语。

### 临床试验文档
```
> 为三期试验中的严重不良事件撰写 SAE 报告
> 按照 ICH-E3 创建临床研究报告大纲
```
Claude 将确保监管合规并进行适当的因果关系评估。

### 患者文档
```
> 为复诊创建 SOAP 记录
> 为心力衰竭患者生成出院小结
```
Claude 将使用标准临床文档格式，并支持计费。

### 验证与合规
```
> 检查这份病例报告是否包含 HIPAA 标识符
> 按照 ICH-E3 结构验证临床试验报告
```
Claude 将使用验证脚本确保合规与质量。

---

### 7. Clinical Decision Support
**位置**：`.claude/skills/clinical-decision-support/`

**功能**：
- 为医疗专业人员生成专业的临床决策支持（CDS）文档
- 创建按生物标志物或临床特征分层的患者队列分析
- 使用 GRADE 方法学开发基于证据的治疗建议报告
- 使用 TikZ 流程图构建临床决策算法与路径
- 生成生物标志物指导的治疗选择报告
- 支持三类文档：个体治疗方案、队列分析和建议报告
- LaTeX/PDF 输出，采用紧凑的专业排版（0.5in 页边距）

**文档类型**：

1. **Individual Patient Treatment Plans**
   - 针对特定疾病的个体化治疗方案
   - 药物剂量、监测计划、随访方案
   - 符合 HIPAA 的去标识化
   
2. **Patient Cohort Analysis**
   - 生物标志物分层的群体分析（如 PD-L1 表达水平、分子亚型）
   - 结局比较与统计检验（OS、PFS、ORR、安全性）
   - 面向临床研究的药品级报告
   
3. **Treatment Recommendation Reports**
   - 基于证据的临床指南与 GRADE 分级
   - 治疗算法与决策路径
   - 生物标志物指导的治疗选择

**参考资料（6 份综合指南）**：
- `patient_cohort_analysis.md`：分层方法、生物标志物、结局指标、统计比较
- `treatment_recommendations.md`：证据分级（GRADE）、治疗顺序、监测方案
- `clinical_decision_algorithms.md`：决策树、风险分层工具、TikZ 流程图
- `biomarker_classification.md`：基因组生物标志物、分子亚型、伴随诊断、可行动性框架
- `outcome_analysis.md`：生存分析（Kaplan-Meier、Cox 回归）、反应评估（RECIST）、统计方法
- `evidence_synthesis.md`：指南整合（NCCN、ASCO、ESMO）、系统综述、GRADE 方法学

**模板（4 个 LaTeX 模板）**：
- `cohort_analysis_template.tex`：患者群体分析，包含人口学特征、生物标志物谱、结局、统计
- `treatment_recommendation_template.tex`：带颜色编码建议框的循证指南
- `clinical_pathway_template.tex`：用于临床决策算法的 TikZ 流程图（横向格式）
- `biomarker_report_template.tex`：包含治疗匹配的综合基因组分析报告

**脚本（5 个分析工具）**：
- `generate_survival_analysis.py`：Kaplan-Meier 曲线、log-rank 检验、风险比、LaTeX 表格生成
- `create_cohort_tables.py`：基线特征、疗效结局、安全性表格与统计检验
- `build_decision_tree.py`：根据 JSON/文本规范自动生成 TikZ 流程图
- `biomarker_classifier.py`：患者分层算法（PD-L1、HER2、分子亚型）
- `validate_cds_document.py`：证据引文、GRADE 格式、HIPAA 合规的质量检查

**资源**：
- `example_gbm_cohort.md`：GBM 分子亚型分析示例（Mesenchymal-Immune-Active 与其他组）
- `recommendation_strength_guide.md`：GRADE 框架指南，含示例与措辞模板
- `color_schemes.tex`：用于建议、紧急程度、生物标志物的标准化颜色定义

**特性**：
- **基于证据**：采用 GRADE 方法学衡量建议强度与证据质量
- **生物标志物整合**：基因组改变、表达谱、分子亚型
- **统计严谨性**：适当的假设检验、置信区间、生存分析
- **专业输出**：符合制药行业标准的紧凑 LaTeX/PDF
- **指南一致性**：整合 NCCN、ASCO、ESMO、AHA/ACC 指南
- **临床可操作性**：分层分类（FDA-approved、investigational、VUS）

**适用场景**：
- 为个体患者创建治疗方案
- 分析按生物标志物分层的患者队列
- 生成基于证据的临床建议
- 产出制药级临床分析文档
- 开发临床路径与决策算法
- 报告生物标志物指导的治疗选择

**示例用法**：

### 个体治疗方案
```
> 为一位新诊断为 2 型糖尿病并合并高血压的 55 岁患者创建治疗方案
```
Claude 将生成包含监测与随访的个体化治疗方案。

### 患者队列分析
```
> 分析一组 45 例按 PD-L1 表达（<1%、1-49%、≥50%）分层的 NSCLC 患者，包括 ORR、PFS 和 OS 结局

> 为 30 例 GBM 患者生成队列分析，将其分为 mesenchymal-immune-active 和 proneural 分子亚型，并比较治疗结局
```
Claude 将创建包含生物标志物谱、结局比较、统计分析和临床建议的综合队列报告。

### 治疗建议报告
```
> 为 HER2 阳性转移性乳腺癌创建基于证据的治疗建议，包括一线和二线方案

> 根据 NYHA 分级和射血分数生成心力衰竭管理的治疗算法，并附 GDMT 方案
```
Claude 将开发包含 GRADE 分级选项、决策算法和监测方案的建议报告。

### 生物标志物报告
```
> 为一名具有 EGFR L858R 突变的 NSCLC 患者创建基因组分析报告，包括 FDA 批准的治疗和临床试验匹配
```
Claude 将生成具有分层可行动性和个体化治疗建议的生物标志物报告。

### 验证
```
> 验证这份队列分析文档的证据引文和统计报告完整性
```
Claude 将使用验证脚本检查质量与合规性。

---

### 8. LaTeX Research Posters（默认）
**位置**：`.claude/skills/latex-posters/`

**⚠️ 这是所有海报请求的默认技能。** 除非用户明确要求 PPTX/PowerPoint 格式，否则都使用它。

**功能**：
- 使用 LaTeX 创建专业研究海报（beamerposter、tikzposter、baposter）
- AI 驱动的视觉元素生成（在组装海报前先生成图形）
- 会议海报设计与版式
- 具有适当留白的整页海报模板
- 配色方案与视觉设计原则
- 排版与可读性优化
- PDF 生成与质量控制
- 可访问性与包容性设计
- 海报尺寸配置（A0、A1、36×48" 等）
- 防止内容溢出与内容密度指南

**参考资料**：
- `latex_poster_packages.md`：beamerposter、tikzposter 和 baposter 的详细比较
- `poster_design_principles.md`：排版、色彩理论、视觉层级与可访问性
- `poster_layout_design.md`：网格系统、空间组织与视觉流
- `poster_content_guide.md`：内容策略、写作风格与分节指导

**脚本**：
- `review_poster.sh`：自动化 PDF 质量检查脚本

**资源**：
- `beamerposter_template.tex`：经典学术海报模板
- `tikzposter_template.tex`：现代、色彩丰富的海报模板
- `baposter_template.tex`：结构化多栏海报模板
- `poster_quality_checklist.md`：完整的印前检查清单

**特性**：
- **AI 驱动的视觉生成**：在创建海报前，使用 scientific-schematics 生成所有图形
- **海报字号要求**：AI 生成图形中可读文本的规范（关键数字 72pt+）
- **防溢出**：内容限制（最多 5-6 个部分，300-800 词）以避免截断
- 确保海报铺满整页而不过度留白
- PDF 审阅与质量控制指南，含溢出检查
- 页面尺寸、字体和图像的自动化检查脚本
- 缩尺打印测试说明
- 色彩对比与可访问性验证
- 常见问题排查指南

**对于 PPTX/PowerPoint 海报**：仅当用户明确要求 PPTX 格式时，才使用 `pptx-posters` 技能。位置为 `.claude/skills/pptx-posters/`。

---

### 9. Scientific Slides and Presentations
**位置**：`.claude/skills/scientific-slides/`

**功能**：
- 使用 Nano Banana Pro AI 创建令人惊艳的 PDF 幻灯片
- 为不同场景组织演示文稿（5-60 分钟报告）
- AI 生成具有出版级视觉效果的幻灯片
- 针对演示场景优化数据可视化
- 提供时间安排与节奏指导，并附练习策略
- 带自动验证的视觉审阅工作流
- 与 research-lookup 集成以获取准确引文

**支持的演讲类型**：
- **Conference talks**（10-20 分钟）：简短，聚焦关键发现
- **Academic seminars**（45-60 分钟）：全面，方法细致
- **Thesis defenses**（45-60 分钟）：完整论文概述
- **Grant pitches**（15-20 分钟）：强调重要性与可行性
- **Journal clubs**（20-45 分钟）：对已发表工作的批判性分析
- **Lightning talks**（5 分钟）：极度聚焦的单一信息

**参考资料**：
- `presentation_structure.md`：各类演讲的结构、时间分配、叙事弧线
- `slide_design_principles.md`：排版、色彩理论、布局、可访问性
- `data_visualization_slides.md`：将图表简化用于演示
- `talk_types_guide.md`：各类演示的具体指导
- `visual_review_workflow.md`：将 PDF 转为图像、系统检查、迭代

**资源**：
- `timing_guidelines.md`：全面的时间、节奏与练习策略

**脚本**：
- `validate_presentation.py`：检查幻灯片数量、时长、字体、文件大小
- `pdf_to_images.py`：将 PDF 转换为图像以便视觉检查

**特性**：
- **Nano Banana Pro AI**：生成带 AI 视觉效果的惊艳 PDF 幻灯片
- **research-lookup 集成**：自动收集背景与讨论所需引文
- **视觉验证工作流**：转为图像、系统检查、迭代
- **时间指导**：每分钟一页规则，并可调整
- **设计原则**：少文字（24pt+）、高对比度、色盲友好
- **练习策略**：带时间检查点的系统排练

**适用场景**：
- 创建任何科学演示或幻灯片
- 准备会议报告或研究研讨会
- 制作论文答辩演示
- 制作 grant pitch 幻灯片
- 构建讲座或教程演示
- 将论文转换为演示格式

**示例用法**：

### 会议报告
```
> 为我的机器学习研究创建一份 15 分钟的会议演示
```
Claude 将使用 research-lookup 收集引文、组织演讲结构，并借助 Nano Banana Pro AI 生成令人惊艳的 PDF 幻灯片。

### 研讨会演示
```
> 帮我制作一场关于 CRISPR 基因编辑的 45 分钟研讨会，包含完整方法
```
Claude 将组织一场详尽的学术研讨会，并提供准确引文与时间安排指导。

### 论文答辩
```
> 为我的论文答辩创建幻灯片，涵盖三项研究
```
Claude 将按照学术标准组织一份完整的答辩演示。

### 视觉验证
```
> 将我的演示转换为图像并审查布局问题
```
Claude 将使用脚本把 PDF 转为图像，并系统检查文本溢出、重叠和设计问题。

### 时间检查
```
> 验证我的 20 页幻灯片是否适合 15 分钟报告
```
Claude 将检查幻灯片数量是否合适，并提供时间建议。

**关键原则**：
- **结构**：将 40-50% 的时间用于结果，遵循清晰的叙事主线
- **设计**：少文字、大字体（24pt+）、每页一个想法
- **引文**：使用 research-lookup 收集 8-12 篇论文以获得恰当背景
- **时间**：练习 3-5 次，设置检查点，切勿跳过结论
- **验证**：通过视觉审阅工作流发现溢出和重叠问题

---

### 10. Scientific Schematics and Diagrams
**位置**：`.claude/skills/scientific-schematics/`

**功能**：
- 创建方法流程图（临床试验的 CONSORT 图）
- 生成电路图和电气原理图
- 可视化生物通路和信号级联
- 设计系统架构与框图
- 创建流程图和决策树
- 网络图和图可视化
- 使用 TikZ/LaTeX 制作可发表级矢量图形
- 使用 Python（Schemdraw、NetworkX、Matplotlib）进行程序化图示生成

**参考资料**：
- `tikz_guide.md`：全面的 TikZ 语法、定位、样式与技巧
- `diagram_types.md`：科学图示类型目录，含应用场景与示例
- `best_practices.md`：出版标准、可访问性与色盲安全设计
- `python_libraries.md`：关于使用 Schemdraw、NetworkX 和 Matplotlib 进行程序化生成的指南

**脚本**：
- `generate_flowchart.py`：将文本描述转换为 TikZ 流程图
- `circuit_generator.py`：使用 Schemdraw 生成电路图
- `pathway_diagram.py`：使用 Matplotlib 创建生物通路图
- `compile_tikz.py`：独立的 TikZ 编译工具（输出 PDF/PNG）

**资源**：
- `tikz_styles.tex`：可复用样式定义，采用 Okabe-Ito 色盲安全调色板
- `flowchart_template.tex`：CONSORT 风格的方法流程图模板
- `circuit_template.tex`：基于 CircuitikZ 的电气电路图模板
- `pathway_template.tex`：生物通路图模板
- `block_diagram_template.tex`：系统架构图模板

**特性**：
- 全程采用色盲安全的 Okabe-Ito 调色板
- 矢量图形，具备无限缩放性
- 与 LaTeX 集成，保持排版一致
- 可根据编号列表自动生成流程图
- 可直接用于发表的输出（PDF、SVG、PNG）
- 符合 WCAG 标准的可访问性设计
- 灰度兼容性验证

**使用场景**：
- **CONSORT 图**：临床试验的受试者流向
- **电子论文**：电路原理图与信号处理图
- **生物论文**：信号级联、代谢通路、基因网络
- **工程论文**：系统架构、数据流、框图
- **方法学部分**：研究设计、数据处理流水线
- **概念框架**：流程、决策树

---

### 11. Market Research Reports
**位置**：`.claude/skills/market-research-reports/`

**功能**：
- 以咨询公司风格生成综合性市场研究报告（50+ 页）
- 使用自定义 `market_research.sty` 样式包进行专业 LaTeX 排版
- 利用 scientific-schematics 进行大量视觉生成（每份报告 25-30 张图）
- 多框架战略分析（Porter’s Five Forces、PESTLE、SWOT、BCG Matrix）
- 基于数据的 TAM/SAM/SOM 市场规模测算与预测
- 具有定位矩阵的竞争格局分析
- 使用热图与缓解框架进行风险评估
- 具有实施路线图的战略建议
- 含财务预测的投资论证构建

**参考资料**：
- `report_structure_guide.md`：全部 11 个章节的逐节内容要求
- `visual_generation_guide.md`：生成全部 28 个标准报告可视化图表的完整提示
- `data_analysis_patterns.md`：Porter’s、PESTLE、SWOT、BCG Matrix、TAM/SAM/SOM 模板

**脚本**：
- `generate_market_visuals.py`：通过单条命令批量生成所有标准市场报告图示

**资源**：
- `market_research.sty`：包含专业配色、box 环境与排版的 LaTeX 样式包
- `market_report_template.tex`：完整的 50+ 页 LaTeX 模板，所有章节均已预结构化
- `FORMATTING_GUIDE.md`：关于 box 环境、颜色、表格与样式的快速参考

**特性**：
- **篇幅充足**：报告设计为 50+ 页，不受 token 限制
- **视觉密度高**：25-30 张生成图像/图示（约每 2 页 1 张）
- **数据驱动**：与 research-lookup 深度集成，用于市场数据和统计信息
- **多框架**：Porter’s Five Forces、PESTLE、SWOT、BCG Matrix、Value Chain Analysis
- **专业排版**：咨询公司级别的排版、配色与版式
- **可执行建议**：以优先级矩阵与实施路线图形式呈现战略重点

**报告结构（50+ 页）**：
- 前置内容：封面、目录、执行摘要（5 页）
- 核心分析：市场概览、市场规模与增长、行业驱动因素、竞争格局、客户分析、技术格局、监管环境、风险分析（35 页）
- 战略建议：机会、实施路线图、投资论证（10 页）
- 后置内容：方法学、数据表、公司简介、参考文献（5 页）

**适用场景**：
- 为投资决策创建全面的市场分析
- 开发用于战略规划的行业报告
- 分析竞争格局与市场动态
- 开展市场规模测算（TAM/SAM/SOM）
- 评估市场进入机会
- 为并购活动准备尽职调查材料
- 创建思想领导力内容
- 开发 go-to-market 战略文档

**示例用法**：

### 生成市场研究报告
```
> 创建一份关于 Electric Vehicle Charging Infrastructure 市场的综合市场研究报告
```
Claude 将使用 market-research-reports 技能创建一份带有大量可视化内容的 50+ 页专业报告。

### 市场规模分析
```
> 分析 AI in Healthcare 市场，并给出 TAM/SAM/SOM 拆分和 10 年预测
```
Claude 将提供全面的市场规模分析，包括增长轨迹图和区域拆分。

### 竞争格局报告
```
> 为 Cloud Computing 市场创建竞争格局分析，包括 Porter’s Five Forces 和定位矩阵
```
Claude 将生成包含战略框架和可视化内容的竞争分析。

---

## 文档处理技能

### 12. MarkItDown - 通用文件转 Markdown 转换器
**位置**：`.claude/skills/markitdown/`

**功能**：
- 将 15+ 种文件格式转换为 Markdown（PDF、DOCX、PPTX、XLSX、图像、音频等）
- 使用先进视觉模型进行 AI 增强的图像描述
- 扫描文档和图像的 OCR
- 音频文件的语音转文本转录
- YouTube 视频转录提取
- 支持并行执行的批处理
- 用于复杂 PDF 的 Azure Document Intelligence 集成
- 用于自定义转换器的插件系统

**参考资料**：
- `api_reference.md`：完整 API 文档与类参考
- `file_formats.md`：针对特定格式的转换指南与最佳实践

**脚本**：
- `batch_convert.py`：多个文件的并行批量转换
- `convert_with_ai.py`：带自定义提示词的 AI 增强转换
- `convert_literature.py`：带元数据提取的科学文献转换

**资源**：
- `example_usage.md`：常见用例的综合示例

**特性**：
- 针对 LLM 处理优化的高 token 效率 Markdown 输出
- 支持特定文件格式的可选依赖
- 面向科学、医学和数据可视化场景的自定义提示词
- 元数据提取与整理
- 错误处理与稳健的批处理
- 与科学工作流集成

**来源**：https://github.com/microsoft/markitdown（MIT License）

---

### 13. DOCX（Word 文档）
**位置**：`.claude/skills/document-skills/docx/`

**功能**：
- 以程序化方式创建和编辑 Word 文档
- 处理 OOXML 格式
- 管理批注与修订
- 验证文档结构
- 处理模板

**脚本**：
- `document.py`：核心文档操作
- `utilities.py`：辅助函数
- OOXML 验证与操作工具

**参考资料**：
- `docx-js.md`：JavaScript 集成指南
- `ooxml.md`：OOXML 格式规范

---

### 14. PDF Documents
**位置**：`.claude/skills/document-skills/pdf/`

**功能**：
- 从 PDF 中提取文本和元数据
- 检查边界框与版式
- 处理可填写的 PDF 表单
- 将 PDF 转换为图像
- 提取表单字段信息

**脚本**：
- `check_bounding_boxes.py`：分析 PDF 版式
- `check_fillable_fields.py`：识别表单字段
- `fill_fillable_fields.py`：填写 PDF 表单
- `convert_pdf_to_images.py`：PDF 转图像
- `extract_form_field_info.py`：提取表单元数据

**参考资料**：
- `forms.md`：处理 PDF 表单
- `reference.md`：PDF 操作参考

---

### 15. PPTX（PowerPoint 演示文稿）
**位置**：`.claude/skills/document-skills/pptx/`

**功能**：
- 创建和修改 PowerPoint 演示文稿
- 将 HTML 转为 PowerPoint
- 管理幻灯片与版式
- 处理 OOXML 格式
- 生成缩略图

**脚本**：
- `html2pptx.js`：HTML 转 PowerPoint
- `inventory.py`：演示文稿库存管理
- `rearrange.py`：幻灯片重排
- `replace.py`：内容替换
- `thumbnail.py`：生成缩略图

**参考资料**：
- `html2pptx.md`：HTML 转换指南
- `ooxml.md`：OOXML 格式规范

---

### 16. XLSX（Excel 电子表格）
**位置**：`.claude/skills/document-skills/xlsx/`

**功能**：
- 读取和写入 Excel 文件
- 管理公式与计算
- 处理复杂电子表格操作
- 重新计算公式

**脚本**：
- `recalc.py`：公式重新计算工具

---

## 技能如何使用

当你使用 Scientific Writer CLI 时，Claude 会自动：

1. **检测相关技能**：根据你的请求，Claude 识别应使用哪些技能
2. **加载资源**：访问参考资料、脚本和模板
3. **应用最佳实践**：遵循每项技能中的指南与标准
4. **执行工具**：在需要文档处理或数据处理时使用脚本

## 技能集成

所有技能都从 `.claude/skills/` 目录加载，并在你运行 CLI 时自动可用。你无需手动选择或激活它们——Claude 会根据你的请求使用合适的技能。

## 示例用法

### 使用 Scientific Writing 技能
```
> 帮我为随机对照试验构建方法部分的结构
```
Claude 将使用 scientific-writing 技能，提供符合 IMRaD 的指导。

### 使用 Literature Review 技能
```
> 为农业中的 CRISPR 基因编辑创建一篇文献综述
```
Claude 将使用 literature-review 技能来构建一篇全面的综述。

### 使用文档技能
```
> 从 results.pdf 的 Table 1 中提取数据并创建摘要
```
Claude 将使用 PDF 技能提取数据，并在必要时使用 XLSX 技能进行整理。

### 使用 MarkItDown 技能
```
> 将 literature 文件夹中的所有 PDF 转换为 Markdown
```
Claude 将使用 markitdown 技能批量转换文件。

```
> 将这份 PowerPoint 演示文稿转换为带 AI 生成描述的 Markdown
```
Claude 将使用带 AI 增强的 markitdown，生成详细的图像描述。

### 使用 Peer Review 技能
```
> 帮我审查讨论部分的逻辑流和对报告规范的遵循情况
```
Claude 将使用 peer-review 技能提供建设性反馈。

### 使用 Scholar Evaluation 技能
```
> 使用 ScholarEval 框架评估这篇论文
```
Claude 将使用 scholar-evaluation 技能，从 8 个维度提供系统化定量评估。

```
> 评估其在 Nature Machine Intelligence 的发表准备度
```
Claude 将评估该论文并提供投稿准备度的评分与建议。

### 使用 Research Grants 技能
```
> 帮我为我的计算神经科学研究撰写 NSF 提案
```
Claude 将使用 research-grants 技能提供 NSF 相关指导。

```
> 我需要为我的癌症免疫治疗 R01 起草 NIH Specific Aims
```
Claude 将帮助你使用 NIH 最佳实践构建 1 页的 specific aims。

```
> 在 NSF Materials Research 提案的 broader impacts 中我应该包含什么？
```
Claude 将提供符合 NSF 标准的实质性 broader impacts 策略。

### 使用 Scientific Schematics 技能
```
> 为我的临床试验创建一张 CONSORT 流程图，展示从筛查（n=500）到随机分组再到最终分析的受试者流向
```
Claude 将按照 CONSORT 指南生成方法流程图。

```
> 生成一个 RC 低通滤波器的电路图
```
Claude 将使用 CircuitikZ 或 Schemdraw 创建电气原理图。

```
> 创建一张生物通路图，展示从受体到基因表达的 MAPK 信号级联
```
Claude 将用恰当样式的蛋白和激活箭头可视化该信号通路。

```
> 设计一张框图，展示我的数据采集系统架构，包括传感器、ADC、微控制器和无线传输
```
Claude 将创建包含标注组件和数据流的系统架构图。

### 11. Venue Templates
**位置**：`.claude/skills/venue-templates/`

**功能**：
- 查询 50+ 个主要期刊和会议的 LaTeX 模板
- 访问 grant 提案模板（NSF、NIH、DOE、DARPA）
- 获取学术会议海报模板
- 查看格式要求与投稿指南
- 使用作者和项目信息自定义模板
- 根据场地要求验证文档格式

**参考资料**：
- `journals_formatting.md`：Nature、Science、PLOS、IEEE、ACM、Cell Press 及其他主要期刊的要求
- `conferences_formatting.md`：机器学习、计算机科学、生物学会议论文格式（NeurIPS、ICML、ICLR、CVPR、CHI、ISMB 等）
- `posters_guidelines.md`：海报设计、尺寸、版式原则与最佳实践
- `grants_requirements.md`：联邦和私人 grant 提案格式（NSF、NIH、DOE、DARPA）

**脚本**：
- `query_template.py`：按场地名称或关键词搜索和检索模板
- `customize_template.py`：使用作者信息自定义模板
- `validate_format.py`：检查文档是否符合场地要求

**资源**：
- `journals/`：Nature、Science、PLOS ONE、NeurIPS 及其他主要场地的 LaTeX 模板
- `posters/`：学术海报模板（beamerposter、tikzposter、baposter）
- `grants/`：grant 提案模板（NSF、NIH Specific Aims、DOE、DARPA）

**特性**：
- 面向主要发表场地的综合格式指南
- 可直接使用、结构完整的 LaTeX 模板
- 用于模板查找与自定义的辅助脚本
- 格式验证工具
- 与科学写作工作流集成

**使用场景**：
- **期刊投稿**：为 Nature、Science、PLOS、IEEE、ACM 期刊获取正确格式
- **会议论文**：为 NeurIPS、ICML、CVPR、CHI 及其他主要会议提供模板
- **研究海报**：用于 A0、A1 和美标尺寸的专业海报模板
- **grant 提案**：NSF、NIH R01、DOE、DARPA 提案模板及要求
- **格式验证**：检查你的文档是否符合场地规范

**示例用法**：

### 查询期刊模板
```
> 我需要投稿到 Nature
```
Claude 将提供 Nature 文章模板和格式要求。

### 获取会议论文模板
```
> 给我看看 NeurIPS 论文模板
```
Claude 将提供 NeurIPS 会议论文模板及匿名化指南。

### Grant 提案模板
```
> 我需要一个 NSF 提案模板
```
Claude 将提供包含全部必需部分和格式要求的 NSF 提案模板。

### 会议海报
```
> 为 ISMB 会议创建一张研究海报
```
Claude 将提供适用于该会议的海报模板和尺寸规格。

### 格式验证
```
> 检查我的论文是否符合 Nature 的要求
```
Claude 可以指导你使用验证脚本来检查格式符合性。

---

## 添加自定义技能

要添加你自己的技能：

1. 在 `.claude/skills/` 中创建一个新目录
2. 添加一个 `SKILL.md` 文件，定义你的技能
3. 如有需要，可添加 `references/`、`scripts/` 和 `assets/` 子目录
4. 重启 CLI

新技能将自动加载并可用。
