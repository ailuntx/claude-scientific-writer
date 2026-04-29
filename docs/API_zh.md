# Scientific Writer API

**Scientific Writer 是一款深度研究与写作工具**，将 AI 驱动的深度研究与格式完善的书面输出相结合。此 API 允许你以程序化方式生成可直接用于发表的文档，并由实时文献检索和已验证的引用提供支持。

Scientific Writer v2.0 程序化 API 的完整参考。快速开始请参阅 README。此页面包含完整细节、示例和最佳实践。

## 安装

```bash
# 使用 uv 安装（推荐）
uv sync

# 或在当前环境中安装
uv pip install -e .
```

## 快速开始

```python
import asyncio
from scientific_writer import generate_paper

async def main():
    async for update in generate_paper("Create a Nature paper on CRISPR"):
        if update["type"] == "progress":
            print(f"[{update['stage']}] {update['message']}")
        else:
            print(f"PDF: {update['files']['pdf_final']}")

asyncio.run(main())
```

## API 函数

### `generate_paper()`

异步生成器，用于创建一篇科学论文并产出进度更新。

**签名：**
```python
from typing import AsyncGenerator, Dict, Any, Optional, List

async def generate_paper(
    query: str,
    output_dir: Optional[str] = None,
    api_key: Optional[str] = None,
    model: str = "claude-sonnet-4-6",
    data_files: Optional[List[str]] = None,
    cwd: Optional[str] = None,
    track_token_usage: bool = False,
) -> AsyncGenerator[Dict[str, Any], None]
```

**参数：**

| 参数 | 类型 | 必需 | 默认值 | 描述 |
|-----------|------|----------|---------|-------------|
| `query` | `str` | 是 | - | 论文生成请求（例如，“Create a Nature paper on CRISPR”） |
| `output_dir` | `str` | 否 | `None` | 自定义输出目录。默认值为 `cwd/writing_outputs` |
| `api_key` | `str` | 否 | `None` | Anthropic API key。默认使用 `ANTHROPIC_API_KEY` 环境变量 |
| `model` | `str` | 否 | `"claude-sonnet-4-6"` | 要使用的 Claude 模型 |
| `data_files` | `List[str]` | 否 | `None` | 要包含在论文中的文件路径列表 |
| `cwd` | `str` | 否 | `None` | 工作目录。默认值为包的父目录 |
| `track_token_usage` | `bool` | 否 | `False` | 若为 True，则在最终结果中跟踪并返回 token 使用量 |

**返回：**

一个异步生成器，产出：
1. 执行期间的进度更新（type="progress"）
2. 带有完整论文信息的最终结果（type="result"）

**示例：**
```python
import asyncio
from scientific_writer import generate_paper

async def example():
    async for update in generate_paper(
        query="Create a NeurIPS paper on transformers",
        output_dir="./my_papers",
        data_files=["results.csv", "figure.png"],
    ):
        if update["type"] == "progress":
            print(f"[{update['stage']}] {update['message']}")
        else:
            print(f"Done! PDF: {update['files']['pdf_final']}")

asyncio.run(example())
```

## 数据模型

### `ProgressUpdate`

论文生成期间产出的进度信息。

**字段：**
```python
{
    "type": "progress",
    "timestamp": str,      # ISO 8601 时间戳
    "message": str,        # 进度消息
    "stage": str,          # 当前阶段（见下方阶段）
    "details": dict | None # 可选的附加上下文（工具名称、文件等）
}
```

**阶段：**
- `initialization` - 设置论文生成
- `research` - 进行文献研究
- `writing` - 编写论文各部分
- `compilation` - 将 LaTeX 编译为 PDF
- `complete` - 完成并扫描结果

### `PaperResult`

包含所有论文信息的完整最终结果。

**字段：**
```python
{
    "type": "result",
    "status": str,                    # "success" | "partial" | "failed"
    "paper_directory": str,           # 论文目录的完整路径
    "paper_name": str,                # 论文目录名称
    "metadata": PaperMetadata,        # 论文元数据
    "files": PaperFiles,              # 所有生成的文件
    "citations": dict,                # 引用信息
    "figures_count": int,             # 图表数量
    "compilation_success": bool,      # 是否生成了 PDF
    "errors": List[str],              # 任意错误消息
    "token_usage": TokenUsage | None  # token 使用量（当 track_token_usage=True 时）
}
```

**状态值：**
- `success` - 论文已完整生成并包含 PDF
- `partial` - 已创建 TeX 但 PDF 编译失败
- `failed` - 生成失败（见 `errors` 字段）

### `PaperMetadata`

关于生成论文的元数据。

