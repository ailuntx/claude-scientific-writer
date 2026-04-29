# 使用示例和工作流程

## 完整工作流程示例

### 示例 1：会议演示套件

**场景**：为大型会议演示准备网站、海报和视频。

**用户请求**："我需要为我的 NeurIPS 论文提交创建一个完整的演示套件。生成一个网站、海报和视频演示。"

**工作流程**：

```bash
# 第 1 步：整理论文文件
mkdir -p input/neurips2025_paper
cp main.tex input/neurips2025_paper/
cp -r figures/ input/neurips2025_paper/
cp -r tables/ input/neurips2025_paper/
cp bibliography.bib input/neurips2025_paper/

# 第 2 步：生成所有组件
python pipeline_all.py \
  --input-dir input/neurips2025_paper \
  --output-dir output/ \
  --model-choice 1 \
  --generate-website \
  --generate-poster \
  --generate-video \
  --poster-width-inches 48 \
  --poster-height-inches 36 \
  --enable-logo-search

# 第 3 步：查看输出
ls -R output/neurips2025_paper/
# - website/index.html
# - poster/poster_final.pdf
# - video/final_video.mp4
```

**输出**：
- 展示研究内容的交互式网站
- 4'×3' 会议海报（可直接打印）
- 12 分钟演示视频
- 处理时间：约 45 分钟（不含人物解说）

---

### 示例 2：预印本快速建站

**场景**：为 bioRxiv 预印本创建一个可探索的主页。

**用户请求**："将我的基因组学预印本转换为交互式网站，以配合 bioRxiv 提交。"

**工作流程**：

```bash
# 使用 PDF 输入（没有 LaTeX）
python pipeline_all.py \
  --input-dir papers/genomics_preprint/ \
  --output-dir output/genomics_web/ \
  --model-choice 1 \
  --generate-website

# 部署到 GitHub Pages 或个人服务器
cd output/genomics_web/website/
# 添加 bioRxiv 论文链接、数据仓库、代码链接
# 上传到托管服务
```

**提示**：
- 包含 bioRxiv DOI 链接
- 添加 GitHub 仓库链接
- 包含数据可用性部分
- 如有可能嵌入交互式可视化

---

### 示例 3：期刊投稿视频摘要

**场景**：为鼓励多媒体投稿的期刊创建视频摘要。

**用户请求**："为我的 Nature Communications 投稿生成一个 5 分钟的视频摘要。"

**工作流程**：

```bash
# 生成聚焦关键发现的简洁视频
python pipeline_light.py \
  --model_name_t gpt-4.1 \
  --model_name_v gpt-4.1 \
  --result_dir output/video_abstract/ \
  --paper_latex_root papers/nature_comms/ \
  --video-duration 300 \
  --slides-per-minute 3

# 可选：添加自定义开场/结尾幻灯片
# 可选：包含人物解说作为介绍
```

**输出**：
- 5 分钟视频摘要
- 聚焦视觉结果
- 清晰、易懂的旁白
- 符合期刊要求的格式

---

### 示例 4：多论文网站生成

**场景**：为研究组的多篇论文创建网站。

**用户请求**："为我们实验室今年发表的所有 5 篇论文生成网站。"

**工作流程**：

``` 步骤：

```bash
# 整理论文
mkdir -p batch_input/
# 创建子目录：paper1/、paper2/、paper3/、paper4/、paper5/
# 每个目录包含其 LaTeX 源码

# 批量处理
python pipeline_all.py \
  --input-dir batch_input/ \
  --output-dir batch_output/ \
  --model-choice 1 \
  --generate-website \
  --enable-logo-search

# 生成结果：
# batch_output/paper1/website/
# batch_output/paper2/website/
# batch_output/paper3/website/
# batch_output/paper4/website/
# batch_output/paper5/website/
```

**最佳实践**：
- 使用一致的命名规范
- 大批量处理过夜进行
- 检查每个网站的准确性
- 部署到统一的实验室网站

---

### 示例 5：虚拟会议海报

**场景**：为具有交互元素的虚拟会议创建数字海报。

**用户请求**："为虚拟 ISMB 会议创建一个海报，包含可点击的代码和数据链接。"

**工作流程**：

```bash
# 生成带二维码和链接的海报
python pipeline_all.py \
  --input-dir papers/ismb_submission/ \
  --output-dir output/ismb_poster/ \
  --model-choice 1 \
  --generate-poster \
  --poster-width-inches 48 \
  --poster-height-inches 36 \
  --enable-qr-codes

# 手动添加二维码到：
# - GitHub 仓库
# - 交互式结果仪表板
# - 补充数据
# - 视频演示
```

**数字增强**：
- 带嵌入超链接的 PDF
- 用于虚拟平台的高分辨率 PNG
- 带视频链接的独立下载 PDF

---

### 示例 6：宣传短视频

**场景**：为社交媒体创建简短的宣传视频。

**用户请求**："为我们的 Cell 论文生成一个 2 分钟的精选视频用于 Twitter。"

**工作流程**：

```bash
# 生成简短吸引人的视频
python pipeline_light.py \
  --model_name_t gpt-4.1 \
  --model_name_v gpt-4.1 \
  --result_dir output/promo_video/ \
  --paper_latex_root papers/cell_paper/ \
  --video-duration 120 \
  --presentation-style public

