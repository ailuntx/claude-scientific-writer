---
name: paper-2-web
description: 此技能用于将学术论文转换为宣传和演示格式，包括互动网站（Paper2Web）、演示视频（Paper2Video）和会议海报（Paper2Poster）。将此技能用于论文传播、会议准备、创建可探索的学术主页、生成视频摘要，或从LaTeX或PDF来源制作打印就绪的海报。
allowed-tools: [Read, Write, Edit, Bash]
---

# Paper2All：学术论文转换管道

## 概述

此技能使用Paper2All自主管道将学术论文转换为多种宣传和演示格式。该系统将研究论文（LaTeX或PDF）转换为三种主要输出：

1. **Paper2Web**：具有布局感知的互动学术主页
2. **Paper2Video**：专业的演示视频，包含旁白、幻灯片和可选的 Talking-head
3. **Paper2Poster**：具有专业布局的打印就绪会议海报

该管道利用LLM驱动的内容提取、设计生成和迭代 refinement 来创建适合会议、期刊、预印本仓库和学术推广的高质量输出。

##何时使用此技能

在以下情况下使用此技能：

- **创建会议材料**：学术会议的海报、演示视频和配套网站
- **推广研究**：将已发表的论文或预印本转换为易于访问、引人入胜的网页格式
- **准备演示**：从论文内容生成视频摘要或完整演示视频
- **传播研究发现**：为社交媒体、实验室网站或机构展示创建宣传材料
- **增强预印本**：为bioRxiv、arXiv或其他预印本提交添加互动主页
- **批量处理**：同时为多篇论文生成宣传材料

**触发短语**：
- "将这篇论文转换为网站"
- "从我的LaTeX论文生成会议海报"
- "从这项研究创建演示视频"
- "为我的论文创建互动主页"
- "将我的论文转换为宣传材料"
- "为我的会议演讲生成海报和视频"

## 使用科学图表进行视觉增强

**使用此技能创建文档时，请始终考虑添加科学图表和示意图以增强视觉传达。**

如果您的文档尚未包含示意图或图表：
- 使用 **scientific-schematics** 技能生成AI驱动的出版质量图表
- 只需用自然语言描述您想要的图表
- Nano Banana Pro 将自动生成、审查和优化示意图

**对于新文档：** 默认情况下应生成科学示意图，以直观地表示文本中描述的关键概念、工作流程、架构或关系。

**如何生成示意图：**
```bash
python scripts/generate_schematic.py "your diagram description" -o figures/output.png
```

AI将自动：
- 创建具有正确格式的出版质量图像
- 通过多次迭代进行审查和优化
- 确保可访问性（适合色盲、高对比度）
- 将输出保存到 figures/ 目录

**何时添加示意图：**
- 论文转换管道示意图
- 网站布局架构图
- 视频制作工作流程图
- 海报设计流程图
- 内容提取图
- 系统架构可视化
- 任何受益于可视化的复杂概念

有关创建示意图的详细指导，请参阅scientific-schematics技能文档。

---

## 核心能力

### 1. Paper2Web：互动网站生成

将论文转换为超越简单HTML转换的布局感知、互动学术主页。

**主要功能**：
- 响应式、多部分布局，适应论文内容
- 互动图表、表格和引用
- 带有导航的移动端友好设计
- 自动Logo发现（使用Google Search API）
- 美学优化和质量评估

**最佳用途**：发表后推广、预印本增强、实验室网站、永久研究展示

→ **详细文档见 `references/paper2web.md`**

---

### 2. Paper2Video：演示视频生成

生成包含幻灯片、旁白、光标移动和可选Talking-head视频的专业演示视频。

**主要功能**：
- 从论文结构自动生成幻灯片
- 自然流畅的语音合成
- 同步的光标移动和高亮
- 可选的Talking-head视频使用Hallo2（需要GPU）
- 多语言支持

**最佳用途**：视频摘要、会议演示、在线讲座、课程材料、YouTube推广

→ **详细文档见 `references/paper2video.md`**

---

### 3. Paper2Poster：会议海报生成

创建具有专业布局和视觉设计的打印就绪学术海报。

**主要功能**：
- 自定义海报尺寸（任意大小）
- 专业设计模板
- 机构品牌支持
- 链接二维码生成
- 高分辨率输出（300+ DPI）

**最佳用途**：会议海报展示、研讨会、学术展览、虚拟会议

→ **详细文档见 `references/paper2poster.md`**

---

## 快速开始

### 前置条件

1. **安装Paper2All**：
   ```bash
   git clone https://github.com/YuhangChen1/Paper2All.git
   cd Paper2All
   conda create -n paper2all python=3.11
   conda activate paper2all
   pip install -r requirements.txt
   ```

2. **配置API密钥**（创建 `.env` 文件）：
   ```
   OPENAI_API_KEY=your_openai_api_key_here
   # 可选：用于Logo搜索的GOOGLE_API_KEY和GOOGLE_CSE_ID
   ```

3. **安装系统依赖**：
   - LibreOffice（文档转换）
   - Poppler工具（PDF处理）
   - 48GB NVIDIA GPU（可选，用于Talking-head视频）

