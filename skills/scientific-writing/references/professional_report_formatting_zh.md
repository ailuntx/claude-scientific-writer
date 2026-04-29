# 科学文档专业报告格式设置

本参考指南涵盖科学报告、技术文档和白皮书的专业格式设置。请使用 `scientific_report.sty` LaTeX 样式包以获得一致、专业的输出效果。

---

## 何时使用专业报告格式设置

### 请使用此样式：

- **研究报告** - 内部和外部研究摘要
- **技术报告** - 详细技术文档和分析
- **白皮书** - 观点论文和思想领导力文档
- **资助报告** - 进度报告和最终资助报告
- **政策简报** - 基于研究的政策建议
- **行业报告** - 针对行业受众的技术报告
- **内部研究摘要** - 团队和利益相关者沟通
- **可行性研究** - 技术和研究可行性评估
- **项目文档** - 研究项目交付成果

### **请勿使用此样式**：

- **期刊手稿** → 使用 `venue-templates` 技能进行期刊特定格式设置
- **会议论文** → 使用 `venue-templates` 技能满足会议要求
- **学术论文/学位论文** → 使用机构模板
- **同行评审提交** → 遵循期刊作者指南

**关键区别**：专业报告格式设置注重普通受众的视觉吸引力和可读性，而期刊手稿必须遵循严格的出版商要求。

---

## scientific_report.sty 概述

`scientific_report.sty` 包提供：

| 功能 | 描述 |
|---------|-------------|
| 字体 | Helvetica 字体系列，现代专业外观 |
| 配色方案 | 协调的蓝色、绿色、橙色和紫色 |
| 彩色框环境 | 用于组织内容类型的彩色框 |
| 表格 | 交替行的专业样式 |
| 图表 | 一致的图表说明格式 |
| 页眉/页脚 | 专业的页面页眉和页脚 |
| 科学命令 | p值、效应量、统计量的快捷方式 |

### 基本文档设置

```latex
\documentclass[11pt,letterpaper]{report}
\usepackage{scientific_report}

\begin{document}
% 在此输入您的内容
\end{document}
```

**编译**：使用 XeLaTeX 或 LuaLaTeX 以正确渲染 Helvetica 字体：
```bash
xelatex document.tex
```

---

## 用于内容组织的彩色框环境

### 目的和用法

彩色框帮助读者快速识别不同类型的内容。请策略性地使用它们来突出重要信息。

### 可用的彩色框环境

| 环境 | 颜色 | 用途 |
|-------------|-------|---------|
| `keyfindings` | 蓝色 | 主要发现、发现、关键要点 |
| `methodology` | 绿色 | 方法、程序、研究设计 |
| `resultsbox` | 蓝绿色 | 统计结果、数据亮点 |
| `recommendations` | 紫色 | 建议、行动项目、含义 |
| `limitations` | 橙色 | 局限性、注意事项、附加说明 |
| `criticalnotice` | 红色 | 关键警告、安全提示 |
| `definition` | 灰色 | 定义、注释、补充信息 |
| `executivesummary` | 蓝色（带阴影） | 执行摘要 |
| `hypothesis` | 浅蓝色 | 研究假设 |

### 主要发现框

用于主要发现和重要发现：

```latex
\begin{keyfindings}[研究亮点]
我们的分析揭示了三个重要发现：
\begin{enumerate}
    \item 治疗 A 比对照组有效 40%（\pvalue{0.001}）
    \item 效应量具有临床意义（\effectsize{d}{0.82}）
    \item 益处在 12 个月随访时持续存在
\end{enumerate}
\end{keyfindings}
```

**最佳实践**：
- 谨慎使用（每章最多 1-3 个）
- 仅用于真正重要的发现
- 包含具体数字和统计数据
- 简洁撰写

### 方法论框

用于突出方法和程序：

```latex
\begin{methodology}[研究设计]
这项双盲、随机对照试验采用 2×2 析因设计。参与者（\samplesize{450}）
被随机分配到四个条件之一：（1）治疗 A，（2）治疗 B，（3）联合 A+B，
或（4）安慰剂对照。
\end{methodology}
```

**最佳实践**：
- 总结关键方法特征
- 用于方法部分的开头
- 包含样本量和设计类型
- 保持技术性但易于理解

