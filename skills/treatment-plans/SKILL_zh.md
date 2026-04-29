---
name: treatment-plans
description: "生成简洁（3-4页）、重点突出的LaTeX/PDF格式医学治疗计划，涵盖所有临床专科。支持一般医学治疗、康复治疗、心理健康护理、慢性疾病管理、围手术期护理和疼痛管理。包括SMART目标框架、简短文本引用的循证干预措施、监管合规性（HIPAA）和专业格式。重点是简洁性和临床可操作性。"
allowed-tools: [Read, Write, Edit, Bash]
---

# 治疗计划撰写

## 概述

治疗计划撰写是对临床护理策略的系统文档记录，通过循证干预措施、可衡量目标和结构化随访来解决患者健康状况。本技能提供全面的LaTeX模板和验证工具，用于创建**简洁、重点突出**的治疗计划（标准3-4页），涵盖所有医学专科，并具有完整的监管合规性。

**关键原则：**
1. **简洁且可操作**：治疗计划默认最多3-4页，仅聚焦于影响护理决策的临床必要信息
2. **以患者为中心**：计划必须基于循证、可衡量，并符合医疗法规（HIPAA、文档标准）
3. **最小化引用**：仅在需要支持临床建议时使用简短的文内引用；避免冗长的参考文献

每个治疗计划都应包含明确的目标、具体的干预措施、定义的时间线、监测参数和符合患者偏好及当前临床指南的预期结果——所有内容均以最有效的方式呈现。

## 何时使用本技能

在以下情况下应使用本技能：
- 为患者护理创建个性化治疗计划
- 记录慢性疾病管理的治疗干预措施
- 制定康复计划（物理治疗、作业治疗、心脏康复）
- 撰写心理健康和精神科治疗计划
- 规划围手术期和外科护理路径
- 建立疼痛管理协议
- 使用SMART标准设定以患者为中心的目标
- 协调跨专科的多学科护理
- 确保治疗文档的监管合规性
- 为医疗记录生成专业治疗计划

## 科学示意图的视觉增强

**⚠️强制要求：每个治疗计划必须至少包含1个使用科学示意图技能生成的AI生成图形。**

这不是可选的。治疗计划能从视觉元素中极大获益。在最终确定任何文档之前：
1. 至少生成一个示意图或图表（例如治疗路径流程图、护理协调图或治疗时间线）
2. 对于复杂计划：包含决策算法流程图
3. 对于康复计划：包含里程碑进展图

**如何生成图形：**
- 使用**科学示意图**技能生成AI驱动的出版质量图表
- 只需用自然语言描述您想要的图表
- Nano Banana Pro将自动生成、审查和改进示意图

**如何生成示意图：**
```bash
python scripts/generate_schematic.py "your diagram description" -o figures/output.png
```

AI将自动：
- 创建具有正确格式的出版质量图像
- 通过多次迭代进行审查和改进
- 确保可访问性（适合色盲、高对比度）
- 将输出保存在figures/目录中

**何时添加示意图：**
- 治疗路径流程图
- 护理协调图
- 治疗进展时间线
- 多学科团队互动图
- 药物管理流程图
- 康复方案可视化
- 临床决策算法图表
- 任何受益于可视化的复杂概念

有关创建示意图的详细指南，请参阅科学示意图技能文档。

---

## 文档格式和最佳实践

### 文档长度选项

治疗计划根据临床复杂性和使用情况有三种格式选项：

#### 选项1：一页治疗计划（大多数情况下为首选）

**何时使用**：直接的临床场景、标准协议、繁忙的临床环境

**格式**：单页包含所有可扫描的基本治疗信息
- 无需目录
- 无需冗长叙述
- 仅聚焦于可操作项目
- 类似于精准肿瘤学报告或治疗建议卡

**必需章节**（全部在一页上）：
1. **标题框**：患者信息、诊断、日期、分子/风险档案（如适用）
2. **治疗方案**：具体干预措施的编号列表
3. **支持性护理**：简短的要点
4. **理由**：1-2句话的论证（标准协议可选）
5. **监测**：关键参数和频率
6. **证据等级**：指南引用或证据等级（例如，"1级，FDA批准"）
7. **预期结果**：时间线和成功指标

**设计原则：**
- 使用小框/表格进行组织（如临床治疗建议卡格式）
- 消除所有非必要文本
- 使用临床医生熟悉的缩写
- 密集信息布局——每平方英寸最大化信息
- 想想"快速参考卡"而非"综合文档"

**示例结构：**
```latex
[Patient ID/Diagnosis Box at top]

TARGET PATIENT POPULATION
  Number of patients, demographics, key features

PRIMARY TREATMENT REGIMEN
  • Medication 1: dose, frequency, duration
  • Procedure: specific details
  • Monitoring: what and when

SUPPORTIVE CARE
  • Key supportive medications

RATIONALE
  Brief clinical justification

MOLECULAR TARGETS / RISK FACTORS
  Relevant biomarkers or risk stratification

EVIDENCE LEVEL
  Guideline reference, trial data

MONITORING REQUIREMENTS
  Key labs/vitals, frequency

EXPECTED CLINICAL BENEFIT
  Primary endpoint, timeline
```

#### 选项2：标准3-4页格式

**何时使用**：中等复杂性、需要患者教育材料、多学科协调

使用Foundation Medicine首页摘要模型，加上2-3页详细说明。

#### 选项3：扩展5-6页格式

**何时使用**：复杂合并症、研究协议、需要广泛安全监测

### 首页摘要（Foundation Medicine模型）

**关键要求：所有治疗计划必须在首页仅包含完整的执行摘要，然后才是任何目录或详细章节。**

遵循精准医学报告和临床摘要文档的Foundation Medicine模型，治疗计划以一页执行摘要开始，提供对关键可操作信息的即时访问。整个摘要必须放在首页。

**必需首页结构（按顺序）：**

1. **标题和副标题**
   - 主标题：治疗计划类型（例如，"综合治疗计划"）
   - 副标题：具体状况或重点（例如，"2型糖尿病——年轻成人患者"）

