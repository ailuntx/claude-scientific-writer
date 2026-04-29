# 假设生成报告 - 格式快速参考

## 概述

本指南提供假设生成 LaTeX 模板和样式包的快速参考。完整文档请参阅 `SKILL.md`。

## 快速入门

```latex
% !TEX program = xelatex
\documentclass[11pt,letterpaper]{article}
\usepackage{hypothesis_generation}
\usepackage{natbib}

\title{你的现象名称}
\begin{document}
\maketitle
% 你的内容
\end{document}
```

**编译方式：** 使用 XeLaTeX 或 LuaLaTeX 以获得最佳效果
```bash
xelatex your_document.tex
bibtex your_document
xelatex your_document.tex
xelatex your_document.tex
```

## 配色方案参考

### 假设配色
- **假设 1**：深蓝色 (RGB: 0, 102, 153) - 用于第一个假设
- **假设 2**：森林绿 (RGB: 0, 128, 96) - 用于第二个假设
- **假设 3**：皇家紫 (RGB: 102, 51, 153) - 用于第三个假设
- **假设 4**：青色 (RGB: 0, 128, 128) - 用于第四个假设（如需要）
- **假设 5**：焦橙色 (RGB: 204, 85, 0) - 用于第五个假设（如需要）

### 辅助配色
- **预测**：琥珀色 (RGB: 255, 191, 0) - 用于可检验的预测
- **证据**：浅蓝色 (RGB: 102, 178, 204) - 用于支持性证据
- **比较**：钢灰色 (RGB: 108, 117, 125) - 用于关键比较
- **局限性**：珊瑚红 (RGB: 220, 53, 69) - 用于局限性/挑战

## 自定义盒子环境

### 1. 执行摘要盒子

```latex
\begin{summarybox}[Executive Summary]
  内容在此
\end{summarybox}
```

**用途：** 文档开头的高层次概述

---

### 2. 假设盒子（5 种变体）

```latex
\begin{hypothesisbox1}[Hypothesis 1: 标题]
  \textbf{机制解释:}
  [2-3 段解释如何以及为何]
  
  \textbf{关键支持证据:}
  \begin{itemize}
    \item 证据点 1 \citep{ref1}
    \item 证据点 2 \citep{ref2}
  \end{itemize}
  
  \textbf{核心假设:}
  \begin{enumerate}
    \item 假设 1
    \item 假设 2
  \end{enumerate}
\end{hypothesisbox1}
```

**可用盒子：** `hypothesisbox1`、`hypothesisbox2`、`hypothesisbox3`、`hypothesisbox4`、`hypothesisbox5`

**用途：** 展示每个竞争假设及其机制、证据和假设

**4 页正文的最佳实践：**
- 机制解释仅需 1-2 个简短段落（最多 6-10 句话）
- 包含 2-3 个最重要的证据点及引用
- 列出 1-2 个最关键的假设
- 确保每个假设都是真正独特的
- 所有详细解释移至附录 A
- **在每个假设盒子前使用 `\newpage` 以防止溢出**
- 每个完整的假设盒子应 ≤0.6 页

---

### 3. 预测盒子

```latex
\begin{predictionbox}[Predictions: Hypothesis 1]
  \textbf{Prediction 1.1:} [具体预测]
  \begin{itemize}
    \item \textbf{条件:} 适用的情况/地点
    \item \textbf{预期结果:} 具体可测量的结果
    \item \textbf{证伪:} 什么会证伪它
  \end{itemize}
\end{predictionbox}
```

**用途：** 每个假设衍生的可检验预测

**4 页正文的最佳实践：**
- 使预测具体且尽可能量化
- 明确说明预测应成立的条件
- 始终指定证伪标准
- 主文中仅包含每个假设 1-2 个最关键的预测
- 其他预测放入附录

---

### 4. 证据盒子

```latex
\begin{evidencebox}[Supporting Evidence]
  讨论支持证据的内容
\end{evidencebox}
```

**用途：** 突出关键支持证据或文献综合

**最佳实践：**
- 主文中谨慎使用（详细证据放入附录 A）
- 所有证据都需引用
- 聚焦于最有说服力的证据

