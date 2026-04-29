# 网络搜索

在网络上搜索：$ARGUMENTS

## 命令

选择基于查询的简短描述性文件名（例如 `ai-chip-news`、`react-vs-vue`）。使用小写字母和连字符，不要有空格。

```bash
parallel-cli search "$ARGUMENTS" -q "<keyword1>" -q "<keyword2>" --json --max-results 10 --excerpt-max-chars-total 27000 -o "$FILENAME.json"
```

第一个参数是**目标**——用自然语言描述你要查找的内容。它用一个调用代替多个关键词搜索，适用于宽泛或复杂的查询。添加 `-q` 标志进行特定关键词查询，以补充目标。`-o` 标志将完整结果保存到一个 JSON 文件，供后续提问使用。

如需要，可用的选项：
- `--after-date YYYY-MM-DD` 用于时间敏感的查询
- `--include-domains domain1.com,domain2.com` 限制到特定来源

## 学术来源策略

对于科学或技术查询，运行**两次搜索**，以确保学术来源与一般结果一同出现：

1. **以学术为重点的搜索**——添加 `--include-domains` 并指定学术域名：
   ```bash
   parallel-cli search "$ARGUMENTS" -q "<keyword1>" --json --max-results 10 --excerpt-max-chars-total 27000 --include-domains "scholar.google.com,arxiv.org,pubmed.ncbi.nlm.nih.gov,semanticscholar.org,biorxiv.org,medrxiv.org,ncbi.nlm.nih.gov,nature.com,science.org,ieee.org,acm.org,springer.com,wiley.com,cell.com,pnas.org,nih.gov" -o "$FILENAME-academic.json"
   ```

2. **通用搜索**——使用标准命令，无域名限制，以捕获相关的非学术来源。

合并结果，优先展示学术来源。如果只能进行一次搜索（例如明显非科学查询），则跳过学术搜索。

**何时使用两次搜索模式：** 任何涉及科学主张、医疗信息、研究发现、技术机制、统计数据，或一手文献比二手报道更可靠的查询。

## 解析结果

不要在命令执行中设置 `max_output_tokens`——输出已由 `--max-results` 和 `--excerpt-max-chars-total` 限制。限制输出令牌会截断 JSON 并破坏解析。

解析 stdout 中的 JSON。对于每个结果，提取：
- 标题、URL、发布日期
- 摘录中的有用内容（跳过导航噪音，如菜单、页脚、“跳到内容”）

## 回答格式

**关键：每个主张都必须有行内引用。** 使用仅从 JSON 输出中提取的 markdown 链接。绝不编造或猜测 URL。

对于学术来源，若元数据可用，使用作者-年份引用格式：
- 学术：[Smith et al., 2025](url) 或 [Smith & Jones, 2024](url)
- 非学术：[来源标题](url)

综合回答应做到：
- 若有，首先展示同行评审或预印本来源的研究发现
- 清楚区分基于一手研究的说法与二手报道的说法
- 包含具体的事实、名称、数字、日期
- 每个事实都行内引用——不得有任何未引用的主张
- 如果涉及多个主题，按主题组织
- 注明证据质量（例如，“一项随机对照试验发现……” vs. “一篇博客文章报道……”）

**以“来源”一节结尾**，列出所有引用的 URL，按类型分组：

```
来源：

学术/同行评审：
- [Smith et al., 2025 — 论文标题](https://doi.org/...) (Nature, 2025)
- [Jones & Lee, 2024 — 论文标题](https://arxiv.org/...) (arXiv 预印本)

其他：
- [来源标题](https://example.com/article) (2026年2月)
```

“来源”部分是强制性的，不可省略。如果未找到学术来源，请说明并解释原因（例如，话题太新，尚未研究，或本质上非学术性）。

在“来源”部分之后，提及输出文件路径（`$FILENAME.json`），让用户知道该文件可用于后续提问。