2. **报告信息框**（使用`\begin{infobox}`或`\begin{patientinfo}`）
   - 报告类型/文档目的
   - 计划创建日期
   - 患者人口统计信息（年龄、性别、去标识化）
   - 主要诊断及ICD-10编码
   - 报告作者/诊所（如适用）
   - 分析方法或使用的框架

3. **关键发现或治疗亮点**（2-4个彩色框，使用适当的框类型）
   - **主要治疗目标**（使用`\begin{goalbox}`）
     - 2-3个SMART目标，以要点形式
   - **主要干预措施**（使用`\begin{keybox}`或`\begin{infobox}`）
     - 2-3个关键干预措施（药物、非药物、监测）
   - **关键决策点**（如紧急使用`\begin{warningbox}`）
     - 重要的监测阈值或安全注意事项
   - **时间线概览**（使用`\begin{infobox}`）
     - 简要治疗持续时间/阶段
     - 关键里程碑日期

**视觉格式要求：**
- 使用`\thispagestyle{empty}`去除首页页码
- 所有内容必须放在第1页（在`\newpage`之前）
- 使用彩色框（tcolorbox包）为不同信息类型使用不同颜色
- 框应视觉突出且易于扫描
- 使用简洁的要点格式
- 目录（如包含）从第2页开始
- 详细章节从第3页开始

**示例首页结构：**
```latex
\maketitle
\thispagestyle{empty}

% Report Information Box
\begin{patientinfo}
  Report Type, Date, Patient Info, Diagnosis, etc.
\end{patientinfo}

% Key Finding #1: Treatment Goals
\begin{goalbox}[Primary Treatment Goals]
  • Goal 1
  • Goal 2
  • Goal 3
\end{goalbox}

% Key Finding #2: Main Interventions
\begin{keybox}[Core Interventions]
  • Intervention 1
  • Intervention 2
  • Intervention 3
\end{keybox}

% Key Finding #3: Critical Monitoring (if applicable)
\begin{warningbox}[Critical Decision Points]
  • Decision point 1
  • Decision point 2
\end{warningbox}

\newpage
\tableofcontents  % TOC on page 2
\newpage  % Detailed content starts page 3
```

### 简洁文档

**关键：治疗计划必须优先考虑简洁性和临床相关性。默认最多3-4页，除非临床复杂性绝对需要更多详情。**

治疗计划应优先考虑**清晰度和可操作性**而非详尽细节：

- **聚焦**：仅包含影响护理决策的临床必要信息
- **可操作**：强调需要做什么、何时做、为什么做
- **高效**：促进快速决策，同时不牺牲临床质量
- **目标长度选项**：
  - **1页格式**（直接病例首选）：包含所有基本信息的快速参考卡
  - **3-4页标准**：首页摘要+支持详情的标准格式
  - **5-6页**（罕见）：仅用于具有多种合并症或多学科干预的高度复杂病例

**精简指南：**
- **首页摘要**：使用单独的彩色框整合关键信息（目标、干预措施、决策点）——仅此一项通常就能传达基本治疗计划
- **消除冗余**：如果信息已在首页摘要中，不要在详细章节中逐字重复
- **患者教育部分**：仅关于关键主题和警告信号的3-5个关键要点
- **风险缓解部分**：仅突出关键的药物安全问题和紧急操作（而非详尽清单）
- **预期结果部分**：关于预期反应和时间线的2-3个简明声明
- **干预措施**：聚焦主要干预措施；次要/支持性措施以简要要点形式
- **广泛使用表格和要点**以提高效率
- **在结构化列表足够的情况下避免叙述性 prose**
- **适当合并相关章节**以减少页数

### 质量优先于数量

目标是尊重临床医生时间的同时确保全面患者护理的专业、临床完整文档。每个部分都应增加价值；删除或压缩不直接为治疗决策提供信息的部分。

### 引用和证据支持

**使用最少、有针对性的引用来支持临床建议：**

- **首选文本引用**：使用简短的文内引用（作者年份）或简单参考文献，而非冗长的参考文献，除非特别要求
- **何时引用**：
  - 临床实践指南建议（例如，"根据ADA 2024指南"）
  - 具体药物剂量或方案（例如，"ACC/AHA建议"）
  - 需要证据支持的新颖或争议性干预措施
  - 风险分层工具或验证的评估量表
- **何时不引用**：
  - 该领域广泛接受的标准治疗干预措施
  - 基本医学事实和常规临床实践
  - 一般患者教育内容
- **引用格式**：
  - 行内："开始二甲双胍作为一线治疗（ADA标准护理2024）"
  - 极简："治疗遵循ACC/AHA心力衰竭指南"
  - 避免正式编号引用和冗长的参考文献部分，除非文档用于学术/研究目的
- **保持简洁**：3-4页的治疗计划最多应有0-3个引用，仅在临床可信度或新颖建议所必需时添加

## 核心能力

### 1. 一般医学治疗计划

一般医学治疗计划解决需要结构化治疗干预的常见慢性疾病和急性医学问题。

#### 标准组成部分

**患者信息（去标识化）**
- 人口统计信息（年龄、性别、相关医学背景）
- 活跃医疗状况和合并症
- 当前用药和过敏史
- 相关社会和家族史
- 功能状态和基线评估
- **HIPAA合规**：根据安全港方法移除所有18个标识符

**诊断和评估摘要**
- 主要诊断及ICD-10编码
- 次要诊断和合并症
- 严重程度分类和分期
- 功能限制和生活质量影响
- 风险分层（例如，心血管风险、跌倒风险）
- 预后指标

**治疗目标（SMART格式）**

短期目标（1-3个月）：
- **具体**：明确定义的结果（例如，"将HbA1c降至<7%"）
- **可衡量**：可量化指标（例如，"收缩压降低10 mmHg"）
- **可实现**：考虑到患者能力是现实的
- **相关**：符合患者优先事项和价值观
- **有时限**：具体时间范围（例如，"8周内"）

长期目标（6-12个月）：
- 疾病控制或缓解目标
- 功能改善目标
- 生活质量提升
- 并发症预防
- 维持独立性

**干预措施**

