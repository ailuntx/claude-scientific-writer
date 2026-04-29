---
name: pptx-posters
description: 使用 HTML/CSS 创建可导出为 PDF 或 PPTX 的研究海报。仅当用户明确请求 PowerPoint/PPTX 海报格式时使用此技能。对于标准的研究海报，请改用 latex-posters。此技能提供基于 Web 的现代海报设计，具有响应式布局和轻松的可视化集成。
allowed-tools: Read Write Edit Bash
license: MIT 许可证
metadata:
    skill-author: K-Dense Inc.
---

# PPTX 研究海报（基于 HTML）

## 概述

**⚠️ 仅当用户明确请求 PPTX/POWERPOINT 海报格式时使用此技能。**

对于标准的研究海报，请改用 **latex-posters** 技能，该技能提供更好的排版控制，并且是学术会议的默认选择。

本技能使用 HTML/CSS 创建研究海报，然后可以导出为 PDF 或转换为 PowerPoint 格式。这种基于 Web 的方法具有以下优势：
- 现代化、响应式的布局
- 轻松集成 AI 生成的视觉元素
- 可在浏览器中快速迭代和预览
- 通过浏览器打印功能导出为 PDF
- 如有特殊需求，可转换为 PPTX

## 何时使用此技能

**仅在以下情况下使用此技能：**
- 用户明确请求“PPTX 海报”、“PowerPoint 海报”或“PPT 海报”
- 用户特别要求使用基于 HTML 的海报
- 用户需要在创建后在 PowerPoint 中编辑海报
- LaTeX 不可用或用户要求非 LaTeX 解决方案

**请勿在以下情况下使用此技能：**
- 用户请求“海报”但未指定格式 → 使用 latex-posters
- 用户请求“研究海报”或“会议海报” → 使用 latex-posters
- 用户提及 LaTeX、tikzposter、beamerposter 或 baposter → 使用 latex-posters

## AI 驱动的视觉元素生成

**标准工作流程：在创建 HTML 海报之前，使用 AI 生成所有主要视觉元素。**

这是创建视觉吸引力海报的推荐方法：
1. 规划所需的所有视觉元素（主图、引言、方法、结果、结论）
2. 使用 scientific-schematics 或 Nano Banana Pro 生成每个元素
3. 在 HTML 模板中组装生成的图片
4. 在视觉元素周围添加文本内容

**目标：海报面积的 60-70% 应为 AI 生成的视觉元素，30-40% 为文本。**

---

### 关键：海报尺寸的字体要求

**⚠️ AI 生成的可视化中的所有文本必须适合海报阅读。**

为海报生成图形时，必须在每个提示中包含字体大小规范。海报图形通常在 4-6 英尺的距离观看，因此文本必须足够大。

**每个海报图形必须包含的强制提示要求：**

```
海报格式要求（严格执行）：
- 每个图形绝对最多包含 3-4 个元素（3 个为理想值）
- 整个图形中绝对最多包含 10 个单词
- 没有包含 5 个以上步骤的复杂工作流程（改为拆分为 2-3 个简单图形）
- 没有多级嵌套图表（展平为单级）
- 没有包含多个子部分的案例研究（每个案例一个关键点）
- 所有文本超大加粗（标签字号 80pt 以上，关键数字字号 120pt 以上）
- 仅使用高对比度（深色文字在白色背景上或白色文字在深色背景上，文本不使用渐变）
- 强制至少 50% 的留白（图形的一半应为空白）
- 仅使用粗线条（5px 以上），大图标（200px 以上）
- 每个图形传达一个单一信息（而不是 3 个相关消息）
```

**⚠️ 在生成之前：审查您的提示并计算元素数量**
- 如果您的描述包含 5 个以上项目 → 停止。拆分为多个图形。
- 如果您的工作流程包含 5 个以上阶段 → 停止。仅显示 3-4 个高级步骤。
- 如果您的比较包含 4 种以上方法 → 停止。仅显示前 3 种或我们的方法与最佳基线对比。

