# 科学报告格式指南

使用 `scientific_report.sty` 样式包的快速参考。

## 概述

`scientific_report.sty` 包为科学报告、技术文档和白皮书提供专业格式设置，具有以下特点：

- **Helvetica 字体系列**，简洁现代的外观
- **专业配色方案**，包含蓝色、绿色和强调色
- **彩色盒子环境**，用于组织不同类型的内容
- **美观的表格**，带有交替行颜色和专业的表头
- **科学符号命令**，用于 p 值、效应量和统计数据
- **专业的页眉页脚**，带有自动章节标题

---

## 配色方案

### 主色（蓝色）

| 颜色名称 | RGB | 十六进制 | 用途 |
|------------|-----|-----|-------|
| `primaryblue` | (0, 51, 102) | `#003366` | 页眉、标题、主要元素 |
| `secondaryblue` | (74, 144, 226) | `#4A90E2` | 子节、次要标题 |
| `lightblue` | (220, 235, 252) | `#DCEBFC` | 关键发现框背景 |
| `accentblue` | (0, 120, 215) | `#0078D7` | 强调高亮、假设框 |

### 科学颜色（绿色）

| 颜色名称 | RGB | 十六进制 | 用途 |
|------------|-----|-----|-------|
| `sciencegreen` | (0, 168, 150) | `#00A896` | 方法论框、积极发现 |
| `lightgreen` | (220, 245, 240) | `#DCF5F0` | 方法论框背景 |
| `darkgreen` | (0, 128, 96) | `#008060` | 结果框、强有力的证据 |

### 警告颜色（橙色/红色）

| 颜色名称 | RGB | 十六进制 | 用途 |
|------------|-----|-----|-------|
| `cautionorange` | (255, 140, 66) | `#FF8C42` | 局限性、警告、注意事项 |
| `lightorange` | (255, 243, 224) | `#FFF3E0` | 局限性框背景 |
| `criticalred` | (198, 40, 40) | `#C62828` | 重要通知、警报 |
| `lightred` | (255, 235, 238) | `#FFEBEE` | 重要通知背景 |

### 推荐颜色

| 颜色名称 | RGB | 十六进制 | 用途 |
|------------|-----|-----|-------|
| `recommendpurple` | (103, 58, 183) | `#673AB7` | 推荐框 |
| `lightpurple` | (237, 231, 246) | `#EDE7F6` | 推荐框背景 |

### 中性颜色

| 颜色名称 | RGB | 十六进制 | 用途 |
|------------|-----|-----|-------|
| `darkgray` | (66, 66, 66) | `#424242` | 正文文本 |
| `mediumgray` | (117, 117, 117) | `#757575` | 次要文本、定义 |
| `lightgray` | (245, 245, 245) | `#F5F5F5` | 背景、定义框 |
| `tablealt` | (248, 250, 252) | `#F8FAFC` | 交替表格行 |

---

## 盒子环境

### 关键发现框（蓝色）

用于主要发现、重要结果和重要结论。

```latex
\begin{keyfindings}[自定义标题]
本研究发现治疗 A 显著优于治疗 B
（\pvalue{0.001}，\effectsize{d}{0.75}）。
\end{keyfindings}
```

### 方法论框（绿色）

用于方法、程序和研究设计亮点。

```latex
\begin{methodology}[研究设计]
本随机对照试验采用 2×2 因子设计
进行前后测量和 6 个月随访。
\end{methodology}
```

### 结果框（蓝绿色）

用于突出显示特定结果和统计发现。

```latex
\begin{resultsbox}[主要结局]
分析显示存在显著主效应，F(2, 147) = 12.45，
\psig{< 0.001}，$\eta^2$ = 0.145。
\end{resultsbox}
```

### 推荐框（紫色）

用于推荐、含义和行动项目。

```latex
\begin{recommendations}[临床意义]
\begin{enumerate}
    \item 为高风险患者实施筛查方案
    \item 根据生物标志物水平调整治疗剂量
    \item 每 3 个月间隔监测患者
\end{enumerate}
\end{recommendations}
```