*药物疗法*：
- 具体剂量、途径、频率的药物
- 滴定方案和目标剂量
- 药物相互作用考虑
- 不良反应监测
- 用药整合

*非药物疗法*：
- 生活方式改变（饮食、运动、戒烟）
- 行为干预
- 患者教育和自我管理
- 监测和自我追踪（血糖、血压、体重）
- 辅助设备或适应性设备

*有创操作*：
- 计划操作或干预措施
- 转诊至专科医生
- 诊断测试时间表
- 预防性护理（疫苗接种、筛查）

**时间线和日程**
- 具有具体时间线的治疗阶段
- 就诊频率（每周、每月、每季度）
- 里程碑评估和目标评估
- 药物调整时间表
- 预期治疗持续时间

**监测参数**
- 要追踪的临床结果（生命体征、实验室值、症状）
- 评估工具和量表（例如，PHQ-9、疼痛量表）
- 监测频率
- 干预或升级的阈值
- 患者报告的结果

**预期结果**
- 主要结果指标
- 成功标准和基准
- 改善的预期时间线
- 治疗修改的标准
- 长期预后

**随访计划**
- 计划就诊和再评估
- 沟通计划（电话、安全消息）
- 紧急联系程序
- 紧急评估的标准
- 转诊或出院计划

**患者教育**
- 对状况和治疗理由的理解
- 自我管理技能培训
- 给药依从性
- 警告信号和何时就医
- 资源和支持服务

**风险缓解**
- 潜在不良影响及其处理
- 药物相互作用和禁忌症
- 跌倒预防、感染预防
- 紧急行动计划
- 安全监测

#### 常见应用

- 糖尿病管理
- 高血压控制
- 心力衰竭治疗
- COPD管理
- 哮喘护理计划
- 高脂血症治疗
- 骨关节炎管理
- 慢性肾脏病

### 2. 康复治疗计划

康复计划侧重于通过结构化治疗项目恢复功能、改善移动性和增强生活质量。

#### 核心组成部分

**功能评估**
- 基线功能状态（ADL、IADL）
- 关节活动度、力量、平衡、耐力
- 步态分析和移动性评估
- 标准化措施（FIM、Barthel指数、Berg平衡量表）
- 环境评估（家庭安全、无障碍）

**康复目标**

*损伤级别目标*：
- 改善肩关节屈曲至140度
- 股四头肌力量增加2/5 MMT等级
- 增强平衡（Berg评分>45/56）

*活动级别目标*：
- 使用辅助设备独立行走150英尺
- 在监督下使用扶手爬12级楼梯
- 独立进行床椅转移

*参与级别目标*：
- 带着调整重返工作
- 恢复娱乐活动
- 独立的社区移动

**治疗干预措施**

*物理治疗*：
- 治疗性运动（力量、伸展、耐力）
- 手法治疗技术
- 步态训练和平衡活动
- 物理因子（热、冰、电刺激、超声）
- 辅助设备训练

*作业治疗*：
- ADL训练（沐浴、穿衣、修饰、进食）
- 上肢力量和协调
- 适应性设备和改造
- 节能技术
- 认知康复

*语言病理学*：
- 吞咽治疗和吞咽困难管理
- 沟通策略和增强设备
- 认知语言治疗
- 语音治疗

*其他服务*：
- 娱乐治疗
- 水中治疗
- 心脏康复
- 肺康复
- 前庭康复

**治疗日程**
- 频率：PT每周3次，OT每周2次（示例）
- 治疗时长：45-60分钟
- 治疗阶段持续时间（急性、亚急性、维持）
- 预期总时长：8-12周
- 再评估间隔

**进展监测**
- 每周功能评估
- 标准化结果措施
- 目标达成量表
- 疼痛和症状追踪
- 患者满意度

**家庭锻炼计划**
- 具体运动及重复/组/频率
- 预防措施和安全说明
- 进展标准
- 自我监测策略

#### 专科康复

- 中风后康复
- 骨科康复（关节置换、骨折）
- 心脏康复（心梗后、手术后）
- 肺康复
- 前庭康复
- 神经康复
- 运动损伤康复

### 3. 心理健康治疗计划

心理健康治疗计划通过整合的心理治疗、药物和社会心理干预来解决精神科状况。

#### 必要组成部分

**精神科评估**
- 主要精神科诊断（DSM-5标准）
- 症状严重程度和功能损害
- 共病心理健康状况
- 物质使用评估
- 自杀/杀人风险评估
- 创伤史和PTSD筛查
- 心理健康的社会决定因素

**治疗目标**

*症状减轻*：
- 减轻抑郁严重程度（PHQ-9评分从18降至<10）
- 减少焦虑症状（GAD-7评分<5）
- 改善睡眠质量（匹兹堡睡眠质量指数）
- 稳定情绪（减少情绪发作）

*功能改善*：
- 重返工作或学校
- 改善社会关系和支持
- 增强应对技能和情绪调节
- 增加参与有意义的活动

*恢复导向目标*：
- 建立韧性和自我效能
- 发展危机管理技能
- 建立可持续的健康常规
- 实现个人恢复目标

**治疗干预措施**

*心理治疗*：
- 循证模式（CBT、DBT、ACT、心理动力学、IPT）
- 治疗频率（每周、隔周）
- 治疗持续时间（12-16周，持续）
- 具体技术和目标
- 团体治疗参与

*精神药理学*：
- 药物类别和理由
- 起始剂量和滴定方案
- 目标症状
- 预期反应时间线（抗抑郁药2-4周）
- 副作用监测
- 联合治疗考虑

*社会心理干预*：
- 病例管理服务
- 同伴支持项目
- 家庭治疗或心理教育
- 职业康复
- 支持性住房或社区整合
- 物质滥用治疗

**安全计划**
- 危机联系和紧急服务
- 警告信号和触发因素
- 应对策略和自我安慰技术
- 安全环境改造
- 手段限制（火器、药物）
- 支持系统激活

**监测和评估**
- 症状评定量表（每周或隔周）
- 用药依从性和副作用
- 自杀意念筛查
- 功能状态评估
- 治疗参与和治疗联盟

