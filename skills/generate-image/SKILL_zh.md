---
name: generate-image
description: 使用AI模型（FLUX、Gemini）生成或编辑图片。用于通用图片生成，包括照片、插画、艺术作品、视觉资产、概念艺术，以及任何非技术图表或原理图的内容。对于流程图、电路、路径和技术图表，请使用scientific-schematics技能。
---

# 生成图片

使用OpenRouter的图片生成模型（包括FLUX.2 Pro和Gemini 3 Pro）生成和编辑高质量图片。

## 何时使用此技能

**使用generate-image的场景：**
- 照片和逼真的图像
- 艺术插画和艺术作品
- 概念艺术和视觉概念
- 演示文稿或文档的视觉资产
- 图片编辑和修改
- 任何通用图片生成需求

**改用scientific-schematics的场景：**
- 流程图和流程图
- 电路图和电气原理图
- 生物途径和信号级联
- 系统架构图
- CONSORT流程图和方法论流程图
- 任何技术/原理图

## 快速开始

使用`scripts/generate_image.py`脚本生成或编辑图片：

```bash
# 生成新图片
python scripts/generate_image.py "A beautiful sunset over mountains"

# 编辑现有图片
python scripts/generate_image.py "Make the sky purple" --input photo.jpg
```

此脚本会生成/编辑图片并将其保存为当前目录下的`generated_image.png`。

## API密钥设置

**重要**：脚本需要OpenRouter API密钥。运行前，请检查用户是否已配置API密钥：

1. 在项目目录或父目录中查找`.env`文件
2. 检查`.env`文件中是否有`OPENROUTER_API_KEY=<key>`
3. 如果未找到，请告知用户需要：
   - 创建包含`OPENROUTER_API_KEY=your-api-key-here`的`.env`文件
   - 或设置环境变量：`export OPENROUTER_API_KEY=your-api-key-here`
   - 从以下地址获取API密钥：https://openrouter.ai/keys

脚本将自动检测`.env`文件，并在API密钥缺失时提供清晰的错误消息。

## 模型选择

**默认模型**：`google/gemini-3-pro-image-preview`（高质量，推荐）

**可用于生成和编辑的模型**：
- `google/gemini-3-pro-image-preview` - 高质量，支持生成+编辑
- `black-forest-labs/flux.2-pro` - 快速，高质量，支持生成+编辑

**仅生成**：
- `black-forest-labs/flux.2-flex` - 快速且便宜，但质量不如pro版

根据以下因素选择：
- **质量**：使用gemini-3-pro或flux.2-pro
- **编辑**：使用gemini-3-pro或flux.2-pro（两者都支持图片编辑）
- **成本**：仅生成时使用flux.2-flex

## 常见用法

### 基础生成
```bash
python scripts/generate_image.py "Your prompt here"
```

### 指定模型
```bash
python scripts/generate_image.py "A cat in space" --model "black-forest-labs/flux.2-pro"
```

### 自定义输出路径
```bash
python scripts/generate_image.py "Abstract art" --output artwork.png
```

### 编辑现有图片
```bash
python scripts/generate_image.py "Make the background blue" --input photo.jpg
```

### 使用特定模型编辑
```bash
python scripts/generate_image.py "Add sunglasses to the person" --input portrait.png --model "black-forest-labs/flux.2-pro"
```

### 自定义输出编辑
```bash
python scripts/generate_image.py "Remove the text from the image" --input screenshot.png --output cleaned.png
```

### 多张图片
使用不同的提示词或输出路径多次运行脚本：
```bash
python scripts/generate_image.py "Image 1 description" --output image1.png
python scripts/generate_image.py "Image 2 description" --output image2.png
```

## 脚本参数

- `prompt`（必需）：要生成的图片的文本描述，或编辑指令
- `--input`或`-i`：用于编辑的输入图片路径（启用编辑模式）
- `--model`或`-m`：OpenRouter模型ID（默认：google/gemini-3-pro-image-preview）
- `--output`或`-o`：输出文件路径（默认：generated_image.png）
- `--api-key`：OpenRouter API密钥（覆盖.env文件）

## 示例用例

### 用于科学文档
```bash
# 为论文生成概念性插图
python scripts/generate_image.py "Microscopic view of cancer cells being attacked by immunotherapy agents, scientific illustration style" --output figures/immunotherapy_concept.png

# 为演示文稿创建视觉元素
python scripts/generate_image.py "DNA double helix structure with highlighted mutation site, modern scientific visualization" --output slides/dna_mutation.png
```

### 用于演示文稿和海报
```bash
# 标题幻灯片背景
python scripts/generate_image.py "Abstract blue and white background with subtle molecular patterns, professional presentation style" --output slides/background.png

# 海报主图
python scripts/generate_image.py "Laboratory setting with modern equipment, photorealistic, well-lit" --output poster/hero.png
```

### 用于通用视觉内容
```bash
# 网站或文档图片
python scripts/generate_image.py "Professional team collaboration around a digital whiteboard, modern office" --output docs/team_collaboration.png

# 营销材料
python scripts/generate_image.py "Futuristic AI brain concept with glowing neural networks" --output marketing/ai_concept.png
```

## 错误处理

脚本为以下情况提供清晰的错误消息：
- API密钥缺失（包含设置说明）
- API错误（包含状态码）
- 意外的响应格式
- 依赖缺失（requests库）

如果脚本失败，请阅读错误消息并在重试前解决问题。

## 关键提示词要求

**重要：输出中不含元指令**

为AI图片生成模型生成提示词时，确保生成的图片不包含任何可见的文本显示：
- 用于生成图片的提示词或指令
- 系统指令或AI相关元数据
- 描述图片创建方式的任何"元"文本
- 指示AI生成的 watermark 或标签
- 布局描述（例如"左侧面板"、"右侧面板"、"中间面板"）
- 字体规格或排版指令
- 配色方案或调色板信息

图片应仅包含请求的视觉内容。在提示词中始终包含此指令："Do not include any text showing the prompt, instructions, layout descriptions, font/color specifications, or metadata in the generated image."

## 说明

- 图片以base64编码的数据URL形式返回，并自动保存为PNG文件
- 脚本支持不同OpenRouter模型的`images`和`content`响应格式
- 生成时间因模型而异（通常5-30秒）
- 对于图片编辑，输入图片被编码为base64并发送到模型
- 支持的输入图片格式：PNG、JPEG、GIF、WebP
- 有关定价信息请查看OpenRouter：https://openrouter.ai/models

## 图片编辑技巧

- 具体说明想要更改的内容（例如"把天空改成日落颜色"vs"编辑天空"）
- 尽可能引用图片中的具体元素
- 为获得最佳效果，请使用清晰详细的编辑指令
- Gemini 3 Pro和FLUX.2 Pro都支持通过OpenRouter进行图片编辑

## 与其他技能的集成

- **scientific-schematics**：用于技术图表、流程图、电路、路径
- **generate-image**：用于照片、插画、艺术作品、视觉概念
- **scientific-slides**：与generate-image结合使用，创建视觉丰富的演示文稿
- **latex-posters**：使用generate-image制作海报视觉元素和主图