---

### 5. 比较盒子

```latex
\begin{comparisonbox}[H1 vs. H2: Key Distinction]
  \textbf{根本区别:}
  [核心差异描述]
  
  \textbf{区分性实验:}
  [实验描述]
  
  \textbf{结果解释:}
  \begin{itemize}
    \item \textbf{如果 [结果 A]:} 支持 H1
    \item \textbf{如果 [结果 B]:} 支持 H2
  \end{itemize}
\end{comparisonbox}
```

**用途：** 解释如何区分竞争假设

**最佳实践：**
- 聚焦于根本的机制差异
- 提出清晰可行的区分实验
- 指定具体的结果解释
- 为所有主要假设对创建比较

---

### 6. 局限性盒子

```latex
\begin{limitationbox}[Limitations & Challenges]
  局限性讨论
\end{limitationbox}
```

**用途：** 突出重要的局限性或挑战

**最佳实践：**
- 当局限性特别重要时使用
- 对挑战保持诚实
- 建议如何解决局限性

---

## 文档结构

### 主文（最多 4 页 - 高度简洁）

1. **执行摘要**（0.5-1 页）
   - 使用 `summarybox`
   - 简要的现象概述
   - 每个假设用一句话列出
   - 推荐的方法

2. **竞争假设**（2-2.5 页）
   - 使用 `hypothesisbox1`、`hypothesisbox2` 等
   - 每个假设一个盒子
   - 简要的机制解释（1-2 段）+ 必要证据（2-3 点）+ 关键假设（1-2 个）
   - 目标：3-5 个假设
   - 保持高度简洁 - 细节移至附录

3. **可检验预测**（0.5-1 页）
   - 每个假设使用 `predictionbox`
   - 每个假设仅 1-2 个最关键的预测
   - 非常简要 - 完整预测在附录中

4. **关键比较**（0.5-1 页）
   - 仅在主文中使用 `comparisonbox` 处理最高优先级的比较
   - 展示如何区分顶级假设
   - 其他比较在附录中

**主文总计：最多 4 页 - 对放入的内容要极其精选**

### 附录（全面、详细）

**附录 A：综合文献综述**
- 详细背景（大量引用）
- 当前理解
- 每个假设的证据（详细）
- 冲突的发现
- 知识空白
- **目标：40-60+ 引用**

**附录 B：详细实验设计**
- 每个假设的完整方案
- 方法、对照、样本量
- 统计方法
- 可行性评估
- 时间和资源需求

**附录 C：质量评估**
- 详细评估表
- 优势与劣势分析
- 比较评分
- 建议

**附录 D：补充证据**
- 类似机制
- 初步数据
- 理论框架
- 历史背景

**参考文献**
- **目标：总计 50+ 引用**

## 引用最佳实践

### 主文中
- 引用 15-20 篇关键论文
- 使用 `\citep{author2023}` 进行括号引用
- 使用 `\citet{author2023}` 进行文内引用
- 聚焦于最重要/最近的证据

### 附录中
- 总共引用 40-60+ 篇论文
- 全面覆盖相关文献
- 包含综述、原始研究、理论论文
- 每个论断和证据都需引用

### 引用密度指南
- 主文假设盒子：每个盒子 2-3 引用（仅最必要的）
- 主文总计：最多 10-15 引用（保持简洁）
- 附录 A 文献部分：每个小节 8-15 引用
- 实验设计：方法/先例 2-5 引用
- 质量评估：评估标准需要时引用
- 全文总计：50+ 引用（绝大部分在附录中）

## 表格

### 专业表格格式

```latex
\begin{hypotable}{标题}
\begin{tabular}{|l|l|l|}
\hline
\tableheadercolor
\textcolor{white}{\textbf{Header 1}} & \textcolor{white}{\textbf{Header 2}} \\
\hline
数据行 1 & 数据 \\
\hline
\tablerowcolor  % 交替灰色背景
数据行 2 & 数据 \\
\hline
\end{tabular}
\caption{你的标题}
\end{hypotable}
```