**患者和家属教育**
- 关于诊断的心理教育
- 治疗理由和预期
- 用药信息
- 复发预防策略
- 社区资源

#### 心理健康状况

- 重度抑郁症
- 焦虑障碍（GAD、惊恐、社交焦虑）
- 双相情感障碍
- 精神分裂症和精神病性障碍
- PTSD和创伤相关障碍
- 进食障碍
- 物质使用障碍
- 人格障碍

### 4. 慢性疾病管理计划

针对需要持续监测、治疗调整和多学科协调的慢性疾病的综合长期护理计划。

#### 关键特征

**疾病特定目标**
- 每项指南的循证治疗目标
- 分期适当的干预措施
- 并发症预防策略
- 疾病进展监测

**自我管理支持**
- 患者激活和参与
- 共同决策
- 症状变化行动计划
- 技术支持的监测（应用、远程监测）

**护理协调**
- 主治医生监督
- 专科会诊和共同管理
- 护理过渡（医院到家庭）
- 跨提供者的药物管理
- 沟通协议

**人群健康整合**
- 登记追踪和外展
- 预防性护理和筛查日程
- 质量指标报告
- 护理差距识别

#### 适用状况

- 1型和2型糖尿病
- 心血管疾病（CHF、CAD）
- 慢性呼吸系统疾病（COPD、哮喘）
- 慢性肾脏病
- 炎症性肠病
- 类风湿关节炎和自身免疫状况
- 艾滋病/艾滋病
- 癌症生存护理

### 5. 围手术期护理计划

针对外科和操作患者的结构化计划，涵盖术前准备、术中管理和术后恢复。

#### 组成部分

**术前评估**
- 手术适应症和计划操作
- 术前风险分层（ASA分级、心脏风险）
- 医疗状况优化
- 药物管理（继续、停用）
- 术前检查和 clearance
- 知情同意和患者教育

**围手术期干预措施**
- 手术后增强恢复（ERAS）方案
- 静脉血栓栓塞预防
- 抗生素预防
- 血糖控制策略
- 疼痛管理计划（多模式镇痛）

**术后护理**
- 即时恢复目标（24-48小时）
- 早期活动方案
- 饮食推进
- 伤口护理和引流管管理
- 疼痛控制方案
- 并发症监测

**出院计划**
- 活动限制和推进
- 用药整合
- 随访预约
- 家庭健康或康复服务
- 重返工作时间线

### 6. 疼痛管理计划

使用循证干预措施和阿片类药物节约策略的多模式方法治疗急性和慢性疼痛。

#### 综合组成部分

**疼痛评估**
- 疼痛位置、质量、强度（0-10量表）
- 时间模式（持续、间歇、爆发性）
- 加重和缓解因素
- 功能影响（睡眠、活动、情绪）
- 既往治疗和反应
- 社会心理因素

**多模式干预措施**

*药物疗法*：
- 非阿片类镇痛药（对乙酰氨基酚、NSAIDs）
- 辅助药物（抗抑郁药、抗惊厥药、肌肉松弛剂）
- 局部药物（利多卡因、辣椒素、双氯芬酸）
- 阿片类药物治疗（适当时，含风险缓解）
- 滴定和转换策略

*介入性操作*：
- 神经阻滞和注射
- 射频消融
- 脊髓刺激
- 鞘内药物输注

*非药物疗法*：
- 物理治疗和锻炼
- 认知行为疼痛治疗
- 正念和放松技术
- 针灸
- TENS设备

**阿片类药物安全（如开具）**
- 适应症和计划持续时间
- 处方药监测项目（PDMP）检查
- 阿片类药物风险评估工具
- 纳洛酮处方
- 治疗协议
- 随机尿液药物筛查
- 频繁随访和再评估

**功能目标**
- 具体活动改善
- 睡眠质量增强
- 减少疼痛干扰
- 改善生活质量
- 重返工作或有意义活动

## 最佳实践

### 简洁性和聚焦（最高优先级）

**治疗计划必须简洁，聚焦于可操作的临床信息：**

- **1页格式是首选**：对于大多数临床场景，单页治疗计划（如精准肿瘤学报告）提供所有必要信息
- **默认最短格式**：从1页开始；仅在临床复杂性真正需要时才扩展
- **每个句子都必须增加价值**：如果某个部分不改变临床决策，则完全省略
- **想想"快速参考卡"而非"综合教科书"**：忙碌的临床医生需要可扫描的密集信息
- **避免学术冗长**：这是临床文档，不是文献综述或教学文档
- **按复杂性的最大长度**：
  - 简单/标准病例：1页
  - 中等复杂性：3-4页（首页摘要+详情）
  - 高复杂性（罕见）：最多5-6页

### 首页摘要（最重要）

**始终创建一页执行摘要作为首页：**
- 首页必须仅包含：标题、报告信息框和关键发现框
- 这提供了类似精准医学报告的一目了然概览
- 目录和详细章节从第2页或更晚开始
- 想想"临床亮点"页面，忙碌的临床医生可以在30秒内扫描
- 使用2-4个彩色框显示不同的关键发现（目标、干预措施、决策点）
- **强大的首页通常可以独立存在**——后续页面用于详情，而非重复

### SMART目标设定

所有治疗目标应符合SMART标准：

- **具体**："改善HbA1c至<7%"而非"更好的糖尿病控制"
- **可衡量**：使用可量化指标、验证量表、客观措施
- **可实现**：考虑患者能力、资源、社会支持
- **相关**：符合患者价值观、优先事项和生活情况
- **有时限**：为目标实现和再评估定义明确的时间框架

### 以患者为中心的护理

✓ **共同决策**：让患者参与目标设定和治疗选择  
✓ **文化能力**：尊重文化信仰、语言偏好、健康素养  
✓ **患者偏好**：尊重治疗偏好和个人价值观  
✓ **个体化**：根据患者的独特情况调整计划  
✓ **赋能**：支持患者激活和自我管理  

### 循证实践

✓ **临床指南**：遵循当前专科协会建议  
✓ **质量措施**：纳入HEDIS、CMS质量措施  
✓ **比较有效性**：使用疗效已证明的治疗  
✓ **避免低价值护理**：消除不必要的检查和干预  
✓ **保持更新**：根据新出现的证据更新计划  