### 局限性框（橙色）

用于局限性、注意事项和附加说明。

```latex
\begin{limitations}[研究局限性]
\begin{itemize}
    \item 样本仅限于城市人群
    \item 横断面设计无法推断因果关系
    \item 自我报告测量可能引入偏倚
\end{itemize}
\end{limitations}
```

### 重要通知框（红色）

用于重要警告、重要通知或安全信息。

```latex
\begin{criticalnotice}[安全警告]
有禁忌症 X 的患者不应接受此治疗。
继续之前请咨询专科医生。
\end{criticalnotice}
```

### 定义框（灰色）

用于定义、注释和补充信息。

```latex
\begin{definition}[关键术语]
\textbf{效应量}是指现象规模的定量度量，
与样本量无关。
\end{definition}
```

### 执行摘要框（特殊）

用于具有增强样式和阴影效果的执行摘要。

```latex
\begin{executivesummary}[报告概述]
本报告呈现了对[主题]的综合分析结果。
主要发现表明...
\end{executivesummary}
```

### 假设框（浅蓝色）

用于陈述研究假设。

```latex
\begin{hypothesis}[主要假设]
我们假设干预 X 将显著改善
结果 Y，与对照组条件相比。
\end{hypothesis}
```

---

## 引用块

用于突出显示重要引述或声明。

```latex
\begin{pullquote}
"这些发现代表了我们对底层机制理解的范式转变。"
\end{pullquote}
```

---

## 统计框

用于突出显示关键统计数据（在三行中使用）。

```latex
\begin{center}
\statbox{n = 500}{参与者}
\statbox{p < 0.001}{显著性}
\statbox{d = 0.75}{效应量}
\end{center}
```

---

## 科学符号命令

### P 值

```latex
\pvalue{0.023}          % 输出：p = 0.023
\psig{< 0.001}          % 输出：p = < 0.001（显著时加粗）
```

### 置信区间

```latex
\CI{0.45}{0.72}         % 输出：95% CI [0.45, 0.72]
```

### 效应量

```latex
\effectsize{d}{0.75}    % 输出：d = 0.75
\effectsize{r}{0.42}    % 输出：r = 0.42
\effectsize{F(2, 97)}{12.45}  % 输出：F(2, 97) = 12.45
```

### 样本量

```latex
\samplesize{250}        % 输出：n = 250
```

### 均值与标准差

```latex
\meansd{42.5}{8.3}      % 输出：42.5 ± 8.3
```

### 显著性指示符（用于表格）

```latex
Result\sigone           % * 表示 p < 0.05
Result\sigtwo           % ** 表示 p < 0.01
Result\sigthree         % *** 表示 p < 0.001
Result\signs            % ns 表示不显著

% 表格脚注图例：
\siglegend              % 输出：*p < 0.05; **p < 0.01; ***p < 0.001; ns 不显著
```

### 质量/证据指示符

```latex
\qualityhigh            % 高（绿色）
\qualitymedium          % 中（橙色）
\qualitylow             % 低（红色）

\evidencestrong         % 强（绿色）
\evidencemoderate       % 中（橙色）
\evidenceweak           % 弱（红色）
```

### 趋势指示符

```latex
\trendup                % 绿色上三角形 ▲
\trenddown              % 红色下三角形 ▼
\trendflat              % 灰色右箭头 →
```

### 文本高亮

```latex
\highlight{重要文本}  % 蓝色粗体文本
```

---

## 表格格式

### 带交替行的标准表格

