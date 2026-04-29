# 期刊格式要求

主要科学期刊的综合格式要求和投稿指南。

**最后更新**：2024

---

## Nature 期刊系列

### Nature

**期刊类型**：顶级多学科科学期刊  
**出版商**：Nature Publishing Group  
**影响因子**：约64（因年份而异）

**格式要求**：
- **篇幅**：文章约3,000词（不含方法、参考文献、图例）
- **结构**：标题、作者、署名、摘要（≤200词）、正文、方法、参考文献、致谢、作者贡献、利益竞争、图例
- **格式**：投稿用单栏（最终出版为双栏）
- **字体**：任意标准字体（Times、Arial、Helvetica），12pt
- **行距**：双倍行距
- **页边距**：四周2.5 cm（1英寸）
- **页码**：所有页面均需标注
- **引用**：上标编号顺序¹²³
- **参考文献**：Nature格式（期刊名称缩写）
  - 格式：作者, A. A., 作者, B. B. & 作者, C. C. 文章标题. *期刊缩写***卷**, 页码 (年份).
  - 示例：Watson, J. D. & Crick, F. H. C. Molecular structure of nucleic acids. *Nature* **171**, 737–738 (1953).
- **图片**： 
  - 格式：TIFF、EPS、PDF（矢量优先）
  - 分辨率：照片300-600 dpi，线条图1000 dpi
  - 颜色：RGB或CMYK
  - 尺寸：适应单栏（89 mm）或双栏（183 mm）
  - 图例：单独提供，不嵌入图中
- **表格**：可编辑格式（Word、Excel），不要作为图片
- **补充材料**：无限制，PDF格式优先

**LaTeX模板**：`assets/journals/nature_article.tex`

**作者指南**：https://www.nature.com/nature/for-authors

---

### Nature Communications

**期刊类型**：开放获取多学科期刊  
**出版商**：Nature Publishing Group

**格式要求**：
- **篇幅**：无严格限制（通常5,000-8,000词）
- **结构**：与Nature相同（标题、摘要、正文、方法、参考文献等）
- **格式**：单栏
- **字体**：Times New Roman、Arial或类似，12pt
- **行距**：双倍行距
- **页边距**：四周2.5 cm
- **引用**：上标编号顺序
- **参考文献**：Nature格式（与Nature相同）
- **图片**：与Nature要求相同
- **表格**：与Nature要求相同
- **开放获取**：所有文章开放获取（需付APC）

**LaTeX模板**：`assets/journals/nature_communications.tex`

---

### Nature Methods、Nature Biotechnology、Nature Machine Intelligence

**格式**：与Nature Communications相同（Nature系列期刊格式相近）

**学科特定说明**：
- **Nature Methods**：强调方法创新和验证
- **Nature Biotechnology**：聚焦生物技术应用和转化
- **Nature Machine Intelligence**：跨学科AI/ML应用

---

## Science 系列

### Science

**期刊类型**：顶级多学科科学期刊  
**出版商**：美国科学促进会（AAAS）

**格式要求**：
- **篇幅**： 
  - 研究文章：2,500词（仅正文，不含参考文献/图片）
  - 报告：最多2,500词
- **结构**：标题、作者、署名、摘要（≤125词）、正文、材料与方法、参考文献、致谢、补充材料
- **格式**：投稿用单栏
- **字体**：Times New Roman，12pt
- **行距**：双倍行距
- **页边距**：四周1英寸
- **引用**：括号内编号顺序 (1, 2, 3)
- **参考文献**：Science格式（主参考文献中无文章标题，移至补充材料）
  - 格式：A. 作者, B. 作者, *期刊缩写***卷**, 页码 (年份).
  - 示例：J. D. Watson, F. H. C. Crick, *Nature* **171**, 737 (1953).
- **图片**： 
  - 格式：PDF、EPS、TIFF
  - 分辨率：最低300 dpi
  - 颜色：RGB
  - 尺寸：最大宽度9 cm（单栏）或18.3 cm（双栏）
  - 图片计入页数限制
- **表格**：可纳入正文或作为单独文件
- **补充材料**：允许大量材料

**LaTeX模板**：`assets/journals/science_article.tex`

**作者指南**：https://www.science.org/content/page/instructions-authors

---

### Science Advances

**期刊类型**：开放获取多学科期刊  
**出版商**：AAAS

**格式要求**：
- **篇幅**：无严格字数限制（但鼓励简洁写作）
- **结构**：与Science相似（更灵活）
- **格式**：单栏
- **字体**：Times New Roman，12pt
- **引用**：括号内编号
- **参考文献**：Science格式
- **图片**：与Science相同
- **开放获取**：所有文章开放获取