### 文档标准

✓ **完整性**：包含所有必需元素  
✓ **清晰度**：使用清晰、专业的医学语言  
✓ **准确性**：确保事实正确性和当前信息  
✓ **及时性**：及时记录计划  
✓ **可读性**：专业格式和组织  
✓ **签名和日期**：验证所有治疗计划  

### 监管合规

✓ **HIPAA隐私**：去标识化所有受保护健康信息  
✓ **知情同意**：记录患者理解和同意  
✓ **计费支持**：包含支持医疗必要性的文档  
✓ **质量报告**：启用质量指标提取  
✓ **法律保护**：维护可防御的临床文档  

### 多学科协调

✓ **团队沟通**：跨护理团队共享计划  
✓ **角色清晰度**：为每个团队成员定义责任  
✓ **护理过渡**：确保持续跨设置  
✓ **专科整合**：协调亚专科护理  
✓ **以患者为中心的医疗之家**：遵循PCMH原则  

## LaTeX模板使用

### 模板选择

根据临床背景和所需长度选择适当的模板：

#### 简洁模板（首选）

1. **one_page_treatment_plan.tex** - 大多数情况下**首选**
   - 所有临床专科
   - 标准协议和直接病例
   - 类似于精准肿瘤学报告的快速参考格式
   - 密集、可扫描、以临床医生为中心
   - 除非复杂性需要更多详情，否则使用此模板

#### 标准模板（3-4页）

仅当一页格式因复杂性不足时使用：

2. **general_medical_treatment_plan.tex** - 初级护理、慢性病、一般医学
3. **rehabilitation_treatment_plan.tex** - PT/OT、术后、损伤恢复
4. **mental_health_treatment_plan.tex** - 精神科状况、行为健康
5. **chronic_disease_management_plan.tex** - 复杂慢性病、多重状况
6. **perioperative_care_plan.tex** - 外科患者、操作护理
7. **pain_management_plan.tex** - 急性或慢性疼痛状况

**注意**：即使使用标准模板，也要精简使其（最多3-4页），移除非必要章节。

### 模板结构

所有LaTeX模板包括：
- 具有适当边距和字体的专业格式
- 所有必需组成部分的结构化章节
- 药物、干预措施、时间线的表格
- 带有SMART标准的目标追踪部分
- 提供者签名和日期的空间
- HIPAA兼容的去标识化指导
- 带有详细说明的注释

### 生成PDF

```bash
# Compile LaTeX template to PDF
pdflatex general_medical_treatment_plan.tex

# For templates with references
pdflatex treatment_plan.tex
bibtex treatment_plan
pdflatex treatment_plan.tex
pdflatex treatment_plan.tex
```

## 验证和质量保证

### 完整性检查

使用验证脚本确保所有必需章节都存在：

```bash
python check_completeness.py my_treatment_plan.tex
```

脚本检查：
- 患者信息部分
- 诊断和评估
- SMART目标（短期和长期）
- 干预措施（药物、非药物）
- 时间线和日程
- 监测参数
- 预期结果
- 随访计划
- 患者教育
- 风险缓解

### 治疗计划验证

治疗计划质量的综合验证：

```bash
python validate_treatment_plan.py my_treatment_plan.tex
```

验证包括：
- SMART目标标准评估
- 循证干预措施验证
- 时间线可行性检查
- 监测参数充分性
- 安全和风险缓解审查
- 监管合规检查

### 质量检查清单

根据质量检查清单（`quality_checklist.md`）审查治疗计划：

**临床质量**
- [ ] 诊断准确且正确编码（ICD-10）
- [ ] 目标符合SMART且以患者为中心
- [ ] 干预措施循证且符合指南
- [ ] 时间线现实且明确定义
- [ ] 监测计划全面
- [ ] 安全注意事项已解决

**以患者为中心的护理**
- [ ] 纳入患者偏好和价值观
- [ ] 记录共同决策
- [ ] 健康素养适当的语言
- [ ] 解决文化考虑
- [ ] 包含患者教育计划

**监管合规**
- [ ] HIPAA兼容的去标识化
- [ ] 记录医疗必要性
- [ ] 注明知情同意
- [ ] 提供者签名和资质
- [ ] 计划创建/修订日期

**协调和沟通**
- [ ] 记录专科转诊
- [ ] 定义护理团队角色
- [ ] 随访日程清晰
- [ ] 提供紧急联系人
- [ ] 解决过渡计划

## 与其他技能的集成

### 临床报告集成

治疗计划通常伴随其他临床文档：

- **SOAP笔记**（`clinical-reports`技能）：记录持续实施
- **H&P**（`clinical-reports`技能）：初始评估为治疗计划提供信息
- **出院摘要**（`clinical-reports`技能）：总结治疗计划执行
- **进展笔记**：追踪目标实现和计划修改

### 科学写作集成

循证治疗计划需要文献支持：

- **引文管理**（`citation-management`技能）：参考临床指南
- **文献综述**（`literature-review`技能）：了解治疗证据基础
- **研究查询**（`research-lookup`技能）：寻找当前最佳实践
- **期刊模板**（`venue-templates`技能）：用于出版就绪的医学写作风格

**医学写作风格**：准备用于出版的治疗相关内容（病例报告、临床指南）时，请参阅venue-templates技能的`medical_journal_styles.md`，了解NEJM、Lancet、JAMA和BMJ使用的证据分级语言、以患者为中心的术语和结构化摘要格式的指导。

### 研究集成

治疗计划可能是为临床试验或研究开发的：

- **研究资助**（`research-grants`技能）：资助研究的研究方案
- **临床试验报告**（`clinical-reports`技能）：干预措施文档

## 常见用例

### 示例1：2型糖尿病管理

**场景**：58岁新诊断2型糖尿病患者，HbA1c 8.5%，BMI 32

**模板**：`general_medical_treatment_plan.tex`

**目标**：
- 短期：3个月内将HbA1c降至<7.5%
- 长期：6个月内达到HbA1c <7%，减重15磅