```latex
\begin{table}[htbp]
\centering
\caption{按分组的描述性统计}
\label{tab:descriptives}
\begin{tabular}{@{}lccc@{}}
\toprule
\textbf{变量} & \textbf{A组} & \textbf{B组} & \textbf{p} \\
\midrule
年龄（岁） & \meansd{42.5}{8.3} & \meansd{43.1}{7.9} & .58 \\
\rowcolor{tablealt} 分数 1 & \meansd{15.2}{3.4} & \meansd{18.7}{4.1} & <.001\sigthree \\
分数 2 & \meansd{22.8}{5.1} & \meansd{23.4}{4.8} & .42 \\
\rowcolor{tablealt} 分数 3 & \meansd{8.9}{2.2} & \meansd{7.2}{2.5} & .003\sigtwo \\
\bottomrule
\end{tabular}

\vspace{0.5em}
{\small \siglegend}
\end{table}
```

### 带质量指示符的表格

```latex
\begin{tabular}{@{}llcc@{}}
\toprule
\textbf{研究} & \textbf{设计} & \textbf{质量} & \textbf{证据} \\
\midrule
Smith 等（2023） & 随机对照试验 & \qualityhigh & \evidencestrong \\
\rowcolor{tablealt} Jones 等（2022） & 队列研究 & \qualitymedium & \evidencemoderate \\
Lee 等（2021） & 横断面研究 & \qualitylow & \evidenceweak \\
\bottomrule
\end{tabular}
```

### 带趋势指示符的表格

```latex
\begin{tabular}{@{}lrrl@{}}
\toprule
\textbf{指标} & \textbf{基线} & \textbf{随访} & \textbf{变化} \\
\midrule
分数 A & 42.5 & 58.3 & \trendup +37\% \\
\rowcolor{tablealt} 分数 B & 18.2 & 15.1 & \trenddown -17\% \\
分数 C & 7.8 & 7.9 & \trendflat +1\% \\
\bottomrule
\end{tabular}
```

---

## 图表格式

### 标准图表

```latex
\begin{figure}[htbp]
centering
includegraphics[width=0.9\textwidth]{../figures/results_chart.png}
\caption{各治疗条件下结局分数的比较}
\label{fig:results}
\end{figure}
```

### 带来源标注的图表

```latex
\begin{figure}[htbp]
centering
includegraphics[width=0.85\textwidth]{../figures/data_visualization.png}
caption{按类别划分的参与者响应分布}
\figuresource{研究数据，收集于 2024 年 1 月至 3 月}
\label{fig:distribution}
\end{figure}
```

### 带注释的图表

```latex
\begin{figure}[htbp]
centering
includegraphics[width=0.8\textwidth]{../figures/model_diagram.png}
caption{所提出关系的概念模型}
\figurenote{实线箭头表示直接效应；虚线箭头表示调节效应。}
\label{fig:model}
\end{figure}
```

---

## 标题页

### 标准标题页

```latex
\makereporttitle
    {研究报告标题}              % 标题
    {综合分析}           % 副标题
    {作者姓名，博士}                   % 作者
    {研究机构}               % 机构
    {2025年1月}                        % 日期
```

### 带封面图片的标题页

```latex
\makereporttitlewithimage
    {研究报告标题}              % 标题
    {综合分析}           % 副标题
    {../figures/cover_image.png}         % 图片路径
    {作者姓名，博士}                   % 作者
    {研究机构}               % 机构
    {2025年1月}                        % 日期
```

---

## 列表格式

列表自动使用蓝色项目符号/数字。

### 项目符号列表

```latex
\begin{itemize}
    \item 第一个项目，自动蓝色项目符号
    \item 第二个项目
    \item 第三个项目
\end{itemize}
```

### 编号列表

```latex
\begin{enumerate}
    \item 第一个项目，蓝色编号
    \item 第二个项目
    \item 第三个项目
\end{enumerate}
```

---

## 附录章节

```latex
\appendix

\chapter{补充材料}

\appendixsection{附加表格}
% 内容出现在目录中

\appendixsection{研究工具}
% 附加附录内容
```

---

## 编译

使用 XeLaTeX 或 LuaLaTeX 编译以获得最佳字体渲染效果：

```bash
# 使用 XeLaTeX
xelatex report.tex
bibtex report        % 如果使用 BibTeX
xelatex report.tex
xelatex report.tex

# 使用 latexmk（推荐）
latexmk -xelatex report.tex

# 使用 LuaLaTeX
lualatex report.tex
```

