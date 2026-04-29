# 演示文稿视觉审查工作流程

## 概述

视觉审查是演示文稿质量保证的关键步骤，使您能够在演示前识别并修复布局问题、文本溢出、元素重叠和设计问题。本指南涵盖将演示文稿转换为图像、系统化视觉检查、常见问题以及迭代改进策略。

## ⚠️ 关键规则：永远不要直接读取 PDF 演示文稿

**强制要求：始终先将演示文稿 PDF 转换为图像，然后再审查。**

### 此规则存在的原因

- **防止缓冲区溢出**：演示文稿 PDF（尤其是多幻灯片演示文稿）直接读取时会导致"JSON 消息超出最大缓冲区大小"错误
- **视觉准确性**：图像显示的内容与观众看到的内容完全一致，包括渲染问题
- **性能**：基于图像的审查比 PDF 文本提取更快、更可靠
- **一致性**：确保所有演示文稿采用统一的审查流程

### 演示文稿的唯一正确工作流程

1. ✅ 从 PowerPoint/Beamer 源文件生成 PDF
2. ✅ **使用 pdf_to_images.py 脚本将 PDF 转换为图像**
3. ✅ **系统化地审查图像文件**
4. ✅ 按幻灯片编号记录问题
5. ✅ 在源文件中修复问题
6. ✅ 重新生成 PDF 并重复

### 禁止事项

- ❌ 永远不要对演示文稿 PDF 使用 read_file 工具
- ❌ 永远不要尝试将 PDF 幻灯片作为文本读取
- ❌ 永远不要跳过图像转换步骤
- ❌ 永远不要假设 PDF "足够小"可以直接读取

**如果您正在审查演示文稿且尚未转换为图像，请停止并先进行转换。**

## 为什么视觉审查很重要

### 源文件中看不见的常见问题

**LaTeX Beamer 问题**：
- 文本框中的文本溢出
- 元素重叠（公式覆盖图像）
- 行分隔不良
- 图表超出幻灯片边界
- 实际分辨率下的字体大小问题

**PowerPoint 问题**：
- 文本被形状或幻灯片边缘裁剪
- 图像与文本重叠
- 幻灯片之间间距不一致
- 颜色渲染差异
- 字体替换问题

**投影问题**：
- 在笔记本电脑上可见的内容在投影时被裁剪
- 投影仪上颜色看起来不同
- 低对比度元素变得不可见
- 小细节消失

### 视觉审查的好处

- **及早发现布局错误**：在打印或演示前修复
- **验证可读性**：确保文本足够大、对比度足够高
- **检查一致性**：发现跨幻灯片的不一致问题
- **测试无障碍性**：验证颜色对比度和清晰度
- **验证设计**：确保专业外观

## 转换：PDF 转图像

### 方法 1：使用 pdf_to_images.py 脚本（推荐）

**无需外部依赖**：
该脚本使用 PyMuPDF，这是一个独立的 Python 库——无需 poppler 或其他系统软件。

**安装**：
```bash
# PyMuPDF 作为项目依赖包含
pip install pymupdf
```

**基本转换**：
```bash
# 将所有幻灯片转换为 JPEG 图像
python skills/scientific-slides/scripts/pdf_to_images.py presentation.pdf slide --dpi 150

# 生成：slide-001.jpg、slide-002.jpg、slide-003.jpg、...
```

**高分辨率转换**：
```bash
# 用于详细检查的更高质量（300 DPI）
python skills/scientific-slides/scripts/pdf_to_images.py presentation.pdf slide --dpi 300

# PNG 格式（无损，文件更大）
python skills/scientific-slides/scripts/pdf_to_images.py presentation.pdf slide --dpi 150 --format png
```

**转换特定幻灯片**：
```bash
# 仅幻灯片 5-10
python skills/scientific-slides/scripts/pdf_to_images.py presentation.pdf slide --dpi 150 --first 5 --last 10

# 单张幻灯片
python skills/scientific-slides/scripts/pdf_to_images.py presentation.pdf slide --dpi 150 --first 3 --last 3
```

**输出选项**：
```bash
# 不同的输出目录
python skills/scientific-slides/scripts/pdf_to_images.py presentation.pdf review/slide --dpi 150

# 自定义命名
python skills/scientific-slides/scripts/pdf_to_images.py presentation.pdf output/presentation --dpi 150
```

### 方法 2：使用 PowerPoint 缩略图脚本

