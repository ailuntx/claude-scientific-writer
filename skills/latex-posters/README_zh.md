# LaTeX 学术海报生成技能

使用 LaTeX 为会议和学术报告创建专业的、可直接出版的研究海报。

## 概述

本技能提供使用三大 LaTeX 包的完整指导：
- **beamerposter**：传统学术海报，熟悉的 Beamer 语法
- **tikzposter**：现代、彩色设计，集成 TikZ
- **baposter**：结构化多栏布局，自动定位

## 快速开始

### 1. 选择模板

浏览 `assets/` 中的模板：
- `beamerposter_template.tex` - 经典学术风格
- `tikzposter_template.tex` - 现代、彩色设计
- `baposter_template.tex` - 结构化多栏布局

### 2. 自定义内容

使用您的研究内容编辑模板：
- 标题、作者、单位
- 引言、方法、结果、结论
- 用您的图片替换占位图
- 更新参考文献和致谢

### 3. 配置全页海报

海报应占满整个页面，边距最小化：

```latex
% beamerposter - 全页设置
\documentclass[final,t]{beamer}
\usepackage[size=a0,scale=1.4,orientation=portrait]{beamerposter}
\setbeamersize{text margin left=5mm, text margin right=5mm}
\usepackage[margin=10mm]{geometry}

% tikzposter - 全页设置
\documentclass[25pt,a0paper,portrait,margin=10mm,innermargin=15mm]{tikzposter}

% baposter - 全页设置
\documentclass[a0paper,portrait,fontscale=0.285]{baposter}
```

### 4. 编译

```bash
pdflatex poster.tex

# 或获得更好的字体支持：
lualatex poster.tex
xelatex poster.tex
```

### 5. 检查 PDF 质量

**印刷前必做！**

```bash
# 运行自动化检查
./scripts/review_poster.sh poster.pdf

# 手动验证（见下方检查清单）
```

## 主要功能

### 全页覆盖

所有模板配置为最大化内容区域：
- 最小外边距（5-15mm）
- 栏间最佳间距（15-20mm）
- 适当的块间距以提高可读性
- 无浪费的空白区域

### PDF 质量控制

**自动化检查** (`review_poster.sh`)：
- 页面尺寸验证
- 字体嵌入检查
- 图像分辨率分析
- 文件大小优化

**手动验证** (`assets/poster_quality_checklist.md`)：
- 100% 缩放下的目视检查
- 缩小比例打印测试（25%）
- 排版和间距检查
- 内容完整性检查

### 设计原则

所有模板遵循循证的海报设计：
- **排版**：标题 72pt+，标题 48-72pt，正文 24-36pt
- **颜色**：高对比度（≥4.5:1），色盲友好配色
- **布局**：清晰的视觉层次，逻辑流畅
- **内容**：最多 300-800 字，40-50% 视觉内容

## 常见海报尺寸

模板支持所有标准尺寸：

| 尺寸 | 尺寸 | 配置 |
|------|------------|---------------|
| A0 | 841 × 1189 mm | `size=a0` 或 `a0paper` |
| A1 | 594 × 841 mm | `size=a1` 或 `a1paper` |
| 36×48" | 914 × 1219 mm | 自定义页面尺寸 |
| 42×56" | 1067 × 1422 mm | 自定义页面尺寸 |

## 文档

### 参考指南

**完整文档**（位于 `references/`）：

1. **`latex_poster_packages.md`**（746 行）
   - beamerposter、tikzposter、baposter 详细对比
   - 包特定语法和示例
   - 优势、限制、最佳用例
   - 主题和颜色定制
   - 编译技巧和故障排除

2. **`poster_design_principles.md`**（807 行）
   - 视觉层次和空白
   - 排版：字体选择、尺寸、可读性
   - 色彩理论：配色方案、对比度、无障碍
   - 色盲友好配色
   - 图标、图形和视觉元素
   - 避免常见设计错误

3. **`poster_layout_design.md`**（650+ 行）
   - 网格系统（2、3、4栏布局）
   - 视觉流和阅读模式
   - 空间组织策略
   - 空白管理
   - 块和框设计
   - 按研究类型的布局模式

