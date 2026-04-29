# 自然与科学写作风格指南

 Nature、Science 及相关高影响力多学科期刊（Nature Communications、Science Advances、PNAS）的综合写作指南。

**最后更新**：2024

---

## 概述

Nature 和 Science 是全球最顶尖的多学科科学期刊。在此发表论文必须吸引各学科的科学家，而不仅仅是专业人士。这一根本特点决定了写作风格。

### 核心理念

> "如果结构生物学家无法理解您的粒子物理论文为何重要，该论文将无法在 Nature 上发表。"

**主要目标**：向受教育但非专业的受众传播突破性科学成果。

---

## 受众与语气

### 目标读者

- 任何领域的 **博士级** 科学家
- 熟悉科学方法
- **不是** 您特定子领域的专家
- 广泛阅读以跟踪科学前沿

### 语气特点

| 特点 | 描述 |
|---------------|-------------|
| **通俗易懂** | 避免行话；解释技术概念 |
| **引人入胜** | 吸引读者；讲述故事 |
| **重要意义** | 强调为何具有广泛影响 |
| **自信** | 清晰陈述发现（附以适当的保留） |
| **主动** | 使用主动语态；可接受第一人称 |

### 文风

- **鼓励使用第一人称复数（"we"）**："We discovered that..." 而非 "It was discovered that..."
- **优先使用主动语态**："We measured..." 而非 "Measurements were taken..."
- **直接陈述**："Protein X controls Y" 而非 "Protein X appears to potentially control Y"

---

## 摘要

### 风格要求

- **流畅段落**（**不**使用带标签的章节结构）
- Nature 为 **150-200 词**；Nature Communications 最多 250 词
- 摘要中**不引用**文献
- **不使用缩写**（若必要，在首次出现时定义）
- **自包含**：不阅读论文即可理解

### 摘要结构（隐性）

按流畅散文形式撰写，覆盖：

1. **背景**（1-2 句）：为何该领域重要
2. **缺口/问题**（1 句）：什么是未知或有问题的
3. **方法**（1 句）：您做了什么（简要）
4. **关键发现**（2-3 句）：主要结果及关键数据
5. **意义**（1-2 句）：为何重要，意义所在

### 摘要示例（Nature 风格）

```
多细胞生命的起源仍是生物学最大的谜团之一。由于这种转变发生于
6 亿多年前，个体细胞最初如何合作形成复杂有机体一直难以研究。
在这里，我们展示了单细胞藻类莱茵衣藻（Chlamydomonas reinhardtii）
在暴露于捕食压力下，仅需 750 代即可进化出简单的多细胞结构。
通过使用捕食者草履虫（Paramecium）进行实验进化，我们在 10 个
重复种群中的 5 个观察到了稳定的多细胞簇的形成。基因组分析显示，
仅两个基因——编码细胞粘附蛋白的基因——发生突变就足以触发
这一转变。这些结果表明，多细胞生命的进化可能只需要比以往
认为的更少的基因改变，为理解生命的主要转变之一提供了启示。
```

### 不应写的内容

❌ **过于技术化**：
> "Using CRISPR-Cas9-mediated knockout of the CAD1 gene (encoding cadherin-1) in C. reinhardtii strain CC-125, we demonstrated that loss of CAD1 function combined with overexpression of FLA10 under control of the HSP70A/RBCS2 tandem promoter..."

❌ **过于笼统**：
> "We studied how cells can form groups. Our results are interesting and may have implications for understanding evolution."

---

## 引言

### 长度与结构

- **3-5 段**（约 500-800 词）
- **漏斗结构**：从广泛 → 具体 → 您的贡献

### 逐段指南

**第一段：宏观图景**
- 以关于该领域的广泛而引人入胜的陈述开场
- 阐明为何该领域对科学/社会重要
- 任何科学家都能理解

```
示例：
"The ability to predict protein structure from sequence alone has been a grand 
challenge of biology for over 50 years. Accurate predictions would transform 
drug discovery, enable understanding of disease mechanisms, and illuminate the 
fundamental rules governing molecular self-assembly."
```

**第二至第三段：我们已知什么**
- 选择性回顾关键先前工作（而非详尽无遗）
- 逐步引向您将解决的缺口
- 引用聚焦于必要的论文