**LaTeX模板**：`assets/journals/science_advances.tex`

---

## PLOS（科学公共图书馆）

### PLOS ONE

**期刊类型**：开放获取多学科期刊  
**出版商**：科学公共图书馆

**格式要求**：
- **篇幅**：无最大篇幅限制
- **结构**：标题、作者、署名、摘要、引言、材料与方法、结果、讨论、结论（可选）、参考文献、支撑信息
- **格式**：可编辑文件（LaTeX、Word、RTF）
- **字体**：Times、Arial或Helvetica，10-12pt
- **行距**：双倍行距
- **页边距**：四周1英寸（2.54 cm）
- **页码**：需要
- **引用**：温哥华格式，方括号内编号 [1]、[2]、[3]
- **参考文献**：温哥华/NLM格式
  - 格式：作者 AA, 作者 BB, 作者 CC. 文章标题. 期刊缩写. 年;卷(期):页码. doi:xx.xxxx
  - 示例：Watson JD, Crick FHC. Molecular structure of nucleic acids. Nature. 1953;171(4356):737-738.
- **图片**：
  - 格式：TIFF、EPS、PDF、PNG
  - 分辨率：300-600 dpi
  - 颜色：RGB
  - 图例：提供在正文参考文献之后
- **表格**：可编辑格式，每页一个
- **数据可用性**：需要声明
- **开放获取**：所有文章开放获取（需付APC）

**LaTeX模板**：`assets/journals/plos_one.tex`

**作者指南**：https://journals.plos.org/plosone/s/submission-guidelines

---

### PLOS Biology、PLOS Computational Biology 等

**格式**：与PLOS ONE相似，有学科特定变化

**主要区别**：
- PLOS Biology：更具选择性，强调广泛意义
- PLOS Comp Bio：聚焦计算方法与模型

---

## Cell Press

### Cell

**期刊类型**：顶级生物学期刊  
**出版商**：Cell Press (Elsevier)

**格式要求**：
- **篇幅**： 
  - 文章：约5,000词（不含方法、参考文献）
  - 短文章：约2,500词
- **结构**：摘要（≤150词）、关键词、引言、结果、讨论、实验程序、致谢、作者贡献、利益声明、参考文献
- **格式**：双倍行距
- **字体**：12pt
- **页边距**：四周1英寸
- **引用**：作者-年份格式（Smith et al., 2023）
- **参考文献**：Cell格式
  - 格式：作者, A.A., 和作者, B.B. (年份). 标题. *期刊***卷**, 页码.
  - 示例：Watson, J.D., and Crick, F.H. (1953). Molecular structure of nucleic acids. *Nature* 171, 737-738.
- **图片**：
  - 格式：TIFF、EPS优先
  - 分辨率：照片300 dpi，线条图1000 dpi
  - 颜色：RGB或CMYK
  - 多面板图片常见
- **表格**：可编辑格式
- **eTOC简介**：需要30-50词摘要
- **图形摘要**：必需

**LaTeX模板**：`assets/journals/cell_article.tex`

**作者指南**：https://www.cell.com/cell/authors

---

### Neuron、Immunity、Molecular Cell、Developmental Cell

**格式**：与Cell相似，有学科特定要求

---

## IEEE Transactions

### IEEE Transactions on [各类主题]

**期刊类型**：工程和计算机科学期刊  
**出版商**：电气与电子工程师协会

**格式要求**：
- **篇幅**：因会刊而异（通常最终格式8-12页）
- **结构**：摘要、索引词、引言、[正文章节]、结论、致谢、参考文献、简历
- **格式**：双栏
- **字体**：Times New Roman，10pt
- **栏间距**：0.17英寸（4.23 mm）
- **页边距**： 
  - 顶部：19 mm（0.75英寸）
  - 底部：25 mm（1英寸）
  - 侧边：17 mm（0.67英寸）
- **引用**：方括号内编号 [1]、[2]、[3]
- **参考文献**：IEEE格式
  - 格式：[1] A. A. 作者，"论文标题，" *期刊缩写*，卷 x, 期 x, 页码 xxx-xxx, 月 年.
  - 示例：[1] J. D. Watson and F. H. C. Crick, "Molecular structure of nucleic acids," *Nature*, vol. 171, pp. 737-738, Apr. 1953.
- **图片**：
  - 格式：EPS、PDF（矢量）、TIFF（栅格）
  - 分辨率：线条图600-1200 dpi，灰度/彩色300 dpi
  - 颜色：在线用RGB，印刷用CMYK（如需要）
  - 位置：栏顶或栏底