### 结果框

用于突出特定统计结果：

```latex
\begin{resultsbox}[主要结局分析]
混合效应回归显示出显著的治疗 × 时间交互作用，
\effectsize{F(3, 446)}{8.72}，\psig{< 0.001}，
$\eta^2_p$ = 0.055，表明不同治疗条件在研究期间
的改善程度不同。
\end{resultsbox}
```

**最佳实践**：
- 报告完整的统计信息
- 使用科学记号命令
- 与 p 值一起包含效应量
- 每个主要分析一个框

### 建议框

用于建议和含义：

```latex
\begin{recommendations}[临床实践指南]
根据我们的发现，我们建议：
\begin{enumerate}
    \item \textbf{主要建议：}为高危人群实施筛查方案。
    \item \textbf{次要建议：}根据基线严重程度评分调整治疗强度。
    \item \textbf{监测：}每 3 个月重新评估。
\end{enumerate}
\end{recommendations}
```

**最佳实践**：
- 使建议具体且可操作
- 用明确标签优先排序
- 与支持证据关联
- 包含实施指导

### 局限性框

用于局限性、注意事项和警告：

```latex
\begin{limitations}[研究局限性]
应考虑几个局限性：
\begin{itemize}
    \item \textbf{样本：}参与者来自学术医疗中心，
        限制了向社区环境的推广。
    \item \textbf{设计：}观察性设计无法对治疗效果进行因果推断。
    \item \textbf{流失：}15% 的退出率可能引入偏倚。
\end{itemize}
\end{limitations}
```

**最佳实践**：
- 诚实且全面
- 解释每个局限性的含义
- 建议未来研究如何解决局限性
- 不要过度限定发现

### 关键通知框

用于关键警告或安全信息：

```latex
\begin{criticalnotice}[安全警告]
\textbf{禁忌症：}此干预措施禁用于患有 [疾病] 的患者。
监测 [不良反应] 并在 [症状] 出现时立即停止。
向 [联系人] 报告严重不良事件。
\end{criticalnotice}
```

**最佳实践**：
- 仅用于真正关键的信息
- 清晰直接
- 包含要采取的具体行动
- 如相关，提供联系方式

### 定义框

用于定义和解释性说明：

```latex
\begin{definition}[效应量]
\textbf{效应量} 是现象规模的量化度量。与显著性检验不同，
效应量独立于样本量，允许跨研究比较。常用度量包括
Cohen 的 \textit{d} 表示均值差异，Pearson 的 \textit{r} 表示相关性。
\end{definition}
```

**最佳实践**：
- 首次使用时定义技术术语
- 保持定义简洁
- 包含实际解释指导
- 用于适合受众的术语

---

## 专业表格格式设置

### 设计原则

1. **简洁外观**：使用 `booktabs` 线条（`\toprule`、`\midrule`、`\bottomrule`）
2. **交替行**：每行交替应用 `\rowcolor{tablealt}`
3. **清晰的标题**：加粗列标题以便识别
4. **适当的精度**：报告统计数据到适当的小数位数
5. **完整信息**：包含样本量、单位和注释

### 标准数据表

```latex
\begin{table}[htbp]
\centering
\caption{按治疗组的人口统计学特征}
\label{tab:demographics}
\begin{tabular}{@{}lcc@{}}
\toprule
\textbf{特征} & \textbf{治疗组} & \textbf{对照组} \\
 & (\samplesize{225}) & (\samplesize{225}) \\
\midrule
年龄（岁），\meansd{M}{SD} & \meansd{42.3}{12.5} & \meansd{43.1}{11.8} \\
\rowcolor{tablealt} 女性，n（\%）& 128 (56.9) & 121 (53.8) \\
教育年限，\meansd{M}{SD} & \meansd{14.2}{2.8} & \meansd{14.5}{2.6} \\
\rowcolor{tablealt} 基线评分，\meansd{M}{SD} & \meansd{52.4}{15.3} & \meansd{51.8}{14.9} \\
\bottomrule
\end{tabular}
\figurenote{组间基线无显著差异（所有 \textit{p} > .10）。}
\end{table}
```

### 带显著性标记的结果表

