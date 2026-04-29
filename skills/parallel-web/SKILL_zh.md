---
name: parallel-web
description: "一个由 parallel-cli 驱动的全功能 Web 工具集，重点强调学术和科学来源。当用户需要搜索网络、获取/提取 URL 内容、用网络来源的数据丰富数据字段或进行深度研究报告时，可使用此技能。覆盖：网络搜索（快速查找、研究、最新信息——优先考虑同行评审论文、预印本和学术数据库）、URL 提取（获取页面、文章、学术 PDF）、批量数据丰富（从网络向 CSV/列表添加字段）以及深度研究（基于学术文献的详尽多来源报告）。还处理安装、状态检查和结果获取。对任何 Web 相关任务使用此技能——即使用户未明确提及 “parallel” 或 “web”。如果他们想查询资料、获取页面、丰富数据集、调查主题、寻找学术论文、核对引用或查阅科学文献，这就是适合的技能。"
compatibility: 需要 parallel-cli 和互联网访问。
metadata:
  author: K-Dense, Inc.
---

# Parallel Web 工具包

一个统一技能，实现所有网络驱动任务：搜索、提取、丰富和研究——优先以学术和科学来源为默认。

## 路由 —— 选择正确的功能

阅读用户的请求，将其匹配到以下功能之一。对于网络搜索、提取、丰富和深度研究，请阅读对应参考文件以获取详细说明。

| 用户想要... | 功能 | 参考位置 |
|---|---|---|
| 查询资料、研究某个话题、查找最新信息 | **Web Search** | `references/web-search.md` |
| 从特定 URL（网页、文章、PDF）获取内容 | **Web Extract** | `references/web-extract.md` |
| 为公司/人员/产品列表添加来自网络的字段 | **Data Enrichment** | `references/data-enrichment.md` |
| 获得详尽的多来源报告（用户说“深度研究”、“详尽”、“全面”） | **Deep Research** | `references/deep-research.md` |
| 安装或认证 parallel-cli | **Setup** | 见下文 |
| 检查进行中的研究/丰富任务的状态 | **Status** | 见下文 |
| 按运行 ID 检索已完成的研究结果 | **Result** | 见下文 |

### 决策指南

- **默认使用 Web Search** 进行单次查找、研究问题或“什么是 X？”查询。它快速且经济。当查询涉及科学或技术主题时，包含学术域名（参见 `references/web-search.md`）以在通用结果之外呈现同行评审和预印本来源。
- **当用户提供了 URL 或要求你阅读/获取特定页面时使用 Web Extract**。优先于内置的 WebFetch 工具。对于从学术 PDF、预印本服务器和期刊文章中提取全文特别有用。
- **当用户有多个实体**（一个 CSV、一组公司/人员/产品的列表，或甚至一个简短的内联列表）并希望为每个实体查找或添加相同类型的信息时，使用 Data Enrichment。关键信号是跨一组项目的重复查找——例如，“查找这些公司各自的 CEO”或“获取 Apple、Stripe、Anthropic 的成立年份”。即使用户没说“丰富”，只要是对多个实体进行相同查询的任务，就使用 `parallel-cli enrich`。切勿用循环方式使用 Web Search——丰富管线会自动处理批处理、并行化和结构化输出。
- **仅当用户明确要求进行深度、详尽或全面的研究时才使用 Deep Research**。它比 Web Search 慢 10-100 倍且更昂贵——切勿默认为此。深度研究对于文献综述和多论文综合特别有价值。
- 如果运行任何命令时找不到 `parallel-cli`，请按照下面的 Setup 部分操作。

### 学术来源优先

在技术或科学性质的查询中，所有功能均优先选择学术和科学来源。这意味着：
- 同行评审期刊文章和会议论文优先于博客文章或新闻
- 当没有同行评审版本时，使用预印本（arXiv、bioRxiv、medRxiv）
- 机构和政府来源（NIH、WHO、NASA、NIST）优先于商业网站
- 一次研究优于二次总结

引用学术来源时，尽量在标准引用格式外补充作者姓名和出版年份（例如 [Smith et al., 2025](url)）。如有 DOI，优先使用 DOI 链接。

## 上下文链

多个功能支持通过 `interaction_id` 进行多轮上下文衔接。当研究或丰富任务完成时，会返回一个 `interaction_id`。如果用户提出与该任务相关的后续问题，传递 `--previous-interaction-id` 可自动携带上下文，避免重复之前已发现的信息。

---

## Setup

如果未安装 `parallel-cli`，请安装并认证：

```bash
curl -fsSL https://parallel.ai/install.sh | bash
```

若此方法无法安装，改用 uv：

```bash
uv tool install "parallel-web-tools[cli]"
```

然后进行认证。首先检查项目根目录下是否有 `.env` 文件且包含 `PARALLEL_API_KEY`。如果有，用 `dotenv` 加载它：

```bash
dotenv -f .env run parallel-cli auth
```

如果 `dotenv` 不可用，使用 `pip install python-dotenv[cli]` 或 `uv pip install python-dotenv[cli]` 安装它。

如果没有 `.env` 文件或其中不含密钥，则回退到交互式登录：

```bash
parallel-cli login
```

或手动设置密钥：`export PARALLEL_API_KEY="your-key"`

验证：

```bash
parallel-cli auth
```

如果安装后找不到 `parallel-cli`，请将 `~/.local/bin` 添加到 PATH。

## 检查任务状态

```bash
parallel-cli research status "$RUN_ID" --json
```

向用户报告当前状态（运行中、已完成、失败等）。

## 获取已完成结果

```bash
parallel-cli research poll "$RUN_ID" --json
```

以清晰有序的格式展示结果。