---

## 常见模式

### 结果部分示例

```latex
\section{主要结局}

\begin{resultsbox}[主要发现]
干预组分数显著高于对照组，
\effectsize{t(98)}{3.45}，\psig{< 0.001}，
\effectsize{d}{0.69}，\CI{0.42}{0.96}。
\end{resultsbox}

表~\ref{tab:outcomes} 呈现了所有结局指标的完整结果。

\begin{table}[htbp]
\centering
caption{按治疗条件划分的结局指标}
\label{tab:outcomes}
\begin{tabular}{@{}lcccc@{}}
\toprule
\textbf{指标} & \textbf{对照组} & \textbf{治疗组} & \textbf{d} & \textbf{p} \\
\midrule
主要指标 & \meansd{42.1}{8.2} & \meansd{51.3}{9.1} & 0.69\sigthree & <.001 \\
\rowcolor{tablealt} 次要指标 & \meansd{3.2}{1.1} & \meansd{4.1}{1.3} & 0.52\sigtwo & .004 \\
次要指标 & \meansd{18.5}{4.2} & \meansd{19.2}{4.5} & 0.16\signs & .328 \\
\bottomrule
\end{tabular}
\end{table}
```

### 讨论部分示例

```latex
\section{对发现的解释}

\begin{keyfindings}[摘要]
\begin{enumerate}
    \item 主要假设 \highlight{得到支持}，效应量大
    \item 次要假设部分得到支持
    \item 证据质量：\evidencestrong
\end{enumerate}
\end{keyfindings}

\begin{limitations}
本研究存在一些应予以考虑的局限性...
\end{limitations}

\begin{recommendations}[未来研究]
未来研究应解决以下问题：
\begin{enumerate}
    \item 在不同人群中重复验证发现
    \item 延长随访期以评估长期效应
    \item 研究调节变量
\end{enumerate}
\end{recommendations}
```

---

## 故障排除

### 盒子溢出
如果盒子内容溢出页面：
```latex
\newpage
\begin{keyfindings}[续...]
```

### 图表放置
使用 `[htbp]` 灵活放置，或使用 `[H]`（需要 `float` 包）精确定位：
```latex
\usepackage{float}
\begin{figure}[H]
```

### 表格过宽
使用 `\resizebox` 或减小字体：
```latex
\resizebox{\textwidth}{!}{
\begin{tabular}{...}
...
\end{tabular}
}
```

### 字体问题
如果 Helvetica 字体无法渲染，请确保使用 XeLaTeX 或 LuaLaTeX：
```bash
xelatex report.tex   % 不是 pdflatex
```

---

## 快速参考卡

| 用途 | 命令/环境 |
|---------|---------------------|
| 主要发现 | `\begin{keyfindings}...\end{keyfindings}` |
| 方法 | `\begin{methodology}...\end{methodology}` |
| 结果 | `\begin{resultsbox}...\end{resultsbox}` |
| 推荐 | `\begin{recommendations}...\end{recommendations}` |
| 局限性 | `\begin{limitations}...\end{limitations}` |
| 警告 | `\begin{criticalnotice}...\end{criticalnotice}` |
| 定义 | `\begin{definition}...\end{definition}` |
| 执行摘要 | `\begin{executivesummary}...\end{executivesummary}` |
| 假设 | `\begin{hypothesis}...\end{hypothesis}` |
| P 值 | `\pvalue{0.05}` 或 `\psig{< 0.001}` |
| 效应量 | `\effectsize{d}{0.75}` |
| 样本量 | `\samplesize{250}` |
| 均值 ± 标准差 | `\meansd{42.5}{8.3}` |
| 置信区间 | `\CI{0.38}{0.72}` |
| 高亮 | `\highlight{文本}` |
| 交替行 | `\rowcolor{tablealt}` |
| 显著性 | `\sigone`、`\sigtwo`、`\sigthree`、`\signs` |
