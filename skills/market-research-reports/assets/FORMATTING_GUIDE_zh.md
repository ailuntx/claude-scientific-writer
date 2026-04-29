# 市场研究报告格式指南

使用 `market_research.sty` 样式包的快速参考指南。

## 配色方案

### 主色
| 颜色名称 | RGB | 十六进制 | 用途 |
|------------|-----|-----|-------|
| `primaryblue` | (0, 51, 102) | `#003366` | 标题、标题、链接 |
| `secondaryblue` | (51, 102, 153) | `#336699` | 子章节、次要元素 |
| `lightblue` | (173, 216, 230) | `#ADD8E6` | 关键洞察框背景 |
| `accentblue` | (0, 120, 215) | `#0078D7` | 强调高亮、机会框 |

### 辅色
| 颜色名称 | RGB | 十六进制 | 用途 |
|------------|-----|-----|-------|
| `accentgreen` | (0, 128, 96) | `#008060` | 市场数据框、正面指标 |
| `lightgreen` | (200, 230, 201) | `#C8E6C9` | 市场数据框背景 |
| `warningorange` | (255, 140, 0) | `#FF8C00` | 风险框、警告 |
| `alertred` | (198, 40, 40) | `#C62828` | 关键风险 |
| `recommendpurple` | (103, 58, 183) | `#673AB7` | 推荐框 |

### 中性色
| 颜色名称 | RGB | 十六进制 | 用途 |
|------------|-----|-----|-------|
| `darkgray` | (66, 66, 66) | `#424242` | 正文文本 |
| `mediumgray` | (117, 117, 117) | `#757575` | 次要文本 |
| `lightgray` | (240, 240, 240) | `#F0F0F0` | 背景、标注框 |
| `tablealt` | (245, 247, 250) | `#F5F7FA` | 交替表格行 |

---

## 盒子环境

### 关键洞察框（蓝色）
用于主要发现、洞察和重要发现。

```latex
\begin{keyinsightbox}[自定义标题]
市场预计以15.3%的复合年增长率增长至2030年，这得益于
企业采用率上升和监管条件的改善。
\end{keyinsightbox}
```

### 市场数据框（绿色）
用于市场统计、指标和数据亮点。

```latex
\begin{marketdatabox}[市场快照]
\begin{itemize}
    \item \textbf{市场规模（2024）：} \marketsize{452亿}
    \item \textbf{预计规模（2030）：} \marketsize{987亿}
    \item \textbf{复合年增长率：} \growthrate{15.3}
\end{itemize}
\end{marketdatabox}
```

### 风险框（橙色/警告）
用于风险因素、警告和注意事项。

```latex
\begin{riskbox}[市场风险]
欧盟的监管变化可能在未来18个月内影响40%的市场
参与者。
\end{riskbox}
```

### 关键风险框（红色）
用于高严重性或关键风险。

```latex
\begin{criticalriskbox}[关键：供应链中断]
重大供应链中断可能导致6-12个月的延迟
和30%的成本增加。
\end{criticalriskbox}
```

### 推荐框（紫色）
用于战略建议和行动项。

```latex
\begin{recommendationbox}[战略建议]
\begin{enumerate}
    \item 优先进入亚太地区市场
    \item 与当地分销商建立战略合作伙伴关系
    \item 投资产品本地化
\end{enumerate}
\end{recommendationbox}
```

### 标注框（灰色）
用于定义、说明和补充信息。

```latex
\begin{calloutbox}[定义：TAM]
潜在市场总量（TAM）代表如果实现100%市场份额
可获得的总收入机会。
\end{calloutbox}
```

### 执行摘要框
用于执行摘要亮点的特殊样式。

```latex
\begin{executivesummarybox}[执行摘要]
报告的主要发现和亮点...
\end{executivesummarybox}
```

### 机会框（青色/强调蓝色）
用于机会和正面发现。

```latex
\begin{opportunitybox}[增长机会]
亚太市场代表150亿美元的机会，
以22%的复合年增长率增长。
\end{opportunitybox}
```

### 框架盒子
用于战略分析框架。

```latex
% SWOT分析
\begin{swotbox}[SWOT分析摘要]
内容...
\end{swotbox}

% 波特的五力模型
\begin{porterbox}[波特五力分析]
内容...
\end{porterbox}
```

---

## 引用框

用于突出重要的统计数据或引用。

```latex
\begin{pullquote}
"人工智能与医疗健康的融合代表到2034年
1990亿美元的机会。"
\end{pullquote}
```

---

## 统计框

用于突出关键统计数据（使用三行）。

```latex
\begin{center}
\statbox{452亿}{市场规模 2024}
\statbox{15.3\%}{复合年增长率 2024-2030}
\statbox{23\%}{市场领导者份额}
\end{center}
```

---

## 自定义命令

### 文本高亮
```latex
\highlight{重要文本}  % 蓝色粗体
```

### 市场规模格式
```latex
\marketsize{452亿}   % 输出：绿色显示452亿
```

### 增长率格式
```latex
\growthrate{15.3}           % 输出：绿色显示15.3%
```

### 风险指标
```latex
\riskhigh{}     % 输出：红色显示“高”
\riskmedium{}   % 输出：橙色显示“中”
\risklow{}      % 输出：绿色显示“低”
```

### 评级星号（1-5）
```latex
\rating{4}      % 输出：★★★★☆
```

### 趋势指示符
```latex
\trendup{}      % 绿色上三角
\trenddown{}    % 红色下三角
\trendflat{}    % 灰色右箭头
```

---

## 表格格式