对于 PowerPoint 演示文稿，使用 pptx skill 的缩略图工具：

```bash
# 创建缩略网格
python scripts/thumbnail.py presentation.pptx output --cols 4

# 单独幻灯片
python scripts/thumbnail.py presentation.pptx slides/slide --individual
```

**优点**：
- 针对 PowerPoint 文件优化
- 可以创建概览网格
- 直接处理 .pptx 格式
- 可自定义布局

### 方法 3：使用 ImageMagick

**安装**：
```bash
# Ubuntu/Debian
sudo apt-get install imagemagick

# macOS
brew install imagemagick
```

**转换**：
```bash
# 将 PDF 转换为图像
convert -density 150 presentation.pdf slide.jpg

# 更高质量
convert -density 300 presentation.pdf slide.jpg

# 特定格式
convert -density 150 presentation.pdf slide.png
```

### 方法 4：使用 Python（编程方式）

```python
import fitz  # PyMuPDF

# 打开 PDF
doc = fitz.open('presentation.pdf')

# 将每页转换为图像
zoom = 200 / 72  # 200 DPI（72 是基础 DPI）
matrix = fitz.Matrix(zoom, zoom)

for i, page in enumerate(doc, start=1):
    pixmap = page.get_pixmap(matrix=matrix)
    pixmap.save(f'slide-{i:03d}.jpg', output='jpeg')

doc.close()
```

**安装 PyMuPDF**：
```bash
pip install pymupdf
# 无需外部依赖！
```

## 系统化视觉检查

### 检查工作流程

**步骤 1：概览浏览**
- 快速查看所有幻灯片
- 记录整体一致性
- 识别明显有问题的幻灯片
- 创建需要详细审查的幻灯片列表

**步骤 2：详细检查**
- 仔细审查每个标记的幻灯片
- 根据问题清单进行检查（见下文）
- 用幻灯片编号记录具体问题
- 记录所需的修复

**步骤 3：跨幻灯片比较**
- 检查相似幻灯片之间的一致性
- 验证统一的间距和对齐
- 确保字体大小一致
- 检查配色方案的一致性

**步骤 4：距离测试**
- 以缩小尺寸查看图像（模拟投影）
- 检查从约 6 英尺的可读性
- 验证关键元素是否可见
- 测试主要信息是否清晰

### 问题清单

检查每张幻灯片的以下常见问题：

#### 文本问题

**溢出和截断**：
- [ ] 文本在幻灯片边缘被裁剪
- [ ] 文本超出文本框
- [ ] 公式延伸到页边距
- [ ] 标题在底部被裁剪
- [ ] 项目符号超出边界

**可读性**：
- [ ] 字体太小（最小 18pt 可见）
- [ ] 对比度差（文本与背景）
- [ ] 行间距不足
- [ ] 文本太靠近幻灯片边缘
- [ ] 文本行重叠

#### 元素重叠

**文本重叠**：
- [ ] 文本与图像重叠
- [ ] 文本与形状重叠
- [ ] 多个文本框重叠
- [ ] 标签与数据点重叠
- [ ] 标题与内容重叠

**视觉元素重叠**：
- [ ] 图像重叠
- [ ] 形状不适当重叠
- [ ] 图表延伸到页边距
- [ ] 图例与图表重叠
- [ ] 水印遮挡内容

#### 布局和间距

**对齐问题**：
- [ ] 文本框未对齐
- [ ] 页边距不均匀
- [ ] 元素定位不一致
- [ ] 标题未居中
- [ ] 项目符号未对齐

**间距问题**：
- [ ] 内容拥挤（空白空间不足）
- [ ] 空白过多（幻灯片区域使用不当）
- [ ] 元素之间间距不一致
- [ ] 多列布局中间隙不均匀
- [ ] 内容分布不良

#### 颜色和对比度

**可见性**：
- [ ] 对比度不足（文本与背景）
- [ ] 颜色太相似（难以区分）
- [ ] 文本在复杂背景上
- [ ] 浅色文本在浅色背景上
- [ ] 深色文本在深色背景上

**一致性**：
- [ ] 幻灯片之间配色方案不一致
- [ ] 颜色意外变化
- [ ] 颜色组合不协调
- [ ] 数据可视化的颜色选择不佳

#### 图表和图形

**质量**：
- [ ] 图像像素化或模糊
- [ ] 图表分辨率低
- [ ] 纵横比失真
- [ ] 截图质量差
- [ ] 图形边缘锯齿状