**示例 - 错误（7 阶段工作流程）：**
```bash
# ❌ 创建出微小且无法阅读的文本
python scripts/generate_schematic.py "药物发现工作流程：第一阶段 靶点识别，第二阶段 合成，第三阶段 筛选，第四阶段 先导优化，第五阶段 验证，第六阶段 临床试验，第七阶段 FDA 批准，附带指标。" -o figures/workflow.png
```

**示例 - 正确（3 个大型阶段）：**
```bash
# ✅ 相同的内容，简化为可读的海报格式
python scripts/generate_schematic.py "A0 海报格式。超简单 3 框工作流程：'发现' → '验证' → '批准'。每个单词使用超大加粗字体（120pt 以上）。粗箭头（10px）。60% 留白。仅包含这 3 个单词。无子步骤。可在 12 英尺距离阅读。" -o figures/workflow_simple.png
```

---

### 关键：防止内容溢出

**⚠️ 海报边缘不得有文本或内容被截断。**

**预防规则：**

**1. 限制内容部分（最多 5-6 个部分）：**
```
✅ 良好 - 5 个部分，留出呼吸空间：
   - 标题/头部
   - 引言/问题
   - 方法
   - 结果（1-2 个关键发现）
   - 结论

❌ 差 - 8 个以上部分挤在一起
```

**2. 字数限制：**
- **每个部分**：最多 50-100 个单词
- **整个海报**：最多 300-800 个单词
- **如果内容更多**：删减或制作成讲义

---

## 核心能力

### 1. HTML/CSS 海报设计

HTML 模板 (`assets/poster_html_template.html`) 提供：
- 固定的海报尺寸（36×48 英寸 = 2592×3456 点）
- 带有渐变样式的专业标题
- 三栏内容布局
- 基于区块的部分，具有现代样式
- 页脚包含参考文献和联系信息

### 2. 海报结构

**标准布局：**
```
┌─────────────────────────────────────────┐
│  标题区域：标题、作者、主图               │
├─────────────┬─────────────┬─────────────┤
│    引言     │    结果     │   讨论    │
│             │             │             │
│    方法     │   (图表)    │   结论    │
│             │             │             │
│   (示意图)  │   (数据)    │  (总结)   │
├─────────────┴─────────────┴─────────────┤
│  页脚区域：参考文献与联系信息              │
└─────────────────────────────────────────┘
```

### 3. 视觉元素集成

每个部分都应突出显示 AI 生成的视觉元素：

**主图（标题区域）：**
```html
<img src="figures/hero.png" class="hero-image">
```

**部分图形：**
```html
<div class="block">
  <h2 class="block-title">方法</h2>
  <div class="block-content">
    <img src="figures/workflow.png" class="block-image">
    <ul>
      <li>简要的方法论要点</li>
    </ul>
  </div>
</div>
```

### 4. 生成视觉元素

**在创建 HTML 之前，生成所有视觉元素：**

```bash
# 创建 figures 目录
mkdir -p figures

# 主图 - 简单、有冲击力
python scripts/generate_schematic.py "A0 海报格式。主横幅：'[主题]' 使用超大字体（120pt 以上）。深蓝色渐变背景。一个标志性视觉元素。文字极少。可在 15 英尺距离阅读。" -o figures/hero.png

# 引言视觉元素 - 仅 3 个元素
python scripts/generate_schematic.py "A0 海报格式。简单视觉元素，仅包含 3 个图标：[图标1] → [图标2] → [图标3]。每个图标一个单词标签（80pt 以上）。50% 留白。可在 8 英尺距离阅读。" -o figures/intro.png

# 方法流程图 - 仅 4 个步骤
python scripts/generate_schematic.py "A0 海报格式。简单流程图，仅包含 4 个框：步骤1 → 步骤2 → 步骤3 → 步骤4。超大标签（100pt 以上）。粗箭头。50% 留白。没有子步骤。" -o figures/workflow.png

# 结果可视化 - 仅 3 个柱状图
python scripts/generate_schematic.py "A0 海报格式。简单柱状图，仅包含 3 个柱子：基线（70%）、现有（85%）、我们的（95%）。柱子上显示超大百分比（120pt 以上）。没有坐标轴，没有图例。50% 留白。" -o figures/results.png

# 结论 - 恰好 3 个关键发现
python scripts/generate_schematic.py "A0 海报格式。恰好 3 张卡片：'95%'（150pt）'准确率'（60pt）、'2倍'（150pt）'更快'（60pt）、勾号 '就绪'（60pt）。50% 留白。没有其他文本。" -o figures/conclusions.png
```