**最佳实践：**
- 对表头行使用 `\tableheadercolor`
- 对超过 3 行的表格交替使用 `\tablerowcolor`
- 保持表格可读（不太宽）
- 用于质量评估、比较

## 常见格式模式

### 假设部分模式

```latex
% 在假设盒子前使用 \newpage 以防止溢出
\newpage
\subsection*{Hypothesis N: [简洁标题]}

\begin{hypothesisboxN}[Hypothesis N: [标题]]

\textbf{机制解释:}

[1-2 个简短段落解释 - 最多 6-10 句话]

\vspace{0.3cm}

\textbf{关键支持证据:}
\begin{itemize}
  \item [证据 1] \citep{ref1}
  \item [证据 2] \citep{ref2}
  \item [证据 3] \citep{ref3}
\end{itemize}

\vspace{0.3cm}

\textbf{核心假设:}
\begin{enumerate}
  \item [假设 1]
  \item [假设 2]
\end{enumerate}

\end{hypothesisboxN}

\vspace{0.5cm}
```

**注意：** 在假设盒子前的 `\newpage` 确保它从新页面开始，防止溢出。这在盒子包含大量内容时尤为重要。

### 预测部分模式

```latex
\subsection*{Predictions from Hypothesis N}

\begin{predictionbox}[Predictions: Hypothesis N]

\textbf{Prediction N.1:} [陈述]
\begin{itemize}
  \item \textbf{条件:} [条件]
  \item \textbf{预期结果:} [结果]
  \item \textbf{证伪:} [证伪]
\end{itemize}

\vspace{0.2cm}

\textbf{Prediction N.2:} [陈述]
[... 继续 ...]

\end{predictionbox}
```

### 比较部分模式

```latex
\subsection*{Distinguishing Hypothesis X vs. Hypothesis Y}

\begin{comparisonbox}[HX vs. HY: Key Distinction]

\textbf{根本区别:}

[核心差异描述]

\vspace{0.3cm}

\textbf{区分性实验:}

[实验描述]

\vspace{0.3cm}

\textbf{结果解释:}
\begin{itemize}
  \item \textbf{如果 [结果 A]:} 支持 HX
  \item \textbf{如果 [结果 B]:} 支持 HY
  \item \textbf{如果 [结果 C]:} 两者都支持/都不支持
\end{itemize}

\end{comparisonbox}
```

## 间距和布局

### 垂直间距
- `\vspace{0.3cm}` - 盒子内元素之间
- `\vspace{0.5cm}` - 主要部分或盒子之间
- `\vspace{1cm}` - 标题之后、主要内容之前

### 页面分页和溢出预防

**关键：防止内容溢出**

LaTeX 盒子（tcolorbox 环境）不会自动跨页。超过剩余页面空间的内容将溢出并导致格式问题。遵循以下指南：

1. **长盒子前的战略性分页：**
```latex
\newpage  % 如果盒子会很长，从新页面开始
\begin{hypothesisbox1}[Hypothesis 1: 标题]
  % 大量内容在此
\end{hypothesisbox1}
```

2. **监控盒子内容长度：**
   - 每个假设盒子最多 ≤0.7 页
   - 如果机制解释 + 证据 + 假设超过约 0.6 页，内容太长
   - 解决方案：将详细内容移至附录，仅在主文盒子中保留要点

3. **何时使用 `\newpage`：**
   - 在任何包含超过 3 个小节或超过 15 行内容的假设盒子前
   - 在包含大量实验描述的比较盒子前
   - 主要附录部分之间
   - 在当前页面剩余空间少于 0.6 页时开始新盒子

4. **主文内容长度指南：**
   - 执行摘要盒子：最多 0.5-0.8 页
   - 每个假设盒子：最多 0.4-0.6 页
   - 每个预测盒子：最多 0.3-0.5 页
   - 每个比较盒子：最多 0.4-0.6 页