4. **`poster_content_guide.md`**（900+ 行）
   - 内容策略（3-5 分钟规则）
   - 各部分字数预算
   - 视觉与文字比例（40-50% 视觉）
   - 各部分写作指导
   - 图表整合和说明
   - 从论文到海报的改编

### 工具和资源

**脚本**（位于 `scripts/`）：
- `review_poster.sh`：自动化 PDF 质量检查
  - 页面尺寸验证
  - 字体嵌入检查
  - 图像分辨率分析
  - 文件大小评估

**检查清单**（位于 `assets/`）：
- `poster_quality_checklist.md`：印刷前完整检查清单
  - 编译前检查
  - PDF 质量验证
  - 目视检查项目
  - 无障碍检查
  - 同行评审指南
  - 最终印刷检查清单

**模板**（位于 `assets/`）：
- `beamerposter_template.tex`：完整可用的模板
- `tikzposter_template.tex`：完整可用的模板
- `baposter_template.tex`：完整可用的模板

## 工作流程

### 推荐的海报创建流程

**1. 规划**（使用 LaTeX 之前）
- 确定会议要求（尺寸、方向）
- 确定要突出的 3-5 个关键结果
- 创建图表（300+ DPI）
- 起草 300-800 字内容大纲

**2. 选择模板**
- 根据需求选择包：
  - **beamerposter**：传统会议、机构品牌
  - **tikzposter**：现代会议、创意领域
  - **baposter**：多 section 海报、结构化布局

**3. 整合内容**
- 复制模板并自定义
- 替换占位文字
- 添加图表并确保高分辨率
- 配置颜色以匹配品牌

**4. 编译和审查**
- 编译为 PDF
- 运行 `review_poster.sh` 进行自动化检查
- 在 100% 缩放下目视审查
- 对照 `poster_quality_checklist.md` 检查

**5. 试打印**
- **关键步骤！** 按 25% 比例打印
- A0 → A4 纸，36×48" → 信纸
- 从 2-3 英尺处观看（模拟全尺寸海报 8-12 英尺处的效果）
- 验证可读性和颜色

**6. 修改**
- 修复发现的所有问题
- 仔细校对（错误会被放大！）
- 获取同事反馈
- 最终编译

**7. 印刷**
- 验证页面尺寸：`pdfinfo poster.pdf`
- 检查字体嵌入：`pdffonts poster.pdf`
- 在截止日期前 2-3 天发送给专业印刷商
- 保留备份副本

## 故障排除

### 白色边距过大

**问题**：海报边缘周围有过多空白

**解决方案**：
```latex
% beamerposter
\setbeamersize{text margin left=5mm, text margin right=5mm}
\usepackage[margin=10mm]{geometry}

% tikzposter
\documentclass[..., margin=5mm, innermargin=10mm]{tikzposter}

% baposter
\documentclass[a0paper, margin=5mm]{baposter}
```

### 内容被裁切

**问题**：文本或图表超出页面范围

**解决方案**：
- 检查总宽度：栏目间距 + 边距 = 页面宽度
- 减小栏目宽度或间距
- 使用可见的页面边界调试：
```latex
\usepackage{eso-pic}
\AddToShipoutPictureBG{
  \AtPageLowerLeft{
    \put(0,0){\framebox(\LenToUnit{\paperwidth},\LenToUnit{\paperheight}){}}
  }
}
```

### 图像模糊

**问题**：图表像素化或质量低

**解决方案**：
- 尽可能使用矢量图形（PDF、SVG）
- 光栅图像：最终打印尺寸至少 300 DPI
- 对于 A0 宽度（33.1"）：300 DPI = 至少 9930 像素
- 检查方法：`pdfimages -list poster.pdf`

### 字体未嵌入

**问题**：打印机因字体缺失而拒绝 PDF

**解决方案**：
```bash
# 使用嵌入字体重新编译
pdflatex -dEmbedAllFonts=true poster.tex

# 验证嵌入
pdffonts poster.pdf
# 所有字体应在 "emb" 列显示 "yes"
```

### 文件过大

**问题**：PDF 超出邮件大小限制（>50MB）

**解决方案**：
```bash
# 压缩以便于数字分享
gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 \
   -dPDFSETTINGS=/printer -dNOPAUSE -dQUIET -dBATCH \
   -sOutputFile=poster_compressed.pdf poster.pdf

# 保留原始未压缩版本用于打印
```