**干预措施**：
- 药物疗法：二甲双胍500mg每日两次，滴定至1000mg每日两次
- 生活方式：地中海饮食，每周150分钟中等强度运动
- 教育：糖尿病自我管理教育，血糖监测

### 示例2：中风后康复

**场景**：70岁患者左MCA中风伴右侧偏瘫

**模板**：`rehabilitation_treatment_plan.tex`

**目标**：
- 短期：4周内右上肢力量从2/5改善至3/5
- 长期：12周内使用手杖独立行走150英尺

**干预措施**：
- PT每周3次：步态训练、平衡、力量训练
- OT每周3次：ADL训练、上肢功能
- SLP每周2次：吞咽治疗

### 示例3：重度抑郁障碍

**场景**：35岁中度抑郁患者，PHQ-9评分16

**模板**：`mental_health_treatment_plan.tex`

**目标**：
- 短期：8周内将PHQ-9降至<10
- 长期：达到缓解（PHQ-9 <5），重返工作

**干预措施**：
- 心理治疗：每周CBT sessions
- 药物：舍曲林50mg每日，滴定至100mg
- 生活方式：睡眠卫生，每周5次30分钟运动

### 示例4：全膝关节置换术

**场景**：68岁患者因骨关节炎计划右膝TKA

**模板**：`perioperative_care_plan.tex`

**术前目标**：
- 优化糖尿病控制（血糖<180）
- 根据协议停用抗凝药物
- 完成医疗 clearance

**术后目标**：
- POD 1行走50英尺
- POD 3膝关节屈曲90度
- POD 2-3带PT服务出院回家

### 示例5：慢性腰背痛

**场景**：45岁慢性非特异性腰背痛患者，疼痛7/10

**模板**：`pain_management_plan.tex`

**目标**：
- 短期：6周内将疼痛降至4/10
- 长期：全职重返工作，疼痛2-3/10

**干预措施**：
- 药物疗法：加巴喷丁300mg每日三次，度洛西汀60mg每日
- PT：核心力量训练、麦肯锡练习每周2次×8周
- 行为：疼痛CBT、正念冥想
- 介入：如反应不足考虑腰部ESI

## 专业标准和指南

治疗计划应符合：

### 一般医学
- 美国糖尿病协会（ADA）护理标准
- ACC/AHA心血管指南
- GOLD COPD指南
- JNC-8高血压指南
- KDIGO慢性肾脏病指南

### 康复
- APTA临床实践指南
- AOTA实践指南
- 心脏康复指南（AHA/AACVPR）
- 中风康复指南

### 心理健康
- APA实践指南
- VA/DoD临床实践指南
- NICE指南（国家健康和护理卓越研究所）
-  Cochrane关于精神科干预的系统综述

### 疼痛管理
- CDC阿片类药物处方指南
- AAPM/APS慢性疼痛指南
- WHO疼痛阶梯
- 多模式镇痛最佳实践

## 时间线生成

使用时间线生成脚本创建可视化治疗时间线：

```bash
python timeline_generator.py --plan my_treatment_plan.tex --output timeline.pdf
```

生成：
- 治疗阶段的甘特图
- 目标评估的里程碑标记
- 药物滴定时间表
- 随访预约日历
- 随时间变化的干预强度

## 支持和资源

### 模板生成

交互式模板选择：

```bash
cd .claude/skills/treatment-plans/scripts
python generate_template.py

# Or specify type directly
python generate_template.py --type mental_health --output depression_treatment_plan.tex
```

### 验证工作流

1. **创建治疗计划**使用适当的LaTeX模板
2. **检查完整性**：`python check_completeness.py plan.tex`
3. **验证质量**：`python validate_treatment_plan.py plan.tex`
4. **审查检查清单**：与`quality_checklist.md`比较
5. **生成PDF**：`pdflatex plan.tex`
6. **与患者审查**：确保理解和同意
7. **实施和记录**：在临床笔记中追踪进展

### 额外资源

- 专科协会的临床实践指南
- AHRQ有效医疗保健计划
- Cochrane Library关于干预证据
- UpToDate和DynaMed关于治疗建议
- CMS质量措施和HEDIS规范

## 专业文档样式

### 概述

治疗计划可以使用`medical_treatment_plan.sty` LaTeX包增强专业医学文档样式。这种自定义样式将普通的学术文档转换为视觉吸引的、颜色编码的临床文档，在保持科学严谨性的同时提高可读性和可用性。

### 医学治疗计划样式包

`medical_treatment_plan.sty`包（位于`assets/medical_treatment_plan.sty`）提供：

**专业配色方案**
- **主蓝色**（RGB：0, 102, 153）：页眉、章节标题、主要强调
- **次级蓝色**（RGB：102, 178, 204）：浅背景、细微强调
- **强调蓝色**（RGB：0, 153, 204）：超链接、关键高亮
- **成功绿色**（RGB：0, 153, 76）：目标、积极结果
- **警告红色**（RGB：204, 0, 0）：警告、关键信息
- **深灰色**（RGB：64, 64, 64）：正文
- **浅灰色**（RGB：245, 245, 245）：背景填充

**样式元素**
- 带专业线条的自定义彩色页眉和页脚
- 带下划线的蓝色章节标题，层次清晰
- 带彩色标题和交替行的增强表格格式
- 带彩色项目符号和编号的优化列表间距
- 具有适当边距的专业页面布局

### 自定义信息框

样式包包含五个专门的框环境，用于组织临床信息：

#### 1. 信息框（蓝色边框、浅灰色背景）

用于一般信息、临床评估和测试时间表：

```latex
\begin{infobox}[Title]
  \textbf{Key Information:}
  \begin{itemize}
    \item Clinical assessment details
    \item Testing schedules
    \item General guidance
  \end{itemize}
\end{infobox}
```

**用例**：代谢状态、基线评估、监测时间表、滴定方案

#### 2. 警告框（红色边框、黄色背景）

用于关键决策点、安全协议和警报：