**布局**：
- [ ] 图表太小无法阅读
- [ ] 轴标签太小
- [ ] 图例文本难以辨认
- [ ] 复杂图表没有说明
- [ ] 图表未居中或未对齐

#### 技术问题

**渲染**：
- [ ] 字体缺失（被替换）
- [ ] 特殊字符不显示
- [ ] 公式渲染不正确
- [ ] 图像损坏或文件缺失
- [ ] 颜色不正确（RGB vs CMYK）

**一致性**：
- [ ] 幻灯片编号不正确或缺失
- [ ] 页眉/页脚不一致
- [ ] 导航元素损坏
- [ ] 超链接不工作（如果测试交互式）

## 文档模板

### 问题日志格式

创建电子表格或文档来跟踪所有问题：

```
幻灯片 # | 问题类别 | 描述 | 严重程度 | 状态
--------|---------------|-------------|----------|--------
3       | 文本溢出 | 项目符号 4 超出文本框 | 高 | 已修复
7       | 元素重叠 | 图表与标题重叠 | 高 | 已修复
12      | 字体大小 | 轴标签太小 | 中 | 已修复
15      | 对齐 | 标题未居中 | 低 | 已修复
22      | 对比度 | 黄色文本在白色背景上 | 高 | 已修复
```

**严重程度级别**：
- **严重**：使幻灯片无法使用或不专业
- **高**：显著影响可读性或外观
- **中**：可见但不妨碍理解
- **低**：轻微的美容问题

### 问题文档示例

**好的文档**：
```
幻灯片 8：文本溢出问题
- 描述：最后一个项目符号 "...implementation details" 
  超出文本框右边缘约 0.5 英寸
- 原因：项目符号文本太长，超出可用宽度
- 修复：将文本简化为 "...implementation" 或增加文本框宽度
- 验证：检查相邻幻灯片是否有类似问题
```

**差的文档**：
```
幻灯片 8：文本问题
- 修复：弄小一点
```

## 常见问题和解决方案

### 问题 1：文本溢出

**问题**：文本超出边界

**识别**：
- 边缘处可见文本被裁剪
- 文本延伸到页边距
- 可见部分字符

**解决方案**：

**LaTeX Beamer**：
```latex
% 减少文本
\begin{frame}{Title}
  \begin{itemize}
    \item 缩短这个长的项目符号
    % 或
    \item 使用缩写或首字母缩写
    % 或
    \item<alert@1> 拆分为多个项目符号
  \end{itemize}
\end{frame}

% 调整页边距
\newgeometry{margin=1.5cm}
\begin{frame}
  使用更宽边距的内容
\end{frame}
\restoregeometry

% 特定元素使用较小字体
{\small
  需要拟合的长文本
}
```

**PowerPoint**：
- 减少该元素的字体大小
- 缩短文本内容
- 增加文本框大小
- 谨慎使用文本框自动调整选项
- 拆分为多张幻灯片

### 问题 2：元素重叠

**问题**：元素不当地重叠

**识别**：
- 文本被图像遮挡
- 形状覆盖文本
- 图表重叠

**解决方案**：

**LaTeX Beamer**：
```latex
% 使用列更好地分离
\begin{columns}
  \begin{column}{0.5\textwidth}
    文本内容
  \end{column}
  \begin{column}{0.5\textwidth}
    \includegraphics[width=\textwidth]{figure.pdf}
  \end{column}
\end{columns}

% 添加间距
\vspace{0.5cm}

% 调整图表大小
includegraphics[width=0.7\textwidth]{figure.pdf}
```

**PowerPoint**：
- 使用对齐 guides 重新定位
- 减小元素大小
- 使用双列布局
- 发送元素向后/向前（图层）
- 增加元素之间的间距

### 问题 3：对比度差

**问题**：由于颜色选择，文本难以阅读

**识别**：
- 需要眯眼才能阅读文本
- 文本褪入背景
- 颜色太相似

**解决方案**：

**LaTeX Beamer**：
```latex
% 增加对比度
\setbeamercolor{fontsize}{fg=black,bg=white}
\setbeamercolor{normal text}{fg=black,bg=white}

% 使用更深的颜色
\definecolor{darkblue}{RGB}{0,50,100}
\setbeamercolor{structure}{fg=darkblue}

% 用灰度测试
\usepackage{xcolor}
\selectcolormodel{gray}  % 临时测试用
```