```latex
\begin{table}[htbp]
\centering
\caption{治疗对主要和次要结局的影响}
\label{tab:results}
\begin{tabular}{@{}lcccc@{}}
\toprule
\textbf{结局} & \textbf{治疗组} & \textbf{对照组} & \textbf{效应量} & \textbf{p} \\
 & \meansd{M}{SD} & \meansd{M}{SD} & \textbf{(d)} & \\
\midrule
主要结局 & \meansd{68.4}{14.2} & \meansd{54.1}{15.8} & 0.95\sigthree & <.001 \\
\rowcolor{tablealt} 次要结局 A & \meansd{4.2}{1.1} & \meansd{3.5}{1.2} & 0.61\sigtwo & .003 \\
次要结局 B & \meansd{22.8}{5.4} & \meansd{21.2}{5.1} & 0.31\sigone & .042 \\
\rowcolor{tablealt} 次要结局 C & \meansd{8.9}{2.3} & \meansd{8.5}{2.4} & 0.17\signs & .285 \\
\bottomrule
\end{tabular}

\vspace{0.5em}
{\small \siglegend}
\end{table}
```

### 带质量评级的比较表

```latex
\begin{table}[htbp]
\centering
caption{按研究的证据摘要}
\label{tab:evidence}
\begin{tabular}{@{}llccc@{}}
\toprule
\textbf{研究} & \textbf{设计} & \textbf{N} & \textbf{质量} & \textbf{证据} \\
\midrule
Smith 等 (2024) & RCT & 450 & \qualityhigh & \evidencestrong \\
\rowcolor{tablealt} Jones 等 (2023) & 队列 & 1,250 & \qualitymedium & \evidencemoderate \\
Chen 等 (2023) & 病例对照 & 320 & \qualitymedium & \evidencemoderate \\
\rowcolor{tablealt} Lee 等 (2022) & 横断面 & 890 & \qualitylow & \evidenceweak \\
\bottomrule
\end{tabular}
\end{table}
```

---

## 图表和标题样式

### 标题格式设置

样式包自动格式化标题，包括：
- 蓝色、加粗的图表标签
- 灰色的描述文字
- 居中对齐并留有页边距

### 标准图表

```latex
\begin{figure}[htbp]
centering
includegraphics[width=0.9textwidth]{../figures/results_comparison.png}
caption{按治疗条件和时间点的结局评分比较}
\label{fig:results}
\end{figure}
```

### 带来源归属的图表

```latex
\begin{figure}[htbp]
centering
includegraphics[width=0.85textwidth]{../figures/trend_analysis.png}
caption{研究期间关键指标的趋势}
\figuresource{研究数据收集时间为 2024 年 1 月至 12 月}
\label{fig:trends}
\end{figure}
```

### 带解释性说明的图表

```latex
\begin{figure}[htbp]
centering
includegraphics[width=0.8textwidth]{../figures/conceptual_model.png}
caption{假设关系的概念模型}
\figurenote{实线箭头表示主要路径；虚线箭头表示调节关系。数字表示标准化系数。}
\label{fig:model}
\end{figure}
```

---

## 配色方案和视觉层次

### 颜色使用指南

| 颜色 | 用于 | 避免用于 |
|-------|---------|-----------------|
| 主蓝色 | 标题、重要发现 | 警告、注意事项 |
| 科学绿色 | 方法、积极结果 | 负面发现 |
| 橙色 | 注意事项、局限性 | 积极发现 |
| 红色 | 关键警告 | 常规内容 |
| 紫色 | 建议 | 发现、方法 |
| 灰色 | 定义、注释 | 关键发现 |

### 视觉层次

1. **执行摘要框**（带阴影效果）- 最突出
2. **彩色内容框** - 关键内容高突出度
3. **带颜色的表格** - 数据的中等突出度
4. **正文** - 标准突出度
5. **定义框** - 补充信息的较低突出度

### 无障碍注意事项

- 配色方案设计用于区分常见的色觉缺陷
- 所有框同时具有颜色和结构指示（边框、背景）
- 文字保持足够的对比度
- 不要仅依靠颜色来传达含义

---

## 字体指南

### 字体规格