```latex
\begin{warningbox}[Alert Title]
  \textbf{Important Safety Information:}
  \begin{itemize}
    \item Critical drug interactions
    \item Safety monitoring requirements
    \item Red flag symptoms requiring immediate action
  \end{itemize}
\end{warningbox}
```

**用例**：药物安全、决策点、禁忌症、紧急协议

#### 3. 目标框（绿色边框、绿色调背景）

用于治疗目标、指标和成功标准：

```latex
\begin{goalbox}[Treatment Goals]
  \textbf{Primary Objectives:}
  \begin{itemize}
    \item Reduce HbA1c to <7\% within 3 months
    \item Achieve 5-7\% weight loss in 12 weeks
    \item Complete diabetes education program
  \end{itemize}
\end{goalbox}
```

**用例**：SMART目标、目标结果、成功指标、CGM目标

#### 4. 关键点框（蓝色背景）

用于执行摘要、关键要点和重要建议：

```latex
begin{keybox}[Key Highlights]
  \textbf{Essential Points:}
  \begin{itemize}
    \item Main therapeutic approach
    \item Critical patient instructions
    \item Priority interventions
  \end{itemize}
\end{keybox}
```

**用例**：计划概览、餐盘法说明、重要饮食指南

#### 5. 紧急框（大型红色设计）

用于紧急联系人和紧急协议：

```latex
\begin{emergencybox}
  \begin{itemize}
    \item \textbf{Emergency Services:} 911
    \item \textbf{Endocrinology Office:} [Phone] (business hours)
    \item \textbf{After-Hours Hotline:} [Phone] (nights/weekends)
    \item \textbf{Pharmacy:} [Phone and location]
  \end{itemize}
\end{emergencybox}
```

**用例**：紧急联系人、关键热线、紧急资源信息

#### 6. 患者信息框（白色带蓝色边框）

用于患者人口统计信息和基线信息：

```latex
\begin{patientinfo}
  \begin{tabular}{ll}
    \textbf{Age:} & 23 years \\
    \textbf{Sex:} & Male \\
    \textbf{Diagnosis:} & Type 2 Diabetes Mellitus \\
    \textbf{Plan Start Date:} & \today \\
  \end{tabular}
\end{patientinfo}
```

**用例**：患者信息部分、人口统计数据

### 专业表格格式

具有医学样式的增强表格环境：

```latex
\begin{medtable}{Caption Text}
\begin{tabular}{|p{5cm}|p{4cm}|p{4.5cm}|}
\hline
\tableheadercolor  % Blue header with white text
\textcolor{white}{\textbf{Column 1}} & 
\textcolor{white}{\textbf{Column 2}} & 
\textcolor{white}{\textbf{Column 3}} \\
\hline
Data row 1 content & Value 1 & Details 1 \\
\hline
\tablerowcolor  % Alternating light gray row
Data row 2 content & Value 2 & Details 2 \\
\hline
Data row 3 content & Value 3 & Details 3 \\
\hline
\end{tabular}
\caption{Table caption}
\end{medtable}
```

**特点：**
- 白色文字的蓝色标题，视觉突出
- 交替行颜色（`\tablerowcolor`）提高可读性
- 自动居中和间距
- 专业的边框和填充

### 使用样式包

#### 基础设置

1. **添加到文档导言区：**

```latex
% !TEX program = xelatex
\documentclass[11pt,letterpaper]{article}

% Use custom medical treatment plan style
\usepackage{medical_treatment_plan}
\usepackage{natbib}

\begin{document}
\maketitle
% Your content here
\end{document}
```

2. **确保样式文件与您的.tex文件在同一目录**，或安装到LaTeX路径

3. **使用XeLaTeX编译**（推荐获得最佳结果）：

```bash
xelatex treatment_plan.tex
bibtex treatment_plan
xelatex treatment_plan.tex
xelatex treatment_plan.tex
```

#### 自定义标题页

软件包自动格式化为专业的蓝色标题：

```latex
\title{\textbf{Individualized Diabetes Treatment Plan}\\
\large{23-Year-Old Male Patient with Type 2 Diabetes}}
\author{Comprehensive Care Plan}
\date{\today}

\begin{document}
\maketitle
```

这会创建一个带有白色文字和清晰层次结构的引人注目的蓝色框。

### 编译要求

**必需的LaTeX包**（由样式自动加载）：
- `geometry` - 页面布局和边距
- `xcolor` - 颜色支持
- `tcolorbox`带`[most]`库 - 自定义彩色框
- `tikz` - 图形和绘图
- `fontspec` - 字体管理（XeLaTeX/LuaLaTeX）
- `fancyhdr` - 自定义页眉和页脚
- `titlesec` - 章节样式
- `enumitem` - 增强列表格式
- `booktabs` - 专业表格规则
- `longtable` - 多页表格
- `array` - 增强表格功能
- `colortbl` - 彩色表格单元
- `hyperref` - 超链接和PDF元数据
- `natbib` - 参考文献管理

**推荐编译：**

```bash
# Using XeLaTeX (best font support)
xelatex document.tex
bibtex document
xelatex document.tex
xelatex document.tex

# Using PDFLaTeX (alternative)
pdflatex document.tex
bibtex document
pdflatex document.tex
pdflatex document.tex
```

### 自定义选项

#### 更改颜色

编辑样式文件以修改配色方案：

```latex
% In medical_treatment_plan.sty
\definecolor{primaryblue}{RGB}{0, 102, 153}      % Modify these
\definecolor{secondaryblue}{RGB}{102, 178, 204}
\definecolor{accentblue}{RGB}{0, 153, 204}
\definecolor{successgreen}{RGB}{0, 153, 76}
\definecolor{warningred}{RGB}{204, 0, 0}
```

#### 调整页面布局

在样式文件中修改几何设置：

```latex
\RequirePackage[margin=1in, top=1.2in, bottom=1.2in]{geometry}
```

#### 自定义字体（仅限XeLaTeX）

在样式文件中取消注释并修改：

```latex
\setmainfont{Your Preferred Font}
\setsansfont{Your Sans-Serif Font}
```

#### 页眉/页脚自定义

在样式文件中修改：