### 带交替行的标准表格
```latex
\begin{table}[htbp]
\centering
\caption{各地区市场规模}
\begin{tabular}{@{}lrrr@{}}
\toprule
\textbf{地区} & \textbf{规模} & \textbf{份额} & \textbf{复合年增长率} \\
\midrule
北美 & 182亿 & 40.3\% & 12.5\% \\
\rowcolor{tablealt} 欧洲 & 121亿 & 26.8\% & 14.2\% \\
亚太 & 105亿 & 23.2\% & 18.7\% \\
\rowcolor{tablealt} 其他地区 & 44亿 & 9.7\% & 11.3\% \\
\midrule
\textbf{总计} & \textbf{452亿} & \textbf{100\%} & \textbf{15.3\%} \\
\bottomrule
\end{tabular}
\label{tab:regional}
\end{table}
```

### 带趋势指示符的表格
```latex
\begin{tabular}{@{}lrrl@{}}
\toprule
\textbf{公司} & \textbf{收入} & \textbf{份额} & \textbf{趋势} \\
\midrule
A公司 & 52亿 & 15.3\% & \trendup{} +12\% \\
B公司 & 48亿 & 14.1\% & \trenddown{} -3\% \\
C公司 & 42亿 & 12.4\% & \trendflat{} +1\% \\
\bottomrule
\end{tabular}
```

---

## 图片格式

### 标准图片
```latex
\begin{figure}[htbp]
\centering
\includegraphics[width=0.9\textwidth]{../figures/market_growth.png}
\caption{市场增长轨迹（2020-2030）}
\label{fig:growth}
\end{figure}
```

### 带来源标注的图片
```latex
\begin{figure}[htbp]
\centering
\includegraphics[width=0.85\textwidth]{../figures/market_share.png}
caption{市场份额分布（2024）}
\figuresource{公司年报、行业分析}
\label{fig:market_share}
\end{figure}
```

---

## 列表格式

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

### 嵌套列表
```latex
\begin{itemize}
    \item 要点
    \begin{itemize}
        \item 子要点A
        \item 子要点B
    \end{itemize}
    \item 另一个要点
\end{itemize}
```

---

## 标题页

### 使用自定义标题命令
```latex
\makemarketreporttitle
    {市场标题}              % 报告标题
    {副标题}             % 副标题
    {../figures/cover.png}      % 封面图片（留空则无图片）
    {2025年1月}              % 日期
    {市场情报团队}  % 作者/编制者
```

### 手动标题页
有关完整的手动标题页代码，请参见模板。

---

## 附录章节

```latex
\appendix

\chapter{研究方法}

\appendixsection{数据来源}
目录中显示的内容...
```

---

## 常用模式

### 市场快照章节
```latex
\begin{marketdatabox}[市场快照]
\begin{itemize}
    \item \textbf{当前市场规模：} \marketsize{452亿}
    \item \textbf{预计规模（2030）：} \marketsize{987亿}
    \item \textbf{复合年增长率：} \growthrate{15.3}
    \item \textbf{最大细分市场：} 企业（42%份额）
    \item \textbf{增长最快地区：} 亚太（22.1%复合年增长率）
\end{itemize}
\end{marketdatabox}
```

### 风险登记摘要
```latex
\begin{table}[htbp]
\centering
\caption{风险评估摘要}
\begin{tabular}{@{}llccl@{}}
\toprule
\textbf{风险} & \textbf{类别} & \textbf{概率} & \textbf{影响} & \textbf{评级} \\
\midrule
市场中断 & 市场 & 高 & 高 & \riskhigh{} \\
\rowcolor{tablealt} 监管变化 & 监管 & 中 & 高 & \riskhigh{} \\
新进入者 & 竞争 & 中 & 中 & \riskmedium{} \\
\rowcolor{tablealt} 技术过时 & 技术 & 低 & 高 & \riskmedium{} \\
汇率波动 & 金融 & 中 & 低 & \risklow{} \\
\bottomrule
\end{tabular}
\end{table}
```

### 竞争对比表
```latex
\begin{table}[htbp]
\centering
caption{竞争对比}
\begin{tabular}{@{}lccccc@{}}
\toprule
\textbf{因素} & \textbf{A公司} & \textbf{B公司} & \textbf{C公司} & \textbf{D公司} \\
\midrule
市场份额 & \rating{5} & \rating{4} & \rating{3} & \rating{2} \\
\rowcolor{tablealt} 产品质量 & \rating{4} & \rating{5} & \rating{3} & \rating{4} \\
价格竞争力 & \rating{3} & \rating{3} & \rating{5} & \rating{4} \\
\rowcolor{tablealt} 创新 & \rating{5} & \rating{4} & \rating{2} & \rating{3} \\
客户服务 & \rating{4} & \rating{4} & \rating{4} & \rating{5} \\
\bottomrule
\end{tabular}
\end{table}
```

---

## 故障排除

### 盒子溢出
如果盒子内容溢出页面，请拆分为多个盒子或使用分页：
```latex
\newpage
\begin{keyinsightbox}[续...]
```

### 图片放置
使用 `[htbp]` 进行灵活放置，或使用 `[H]`（需要 `float` 包）进行精确放置：
```latex
\begin{figure}[H]  % 需要 \usepackage{float}
```

### 表格过宽
使用 `\resizebox` 或 `adjustbox`：
```latex
\resizebox{\textwidth}{!}{
\begin{tabular}{...}
...
\end{tabular}
}
```

### 颜色不显示
确保 `xcolor` 包已加载 `[table]` 选项（样式文件中已包含）。

---

## 编译

使用 XeLaTeX 编译以获得最佳效果：
```bash
xelatex report.tex
bibtex report
xelatex report.tex
xelatex report.tex
```

或使用 latexmk：
```bash
latexmk -xelatex report.tex
```