5. **拆分长内容：**
   ```latex
   % 好：简洁的主文带分页
   \newpage
   \begin{hypothesisbox1}[Hypothesis 1: 简要标题]
   \textbf{机制解释:}
   1-2 段简要概述（6-10 句话）。
   
   \textbf{关键支持证据:}
   \begin{itemize}
     \item 证据 1 \citep{ref1}
     \item 证据 2 \citep{ref2}
   \end{itemize}
   
   \textbf{核心假设:}
   \begin{enumerate}
     \item 假设 1
   \end{enumerate}
   
   详细机制和全面证据见附录 A。
   \end{hypothesisbox1}
   ```

   ```latex
   % 差：内容过长会溢出
   \begin{hypothesisbox1}[Hypothesis 1]
   \subsection{很长的部分}
   多段内容...
   \subsection{另一个长部分}
   更多段落...
   \subsection{更多内容}
   [内容超出页边距 → 溢出!]
   \end{hypothesisbox1}
   ```

6. **分页命令：**
   - `\newpage` - 强制新页面（建议在长盒子前使用）
   - `\clearpage` - 强制新页面并刷新浮动对象（在附录前使用）

### 章节间距
已由样式包处理，但可调整：
```latex
\vspace{0.5cm}  % 如需要添加额外间距
```

## 故障排除

### 常见问题

**问题：找不到 "hypothesis_generation.sty" 文件**
- 解决方案：确保 .sty 文件与你的 .tex 文件在同一目录，或在你的 LaTeX 路径中

**问题：盒子没有颜色**
- 解决方案：使用 XeLaTeX 或 LuaLaTeX 编译，而非 pdfLaTeX
- 命令：`xelatex yourfile.tex`

**问题：引用显示为 [?]**
- 解决方案：首次 xelatex 编译后运行 bibtex
```bash
xelatex yourfile.tex
bibtex yourfile
xelatex yourfile.tex
xelatex yourfile.tex
```

**问题：找不到字体**
- 解决方案：如果未安装自定义字体，在 .sty 文件中注释掉字体行
- 需要注释的行： `\setmainfont{...}` 和 `\setsansfont{...}`

**问题：盒子标题与内容重叠**
- 解决方案：在标题后添加更多垂直间距，使用 `\vspace{0.3cm}`

**问题：表格太宽**
- 解决方案：在 tabular 前使用 `\small` 或 `\fontsize`，或使用 `p{宽度}` 列规格

**问题：内容溢出页面**
- **原因：** 盒子（tcolorbox 环境）太长，无法容纳在剩余页面空间
- **解决方案 1：** 在盒子前添加 `\newpage` 使其从新页面开始
- **解决方案 2：** 减少盒子内容 - 将详细信息移至附录
- **解决方案 3：** 将内容拆分为多个较小的盒子
- **预防：** 每个假设盒子保持最多 0.4-0.6 页；在有大量内容的盒子前大量使用 `\newpage`

**问题：主文超过 4 页**
- **原因：** 盒子包含太多详细信息
- **解决方案：** 积极将内容移至附录 - 主文盒子应仅包含：
  - 简要的机制概述（1-2 段）
  - 2-3 个关键证据要点
  - 1-2 个核心假设
- 所有详细解释、额外证据和综合讨论应放在附录 A 中

### 包要求

确保已安装这些包：
- `tcolorbox`（带 `most` 选项）
- `xcolor`
- `fontspec`（用于 XeLaTeX/LuaLaTeX）
- `fancyhdr`
- `titlesec`
- `enumitem`
- `booktabs`
- `natbib`

安装缺失的包：
```bash
# 对于 TeX Live
tlmgr install tcolorbox xcolor fontspec fancyhdr titlesec enumitem booktabs natbib

# 对于 MiKTeX (Windows)
# 使用 MiKTeX 包管理器 GUI
```

## 样式一致性提示

1. **颜色使用**
   - 整个文档中每个假设始终使用相同颜色
   - H1 = 蓝色，H2 = 绿色，H3 = 紫色，等等
   - 不要为同一假设混用颜色

2. **盒子使用**
   - 主文：假设盒子、预测盒子、比较盒子
   - 附录：可根据需要使用证据盒子、局限性盒子
   - 不要过度使用盒子 - 保留用于关键内容

3. **引用样式**
   - 整个文档引用格式一致
   - 大多数引用使用 `\citep{}`
   - 分组多个引用： `\citep{ref1, ref2, ref3}`

