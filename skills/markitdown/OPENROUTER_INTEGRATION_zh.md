# MarkItDown 的 OpenRouter 集成

## 概述

此 MarkItDown 技能已配置为使用 **OpenRouter** 而非直接访问 OpenAI API。OpenRouter 提供统一的 API 网关，通过单一、OpenAI 兼容的接口访问来自不同提供商的 100+ 个 AI 模型。

## 为什么选择 OpenRouter？

### 优势

1. **多模型访问**：通过一个 API 访问 GPT-4、Claude、Gemini 和 100+ 其他模型
2. **无供应商锁定**：无需代码更改即可在模型之间切换
3. **有竞争力的定价**：通常比直接访问更优惠
4. **简单迁移**：OpenAI 兼容的 API 意味着最少的代码更改
5. **灵活选择**：为每个任务选择最佳模型

### 图像描述热门模型

| 模型 | 提供商 | 使用场景 | 视觉支持 |
|-------|----------|----------|----------------|
| `anthropic/claude-sonnet-4.5` | Anthropic | **推荐** - 科学分析最佳整体表现 | ✅ |
| `anthropic/claude-opus-4.5` | Anthropic | 优秀的技术分析 | ✅ |
| `openai/gpt-4o` | OpenAI | 强大的视觉理解能力 | ✅ |
| `openai/gpt-4-vision` | OpenAI | 带视觉的 GPT-4 | ✅ |
| `google/gemini-pro-vision` | Google | 成本效益选项 | ✅ |

完整列表请参阅 https://openrouter.ai/models。

## 开始使用

### 1. 获取 API 密钥

1. 访问 https://openrouter.ai/keys
2. 注册或登录
3. 创建新的 API 密钥
4. 复制密钥（以 `sk-or-v1-...` 开头）

### 2. 设置环境变量

```bash
# 添加到您的环境
export OPENROUTER_API_KEY="sk-or-v1-..."

# 使其永久化
echo 'export OPENROUTER_API_KEY="sk-or-v1-..."' >> ~/.zshrc  # macOS
echo 'export OPENROUTER_API_KEY="sk-or-v1-..."' >> ~/.bashrc # Linux

# 重新加载 shell
source ~/.zshrc  # 或 source ~/.bashrc
```

### 3. 在 Python 中使用

```python
from markitdown import MarkItDown
from openai import OpenAI

# 初始化 OpenRouter 客户端（OpenAI 兼容）
client = OpenAI(
    api_key="your-openrouter-api-key",  # 或使用环境变量
    base_url="https://openrouter.ai/api/v1"
)

# 创建带 AI 支持的 MarkItDown
md = MarkItDown(
    llm_client=client,
    llm_model="anthropic/claude-sonnet-4.5"  # 选择您的模型
)

# 使用 AI 增强描述进行转换
result = md.convert("presentation.pptx")
print(result.text_content)
```

## 使用脚本

所有技能脚本已更新为使用 OpenRouter：

### convert_with_ai.py

```bash
# 设置 API 密钥
export OPENROUTER_API_KEY="sk-or-v1-..."

# 使用默认模型（高级视觉模型）转换
python scripts/convert_with_ai.py paper.pdf output.md --prompt-type scientific

# 使用 GPT-4o 作为替代
python scripts/convert_with_ai.py paper.pdf output.md \
  --model openai/gpt-4o \
  --prompt-type scientific

# 使用 Gemini Pro Vision（成本效益）
python scripts/convert_with_ai.py slides.pptx output.md \
  --model google/gemini-pro-vision \
  --prompt-type presentation

# 列出可用的提示类型
python scripts/convert_with_ai.py --list-prompts
```

### 选择合适的模型

```bash
# 对于科学论文 - 使用高级视觉模型进行技术分析
python scripts/convert_with_ai.py research.pdf output.md \
  --model anthropic/claude-sonnet-4.5 \
  --prompt-type scientific

# 对于演示文稿 - 使用高级视觉模型
python scripts/convert_with_ai.py slides.pptx output.md \
  --model anthropic/claude-sonnet-4.5 \
  --prompt-type presentation

# 对于数据可视化 - 使用高级视觉模型
python scripts/convert_with_ai.py charts.pdf output.md \
  --model anthropic/claude-sonnet-4.5 \
  --prompt-type data_viz

# 对于医学图像 - 使用高级视觉模型进行详细分析
python scripts/convert_with_ai.py xray.jpg output.md \
  --model anthropic/claude-sonnet-4.5 \
  --prompt-type medical
```

## 代码示例

### 基本用法

```python
from markitdown import MarkItDown
from openai import OpenAI
import os

# 初始化 OpenRouter 客户端
client = OpenAI(
    api_key=os.environ.get("OPENROUTER_API_KEY"),
    base_url="https://openrouter.ai/api/v1"
)

# 使用高级视觉模型进行图像描述
md = MarkItDown(
    llm_client=client,
    llm_model="anthropic/claude-sonnet-4.5"
)

result = md.convert("document.pptx")
print(result.text_content)
```

### 动态切换模型

