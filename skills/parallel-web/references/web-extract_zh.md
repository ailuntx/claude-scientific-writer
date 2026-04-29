# URL 提取

从以下来源提取内容：$ARGUMENTS

## 命令

基于 URL 或内容选择一个简短、描述性的文件名（例如 `vespa-docs`、`react-hooks-api`）。使用小写字母和连字符，不使用空格。

```bash
parallel-cli extract "$ARGUMENTS" --json -o "$FILENAME.json"
```

如有需要，可添加选项：
- `--objective "关注重点"` 用于聚焦特定内容

## 学术内容处理

从学术来源（arXiv、PubMed、期刊网站、会议论文集）提取时，使用 `--objective` 聚焦于最有价值的部分：

```bash
parallel-cli extract "$URL" --json --objective "extract abstract, methodology, key findings, and conclusions" -o "$FILENAME.json"
```

对于 arXiv 论文，如果可用，优先使用 `/abs/` URL（带有结构化元数据）而不是原始 PDF URL。如果用户提供了 PDF 链接，直接提取——parallel-cli 能够处理 PDF。

## 响应格式

返回格式如下：

**[页面标题](URL)**

对于学术论文，如果可用，请包含结构化元数据：
- **作者：** 作者列表
- **发表信息：** 日期和会议/期刊
- **DOI：** 如果可用
- **摘要：** 论文的摘要

然后逐字提供提取的内容，遵循以下规则：
- 逐字保留内容——不要改写或总结
- 彻底解析列表——提取每一个编号/项目符号条目
- 仅去除明显的噪音：导航菜单、页脚、广告
- 保留所有事实、名称、数字、日期、引用
- 对于学术论文，保留图表/表格的标题和参考文献

在响应之后，提及输出文件路径（`$FILENAME.json`），以便用户知道可用于后续提问。