---

## PPTX 海报创建工作流程

### 阶段 1：规划

1. **确认 PPTX 被明确请求**
2. **确定海报要求：**
   - 尺寸：36×48 英寸（最常见）或 A0
   - 方向：纵向（最常见）
3. **制定内容大纲：**
   - 确定 1-3 个核心信息
   - 规划 3-5 个视觉元素
   - 起草最简文本（总共 300-800 单词）

### 阶段 2：生成视觉元素（AI 驱动）

**关键：生成内容最少的简单图形。**

```bash
mkdir -p figures

# 为每个元素生成图形，并指定海报格式规格
# （参见上文第 4 节中的示例）
```

### 阶段 3：创建 HTML 海报

1. **复制模板：**
   ```bash
   cp skills/pptx-posters/assets/poster_html_template.html poster.html
   ```

2. **更新内容：**
   - 替换占位符标题和作者
   - 插入 AI 生成的图片
   - 添加最简支持性文本
   - 更新参考文献和联系信息

3. **在浏览器中预览：**
   ```bash
   open poster.html  # macOS
   # 或者
   xdg-open poster.html  # Linux
   ```

### 阶段 4：导出为 PDF

**浏览器打印方法：**
1. 在 Chrome 或 Firefox 中打开 poster.html
2. 打印（Cmd/Ctrl + P）
3. 选择“另存为 PDF”
4. 设置纸张大小以匹配海报尺寸
5. 移除页边距
6. 启用“背景图形”

**命令行方法（如果 Chrome 可用）：**
```bash
# Chrome 无头模式导出 PDF
google-chrome --headless --print-to-pdf=poster.pdf \
  --print-to-pdf-no-header \
  --no-margins \
  poster.html
```

### 阶段 5：转换为 PPTX（如果需要）

**选项 1：PDF 到 PPTX 转换**
```bash
# 使用 LibreOffice
libreoffice --headless --convert-to pptx poster.pdf

# 或者对于简单情况，使用在线转换器
```

**选项 2：使用 python-pptx 直接创建 PPTX**
```python
from pptx import Presentation
from pptx.util import Inches, Pt

prs = Presentation()
prs.slide_width = Inches(48)
prs.slide_height = Inches(36)

slide = prs.slides.add_slide(prs.slide_layouts[6])  # 空白版式

# 从 figures/ 添加图片
slide.shapes.add_picture("figures/hero.png", Inches(0), Inches(0), width=Inches(48))
# ... 添加其他元素

prs.save("poster.pptx")
```

---

## HTML 模板结构

提供的模板 (`assets/poster_html_template.html`) 包含：

### 用于自定义的 CSS 变量

```css
/* 海报尺寸 */ 
body {
  width: 2592pt;   /* 36 英寸 */
  height: 3456pt;  /* 48 英寸 */
}

/* 配色方案 - 可自定义 */
.header {
  background: linear-gradient(135deg, #1a365d 0%, #2b6cb0 50%, #3182ce 100%);
}

/* 排版 */
.poster-title { font-size: 108pt; }
.authors { font-size: 48pt; }
.block-title { font-size: 52pt; }
.block-content { font-size: 34pt; }
```

### 关键类