**PowerPoint**：
- 选择高对比度颜色组合
- 深色文本在浅色背景上或反之
- 避免使用 pastel 色调作为文本
- 使用 WebAIM 对比度检查器测试
- 如需要，添加文本背景框

### 问题 4：字体太小

**问题**：文本太小，从距离处无法阅读

**识别**：
- 从 3 英尺外无法阅读文本
- 正常查看时轴标签消失
- 标题难以辨认

**解决方案**：

**LaTeX Beamer**：
```latex
% 增加基础字体大小
\documentclass[14pt]{beamer}  # 而不是默认的 11pt

# 使用更大字体重新创建图表
# 在 matplotlib 中：
plt.rcParams['font.size'] = 18
plt.rcParams['axes.labelsize'] = 20

# 在 R/ggplot2 中：
theme_set(theme_minimal(base_size = 16))
```

**PowerPoint**：
- 正文文本最小 18pt，最好 24pt
- 使用更大的标签重新创建图表
- 直接使用标签而不是图例
- 简化复杂图表
- 将密集内容分散到多张幻灯片

### 问题 5：未对齐

**问题**：元素未正确对齐

**识别**：
- 页边距不均匀
- 标题位置不同
- 间距不规则

**解决方案**：

**LaTeX Beamer**：
```latex
% 使用一致的模板
\setbeamertemplate{fontsize}[default][center]

% 列顶部对齐
\begin{columns}[T]  % T = 顶部对齐
  \begin{column}{0.5\textwidth}
    内容
  \end{column}
  \begin{column}{0.5\textwidth}
    内容
  \end{column}
\end{columns}

% 图表居中
\begin{center}
  \includegraphics[width=0.8\textwidth]{figure.pdf}
\end{center}
```

**PowerPoint**：
- 使用对齐工具（左对齐/居中/右对齐）
- 启用网格线和 guides
- 使用对齐到网格
- 均匀分布对象
- 创建具有一致布局的母版幻灯片

## 迭代改进流程

### 工作流程循环

```
1. 生成 PDF
    ↓
2. 转换为图像
    ↓
3. 系统化视觉检查
    ↓
4. 记录问题
    ↓
5. 优先排序修复
    ↓
6. 对源文件应用修正
    ↓
7. 重新生成 PDF
    ↓
8. 重新检查（返回步骤 2）
    ↓
9. 当没有严重问题时完成
```

### 优先排序策略

**立即修复**（阻止演示）：
- 使内容无法阅读的文本溢出
- 遮挡数据的严重元素重叠
- 图表损坏或内容缺失
- 严重对比度差

**演示前修复**：
- 字体太小
- 中等对齐问题
- 间距不一致
- 中等对比度问题

**时间允许时修复**：
- 轻微未对齐
- 小间距不一致
- 美容改进
- 非关键颜色调整

### 停止标准

**最低标准**：
- [ ] 无文本溢出或截断
- [ ] 无遮挡内容的元素重叠
- [ ] 所有文本在最小 18pt 等效下可读
- [ ] 足够对比度（最低 4.5:1 比率）
- [ ] 图表和图像正确显示
- [ ] 幻灯片结构一致

**理想标准**：
- [ ] 整体专业外观
- [ ] 对齐和间距一致
- [ ] 高对比度（7:1 比率）
- [ ] 最佳字体大小（24pt+）
- [ ] 精美的视觉设计
- [ ] 零布局问题

## 自动检测策略

### 用于文本溢出检测的 Python 脚本

```python
from PIL import Image
import numpy as np

def detect_edge_content(image_path, threshold=10):
    """
    检测内容是否太靠近幻灯片边缘。
    如果检测到潜在溢出则返回 True。
    """
    img = Image.open(image_path).convert('L')  # 灰度
    arr = np.array(img)
    
    # 检查边缘（10 像素边框）
    left_edge = arr[:, :threshold]
    right_edge = arr[:, -threshold:]
    top_edge = arr[:threshold, :]
    bottom_edge = arr[-threshold:, :]
    
    # 寻找非白色像素（内容）
    white_threshold = 240
    
    issues = []
    if np.any(left_edge < white_threshold):
        issues.append("左边缘")
    if np.any(right_edge < white_threshold):
        issues.append("右边缘")
    if np.any(top_edge < white_threshold):
        issues.append("上边缘")
    if np.any(bottom_edge < white_threshold):
        issues.append("下边缘")
    
    return issues

# 使用方法
for slide_num in range(1, 26):
    issues = detect_edge_content(f'slide-{slide_num}.jpg')
    if issues:
        print(f"幻灯片 {slide_num}: 内容靠近 {', '.join(issues)}")
```

