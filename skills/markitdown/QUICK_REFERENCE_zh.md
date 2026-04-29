# MarkItDown 快速参考

## 安装

```bash
# 所有功能
pip install 'markitdown[all]'

# 特定格式
pip install 'markitdown[pdf,docx,pptx,xlsx]'
```

## 基础用法

```python
from markitdown import MarkItDown

md = MarkItDown()
result = md.convert("file.pdf")
print(result.text_content)
```

## 命令行

```bash
# 简单转换
markitdown input.pdf > output.md
markitdown input.pdf -o output.md

# 使用插件
markitdown --use-plugins file.pdf -o output.md
```

## 常见任务

### 转换 PDF
```python
md = MarkItDown()
result = md.convert("paper.pdf")
```

### 使用 AI 转换
```python
from openai import OpenAI

# 使用 OpenRouter 获取多种模型
client = OpenAI(
    api_key="your-openrouter-api-key",
    base_url="https://openrouter.ai/api/v1"
)

md = MarkItDown(
    llm_client=client,
    llm_model="anthropic/claude-sonnet-4.5"  # 推荐用于视觉识别
)
result = md.convert("slides.pptx")
```

### 批量转换
```bash
python scripts/batch_convert.py input/ output/ --extensions .pdf .docx
```

### 文献转换
```bash
python scripts/convert_literature.py papers/ markdown/ --create-index
```

## 支持的格式

| 格式 | 扩展名 | 备注 |
|--------|-----------|-------|
| PDF | `.pdf` | 全文 + OCR |
| Word | `.docx` | 表格、格式 |
| PowerPoint | `.pptx` | 幻灯片 + 备注 |
| Excel | `.xlsx`, `.xls` | 表格 |
| 图片 | `.jpg`, `.png`, `.gif`, `.webp` | EXIF + OCR |
| 音频 | `.wav`, `.mp3` | 转录 |
| HTML | `.html`, `.htm` | 清洁转换 |
| 数据 | `.csv`, `.json`, `.xml` | 结构化 |
| 压缩包 | `.zip` | 遍历内容 |
| 电子书 | `.epub` | 全文 |
| YouTube | URL | 字幕 |

## 可选依赖

```bash
[all]                  # 所有功能
[pdf]                  # PDF 支持
[docx]                 # Word 文档
[pptx]                 # PowerPoint
[xlsx]                 # Excel
[xls]                  # 旧版 Excel
[outlook]              # Outlook 邮件
[az-doc-intel]         # Azure 文档智能
[audio-transcription]  # 音频文件
[youtube-transcription] # YouTube 视频
```

## AI 增强转换

### 科学论文
```python
from openai import OpenAI

# 初始化 OpenRouter 客户端
client = OpenAI(
    api_key="your-openrouter-api-key",
    base_url="https://openrouter.ai/api/v1"
)

md = MarkItDown(
    llm_client=client,
    llm_model="anthropic/claude-sonnet-4.5",  # 推荐用于科学视觉识别
    llm_prompt="用技术精确性描述科学图表"
)
result = md.convert("paper.pdf")
```

### 自定义提示词
```python
prompt = """
分析此数据可视化。描述：
- 图表/图形类型
- 主要趋势和模式
- 值得注意的数据点
"""

md = MarkItDown(
    llm_client=client,
    llm_model="anthropic/claude-sonnet-4.5",
    llm_prompt=prompt
)
```

### 通过 OpenRouter 可用的模型
- `anthropic/claude-sonnet-4.5` - **推荐用于科学视觉识别**
- `anthropic/claude-opus-4.5` - 高级视觉模型
- `openai/gpt-4o` - GPT-4 Omni（视觉）
- `openai/gpt-4-vision` - GPT-4 Vision
- `google/gemini-pro-vision` - Gemini Pro Vision

完整列表请访问 https://openrouter.ai/models

## Azure 文档智能

```python
md = MarkItDown(docintel_endpoint="https://YOUR-ENDPOINT.cognitiveservices.azure.com/")
result = md.convert("complex_layout.pdf")
```

## 批量处理

### Python
```python
from markitdown import MarkItDown
from pathlib import Path

md = MarkItDown()

for file in Path("input/").glob("*.pdf"):
    result = md.convert(str(file))
    output = Path("output") / f"{file.stem}.md"
    output.write_text(result.text_content)
```

### 脚本
```bash
# 并行转换
python scripts/batch_convert.py input/ output/ --workers 8

# 递归
python scripts/batch_convert.py input/ output/ -r
```

## 错误处理

```python
try:
    result = md.convert("file.pdf")
except FileNotFoundError:
    print("File not found")
except Exception as e:
    print(f"Error: {e}")
```

## 流式处理

```python
with open("large_file.pdf", "rb") as f:
    result = md.convert_stream(f, file_extension=".pdf")
```

## 常用提示词

### 科学
```
分析此科学图表。描述：
- 可视化类型
- 主要数据点和趋势
- 轴、标签和图例
- 科学意义
```

### 医学
```
描述此医学图像。包括：
- 成像类型（X 光、MRI、CT 等）
- 可见的解剖结构
- 值得注意的发现
- 临床相关性
```

### 数据可视化
```
分析此数据可视化：
- 图表类型
- 变量和轴
- 数据范围
- 主要模式和异常值
```

## 性能提示

1. **复用实例**：创建一次，多次使用
2. **并行处理**：对多个文件使用 ThreadPoolExecutor
3. **流式处理大文件**：对大文件使用 `convert_stream()`
4. **选择合适格式**：仅安装需要的依赖

## 环境变量

```bash
# OpenRouter 用于 AI 增强转换
export OPENROUTER_API_KEY="sk-or-v1-..."

# Azure 文档智能（可选）
export AZURE_DOCUMENT_INTELLIGENCE_KEY="key..."
export AZURE_DOCUMENT_INTELLIGENCE_ENDPOINT="https://..."
```

## 脚本快速参考

### batch_convert.py
```bash
python scripts/batch_convert.py INPUT OUTPUT [OPTIONS]

Options:
  --extensions .pdf .docx    要转换的文件类型
  --recursive, -r            搜索子目录
  --workers 4                并行工作线程
  --verbose, -v              详细输出
  --plugins, -p              启用插件
```

### convert_with_ai.py
```bash
python scripts/convert_with_ai.py INPUT OUTPUT [OPTIONS]

Options:
  --api-key KEY              OpenRouter API 密钥
  --model MODEL              模型名称（默认：anthropic/claude-sonnet-4.5）
  --prompt-type TYPE         预设提示词（scientific、medical 等）
  --custom-prompt TEXT       自定义提示词
  --list-prompts             显示可用的提示词
```

### convert_literature.py
```bash
python scripts/convert_literature.py INPUT OUTPUT [OPTIONS]

Options:
  --organize-by-year, -y     按年份整理
  --create-index, -i         创建索引文件
  --recursive, -r            搜索子目录
```

## 故障排除

### 缺少依赖
```bash
pip install 'markitdown[pdf]'  # 安装 PDF 支持
```

### 二进制文件错误
```python
# 错误
with open("file.pdf", "r") as f:

# 正确
with open("file.pdf", "rb") as f:  # 二进制模式
```

### OCR 不工作
```bash
# macOS
brew install tesseract

# Ubuntu
sudo apt-get install tesseract-ocr
```

## 更多信息

- **完整文档**：请参阅 `SKILL.md`
- **API 参考**：请参阅 `references/api_reference.md`
- **格式详情**：请参阅 `references/file_formats.md`
- **示例**：请参阅 `assets/example_usage.md`
- **GitHub**：https://github.com/microsoft/markitdown
