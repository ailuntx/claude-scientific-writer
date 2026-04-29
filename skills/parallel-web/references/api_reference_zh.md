# 并行网络系统 API 快速参考

**完整文档：** https://docs.parallel.ai
**API 密钥：** https://platform.parallel.ai
**Python SDK：** `pip install parallel-web`
**环境变量：** `PARALLEL_API_KEY`

---

## 搜索 API（Beta）

**端点：** `POST https://api.parallel.ai/v1beta/search`
**请求头：** `parallel-beta: search-extract-2025-10-10`

### 请求

```json
{
  "objective": "自然语言搜索目标（最多 5000 字符）",
  "search_queries": ["关键词查询 1", "关键词查询 2"],
  "max_results": 10,
  "excerpts": {
    "max_chars_per_result": 10000,
    "max_chars_total": 50000
  },
  "source_policy": {
    "allow_domains": ["example.com"],
    "deny_domains": ["spam.com"],
    "after_date": "2024-01-01"
  }
}
```

### 响应

```json
{
  "search_id": "search_...",
  "results": [
    {
      "url": "https://...",
      "title": "页面标题",
      "publish_date": "2025-01-15",
      "excerpts": ["相关内容..."]
    }
  ]
}
```

### Python SDK

```python
from parallel import Parallel
client = Parallel(api_key="...")
result = client.beta.search(
    objective="...",
    search_queries=["..."],
    max_results=10,
    excerpts={"max_chars_per_result": 10000},
)
```

**费用：** 每 1000 次请求 $5（默认每次 10 个结果）
**速率限制：** 600 请求/分钟

---

## 提取 API（Beta）

**端点：** `POST https://api.parallel.ai/v1beta/extract`
**请求头：** `parallel-beta: search-extract-2025-10-10`

### 请求

```json
{
  "urls": ["https://example.com/page"],
  "objective": "需要关注的内容",
  "excerpts": true,
  "full_content": false
}
```

### 响应

```json
{
  "extract_id": "extract_...",
  "results": [
    {
      "url": "https://...",
      "title": "页面标题",
      "excerpts": ["聚焦内容..."],
      "full_content": null
    }
  ],
  "errors": []
}
```

### Python SDK

```python
result = client.beta.extract(
    urls=["https://..."],
    objective="...",
    excerpts=True,
    full_content=False,
)
```

**费用：** 每 1000 个 URL $1
**速率限制：** 600 请求/分钟

---

## 任务 API（深度研究）

**端点：** `POST https://api.parallel.ai/v1/tasks/runs`

### 创建任务运行

```json
{
  "input": "研究问题（最多 15,000 字符）",
  "processor": "pro-fast",
  "task_spec": {
    "output_schema": {
      "type": "text"
    }
  }
}
```

### 响应（即时）

```json
{
  "run_id": "trun_...",
  "status": "queued"
}
```

### 获取结果（阻塞式）

**端点：** `GET https://api.parallel.ai/v1/tasks/runs/{run_id}/result`

### Python SDK

```python
# 文本输出（带引用标记的 markdown 报告）
from parallel.types import TaskSpecParam
task_run = client.task_run.create(
    input="Research question",
    processor="pro-fast",
    task_spec=TaskSpecParam(output_schema={"type": "text"}),
)
result = client.task_run.result(task_run.run_id, api_timeout=3600)
print(result.output.content)

# 自动模式输出（结构化 JSON）
task_run = client.task_run.create(
    input="Research question",
    processor="pro-fast",
)
result = client.task_run.result(task_run.run_id, api_timeout=3600)
print(result.output.content)  # 结构化字典
print(result.output.basis)    # 每个字段的引用
```

### 处理器

| 处理器 | 延迟 | 费用/1000 | 适用场景 |
|--------|------|-----------|----------|
| `lite-fast` | 10-20秒 | $5 | 基本元数据 |
| `base-fast` | 15-50秒 | $10 | 标准增强 |
| `core-fast` | 15秒-100秒 | $25 | 交叉引用 |
| `core2x-fast` | 15秒-3分钟 | $50 | 高复杂度 |
| **`pro-fast`** | **30秒-5分钟** | **$100** | **默认：探索性研究** |
| `ultra-fast` | 1-10分钟 | $300 | 深度多源 |
| `ultra2x-fast` | 1-20分钟 | $600 | 困难研究 |
| `ultra4x-fast` | 1-40分钟 | $1200 | 非常困难 |
| `ultra8x-fast` | 1小时 | $2400 | 最困难 |

标准（非 fast）处理器费用相同，但延迟更高，数据最新。

---

## 聊天 API（Beta）

**端点：** `POST https://api.parallel.ai/chat/completions`
**兼容 OpenAI SDK。**

### 模型

| 模型 | 延迟 (TTFT) | 费用/1000 | 使用场景 |
|------|-------------|-----------|----------|
| `speed` | ~3秒 | $5 | 低延迟聊天 |
| `lite` | 10-60秒 | $5 | 带引用的简单查询 |
| `base` | 15-100秒 | $10 | 带引用的标准研究 |
| `core` | 1-5分钟 | $25 | 带引用的复杂研究 |

### Python SDK（OpenAI 兼容）

```python
from openai import OpenAI
client = OpenAI(
    api_key="PARALLEL_API_KEY",
    base_url="https://api.parallel.ai",
)
response = client.chat.completions.create(
    model="speed",
    messages=[{"role": "user", "content": "What is Parallel Web Systems?"}],
)
```

---

## 速率限制

| API | 默认限制 |
|-----|----------|
| 搜索 | 600 请求/分钟 |
| 提取 | 600 请求/分钟 |
| 聊天 | 300 请求/分钟 |
| 任务 | 因处理器而异 |

---

## 源策略

控制搜索中使用的来源：

```json
{
  "source_policy": {
    "allow_domains": ["nature.com", "science.org"],
    "deny_domains": ["unreliable-source.com"],
    "after_date": "2024-01-01"
  }
}
```

可与搜索 API 配合使用，将结果聚焦在特定的权威域上。