```
示例：
"Significant progress has been made through template-based methods that 
leverage known structures of homologous proteins. However, for the estimated 
30% of proteins without detectable homologs, prediction accuracy has remained 
limited. Deep learning approaches have shown promise, achieving improved 
accuracy on benchmark datasets, yet still fall short of experimental accuracy 
for many protein families."
```

**第四段：缺口**
- 清楚陈述什么是仍未知的或未解决的
- 将此框定为一个重要问题

```
示例：
"Despite these advances, the fundamental question remains: can we predict 
protein structure with experimental-level accuracy for proteins across all 
of sequence space? This capability would democratize structural biology and 
enable rapid characterization of newly discovered proteins."
```

**最后一段：本文**
- 陈述您做了什么并预告关键发现
- 表明您贡献的意义

```
示例：
"Here we present AlphaFold2, a neural network architecture that predicts 
protein structure with atomic-level accuracy. In the CASP14 blind assessment, 
AlphaFold2 achieved a median GDT score of 92.4, matching experimental 
accuracy for most targets. We show that this system can be applied to predict 
structures across entire proteomes, opening new avenues for understanding 
protein function at scale."
```

### 引言禁忌

- ❌ 不要以"自古以来……"或过于夸大的声明开场
- ❌ 不要提供详尽的文献综述（保留给专业期刊）
- ❌ 不要在引言中包含方法或结果
- ❌ 不要使用未解释的首字母缩写或行话

---

## 结果

### 组织理念

**以故事驱动，而非以实验驱动**

按**发现**组织，而非按实验的时间顺序：

❌ **实验驱动**（避免）：
> "We first performed experiment A. Next, we did experiment B. Then we conducted experiment C."

✅ **发现驱动**（推荐）：
> "We discovered that X. To understand the mechanism, we found that Y. This led us to test whether Z, confirming our hypothesis."

### 结果写作风格

- **过去时**用于描述做了什么/发现了什么
- **现在时**用于提及图表（"Figure 2 shows..."）
- **客观但有解读性**：以最少解读陈述发现，但对非专业人士提供足够背景
- **定量化**：包含关键数据、统计数据、效应量

### 结果段落示例

```
To test whether protein X is required for cell division, we generated 
knockout cell lines using CRISPR-Cas9 (Fig. 1a). Cells lacking protein X 
showed a 73% reduction in division rate compared to controls (P < 0.001, 
n = 6 biological replicates; Fig. 1b). Live-cell imaging revealed that 
knockout cells arrested in metaphase, with 84% showing abnormal spindle 
morphology (Fig. 1c,d). These results demonstrate that protein X is 
essential for proper spindle assembly and cell division.
```

### 小标题

使用传达发现的描述性小标题：

❌ **笼统**："Protein expression analysis"
✅ **信息丰富**："Protein X is upregulated in response to stress"

---

## 讨论

### 结构（4-6 段）

**第一段：主要发现的总结**
- 重述主要发现（不要逐字重复结果）
- 陈述假设是否得到支持

**第二至第三段：解读与背景**
- 这些发现意味着什么？
- 它们与先前工作如何关联？
- 什么机制可以解释这些结果？

**第四段：更广泛的意义**
- 为何这在您的特定系统之外也很重要？
- 与其他领域的联系
- 潜在应用

**第五段：局限性**
- 诚实承认局限性
- 具体，而非笼统

**最后一段：结论与未来**
- 大局要点信息
- 简要提及未来方向

### 讨论写作技巧

- **以意义开头**，而非以注意事项开头
- **建设性地与文献比较**："Our findings extend the work of Smith et al. by demonstrating..."
- **承认其他解读**："An alternative explanation is that..."
- **诚实面对局限性**：具体 > 笼统

### 局限性陈述示例

❌ **笼统**："Our study has limitations that should be addressed in future work."

✅ **具体**："Our analysis was limited to cultured cells, which may not fully recapitulate the tissue microenvironment. Additionally, the 48-hour observation window may miss slower-developing phenotypes."

---

## 方法

### Nature Methods 的位置

- 简短 Methods 放在正文末尾
- 详细 Methods 放在补充信息中
- 必须足够详细以便重复

### 写作风格