## 需要避免的常见错误

### 内容
- ❌ 文字过多（>1000 字）
- ❌ 字体太小（正文 <24pt）
- ❌ 没有明确的主要信息
- ✅ 300-800 字，正文 30pt+，1-3 个关键发现

### 设计
- ❌ 颜色对比度差（<4.5:1）
- ❌ 红绿颜色组合（色盲问题）
- ❌ 布局杂乱，没有空白
- ✅ 高对比度、无障碍颜色、充足的间距

### 技术
- ❌ 海报尺寸错误
- ❌ 图像分辨率低（<300 DPI）
- ❌ 字体未嵌入
- ✅ 验证规格、高分辨率图像、嵌入字体

## 包对比

选择正确包的快速参考：

| 功能 | beamerposter | tikzposter | baposter |
|---------|--------------|------------|----------|
| **学习曲线** | 简单（Beamer 用户） | 中等 | 中等 |
| **美学** | 传统 | 现代 | 专业 |
| **自定义** | 中等 | 高（TikZ） | 结构化 |
| **编译速度** | 快 | 较慢 | 快-中等 |
| **最适合** | 学术会议 | 创意设计 | 多栏布局 |

**推荐**：
- 首次制作海报：**beamerposter**（熟悉、简单）
- 现代会议：**tikzposter**（美观、灵活）
- 复杂布局：**baposter**（自动定位）

## 使用示例

### 在 Scientific Writer CLI 中

```
> 为 NeurIPS 会议创建一个关于 Transformer 注意力机制的研究海报

助手将：
1. 询问海报尺寸和方向
2. 使用您的内容生成完整的 LaTeX 海报
3. 配置全页覆盖
4. 提供编译说明
5. 对生成的 PDF 进行质量检查
```

### 手动创建

```bash
# 1. 复制模板
cp assets/tikzposter_template.tex my_poster.tex

# 2. 编辑内容
vim my_poster.tex

# 3. 编译
pdflatex my_poster.tex

# 4. 审查
./scripts/review_poster.sh my_poster.pdf

# 5. 按 25% 比例试打印
# (A0 在 A4 纸上)

# 6. 最终印刷
```

## 成功技巧

### 内容策略
1. **一个主要信息**：观众应该记住的一件事是什么？
2. **3-5 个关键图表**：视觉内容为主
3. **300-800 字**：少即是多
4. **项目符号**：比段落更易浏览

### 设计策略
1. **高对比度**：深色浅底或浅色深底
2. **大字体**：正文 30pt+，从远处可读
3. **空白**：海报 30-40% 应为空
4. **视觉层次**：尺寸变化显著（标题为正文的 3 倍）

### 技术策略
1. **提前测试**：最终印刷前按 25% 比例打印
2. **矢量图形**：尽可能使用 PDF/SVG
3. **验证规格**：检查页面尺寸、字体、分辨率
4. **获取反馈**：印刷前请同事审查

## 其他资源

### 在线工具
- **颜色对比度检查器**：https://webaim.org/resources/contrastchecker/
- **色盲模拟器**：https://www.color-blindness.com/coblis-color-blindness-simulator/
- **配色生成器**：https://coolors.co/

### LaTeX 包
- `beamerposter`：扩展 Beamer 用于海报尺寸文档
- `tikzposter`：使用 TikZ 创建现代海报
- `baposter`：基于框的自动海报布局
- `qrcode`：在 LaTeX 中生成二维码
- `graphicx`：插入图像
- `tcolorbox`：彩色框和框架

### 进一步阅读
- `references/` 目录中的所有参考文档
- `assets/poster_quality_checklist.md` 中的质量检查清单
- `references/latex_poster_packages.md` 中的包对比

## 支持

如有问题或疑问：
- 查看 `references/` 中的参考文档
- 检查上方的故障排除部分
- 运行自动化审查：`./scripts/review_poster.sh`
- 使用质量检查清单：`assets/poster_quality_checklist.md`

## 版本

LaTeX 海报技能 v1.0
兼容：beamerposter、tikzposter、baposter
最后更新：2025 年 1 月