- **表格**：LaTeX表格环境，置于顶部/底部
- **公式**：连续编号

**LaTeX模板**：`assets/journals/ieee_trans.tex`

**作者指南**：https://journals.ieeeauthorcenter.ieee.org/

---

### IEEE Access

**期刊类型**：开放获取多学科工程期刊  
**出版商**：IEEE

**格式**：与IEEE Transactions相似
- **篇幅**：无页数限制
- **开放获取**：所有文章开放获取
- **快速出版**：比Transactions审稿更快

**LaTeX模板**：`assets/journals/ieee_access.tex`

---

## ACM 出版物

### ACM Transactions

**期刊类型**：计算机科学汇刊  
**出版商**：美国计算机协会

**格式要求**：
- **篇幅**：无严格限制
- **结构**：摘要、CCS概念、关键词、ACM参考文献格式、引言、[正文]、结论、致谢、参考文献
- **格式**：最终双栏，投搞可用单栏
- **字体**：取决于模板（通常9-10pt）
- **文档类**：使用 `acmart` LaTeX文档类
- **引用**：编号 [1] 或作者-年份（视会议/期刊而定）
- **参考文献**：ACM格式
  - 格式：作者. 年份. 标题. 期刊 卷, 期 (年份), 页码. DOI
  - 示例：James D. Watson and Francis H. C. Crick. 1953. Molecular structure of nucleic acids. Nature 171, 4356 (1953), 737-738. https://doi.org/10.1038/171737a0
- **图片**：EPS、PDF（矢量优先），高分辨率栅格
- **CCS概念**：必需（ACM计算分类系统）
- **关键词**：必需

**LaTeX模板**：`assets/journals/acm_article.tex`

**作者指南**：https://www.acm.org/publications/authors

---

## Springer 期刊

### 通用 Springer 期刊

**出版商**：Springer Nature

**格式要求**：
- **篇幅**：因期刊而异（请查阅具体期刊）
- **格式**：投稿用单栏（LaTeX或Word）
- **字体**：10-12pt
- **行距**：双倍或1.5倍
- **引用**：编号或作者-年份（因期刊而异）
- **参考文献**：Springer格式（类似温哥华或作者-年份）
  - 编号：作者 AA, 作者 BB (年份) 标题. 期刊 卷:页码
  - 作者-年份：作者 AA, 作者 BB (年份) 标题. 期刊 卷:页码
- **图片**：TIFF、EPS、PDF；300+ dpi
- **表格**：可编辑格式
- **文档类**：许多Springer期刊使用 `svjour3`

**LaTeX模板**：`assets/journals/springer_article.tex`

**作者指南**：因具体期刊而异

---

## Elsevier 期刊

### 通用 Elsevier 期刊

**出版商**：Elsevier

**格式要求**：
- **篇幅**：因期刊差异很大
- **格式**：单栏（LaTeX或Word）
- **字体**：12pt
- **行距**：双倍行距
- **引用**：编号或作者-年份（请查阅期刊指南）
- **参考文献**：格式因期刊而异（Harvard、温哥华、编号）
  - 请查阅具体期刊的"作者指南"
- **图片**：TIFF、EPS；300+ dpi
- **表格**：可编辑格式
- **文档类**：`elsarticle` LaTeX类

**LaTeX模板**：`assets/journals/elsevier_article.tex`

**作者指南**：https://www.elsevier.com/authors（选择具体期刊）

---

## BMC 期刊

### BMC Biology、BMC Bioinformatics 等

**出版商**：BioMed Central (Springer Nature)

**格式要求**：
- **篇幅**：无最大篇幅限制
- **结构**：摘要（结构化）、关键词、背景、[方法/结果/讨论]、结论、缩写、声明（伦理、同意、可用性、利益竞争、资助、作者贡献、致谢）、参考文献
- **格式**：单栏
- **字体**：Arial或Times，12pt
- **行距**：双倍
- **引用**：温哥华格式，方括号内编号 [1]
- **参考文献**：温哥华/NLM格式
- **图片**：TIFF、EPS、PNG；300+ dpi
- **表格**：可编辑
- **开放获取**：所有BMC期刊开放获取
- **数据可用性**：需要声明

**LaTeX模板**：`assets/journals/bmc_article.tex`

**作者指南**：https://www.biomedcentral.com/getpublished

---

## Frontiers 期刊

### Frontiers in [各类主题]

**出版商**：Frontiers Media