→ **完整安装指南见 `references/installation.md`**

---

### 基本用法

**生成所有组件**（网站 + 海报 + 视频）：
```bash
python pipeline_all.py \
  --input-dir "path/to/paper" \
  --output-dir "path/to/output" \
  --model-choice 1
```

**仅生成网站**：
```bash
python pipeline_all.py \
  --input-dir "path/to/paper" \
  --output-dir "path/to/output" \
  --model-choice 1 \
  --generate-website
```

**生成自定义尺寸的海报**：
```bash
python pipeline_all.py \
  --input-dir "path/to/paper" \
  --output-dir "path/to/output" \
  --model-choice 1 \
  --generate-poster \
  --poster-width-inches 60 \
  --poster-height-inches 40
```

**生成视频**（轻量级管道）：
```bash
python pipeline_light.py \
  --model_name_t gpt-4.1 \
  --model_name_v gpt-4.1 \
  --result_dir "path/to/output" \
  --paper_latex_root "path/to/paper"
```

→ **综合工作流程示例见 `references/usage_examples.md`**

---

## 工作流程决策树

使用此决策树确定要生成哪些组件：

```
用户需要论文的宣传材料？
│
├─ 需要永久在线展示？
│  └─→ 生成Paper2Web（互动网站）
│
├─ 需要物理会议材料？
│  ├─→ 海报展示？→ 生成Paper2Poster
│  └─→ 口头演讲？→ 生成Paper2Video
│
├─ 需要视频内容？
│  ├─→ 期刊视频摘要？→ 生成Paper2Video（5-10分钟）
│  ├─→ 会议演讲？→ 生成Paper2Video（15-20分钟）
│  └─→ 社交媒体？→ 生成Paper2Video（1-3分钟）
│
└─ 需要完整套餐？
   └─→ 生成全部三个组件
```

## 输入要求

### 支持的输入格式

**1. LaTeX源文件**（推荐）：
```
paper_directory/
├── main.tex              # 主论文文件
├── sections/             # 可选：拆分章节
├── figures/              # 所有图表文件
├── tables/               # 表格文件
└── bibliography.bib      # 参考文献
```

**2. PDF**：
- 带有嵌入字体的优质PDF
- 可选择文本（不是扫描图像）
- 高分辨率图表（建议300+ DPI）

### 输入组织

**单篇论文**：
```bash
input/
└── paper_name/
    ├── main.tex (或 paper.pdf)
    ├── figures/
    └── bibliography.bib
```

**多篇论文**（批量处理）：
```bash
input/
├── paper1/
│   └── main.tex
├── paper2/
│   └── main.tex
└── paper3/
    └── main.tex
```

## 常用参数

### 模型选择
- `--model-choice 1`：GPT-4（质量和成本的最佳平衡）
- `--model-choice 2`：GPT-4.1（最新功能，成本更高）
- `--model_name_t gpt-3.5-turbo`：更快，成本更低（质量可接受）

### 组件选择
- `--generate-website`：启用网站生成
- `--generate-poster`：启用海报生成
- `--generate-video`：启用视频生成
- `--enable-talking-head`：为视频添加Talking-head（需要GPU）

### 自定义
- `--poster-width-inches [宽度]`：自定义海报宽度
- `--poster-height-inches [高度]`：自定义海报高度
- `--video-duration [秒数]`：目标视频长度
- `--enable-logo-search`：自动发现机构Logo

## 输出结构

生成的输出按论文和组件组织：

```
output/
└── paper_name/
    ├── website/
    │   ├── index.html
    │   ├── styles.css
    │   └── assets/
    ├── poster/
    │   ├── poster_final.pdf
    │   ├── poster_final.png
    │   └── poster_source/
    └── video/
        ├── final_video.mp4
        ├── slides/
        ├── audio/
        └── subtitles/
```

## 最佳实践

### 输入准备
1. **尽可能使用LaTeX**：提供最佳的内容提取和结构
2. **正确组织文件**：将所有资源（图表、表格、参考文献）保存在论文目录中
3. **高质量图表**：使用矢量格式（PDF、SVG）或高分辨率光栅图像（300+ DPI）
4. **干净的LaTeX**：移除编译产物，确保源文件能成功编译

### 模型选择策略
- **GPT-4**：适用于生产质量输出、会议、出版物
- **GPT-4.1**：当需要最新功能或最佳质量时使用
- **GPT-3.5-turbo**：用于快速草稿、测试或简单的论文

### 组件优先级
对于紧迫的截止日期，按以下顺序生成：
1. **网站**（最快，最多功能，约15-30分钟）
2. **海报**（中等速度，用于打印截止日期，约10-20分钟）
3. **视频**（最慢，可以稍后生成，约20-60分钟）

### 质量保证
在最终确定输出之前：
1. **网站**：在多个设备上测试，验证所有链接正常工作，检查图表质量
2. **海报**：打印测试页，验证3-6英尺外的文本可读性，检查颜色
3. **视频**：观看完整视频，验证音频同步，在不同设备上测试

## 资源要求