- **过去时，被动语态可接受**："Cells were cultured..." 或 "We cultured cells..."
- **精确且可重复**：包含浓度、时间、温度
- **引用既定方案**："Following the method of Smith et al.³..."

---

## 图表

### 图表理念

Nature 重视**概念图**与数据并重：

1. **图 1**：通常显示概念的示意图/模型
2. **数据图**：清晰，不杂乱
3. **最后一图**：通常是总结模型

### 图表设计原则

- **单栏（89 mm）或双栏（183 mm）**宽度
- **高分辨率**：照片 300+ dpi，线条图 1000+ dpi
- **色盲友好**：避免仅靠红绿区分
- **最少图表垃圾**：无 3D 效果、无不必要的网格线
- **完整的图例**：无需阅读正文即可理解

### 图例格式

```
Figure 1 | Protein X controls cell division through spindle assembly.
a, Schematic of the experimental approach. b, Quantification of cell 
division rate in control (grey) and knockout (blue) cells. Data are 
mean ± s.e.m., n = 6 biological replicates. ***P < 0.001, two-tailed 
t-test. c,d, Representative images of spindle morphology in control (c) 
and knockout (d) cells. Scale bars, 10 μm.
```

---

## 参考文献

### 引用风格

- **编号上标**：¹, ², ¹⁻³, ¹'⁵'⁷
- **Nature 格式**用于参考文献

### 参考文献格式

```
1. Watson, J. D. & Crick, F. H. C. Molecular structure of nucleic acids. 
   Nature 171, 737–738 (1953).

2. Smith, A. B., Jones, C. D. & Williams, E. F. Discovery of protein X. 
   Science 380, 123–130 (2023).
```

### 引用最佳实践

- **近期文献**：包含过去 2-3 年的论文
- **开创性论文**：引用奠基性工作
- **多样来源**：不要过度引用自己的工作
- **原始来源**：引用原始发现，而非综述（如可能）

---

## 语言与写作技巧

### 选词

| 避免 | 优先 |
|-------|--------|
| utilize | use |
| methodology | method |
| in order to | to |
| a large number of | many |
| at this point in time | now |
| has the ability to | can |
| it is interesting to note that | [完全删除] |

### 句式结构

- **句长变化**：混合短句和长句
- **重要信息前置**：将关键信息放在开头
- **每句一个想法**：复杂想法需要多句

### 段落结构

- **主题句优先**：陈述主要观点
- **支持证据**：数据和引用
- **过渡**：连接下一段

---

## 比较：Nature 与 Science

| 特征 | Nature | Science |
|---------|--------|---------|
| 摘要长度 | 150-200 词 | ≤125 词 |
| 引用风格 | 编号上标 | 编号括号 (1, 2) |
| 参考文献中的文章标题 | 是 | 否（在主参考文献中） |
| 方法位置 | 论文末尾或补充材料 | 补充材料 |
| 重要性声明 | 否 | 否 |
| 开放获取选项 | 是 | 是 |

---

## 常见拒稿原因

1. **不够广泛引起兴趣**：对 Nature/Science 过于专业化
2. **渐进式进步**：不够具变革性
3. **过度推销**：声明未被数据支持
4. **可读性差**：对普通受众过于技术化
5. **意义声明薄弱**："所以呢？"不明确
6. **创新性不足**：类似发现已在其他地方发表
7. **方法学担忧**：结果不足以令人信服

---

## 投稿前检查清单

### 内容
- [ ] 第一段清楚显示对广泛受众的意义
- [ ] 非专业人士能理解摘要
- [ ] 结果以故事驱动（非逐个实验）
- [ ] 讨论中强调意义
- [ ] 具体承认局限性

### 风格
- [ ] 主动语态为主
- [ ] 行话最少化或加以解释
- [ ] 句长有变化
- [ ] 段落有清晰的主题句

### 技术
- [ ] 图表为高分辨率
- [ ] 引用格式正确
- [ ] 字数在限制内
- [ ] 包含行号
- [ ] 双倍行距

---

## 另见

- `venue_writing_styles.md` - 风格总览
- `journals_formatting.md` - 技术格式要求
- `reviewer_expectations.md` - Nature/Science 审稿人寻求的内容
