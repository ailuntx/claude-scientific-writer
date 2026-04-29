# MarkItDown 技能

此技能提供全面支持，使用微软的 MarkItDown 工具将各种文件格式转换为 Markdown。

## 概述

MarkItDown 是一个 Python 工具，用于将文件和办公文档转换为 Markdown 格式。此技能包括：

- 完整的 API 文档
- 特定格式的转换指南
- 用于批量处理的实用脚本
- AI 增强的转换示例
- 与科学工作流程的集成

## 内容

### 主技能文件
- **SKILL.md** - 使用 MarkItDown 的完整指南，包含快速入门、示例和最佳实践

### 参考文档
- **api_reference.md** - 详细的 API 文档、类引用和方法签名
- **file_formats.md** - 所有支持文件类型的格式详情

### 脚本
- **batch_convert.py** - 批量转换多个文件，支持并行处理
- **convert_with_ai.py** - 使用自定义提示词进行 AI 增强转换
- **convert_literature.py** - 科学文献转换，提取元数据

### 资源文件
- **example_usage.md** - 常见用例的实用示例

## 安装

```bash
# 安装所有功能
pip install 'markitdown[all]'

# 或安装特定功能
pip install 'markitdown[pdf,docx,pptx,xlsx]'
```

## 快速入门

```python
from markitdown import MarkItDown

md = MarkItDown()
result = md.convert("document.pdf")
print(result.text_content)
```

## 支持的格式

- **文档**: PDF, DOCX, PPTX, XLSX, EPUB
- **图片**: JPEG, PNG, GIF, WebP（含 OCR）
- **音频**: WAV, MP3（含转录）
- **网页**: HTML, YouTube 链接
- **数据**: CSV, JSON, XML
- **归档**: ZIP 文件

## 主要功能

### 1. AI 增强的转换
通过 OpenRouter 使用 AI 模型生成详细的图片描述：

```python
from openai import OpenAI

# OpenRouter 提供对 100 多种 AI 模型的访问
client = OpenAI(
    api_key="your-openrouter-api-key",
    base_url="https://openrouter.ai/api/v1"
)

md = MarkItDown(
    llm_client=client,
    llm_model="anthropic/claude-sonnet-4.5"  # 推荐用于视觉
)
result = md.convert("presentation.pptx")
```

### 2. 批量处理
高效转换多个文件：

```bash
python scripts/batch_convert.py papers/ output/ --extensions .pdf .docx
```

### 3. 科学文献
转换和组织研究论文：

```bash
python scripts/convert_literature.py papers/ output/ --organize-by-year --create-index
```

### 4. Azure 文档智能
使用 Microsoft 文档智能增强 PDF 转换：

```python
md = MarkItDown(docintel_endpoint="https://YOUR-ENDPOINT.cognitiveservices.azure.com/")
result = md.convert("complex_document.pdf")
```

## 用例

### 文献综述
将研究论文转换为 Markdown，方便分析和笔记。

### 数据提取
将 Excel 文件中的表格提取为 Markdown 格式。

### 演示文稿处理
转换 PowerPoint 幻灯片，添加 AI 生成的描述。

### 文档分析
处理文档以供 LLM 使用，采用适合 token 的 Markdown 格式。

### YouTube 字幕
获取并转换 YouTube 视频字幕。

## 脚本用法

### 批量转换
```bash
# 转换目录中的所有 PDF
python scripts/batch_convert.py input_dir/ output_dir/ --extensions .pdf

# 递归转换多种格式
python scripts/batch_convert.py docs/ markdown/ --extensions .pdf .docx .pptx -r
```

### AI 增强转换
```bash
# 通过 OpenRouter 使用 AI 描述进行转换
export OPENROUTER_API_KEY="sk-or-v1-..."
python scripts/convert_with_ai.py paper.pdf output.md --prompt-type scientific

# 使用不同模型
python scripts/convert_with_ai.py image.png output.md --model anthropic/claude-sonnet-4.5

# 使用自定义提示词
python scripts/convert_with_ai.py image.png output.md --custom-prompt "Describe this diagram"
```

### 文献转换
```bash
# 转换论文并提取元数据
python scripts/convert_literature.py papers/ markdown/ --organize-by-year --create-index
```

## 与科学写作工具的集成

此技能与 Scientific Writer CLI 无缝集成，用于：
- 转换论文写作的源材料
- 处理综述文献
- 从各种文档格式提取数据
- 准备供 LLM 分析的文档

## 资源

- **MarkItDown GitHub**: https://github.com/microsoft/markitdown
- **PyPI**: https://pypi.org/project/markitdown/
- **OpenRouter**: https://openrouter.ai（AI 模型访问）
- **OpenRouter API 密钥**: https://openrouter.ai/keys
- **OpenRouter 模型**: https://openrouter.ai/models
- **许可证**: MIT

## 要求

- Python 3.10+
- 根据需要的格式选择可选依赖
- OpenRouter API 密钥（用于 AI 增强转换）- 在 https://openrouter.ai/keys 获取
- Azure 订阅（可选，用于文档智能）

## 示例

请参阅 `assets/example_usage.md` 获取全面示例，包含：
- 基本转换
- 科学工作流程
- AI 增强处理
- 批量操作
- 错误处理
- 集成模式