**字段：**
```python
{
    "title": Optional[str],      # 提取出的论文标题
    "created_at": str,           # ISO 8601 时间戳
    "topic": str,                # 从目录名中提取的主题
    "word_count": Optional[int]  # 估算的字数
}
```

### `PaperFiles`

所有生成论文文件的路径。

**字段：**
```python
{
    "pdf_final": Optional[str],      # 最终 PDF 路径
    "tex_final": Optional[str],      # 最终 TeX 源文件路径
    "pdf_drafts": List[str],         # 草稿 PDF 路径列表
    "tex_drafts": List[str],         # 草稿 TeX 路径列表
    "bibliography": Optional[str],   # BibTeX 文件路径
    "figures": List[str],            # 图表文件路径列表
    "data": List[str],               # 数据文件路径列表
    "progress_log": Optional[str],   # progress.md 路径
    "summary": Optional[str]         # SUMMARY.md 路径
}
```

### `TokenUsage`

token 使用统计。仅在 `track_token_usage=True` 时出现。

**字段：**
```python
{
    "input_tokens": int,                  # 消耗的输入 token 总数
    "output_tokens": int,                 # 生成的输出 token 总数
    "total_tokens": int,                  # 输入 + 输出 token 之和
    "cache_creation_input_tokens": int,   # 用于创建缓存的 token
    "cache_read_input_tokens": int        # 从缓存读取的 token
}
```

**示例：**
```python
async for update in generate_paper("Create a paper", track_token_usage=True):
    if update["type"] == "result":
        if "token_usage" in update:
            usage = update["token_usage"]
            print(f"Input: {usage['input_tokens']:,} tokens")
            print(f"Output: {usage['output_tokens']:,} tokens")
            print(f"Total: {usage['total_tokens']:,} tokens")
```

## 使用模式

### 基本论文生成

```python
import asyncio
from scientific_writer import generate_paper

async def create_paper():
    query = "Create a Nature paper on quantum computing"
    
    async for update in generate_paper(query):
        if update["type"] == "progress":
            print(f"进度：{update['message']}")
        else:
            if update["status"] == "success":
                print(f"成功！PDF: {update['files']['pdf_final']}")
            else:
                print(f"失败：{update['errors']}")

asyncio.run(create_paper())
```

### 带阶段的进度跟踪

```python
async def track_progress():
    async for update in generate_paper("Create a paper on ML"):
        if update["type"] == "progress":
            # 显示基于阶段的进度
            stage_icons = {
                "initialization": "🔧",
                "research": "🔍",
                "writing": "✍️",
                "compilation": "📦",
                "complete": "✅"
            }
            icon = stage_icons.get(update["stage"], "⏳")
            print(f"{icon} [{update['stage']:12}] {update['message']}")
        else:
            print(f"\n✅ 完成！PDF: {update['files']['pdf_final']}")
```

### 自定义输出目录

```python
async def custom_directory():
    async for update in generate_paper(
        "Create a conference paper",
        output_dir="./my_research/papers"
    ):
        if update["type"] == "result":
            print(f"论文已保存到：{update['paper_directory']}")
```

### 包含数据文件

```python
async def with_data_files():
    data_files = [
        "./experiment_results.csv",
        "./figures/performance_graph.png",
        "./appendix_data.json"
    ]
    
    async for update in generate_paper(
        "Create a paper analyzing the experimental results",
        data_files=data_files
    ):
        if update["type"] == "result":
            print(f"已包含 {len(data_files)} 个数据文件")
            print(f"结果有 {update['figures_count']} 张图")
```

### 将完整结果保存为 JSON

```python
import json

async def save_to_json():
    result = None
    
    async for update in generate_paper("Create a paper"):
        if update["type"] == "result":
            result = update
    
    if result:
        with open("paper_result.json", "w") as f:
            json.dump(result, f, indent=2)
        print("结果已保存到 paper_result.json")
```

### 错误处理

```python
async def with_error_handling():
    try:
        async for update in generate_paper("Create a paper"):
            if update["type"] == "progress":
                print(f"[{update['stage']}] {update['message']}")
            else:
                if update["status"] == "failed":
                    print("生成失败！")
                    for error in update["errors"]:
                        print(f"  错误：{error}")
                elif update["status"] == "partial":
                    print("部分成功")
                    print(f"  TeX 文件：{update['files']['tex_final']}")
                    print("  PDF 编译失败")
                else:
                    print("成功！")
    except ValueError as e:
        print(f"配置错误：{e}")
    except Exception as e:
        print(f"意外错误：{e}")
```

### 自定义 API Key