# 后期处理：
# - 提取 30 秒关键片段用于 Twitter
# - 添加字幕以便静音观看
# - 优化社交媒体文件大小
```

**社交媒体优化**：
- 正方形格式 (1:1) 用于 Instagram
- 横向格式 (16:9) 用于 Twitter/LinkedIn
- 纵向格式 (9:16) 用于 TikTok/Stories
- 为关键发现添加文字叠加

---

## 常见用例模式

### 模式 1：LaTeX 论文 → 完整套件

**输入**：包含所有资源的 LaTeX 源码
**输出**：网站 + 海报 + 视频
**时间**：45-90 分钟
**最适合**：重要出版物、会议演示

```bash
python pipeline_all.py \
  --input-dir [latex_dir] \
  --output-dir [output_dir] \
  --model-choice 1 \
  --generate-website \
  --generate-poster \
  --generate-video
```

---

### 模式 2：PDF → 交互式网站

**输入**：已发布的 PDF 论文
**输出**：可探索网站
**时间**：15-30 分钟
**最适合**：发表后推广、预印本增强

```bash
python pipeline_all.py \
  --input-dir [pdf_dir] \
  --output-dir [output_dir] \
  --model-choice 1 \
  --generate-website
```

---

### 模式 3：LaTeX → 会议海报

**输入**：LaTeX 论文
**输出**：可直接打印的海报（自定义尺寸）
**时间**：10-20 分钟
**最适合**：会议海报展示

```bash
python pipeline_all.py \
  --input-dir [latex_dir] \
  --output-dir [output_dir] \
  --model-choice 1 \
  --generate-poster \
  --poster-width-inches [width] \
  --poster-height-inches [height]
```

---

### 模式 4：LaTeX → 演示视频

**输入**：LaTeX 论文
**输出**：带旁白的演示视频
**时间**：20-60 分钟（不含人物解说）
**最适合**：视频摘要、在线演示、教学材料

```bash
python pipeline_light.py \
  --model_name_t gpt-4.1 \
  --model_name_v gpt-4.1 \
  --result_dir [output_dir] \
  --paper_latex_root [latex_dir]
```

---

## 平台特定输出

### Twitter/X 推广内容

系统自动检测数字文件夹名的 Twitter 目标：

```bash
# 创建 Twitter 优化内容
mkdir -p input/001_twitter_post/
# 系统生成英文推广内容
```

**生成输出**：
- 简短吸引人的摘要
- 关键图表亮点
- 标签推荐
- 适合长推文格式

---

### 小红书内容

对于中文社交媒体，使用字母数字文件夹名：

```bash
# 创建小红书优化内容
mkdir -p input/xhs_genomics/
# 系统生成中文推广内容
```

**生成输出**：
- 中文语言内容
- 符合平台风格的格式
- 视觉优先呈现
- 互动优化

---

## 常见问题排查

### 场景：大型论文（>50 页）

**挑战**：处理时间和内容选择
**解决方案**：
```bash
# 选项 1：聚焦关键部分
# 编辑 LaTeX 注释掉次要部分

# 选项 2：分批处理
# 生成网站用于概述
# 为方法/结果生成单独的详细视频

# 选项 3：使用更快的模型进行初步处理
# 审查并用更好的模型重新生成关键组件
```

---

### 场景：复杂数学内容

**挑战**：公式可能无法完美渲染
**解决方案**：
- 使用 LaTeX 输入（而非 PDF）以获得最佳公式处理
- 检查生成内容的公式准确性
- 手动调整复杂公式（如需要）
- 考虑对关键公式使用图表截图

---

### 场景：非标准论文结构

**挑战**：论文不符合标准 IMRAD 格式
**解决方案**：
- 在论文元数据中提供自定义部分指导
- 检查生成的结构并进行调整
- 使用更强大的模型 (GPT-4.1) 以获得更好的适应性
- 考虑在 LaTeX 注释中手动标注部分

---

### 场景：有限的 API 预算

**挑战**：在保持质量的同时降低成本
**解决方案**：
```bash
# 对简单论文使用 GPT-3.5-turbo
python pipeline_all.py \
  --input-dir [paper_dir] \
  --output-dir [output_dir] \
  --model-choice 3

# 仅生成需要的组件
# 仅网站（最便宜）
# 仅海报（适中）
# 不含人物配乐的视频（适中）
```

---

### 场景：紧迫的截止日期

**挑战**：需要快速获得输出
**解决方案**：
```bash
# 如有多篇论文则并行处理
# 使用更快的模型 (GPT-3.5-turbo)
# 先只生成必要的组件
# 跳过可选功能（标志搜索、配乐）

python pipeline_light.py \
  --model_name_t gpt-3.5-turbo \
  --model_name_v gpt-3.5-turbo \
  --result_dir [output_dir] \
  --paper_latex_root [latex_dir]
```

**优先级顺序**：
1. 网站（最快、最通用）
2. 海报（速度适中，打印截止日期）
3. 视频（最慢，可稍后生成）

---

## 质量优化建议

### 获得最佳网站结果
1. 使用包含所有资源的 LaTeX 输入
2. 包含高分辨率图表
3. 确保论文有清晰的章节结构
4. 启用标志搜索以获得专业外观
5. 检查并测试所有交互元素

### 获得最佳海报结果
1. 提供高分辨率图表（300+ DPI）
2. 指定所需的确切海报尺寸
3. 包含机构品牌信息
4. 使用专业配色方案
5. 在打印完整海报前先打印小预览测试

### 获得最佳视频结果
1. 使用 LaTeX 以获得最清晰的内容提取
2. 适当指定目标时长
3. 在视频生成前检查脚本
4. 选择适当的演示风格
5. 测试音频质量和节奏

### 获得最佳整体结果
1. 从干净、整理良好的 LaTeX 源码开始
2. 使用 GPT-4 或 GPT-4.1 获得最高质量
3. 在最终确定前检查所有输出
4. 对任何需要调整的组件进行迭代
5. 组合组件以获得统一的演示套件