| 元素 | 字体 | 字号 | 颜色 |
|---------|------|------|-------|
| 正文 | Helvetica | 11pt | 深灰色 (#424242) |
| 章节标题 | Helvetica 加粗 | Huge | 主蓝色 (#003366) |
| 节标题 | Helvetica 加粗 | Large | 主蓝色 (#003366) |
| 小节 | Helvetica 加粗 | large | 次蓝色 (#4A90E2) |
| 子小节 | Helvetica 加粗 | normalsize | 深灰色 (#424242) |

### 间距

- 行距：1.15（为了可读性）
- 段落间距：段落之间 0.5em
- 页边距：各边 1 英寸

### 最佳字体实践

1. **一致性**：对相似元素使用相同的格式
2. **层次**：使用视觉权重表示重要性
3. **可读性**：足够的间距和对比度
4. **专业性**：避免混用字体或过度格式设置

---

## 科学记号命令参考

### 统计报告

| 命令 | 输出 | 使用时机 |
|---------|--------|-------------|
| `\pvalue{0.023}` | *p* = 0.023 | 报告 p 值 |
| `\psig{< 0.001}` | ***p*** = < 0.001 | 显著的 p 值（加粗）|
| `\CI{0.45}{0.72}` | 95% CI [0.45, 0.72] | 置信区间 |
| `\effectsize{d}{0.75}` | d = 0.75 | 效应量 |
| `\samplesize{250}` | *n* = 250 | 样本量 |
| `\meansd{42.5}{8.3}` | 42.5 ± 8.3 | 均值及标准差 |

### 显著性标记

| 命令 | 输出 | 含义 |
|---------|--------|---------|
| `\sigone` | * | p < 0.05 |
| `\sigtwo` | ** | p < 0.01 |
| `\sigthree` | *** | p < 0.001 |
| `\signs` | ns | 不显著 |
| `\siglegend` | 完整图例 | 用于表格脚注 |

### 质量和证据评级

| 命令 | 输出 | 含义 |
|---------|--------|---------|
| `\qualityhigh` | **HIGH**（绿色）| 高质量 |
| `\qualitymedium` | **MEDIUM**（橙色）| 中等质量 |
| `\qualitylow` | **LOW**（红色）| 低质量 |
| `\evidencestrong` | **Strong**（绿色）| 强证据 |
| `\evidencemoderate` | **Moderate**（橙色）| 中等证据 |
| `\evidenceweak` | **Weak**（红色）| 弱证据 |

### 趋势指示

| 命令 | 符号 | 含义 |
|---------|--------|---------|
| `\trendup` | ▲（绿色）| 上升趋势 |
| `\trenddown` | ▼（红色）| 下降趋势 |
| `\trendflat` | →（灰色）| 稳定/无变化 |

---

## 完整 LaTeX 示例

### 执行摘要示例

```latex
chapter*{执行摘要}
\addcontentsline{toc}{chapter}{执行摘要}

\begin{executivesummary}[报告亮点]
本报告呈现了对 [主题] 涉及 \samplesize{450} 名参与者
横跨 12 个研究站点的综合研究结果。该研究使用 [方法] 
解决 [关键问题]。
\end{executivesummary}

subsection*{主要发现}

\begin{keyfindings}
\begin{enumerate}
    \item 主要干预显示出大效应量
          （\effectsize{d}{0.82}，\psig{< 0.001}）。
    \item 益处在 12 个月随访时得以维持。
    \item 成本效益分析支持实施。
\end{enumerate}
\end{keyfindings}

subsection*{建议}

\begin{recommendations}
根据这些发现，我们建议：
\begin{enumerate}
    \item 在 [设置] 中实施干预。
    \item 使用标准化方案培训从业者。
    \item 使用验证过的措施监测结局。
\end{enumerate}
\end{recommendations}
```

### 方法部分示例

```latex
chapter{方法}

\begin{methodology}[研究概述]
这项随机对照试验采用平行组设计，按 1:1 分配到干预组
或对照组。研究于 2023 年 1 月至 2024 年 12 月期间
在 12 个站点进行。
\end{methodology}

section{参与者}

共有 \samplesize{450} 名参与者被纳入。纳入标准为：

\begin{itemize}
    \item 年龄 18--65 岁
    \item 按 [标准] 诊断为 [疾病]
    \item 无 [干预] 禁忌症
\end{itemize}

表~\ref{tab:participants} 呈现参与者特征。

\begin{limitations}[招募挑战}
由于 [原因]，招募速度低于预期。最终样本量比目标低 10%，
这可能影响次要分析的统计效力。
\end{limitations}
```

### 结果部分示例

```latex
chapter{结果}

section{主要结局}

\begin{resultsbox}[主要分析]
混合效应回归显示出显著的治疗效应，
\effectsize{F(1, 448)}{42.18}，\psig{< 0.001}，
效应量大（\effectsize{d}{0.82}）。治疗组显示出显著更大的
改善（\meansd{16.4}{5.2} 分）相比对照组（\meansd{8.1}{4.8} 分）。
\end{resultsbox}

图~\ref{fig:primary} 说明了随时间变化的治疗效果。

\begin{figure}[htbp]
centering
includegraphics[width=0.9textwidth]{../figures/primary_outcome.png}
caption{按治疗组和时间点的主要结局评分}
\figurenote{误差条表示 95% 置信区间。}
\label{fig:primary}
\end{figure}

section{次要结局}

次要结局的结果见表~\ref{tab:secondary}。
```

### 讨论部分示例

```latex
chapter{讨论}

section{发现摘要}

\begin{keyfindings}[主要结论]
\begin{enumerate}
    \item 干预非常有效（主要假设 \highlight{得到支持}）
    \item 效果具有临床意义且持久
    \item 证据强度：\evidencestrong
\end{enumerate}
\end{keyfindings}

section{局限性}

\begin{limitations}
几个局限性值得考虑：
\begin{itemize}
    \item 样本主要为 [人口统计学特征]，限制了推广性。
    \item 对照组流失率更高（18% vs. 12%）。
    \item 自我报告测量可能受到反应偏倚影响。
\end{itemize}
\end{limitations}

section{含义}

\begin{recommendations}[研究含义]
\begin{enumerate}
    \item 在不同人群中复制
    \item 研究变化的机制
    \item 测试实施策略
\end{enumerate}
\end{recommendations}

\begin{recommendations}[实践含义]
\begin{enumerate}
    \item 在 [设置] 中采用干预
    \item 使用标准化方案培训提供者
    \item 监测保真度和结局
\end{enumerate}
\end{recommendations}
```

---

## 清单：专业报告质量

在最终确定您的报告之前，请验证：

### 格式设置
- [ ] 使用 `scientific_report.sty` 包
- [ ] 使用 XeLaTeX 或 LuaLaTeX 编译
- [ ] Helvetica 字体渲染正确
- [ ] 颜色显示正常

### 内容组织
- [ ] 存在完整的执行摘要
- [ ] 关键发现用框突出显示
- [ ] 方法描述清晰
- [ ] 结果正确格式化并包含统计数据
- [ ] 局限性已承认
- [ ] 建议具体且可操作

### 表格
- [ ] 所有表格都有标题和标签
- [ ] 应用了交替行颜色
- [ ] 显著性标记已解释
- [ ] 数字格式一致

### 图表
- [ ] 所有图表都有标题和标签
- [ ] 适当的地方注明了来源
- [ ] 分辨率足以打印（300 DPI）
- [ ] 在正文中被引用

### 统计报告
- [ ] p 值适当报告
- [ ] 包含效应量
- [ ] 适当的地方包含置信区间
- [ ] 声明了样本量

### 专业外观
- [ ] 整个文档格式一致
- [ ] 无孤立的标题或寡页
- [ ] 分页符位于适当位置
- [ ] 参考文献完整且格式正确

---

## 资源

### 此技能中的文件

- `assets/scientific_report.sty` - LaTeX 样式包
- `assets/scientific_report_template.tex` - 完整报告模板
- `assets/REPORT_FORMATTING_GUIDE.md` - 快速参考指南

### 相关技能

- `venue-templates` - 用于期刊手稿和会议论文
- `scientific-schematics` - 用于生成图表和图形
- `generate-image` - 用于创建插图和图形

### 外部资源

- [LaTeX Wikibook](https://en.wikibooks.org/wiki/LaTeX) - 通用 LaTeX 参考
- [Booktabs 包文档](https://ctan.org/pkg/booktabs) - 专业表格样式
- [tcolorbox 包文档](https://ctan.org/pkg/tcolorbox) - 彩色框环境