```python
from markitdown import MarkItDown
from openai import OpenAI
import os

client = OpenAI(
    api_key=os.environ["OPENROUTER_API_KEY"],
    base_url="https://openrouter.ai/api/v1"
)

# 为不同文件类型使用不同的模型
def convert_with_best_model(filepath):
    if filepath.endswith('.pdf'):
        # 对技术 PDF 使用高级视觉模型
        md = MarkItDown(
            llm_client=client,
            llm_model="anthropic/claude-sonnet-4.5",
            llm_prompt="以技术精度描述科学图表"
        )
    elif filepath.endswith('.pptx'):
        # 对演示文稿使用高级视觉模型
        md = MarkItDown(
            llm_client=client,
            llm_model="anthropic/claude-sonnet-4.5",
            llm_prompt="描述幻灯片内容和视觉元素"
        )
    else:
        # 默认使用高级视觉模型
        md = MarkItDown(
            llm_client=client,
            llm_model="anthropic/claude-sonnet-4.5"
        )
    
    return md.convert(filepath)

# 使用它
result = convert_with_best_model("paper.pdf")
```

### 每个模型的自定义提示

```python
from markitdown import MarkItDown
from openai import OpenAI

client = OpenAI(
    api_key="your-openrouter-api-key",
    base_url="https://openrouter.ai/api/v1"
)

# 使用高级视觉模型进行科学分析
scientific_prompt = """
分析此科学图表。提供：
1. 可视化类型和方法论
2. 定量数据点和趋势
3. 统计显著性
4. 技术解释
精确并使用科学术语。
"""

md_scientific = MarkItDown(
    llm_client=client,
    llm_model="anthropic/claude-sonnet-4.5",
    llm_prompt=scientific_prompt
)

# 使用高级视觉模型进行视觉分析
visual_prompt = """
全面描述此图像：
1. 主要视觉元素和构图
2. 颜色、布局和设计
3. 文字和标签
4. 整体信息
"""

md_visual = MarkItDown(
    llm_client=client,
    llm_model="anthropic/claude-sonnet-4.5",
    llm_prompt=visual_prompt
)
```

## 模型比较

### 对于科学内容

**推荐：anthropic/claude-sonnet-4.5**
- 擅长技术分析
- 卓越的推理能力
- 最擅长理解科学图表
- 最详细和准确的解释
- 先进的视觉能力

**替代方案：openai/gpt-4o**
- 良好的视觉理解
- 处理速度快
- 擅长图表和图形

### 对于演示文稿

**推荐：anthropic/claude-sonnet-4.5**
- 卓越的视觉能力
- 擅长理解幻灯片布局
- 快速可靠
- 最佳技术理解能力

### 对于成本效益

**推荐：google/gemini-pro-vision**
- 每次请求成本较低
- 质量良好
- 处理速度快

## 定价注意事项

OpenRouter 定价因模型而异。在 https://openrouter.ai/models 查看当前费率

**成本优化技巧：**
1. 在复杂科学内容上使用高级视觉模型以获得最佳质量
2. 对简单图像使用更便宜的模型（Gemini）
3. 使用相同模型批量处理相似内容
4. 使用适当的提示以在更少重试中获得更好的结果

## 故障排除

### API 密钥问题

```bash
# 检查是否设置了密钥
echo $OPENROUTER_API_KEY

# 应显示：sk-or-v1-...
# 如果为空，设置它：
export OPENROUTER_API_KEY="sk-or-v1-..."
```

### 找不到模型

如果遇到"找不到模型"错误，请检查：
1. 模型名称格式：`provider/model-name`
2. 模型可用性：https://openrouter.ai/models
3. 视觉支持：确保模型支持图像描述的视觉能力

### 速率限制

OpenRouter 有速率限制。如果遇到限制：
1. 在请求之间添加延迟
2. 使用带 `--workers` 参数的批处理脚本
3. 考虑升级您的 OpenRouter 计划

## 迁移说明

此技能已从直接 OpenAI API 更新为 OpenRouter。主要更改：

1. **环境变量**：`OPENAI_API_KEY` → `OPENROUTER_API_KEY`
2. **客户端初始化**：添加 `base_url="https://openrouter.ai/api/v1"`
3. **模型名称**：`gpt-4o` → `openai/gpt-4o`（带提供商前缀）
4. **脚本更新**：所有脚本现在默认使用 OpenRouter

## 资源

- **OpenRouter 网站**：https://openrouter.ai
- **获取 API 密钥**：https://openrouter.ai/keys
- **模型列表**：https://openrouter.ai/models
- **定价**：https://openrouter.ai/models（点击模型查看详情）
- **文档**：https://openrouter.ai/docs
- **支持**：https://openrouter.ai/discord

## 示例工作流程

以下是使用 OpenRouter 的完整工作流程：

```bash
# 1. 设置 API 密钥
export OPENROUTER_API_KEY="sk-or-v1-your-key-here"

# 2. 使用 Claude 转换科学论文
python scripts/convert_with_ai.py \
  research_paper.pdf \
  output.md \
  --model anthropic/claude-opus-4.5 \
  --prompt-type scientific

# 3. 使用 GPT-4o 转换演示文稿
python scripts/convert_with_ai.py \
  talk_slides.pptx \
  slides.md \
  --model openai/gpt-4o \
  --prompt-type presentation

# 4. 使用成本效益模型批量转换
python scripts/batch_convert.py \
  images/ \
  markdown_output/ \
  --extensions .jpg .png
```

## 支持

对于 OpenRouter 特定问题：
- Discord：https://openrouter.ai/discord
- 邮箱：support@openrouter.ai

对于 MarkItDown 技能问题：
- 查看此技能目录中的文档
- 查看 `assets/example_usage.md` 中的示例