| 类名 | 用途 | 字体大小 |
|-------|---------|-----------|
| `.poster-title` | 主标题 | 108pt |
| `.authors` | 作者姓名 | 48pt |
| `.affiliations` | 机构 | 38pt |
| `.block-title` | 部分标题 | 52pt |
| `.block-content` | 正文 | 34pt |
| `.key-finding` | 高亮框 | 36pt |

---

## 质量检查清单

### 第 0 步：生成前审查（强制）

**对于每个计划生成的图形，验证：**
- [ ] 是否可以用 3-4 个或更少的项目描述？（不是 5 个以上）
- [ ] 是否是简单的工作流程（3-4 步，而不是 7 步以上）？
- [ ] 所有文本是否可以用 10 个单词或更少描述？
- [ ] 是否传达一个信息（而不是多个）？

**拒绝这些模式：**
- ❌ “7 阶段工作流程” → 简化为“3 个大型阶段”
- ❌ “多个案例研究” → 每个图形一个案例
- ❌ “2015-2024 年每年时间线” → “仅 3 个关键年份”
- ❌ “比较 6 种方法” → “仅 2 种：我们的方法 vs 最佳方法”

### 第 2b 步：生成后审查（强制）

**对于每个以 25% 缩放比例查看的生成图形：**

**✅ 通过标准（必须全部为真）：**
- [ ] 可以清晰阅读所有文本
- [ ] 计数：3-4 个或更少元素
- [ ] 留白：50% 以上为空白
- [ ] 2 秒内理解
- [ ] 不是复杂的 5 阶段以上工作流程
- [ ] 没有多个嵌套部分

**❌ 失败标准（如果任一为真，则重新生成）：**
- [ ] 文本小/难以阅读 → 使用“150pt 以上”重新生成
- [ ] 超过 4 个元素 → 使用“仅 3 个元素”重新生成
- [ ] 少于 50% 留白 → 使用“60% 留白”重新生成
- [ ] 复杂的多阶段 → 拆分为 2-3 个图形
- [ ] 多个案例挤在一起 → 拆分为单独的图形

### 导出后检查

- [ ] 所有 4 个边缘均没有内容被截断（仔细检查）
- [ ] 所有图片正确显示
- [ ] 颜色渲染符合预期
- [ ] 以 25% 比例查看文本可读
- [ ] 图形看起来简单（不像复杂的 7 阶段工作流程）

---

## 需要避免的常见错误

**AI 生成的图形错误：**
- ❌ 元素太多（10 个以上） → 保持在 3-5 个以内
- ❌ 文字太小 → 在提示中指定“超大（100pt 以上）”
- ❌ 没有留白 → 在每个提示中添加“50% 留白”
- ❌ 复杂的流程图（8 步以上） → 限制在 4-5 步

**HTML/导出错误：**
- ❌ 内容超出海报尺寸 → 在浏览器中检查溢出
- ❌ PDF 中缺少背景图形 → 在打印设置中启用
- ❌ PDF 中纸张尺寸错误 → 完全匹配海报尺寸
- ❌ 低分辨率图片 → 使用至少 300 DPI

**内容错误：**
- ❌ 文本过多（超过 1000 单词） → 缩减到 300-800 单词
- ❌ 部分过多（7 个以上） → 合并为 5-6 个
- ❌ 没有清晰的视觉层次 → 突出关键发现

---

## 与其他技能的集成

此技能与以下技能配合使用：
- **Scientific Schematics**：生成所有海报示意图和流程图
- **Generate Image / Nano Banana Pro**：创建风格化图形和主图
- **LaTeX Posters**：海报创建的默认技能（除非明确请求 PPTX，否则应使用此项）

---

## 模板资源

位于 `assets/` 目录中：

- `poster_html_template.html`：主要 HTML 海报模板（36×48 英寸）
- `poster_quality_checklist.md`：提交前验证清单

## 参考资料

位于 `references/` 目录中：

- `poster_content_guide.md`：内容组织和写作指南
- `poster_design_principles.md`：排版、色彩理论和视觉层次
- `poster_layout_design.md`：布局原则和网格系统