```latex
\fancyhead[L]{\color{primaryblue}\sffamily\small\textbf{Treatment Plan Title}}
\fancyhead[R]{\color{darkgray}\sffamily\small Patient Info}
```

### 样式包下载和安装

#### 选项1：复制到项目目录

将`assets/medical_treatment_plan.sty`复制到与您的`.tex`文件相同的目录。

#### 选项2：安装到用户TeX目录

```bash
# Find your local texmf directory
kpsewhich -var-value TEXMFHOME

# Copy to appropriate location (usually ~/texmf/tex/latex/)
mkdir -p ~/texmf/tex/latex/medical_treatment_plan
cp assets/medical_treatment_plan.sty ~/texmf/tex/latex/medical_treatment_plan/

# Update TeX file database
texhash ~/texmf
```

#### 选项3：系统级安装

```bash
# Copy to system texmf directory (requires sudo)
sudo cp assets/medical_treatment_plan.sty /usr/local/texlive/texmf-local/tex/latex/
sudo texhash
```

### 其他专业样式（可选）

可从CTAN获取的其他医学/临床文档样式：

**期刊样式：**
```bash
# Install via TeX Live Manager
tlmgr install nejm        # New England Journal of Medicine
tlmgr install jama        # JAMA style
tlmgr install bmj         # British Medical Journal
```

**一般专业样式：**
```bash
tlmgr install apa7        # APA 7th edition (health sciences)
tlmgr install IEEEtran    # IEEE (medical devices/engineering)
tlmgr install springer    # Springer journals
```

**从CTAN下载：**
- 访问：https://ctan.org/
- 搜索医学文档类
- 按包说明下载和安装

### 故障排除

**问题：找不到包**
```bash
# Install missing packages via TeX Live Manager
sudo tlmgr update --self
sudo tlmgr install tcolorbox tikz pgf
```

**问题：缺少字符（✓、≥等）**
- 使用XeLaTeX而非PDFLaTeX
- 或替换为LaTeX命令：`$\checkmark$`、`$\geq$`
- 需要`amssymb`包用于数学符号

**问题：页眉高度警告**
- 样式文件设置`\setlength{\headheight}{22pt}`
- 根据需要进行调整

**问题：框不呈现**
```bash
# Ensure complete tcolorbox installation
sudo tlmgr install tcolorbox tikz pgf
```

**问题：找不到字体（XeLaTeX）**
- 注释掉.sty文件中的自定义字体行
- 或在系统上安装指定的字体

### 样式文档最佳实践

1. **适当使用框**
   - 将框类型与内容目的匹配（目标→绿色，警告→黄色/红色）
   - 不要过度使用框；仅保留给真正重要的信息
   - 保持框内容简洁和聚焦

2. **视觉层次**
   - 使用章节样式进行结构
   - 框用于强调和组织
   - 表格用于比较数据
   - 列表用于顺序或分组项目

3. **颜色一致性**
   - 坚持定义的配色方案
   - 使用`\textcolor{primaryblue}{\textbf{Text}}`进行强调
   - 保持含义一致（红色=警告，绿色=目标）

4. **空白**
   - 不要用框把页面填得太满
   - 主要部分之间使用`\vspace{0.5cm}}`
   - 彩色元素周围留出呼吸空间

5. **专业外观**
   - 始终将可读性作为首要任务
   - 确保足够的对比度以确保可访问性
   - 在灰度模式下测试打印输出
   - 整个文档保持样式一致

6. **表格格式**
   - 所有标题行使用`\tableheadercolor`
   - 在>3行的表格中交替应用`\tablerowcolor`
   - 保持列宽平衡
   - 大表格使用`\small\sffamily`

### 示例：样式治疗计划结构

```latex
% !TEX program = xelatex
\documentclass[11pt,letterpaper]{article}
\usepackage{medical_treatment_plan}
\usepackage{natbib}

\title{\textbf{Comprehensive Treatment Plan}\\
\large{Patient-Centered Care Strategy}}
\author{Multidisciplinary Care Team}
\date{\today}

\begin{document}
\maketitle

\section*{Patient Information}
\begin{patientinfo}
  % Demographics table
\end{patientinfo}

\section{Executive Summary}
\begin{keybox}[Plan Overview]
  % Key highlights
\end{keybox}

\section{Treatment Goals}
\begin{goalbox}[SMART Goals - 3 Months]
  \begin{medtable}{Primary Treatment Targets}
    % Goals table with colored headers
  \end{medtable}
\end{goalbox}

\section{Medication Plan}
\begin{infobox}[Titration Schedule]
  % Medication instructions
\end{infobox}

\begin{warningbox}[Critical Decision Point]
  % Important safety information
\end{warningbox}

\section{Emergency Protocols}
\begin{emergencybox}
  % Emergency contacts
\end{emergencybox}

\bibliographystyle{plainnat}
\bibliography{references}
\end{document}
```

### 专业样式的好处

**临床实践：**
- 患者就诊期间更快地扫描信息
- 关键与常规信息的清晰视觉层次
- 适合患者文件的专业外观
- 颜色编码部分减少认知负荷

**教育用途：**
- 教学材料增强可读性
- 概念类型的视觉区分（目标、警告、操作程序）
- 病例讨论的专业演示
- 打印和数字就绪格式

**文档质量：**
- 现代、精美的外观
- 在改善美学的同时保持临床准确性
- 跨治疗计划的标准化格式
- 易于根据机构品牌进行定制

**患者参与：**
- 比密集文本文档更易于接近
- 颜色编码帮助患者识别关键部分
- 专业外观建立信任
- 清晰的组织促进理解

## 伦理考虑

### 知情同意
所有治疗计划应涉及患者对拟议干预措施的理解和自愿同意。

### 文化敏感性
治疗计划必须尊重多元化的文化信仰、健康实践和沟通方式。

### 健康公平
在制定计划时考虑健康的社会决定因素、获取障碍和健康差距。

### 隐私保护
保持严格的HIPAA合规；在共享文档中去标识化所有受保护健康信息。

### 自主性和行善
在促进患者福祉的同时，平衡医学建议与患者自主权和价值观。

## 许可

Claude科学作家项目的一部分。请参阅主许可文件。
