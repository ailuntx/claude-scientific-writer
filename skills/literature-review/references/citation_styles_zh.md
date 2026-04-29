# 引用格式参考

本文档详细介绍了文献综述中常用的各种学术引用格式的指南。

## APA 格式（第7版）

### 期刊文章

**格式**：Author, A. A., Author, B. B., & Author, C. C. (Year). Title of article. *Title of Periodical*, *volume*(issue), page range. https://doi.org/xx.xxx/yyyy

**示例**：Smith, J. D., Johnson, M. L., & Williams, K. R. (2023). Machine learning approaches in drug discovery. *Nature Reviews Drug Discovery*, *22*(4), 301-318. https://doi.org/10.1038/nrd.2023.001

### 书籍

**格式**：Author, A. A. (Year). *Title of work: Capital letter also for subtitle*. Publisher Name. https://doi.org/xxxx

**示例**：Kumar, V., Abbas, A. K., & Aster, J. C. (2021). *Robbins and Cotran pathologic basis of disease* (10th ed.). Elsevier.

### 书籍章节

**格式**：Author, A. A., & Author, B. B. (Year). Title of chapter. In E. E. Editor & F. F. Editor (Eds.), *Title of book* (pp. xx-xx). Publisher.

**示例**：Brown, P. O., & Botstein, D. (2020). Exploring the new world of the genome with DNA microarrays. In M. B. Eisen & P. O. Brown (Eds.), *DNA microarrays: A molecular cloning manual* (pp. 1-45). Cold Spring Harbor Laboratory Press.

### 预印本

**格式**：Author, A. A., & Author, B. B. (Year). Title of preprint. *Repository Name*. https://doi.org/xxxx

**示例**：Zhang, Y., Chen, L., & Wang, H. (2024). Novel therapeutic targets in Alzheimer's disease. *bioRxiv*. https://doi.org/10.1101/2024.01.001

### 会议论文

**格式**：Author, A. A. (Year, Month day-day). Title of paper. In E. E. Editor (Ed.), *Title of conference proceedings* (pp. xx-xx). Publisher. https://doi.org/xxxx

---

## Nature 格式

### 期刊文章

**格式**：Author, A. A., Author, B. B. & Author, C. C. Title of article. *J. Name* **volume**, page range (year).

**示例**：Smith, J. D., Johnson, M. L. & Williams, K. R. Machine learning approaches in drug discovery. *Nat. Rev. Drug Discov.* **22**, 301-318 (2023).

### 书籍

**格式**：Author, A. A. & Author, B. B. *Book Title* (Publisher, Year).

**示例**：Kumar, V., Abbas, A. K. & Aster, J. C. *Robbins and Cotran Pathologic Basis of Disease* 10th edn (Elsevier, 2021).

### 多位作者

- 1-2位作者：列出全部
- 3位及以上作者：列出第一位作者后加"et al."

**示例**：Zhang, Y. et al. Novel therapeutic targets in Alzheimer's disease. *bioRxiv* https://doi.org/10.1101/2024.01.001 (2024).

---

## Chicago 格式（作者-日期）

### 期刊文章

**格式**：Author, First Name Middle Initial. Year. "Article Title." *Journal Title* volume, no. issue (Month): page range. https://doi.org/xxxx.

**示例**：Smith, John D., Mary L. Johnson, and Karen R. Williams. 2023. "Machine Learning Approaches in Drug Discovery." *Nature Reviews Drug Discovery* 22, no. 4 (April): 301-318. https://doi.org/10.1038/nrd.2023.001.

### 书籍

**格式**：Author, First Name Middle Initial. Year. *Book Title: Subtitle*. Edition. Place: Publisher.

**示例**：Kumar, Vinay, Abul K. Abbas, and Jon C. Aster. 2021. *Robbins and Cotran Pathologic Basis of Disease*. 10th ed. Philadelphia: Elsevier.

---

## Vancouver 格式（编号）

### 期刊文章

**格式**：Author AA, Author BB, Author CC. Title of article. Abbreviated Journal Name. Year;volume(issue):page range.

**示例**：Smith JD, Johnson ML, Williams KR. Machine learning approaches in drug discovery. Nat Rev Drug Discov. 2023;22(4):301-18.

### 书籍

**格式**：Author AA, Author BB. Title of book. Edition. Place: Publisher; Year.

**示例**：Kumar V, Abbas AK, Aster JC. Robbins and Cotran pathologic basis of disease. 10th ed. Philadelphia: Elsevier; 2021.

### 正文引用

按出现顺序使用上标数字："Recent studies^1,2^ have shown..."

---

## IEEE 格式

### 期刊文章

**格式**：[#] A. A. Author, B. B. Author, and C. C. Author, "Title of article," *Abbreviated Journal Name*, vol. x, no. x, pp. xxx-xxx, Month Year.

**示例**[1] J. D. Smith, M. L. Johnson, and K. R. Williams, "Machine learning approaches in drug discovery," *Nat. Rev. Drug Discov.*, vol. 22, no. 4, pp. 301-318, Apr. 2023.

### 书籍

**格式**：[#] A. A. Author, *Title of Book*, xth ed. City, State: Publisher, Year.

**示例**[2] V. Kumar, A. K. Abbas, and J. C. Aster, *Robbins and Cotran Pathologic Basis of Disease*, 10th ed. Philadelphia, PA: Elsevier, 2021.

---

## 期刊名称常用缩写

- Nature: Nat.
- Science: Science
- Cell: Cell
- Nature Reviews Drug Discovery: Nat. Rev. Drug Discov.
- Journal of the American Chemical Society: J. Am. Chem. Soc.
- Proceedings of the National Academy of Sciences: Proc. Natl. Acad. Sci. U.S.A.
- PLOS ONE: PLoS ONE
- Bioinformatics: Bioinformatics
- Nucleic Acids Research: Nucleic Acids Res.

---

## DOI 最佳实践

1. **始终验证 DOI**：使用 verify_citations.py 脚本检查所有 DOI
2. **格式化为 URL**：https://doi.org/10.xxxx/yyyy（优于 doi:10.xxxx/yyyy）
3. **DOI 后不加句号**：DOI 应为最后一个元素，后面不加标点
4. **检查重定向**：确保 DOI 解析到正确的文章

---

## 正文引用指南

### APA 格式
- (Smith et al., 2023)
- Smith et al. (2023) demonstrated...
- 多次引用：(Brown, 2022; Smith et al., 2023; Zhang, 2024)

### Nature 格式
- 上标数字：Recent studies^1,2^ have shown...
- 或：Recent studies (refs 1,2) have shown...

### Chicago 格式
- (Smith, Johnson, and Williams 2023)
- Smith, Johnson, and Williams (2023) found...

---

## 参考文献列表组织

### 按引用格式
- **APA, Chicago**：按第一位作者的姓氏字母顺序排列
- **Nature, Vancouver, IEEE**：按正文首次出现顺序编号

### 悬挂缩进
大多数格式使用悬挂缩进，即第一行左对齐，后续行缩进。

### 一致性
保持全文格式一致：
- 大小写（标题式大写 vs 句式大写）
- 期刊名称缩写
- DOI 呈现方式
- 作者姓名格式