### 处理时间
- **网站**：每篇论文15-30分钟
- **海报**：每篇论文10-20分钟
- **视频（无Talking-head）**：每篇论文20-60分钟
- **视频（带Talking-head）**：每篇论文60-120分钟

### 计算要求
- **CPU**：用于并行处理的多核处理器
- **RAM**：最低16GB，大型论文建议32GB
- **GPU**：标准输出可选，Talking-head需要（NVIDIA A6000 48GB）
- **存储**：每篇论文1-5GB，取决于组件和质量设置

### API成本（近似）
- **网站**：每篇论文0.50-2.00美元（GPT-4）
- **海报**：每篇论文0.30-1.00美元（GPT-4）
- **视频**：每篇论文1.00-3.00美元（GPT-4）
- **完整套餐**：每篇论文2.00-6.00美元（GPT-4）

## 故障排除

### 常见问题

**LaTeX解析错误**：
- 确保LaTeX源文件能成功编译：`pdflatex main.tex`
- 检查所有引用的文件都存在
- 验证没有自定义包阻止解析

**图表质量差**：
- 使用矢量格式（PDF、SVG、EPS）代替光栅图像
- 确保光栅图像达到300+ DPI
- 验证图表在编译后的PDF中正确渲染

**视频生成失败**：
- 验证足够的磁盘空间（建议5GB+）
- 检查所有依赖已安装（LibreOffice、Poppler）
- 查看输出目录中的错误日志

**海报布局问题**：
- 验证海报尺寸合理（24"-72"范围）
- 检查内容长度（很长的论文可能需要手动整理）
- 确保图表具有适合海报尺寸的分辨率

**API错误**：
- 验证`.env`文件中的API密钥
- 检查API信用余额
- 确保没有速率限制（等待并重试）

## 平台特定功能

### 社交媒体优化

系统自动检测目标平台：

**Twitter/X**（英语，数字文件夹名称）：
```bash
mkdir -p input/001_twitter/
# 生成英语宣传内容
```

**小红书**（中文，字母数字文件夹名称）：
```bash
mkdir -p input/xhs_paper/
# 生成中文宣传内容
```

### 会议特定格式

指定会议要求：
- 标准海报尺寸（4'×3'、5'×4'、A0、A1）
- 视频摘要长度限制（通常3-5分钟）
- 机构品牌要求
- 配色方案偏好

## 集成和部署

### 网站部署
将生成的网站部署到：
- **GitHub Pages**：免费托管，支持自定义域名
- **学术托管**：大学网络服务器
- **个人服务器**：AWS、DigitalOcean等
- **Netlify/Vercel**：现代托管，支持CI/CD

### 海报打印
打印就绪的文件适用于：
- 专业海报打印服务
- 大学打印店
- 在线服务（如Spoonflower、VistaPrint）
- 大幅面打印机（如果可用）

### 视频分发
在以下平台分享视频：
- **YouTube**：公开或未公开，最大覆盖范围
- **机构仓库**：大学视频平台
- **会议平台**：虚拟会议系统
- **社交媒体**：Twitter、LinkedIn、ResearchGate

## 高级用法

### 批量处理
高效处理多篇论文：
```bash
# 在批量目录中组织论文
for paper in paper1 paper2 paper3; do
    python pipeline_all.py \
      --input-dir input/$paper \
      --output-dir output/$paper \
      --model-choice 1 &
done
wait
```

### 自定义品牌
应用机构或实验室品牌：
- 在论文目录中提供Logo文件
- 在配置中指定配色方案
- 使用自定义模板（高级）
- 匹配会议主题要求

### 多语言支持
生成不同语言的内容：
- 在配置中指定目标语言
- 系统适当翻译内容
- 为视频旁白选择合适的声音
- 适应文化设计惯例

## 参考资料和资源

此技能包含全面的参考文档：

- **`references/installation.md`**：完整的安装和配置指南
- **`references/paper2web.md`**：详细的Paper2Web文档，包含所有功能
- **`references/paper2video.md`**：全面的Paper2Video指南，包括Talking-head设置
- **`references/paper2poster.md`**：完整的Paper2Poster文档，包含设计模板
- **`references/usage_examples.md`**：真实示例和工作流程模式

**外部资源**：
- GitHub仓库：https://github.com/YuhangChen1/Paper2All
- 策划数据集：Hugging Face上可用（13个研究类别）
- 基准套件：参考网站和评估指标

## 评估和质量指标

Paper2All系统包含内置的质量评估：

### 内容质量
- **完整性**：论文内容的覆盖范围
- **准确性**：研究结果的忠实表示
- **清晰度**：可访问性和可理解性
- **信息量**：关键信息的突出程度

### 设计质量
- **美学**：视觉吸引力和专业性
- **布局**：平衡、层次和组织
- **可读性**：文本清晰度和图表清晰度
- **一致性**：统一的风格和品牌

### 技术质量
- **性能**：加载时间、响应能力
- **兼容性**：跨浏览器、跨设备支持
- **可访问性**：WCAG合规、屏幕阅读器支持
- **标准**：有效的HTML/CSS、打印就绪的PDF

所有输出在生成完成前都会经过自动质量检查。