### 对比度检查

```python
from PIL import Image
import numpy as np

def check_contrast(image_path):
    """
    估计图像中的对比度比率。
    简单版本：比较最亮和最暗的区域。
    """
    img = Image.open(image_path).convert('L')
    arr = np.array(img)
    
    # 获取亮度值
    bright = np.percentile(arr, 95)
    dark = np.percentile(arr, 5)
    
    # 粗略对比度比率
    contrast = (bright + 0.05) / (dark + 0.05)
    
    if contrast < 4.5:
        return f"低对比度: {contrast:.1f}:1（最低 4.5:1）"
    return f"正常: {contrast:.1f}:1"

# 使用方法
for slide_num in range(1, 26):
    result = check_contrast(f'slide-{slide_num}.jpg')
    print(f"幻灯片 {slide_num}: {result}")
```

## 手动审查最佳实践

### 审查环境

**设置**：
- 大显示器或双显示器
- 良好的照明（不太亮，也不暗）
- 无干扰的环境
- 具有缩放功能的图像查看器
- 记事本或电子表格用于跟踪问题

**查看选项**：
- 100% 比例查看以进行详细检查
- 50% 比例查看以模拟距离
- 顺序查看以检查一致性
- 并排比较相似幻灯片

### 审查技巧

**新鲜眼光**：
- 每 15-20 张幻灯片休息一下
- 在一天中的不同时间审查
- 让同事审查
- 第二天回来进行最终检查

**系统化方法**：
- 按顺序审查（幻灯片 1 → 结束）
- 一次专注于一种问题类型
- 使用清单确保彻底性
- 边记录边记录，不要靠记忆

**常见遗漏**：
- 备用幻灯片（也要审查！）
- 标题幻灯片（第一印象很重要）
- 致谢幻灯片（经常被遗忘）
- 最后一张幻灯片（问答环节可见）

## 工具和资源

### 推荐软件

**PDF 转图像转换**：
- **PyMuPDF**（Python）：快速，无外部依赖（推荐）
- **pdf_to_images.py 脚本**：易于使用的 CLI 封装器
- **ImageMagick**：灵活，选项多（可选）

**图像查看**：
- **IrfanView**（Windows）：快速，支持多种格式
- **Preview**（macOS）：内置，简单
- **Eye of GNOME**（Linux）：轻量级
- **XnView**：跨平台，批量操作

**问题跟踪**：
- **电子表格**（Excel、Google Sheets）：简单，灵活
- **Markdown 文件**：版本控制友好
- **问题跟踪器**（GitHub、Jira）：如果团队协作
- **清单应用**：用于移动审查

### 对比度检查器

- **WebAIM 对比度检查器**：https://webaim.org/resources/contrastchecker/
- **色彩对比度分析器**：桌面应用程序
- **Chrome DevTools**：内置对比度检查

### 色盲模拟器

- **Coblis**：https://www.color-blindness.com/coblis-color-blindness-simulator/
- **Color Oracle**：免费桌面应用程序
- **Photoshop/GIMP**：内置色盲滤镜

## 总结清单

在最终确定您的演示文稿之前：

**转换**：
- [ ] PDF 以足够分辨率（150-300 DPI）转换为图像
- [ ] 所有幻灯片都已转换（包括备用幻灯片）
- [ ] 图像保存在有组织的目录中

**视觉检查**：
- [ ] 系统化地审查了所有幻灯片
- [ ] 每张幻灯片都完成了问题清单
- [ ] 用幻灯片编号记录了问题
- [ ] 为每个问题分配了严重程度

**问题解决**：
- [ ] 修复了严重问题
- [ ] 解决了高优先级问题
- [ ] 更新了源文件（不仅是 PDF）
- [ ] 重新生成并重新检查

**最终验证**：
- [ ] 无文本溢出或截断
- [ ] 无不当的元素重叠
- [ ] 整个演示文稿有足够的对比度
- [ ] 布局和间距一致
- [ ] 专业外观
- [ ] 准备好投影或分发

**测试**：
- [ ] 如果可能，在投影仪上测试
- [ ] 从房间后部距离查看
- [ ] 在各种照明条件下检查
- [ ] 保存了备份副本