```python
async def with_custom_api_key():
    # 覆盖 ANTHROPIC_API_KEY 环境变量
    async for update in generate_paper(
        "Create a paper",
        api_key="sk-ant-your-api-key-here"
    ):
        # 处理更新...
        pass
```

### 访问所有生成的文件

```python
async def list_all_files():
    async for update in generate_paper("Create a paper"):
        if update["type"] == "result":
            files = update["files"]
            
            print("生成的文件：")
            print(f"  PDF: {files['pdf_final']}")
            print(f"  TeX: {files['tex_final']}")
            print(f"  Bibliography: {files['bibliography']}")
            
            print(f"\n草稿（{len(files['pdf_drafts'])} 个版本）：")
            for draft in files['pdf_drafts']:
                print(f"  - {draft}")
            
            print(f"\n图表（{len(files['figures'])} 个文件）：")
            for fig in files['figures']:
                print(f"  - {fig}")
            
            print(f"\n数据文件（{len(files['data'])} 个文件）：")
            for data in files['data']:
                print(f"  - {data}")
```

## 环境变量

| 变量 | 必需 | 描述 |
|----------|----------|-------------|
| `ANTHROPIC_API_KEY` | 是* | 你的 Anthropic API key，用于 Scientific-Writer |
| `OPENROUTER_API_KEY` | 否 | 通过 Perplexity Sonar Pro Search 进行实时研究检索 |

\* 可通过向 `generate_paper()` 传递 `api_key` 参数来覆盖

### Research Lookup

当设置了 `OPENROUTER_API_KEY` 时，系统将获得实时研究能力：

- 论文生成期间的**实时互联网搜索**
- 来自 2024-2025 的**近期出版物**
- 使用当前数据进行**事实验证**
- 针对最新研究的**引用发现**

需要时会自动调用 research lookup——你无需显式请求它。

### 原生 Web Search

除了 research lookup，系统还包含 Claude 的原生 **WebSearch** 工具，用于：

- **时事** 和一般信息
- **非学术来源**（新闻、博客、文档）
- 可能不在学术数据库中的**实时信息**
- 来自多样来源的**事实核查**与验证

这两个工具协同工作：research-lookup 用于学术/科研内容，WebSearch 用于更广泛的网络信息。

**设置：**
```bash
# 添加到你的 .env 文件
echo "OPENROUTER_API_KEY=your_key_here" >> .env
```

**示例用法：**
```python
# 将自动使用 research lookup 查找近期论文
async for update in generate_paper(
    "Create a paper on recent advances in quantum computing (2024)"
):
    pass
```

## 错误处理

该 API 会优雅地处理错误：

1. 配置错误（缺少 API key）：返回一个 `status="failed"` 的结果
2. 生成错误：收集在结果的 `errors` 字段中
3. 部分失败：已创建 TeX 但 PDF 失败 -> `status="partial"`

## 最佳实践

1. 始终检查更新类型：
   ```python
   if update["type"] == "progress":
       # 处理进度
   else:  # type == "result"
       # 处理最终结果
   ```

2. 在访问文件之前检查状态：
   ```python
   if update["status"] == "success":
       pdf_path = update["files"]["pdf_final"]
   ```

3. 同时处理成功和失败：
   ```python
   if update["status"] == "failed":
       print(f"错误：{update['errors']}")
   elif update["status"] == "partial":
       print("TeX 已创建但 PDF 失败")
   else:
       print("成功！")
   ```

4. 正确使用 async 上下文：
   ```python
   import asyncio
   asyncio.run(main())  # 用于脚本
   ```

5. 保存重要结果：
   ```python
   import json
   with open("result.json", "w") as f:
       json.dump(update, f, indent=2)
   ```

## 高级功能

### 数据文件处理

API 会自动处理数据文件并进行适当组织：

```python
async for update in generate_paper(
    query="Analyze experimental results",
    data_files=[
        "./results.csv",           # → 复制到 data/
        "./performance_plot.png",  # → 复制到 figures/
        "./supplementary.json"     # → 复制到 data/
    ]
):
    if update["type"] == "result":
        # 文件可在论文目录中获取
        data_files = update["files"]["data"]
        figures = update["files"]["figures"]
```

**注意：** 使用 API 时，原始文件会被保留（不会删除）。在 CLI 模式下，它们会在复制后被删除。

### 智能论文检测（仅 CLI）

CLI 会自动检测对现有论文的引用：

```bash
# CLI 会自动跟踪上下文
> Create a Nature paper on CRISPR
# 创建新论文

> Add a methods section
# 继续编辑 CRISPR 论文

> Find the acoustics paper
# 切换到 acoustics 论文

> new paper on quantum computing
# 明确开始一篇新论文
```

此功能仅限 CLI，因为 API 是无状态的。每次调用 `generate_paper()` 都会创建一篇新论文。