**格式要求**：
- **篇幅**：因文章类型而异（研究文章约12页，简短研究报告约4页）
- **结构**：摘要、关键词、引言、材料与方法、结果、讨论、结论、数据可用性声明、伦理声明、作者贡献、资助、致谢、利益竞争、参考文献
- **格式**：单栏
- **字体**：Times New Roman，12pt
- **行距**：双倍
- **引用**：编号（Frontiers格式）
- **参考文献**：Frontiers格式
  - 格式：作者 A., 作者 B., 作者 C. (年份). 标题. *期刊缩写***卷**:页码. doi
  - 示例：Watson J. D., Crick F. H. C. (1953). Molecular structure of nucleic acids. *Nature* 171:737-738. doi:10.1038/171737a0
- **图片**：TIFF、EPS；最低300 dpi
- **表格**：可编辑
- **开放获取**：所有Frontiers期刊开放获取
- **图例**：详细，每图最多350词

**LaTeX模板**：`assets/journals/frontiers_article.tex`

**作者指南**：https://www.frontiersin.org/guidelines/author-guidelines

---

## 专业期刊

### PNAS（美国国家科学院院刊）

**格式要求**：
- **篇幅**：6页（正文、图片、表格合计）
- **摘要**：最多250词
- **意义声明**：最多120词（必需）
- **结构**：摘要、意义、正文、材料与方法、致谢、参考文献
- **格式**：单栏
- **引用**：编号
- **参考文献**：PNAS格式
- **LaTeX类**：`pnas-new`

**LaTeX模板**：`assets/journals/pnas_article.tex`

---

### Physical Review Letters (PRL)

**出版商**：美国物理学会

**格式要求**：
- **篇幅**：4页（含图片和参考文献）
- **格式**：双栏（REVTeX 4.2）
- **摘要**：不超过600字符
- **引用**：编号
- **参考文献**：APS格式
- **文档类**：`revtex4-2`

**LaTeX模板**：`assets/journals/prl_article.tex`

---

### New England Journal of Medicine (NEJM)

**格式要求**：
- **篇幅**：原创文章约3,000词
- **结构**：摘要（结构化，250词）、引言、方法、结果、讨论、参考文献
- **格式**：双倍行距
- **引用**：编号
- **参考文献**：NEJM格式（改良温哥华格式）
- **图片**：高分辨率，专业质量
- **倾向Word投稿**（LaTeX较少见）

---

### The Lancet

**格式要求**：
- **篇幅**：文章约3,000词
- **摘要**：结构化，300词
- **结构**：面板（摘要框）、引言、方法、结果、讨论、参考文献
- **引用**：编号
- **参考文献**：Lancet格式（改良温哥华格式）
- **倾向Word投稿**

---

## 快速参考表

| 期刊 | 最大篇幅 | 格式 | 引用 | 模板 |
|---------|-----------|--------|-----------|----------|
| **Nature** | 约3,000词 | 单栏 | 上标 | `nature_article.tex` |
| **Science** | 2,500词 | 单栏 | (1) 括号 | `science_article.tex` |
| **PLOS ONE** | 无限制 | 单栏 | [1] 温哥华 | `plos_one.tex` |
| **Cell** | 约5,000词 | 双倍行距 | (作者, 年份) | `cell_article.tex` |
| **IEEE Trans** | 8-12页 | 双栏 | [1] IEEE | `ieee_trans.tex` |
| **ACM Trans** | 可变 | 双栏 | [1] 或作者-年 | `acm_article.tex` |
| **Springer** | 可变 | 单栏 | 编号/作者-年 | `springer_article.tex` |
| **BMC** | 无限制 | 单栏 | [1] 温哥华 | `bmc_article.tex` |
| **Frontiers** | 约12页 | 单栏 | 编号 | `frontiers_article.tex` |

---

## 备注

1. **始终查阅官方指南**：期刊要求会变化；投稿前请核实
2. **模板时效性**：这些模板会定期更新，但可能滞后于官方变更
3. **补充材料**：大多数期刊允许大量补充材料
4. **预印本政策**：查阅期刊的预印本政策（大多数允许arXiv、bioRxiv）
5. **开放获取选项**：许多订阅期刊提供开放获取选项（需付费）
6. **LaTeX vs. Word**：大多数期刊两者都接受；数学内容多的文章首选LaTeX

## 获取官方模板

许多期刊提供官方LaTeX模板：
- **Nature**：从期刊网站下载
- **IEEE**：IEEEtran类（广泛可用）
- **ACM**：acmart类（CTAN）
- **Elsevier**：elsarticle类（CTAN）
- **Springer**：svjour3类（期刊网站）

查阅期刊的"For Authors"或"Submit"页面获取最新模板。