4. **假设编号**
   - 一致编号假设（H1、H2、H3 等）
   - 预测中使用相同编号（P1.1、P1.2 对应 H1）
   - 比较中使用相同编号（H1 vs. H2）

5. **语言**
   - 精确且具体
   - 避免模糊语言（"可能"、"可以"、"或许"）
   - 尽可能使用主动语态
   - 可行时使预测量化

## 快速检查清单

最终确定文档前：

- [ ] 标题页有现象名称
- [ ] **主文最多 4 页**
- [ ] 执行摘要简洁（0.5-1 页）
- [ ] 每个假设在其各自的彩色盒子中
- [ ] 呈现 3-5 个假设（不超过）
- [ ] 每个假设有简要的机制解释（1-2 段）
- [ ] 每个假设有 2-3 个最重要的证据点及引用
- [ ] 每个假设有 1-2 个最关键的假设
- [ ] 预测盒子每个假设 1-2 个关键预测
- [ ] 主文中有优先比较盒子（其他在附录中）
- [ ] 确定了优先实验
- [ ] **长盒子前使用了分页 (`\newpage`) 以防止溢出**
- [ ] **没有内容溢出页边界（仔细检查 PDF）**
- [ ] **每个假设盒子 ≤0.6 页（如更长，将细节移至附录）**
- [ ] 附录 A 有综合文献综述及详细证据
- [ ] 附录 B 有详细实验方案
- [ ] 附录 C 有质量评估表
- [ ] 附录 D 有补充证据
- [ ] 主文 10-15 引用（精选）
- [ ] 全文总计 50+ 引用
- [ ] 所有盒子使用正确颜色
- [ ] 文档编译无错误
- [ ] 参考文献格式正确
- [ ] **已检查编译的 PDF 是否有溢出问题**

## 最小文档示例

```latex
% !TEX program = xelatex
\documentclass[11pt,letterpaper]{article}
\usepackage{hypothesis_generation}
\usepackage{natbib}

\title{X 在 Y 中的作用}

\begin{document}
\maketitle

\section*{Executive Summary}
\begin{summarybox}[Executive Summary]
现象和假设的简要概述。
\end{summarybox}

\section{Competing Hypotheses}

% 在每个假设盒子前使用 \newpage 以防止溢出
\newpage
\subsection*{Hypothesis 1: 标题}
\begin{hypothesisbox1}[Hypothesis 1: 标题]
\textbf{机制解释:}
1-2 段简要解释。

\textbf{关键支持证据:}
\begin{itemize}
  \item 证据点 \citep{ref1}
\end{itemize}
\end{hypothesisbox1}

\newpage
\subsection*{Hypothesis 2: 标题}
\begin{hypothesisbox2}[Hypothesis 2: 标题]
\textbf{机制解释:}
1-2 段简要解释。

\textbf{关键支持证据:}
\begin{itemize}
  \item 证据点 \citep{ref2}
\end{itemize}
\end{hypothesisbox2}

\section{Testable Predictions}

\subsection*{Predictions from Hypothesis 1}
\begin{predictionbox}[Predictions: Hypothesis 1]
预测内容。
\end{predictionbox}

\section{Critical Comparisons}

\subsection*{H1 vs. H2}
\begin{comparisonbox}[H1 vs. H2]
比较内容。
\end{comparisonbox}

% 附录前强制新页面
\appendix
\newpage
\appendixsection{Appendix A: Literature Review}
详细文献综述。

\newpage
\bibliographystyle{plainnat}
\bibliography{references}

\end{document}
```

**要点：**
- 在每个假设盒子前使用 `\newpage` 确保它们从新页面开始
- 这防止了内容溢出问题
- 主文盒子保持简洁（1-2 段 + 要点）
- 详细内容移至附录

## 其他资源

- 参阅 `hypothesis_report_template.tex` 获取完整注解模板
- 参阅 `SKILL.md` 获取工作流和方法指导
- 参阅 `references/hypothesis_quality_criteria.md` 获取评估框架
- 参阅 `references/experimental_design_patterns.md` 获取设计指导
- 参阅 treatment-plans skill 获取额外 LaTeX 样式示例