### 自定义输出组织

控制论文保存位置：

```python
# 自定义输出目录
async for update in generate_paper(
    query="Create a paper",
    output_dir="~/my_research/papers"
):
    pass

# 自定义工作目录
async for update in generate_paper(
    query="Create a paper",
    cwd="/path/to/project",
    output_dir="./outputs"
):
    pass
```

### 模型选择

选择不同的 Claude 模型（不过推荐 Sonnet 4.5）：

```python
async for update in generate_paper(
    query="Create a paper",
    model="claude-sonnet-4-6"  # 最新 Opus 4.6
):
    pass
```

### Token 使用量跟踪

跟踪 token 消耗，用于成本监控和使用分析：

```python
async for update in generate_paper(
    query="Create a paper on quantum computing",
    track_token_usage=True
):
    if update["type"] == "result":
        if "token_usage" in update:
            usage = update["token_usage"]
            print(f"Token 使用摘要：")
            print(f"  输入 tokens:  {usage['input_tokens']:,}")
            print(f"  输出 tokens: {usage['output_tokens']:,}")
            print(f"  总 tokens: {usage['total_tokens']:,}")
            
            # 缓存统计（如适用）
            if usage.get('cache_read_input_tokens', 0) > 0:
                print(f"  缓存读取:   {usage['cache_read_input_tokens']:,}")
```

**说明：**
- token 使用量会静默返回（不会打印到终端）
- 在最终结果中以字典形式提供
- 启用跟踪时，也会包含在错误结果中
- 适用于成本估算和 API 使用监控

### 元数据提取

API 会自动从生成的论文中提取元数据：

```python
async for update in generate_paper(query):
    if update["type"] == "result":
        # 提取出的元数据
        title = update["metadata"]["title"]        # 来自 LaTeX 中的 \title{}
        word_count = update["metadata"]["word_count"]  # 从 TeX 估算
        created_at = update["metadata"]["created_at"]  # ISO 8601 时间戳
        topic = update["metadata"]["topic"]        # 来自目录名
        
        # 引用信息
        citation_count = update["citations"]["count"]  # 来自 .bib 文件
        citation_style = update["citations"]["style"]  # BibTeX style
        bib_file = update["citations"]["file"]     # .bib 路径
```

### 进度监控模式

#### 简单阶段显示

```python
def format_stage(stage: str) -> str:
    """使用图标格式化阶段名称。"""
    icons = {
        "initialization": "🔧",
        "research": "🔍", 
        "writing": "✍️",
        "compilation": "📦",
        "complete": "✅"
    }
    return f"{icons.get(stage, '⏳')} {stage}"

async for update in generate_paper(query):
    if update["type"] == "progress":
        print(f"\r{format_stage(update['stage'])}: {update['message']}", end="")

#### 基于阶段的更新

```python
stage_emojis = {
    "initialization": "🔧",
    "research": "🔍",
    "writing": "✍️",
    "compilation": "📦",
    "complete": "✅"
}

async for update in generate_paper(query):
    if update["type"] == "progress":
        emoji = stage_emojis.get(update["stage"], "⏳")
        print(f"{emoji} [{update['stage']}] {update['message']}")
```

#### 记录到文件

```python
import json
from datetime import datetime

log_file = "paper_generation.log"

async for update in generate_paper(query):
    # 记录所有更新
    with open(log_file, "a") as f:
        f.write(json.dumps(update) + "\n")
    
    if update["type"] == "progress":
        print(f"[{update['stage']}] {update['message']}")
```

### 多篇论文

按顺序或并行生成多篇论文：

```python
import asyncio

# 顺序生成
async def generate_multiple_sequential():
    papers = [
        "Create a paper on quantum computing",
        "Create a paper on machine learning",
        "Create a paper on climate change"
    ]
    
    results = []
    for query in papers:
        async for update in generate_paper(query):
            if update["type"] == "result":
                results.append(update)
    
    return results

# 并行生成（高级）
async def generate_multiple_parallel():
    async def generate_one(query):
        async for update in generate_paper(query):
            if update["type"] == "result":
                return update
    
    papers = [
        "Create a paper on quantum computing",
        "Create a paper on machine learning",
        "Create a paper on climate change"
    ]
    
    results = await asyncio.gather(*[generate_one(q) for q in papers])
    return results
```

## 另请参阅

- [README.md](../README.md) - 概览和快速开始
- [FEATURES.md](FEATURES.md) - 完整功能指南
- [TROUBLESHOOTING.md](TROUBLESHOOTING.md) - 故障排查
- [example_api_usage.py](../example_api_usage.py) - 完整代码示例
