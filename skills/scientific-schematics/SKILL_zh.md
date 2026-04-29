---
name: scientific-schematics
description: 使用Nano Banana 2 AI创建具有智能迭代优化的出版级科学示意图。利用Gemini 3.1 Pro Preview进行质量审核。仅当质量低于您文档类型的阈值时才重新生成。擅长神经网络架构、系统图、流程图、生物通路和复杂的科学可视化。
allowed-tools: Read Write Edit Bash
license: MIT license
metadata:
    skill-author: K-Dense Inc.
---

# 科学示意图与图表

## 概述

科学示意图和图表将复杂概念转化为清晰的视觉表达，用于出版。**本技能使用Nano Banana 2 AI生成图表，并由Gemini 3.1 Pro Preview进行质量审核。**

**工作原理：**
- 用自然语言描述您的图表
- Nano Banana 2自动生成出版级质量的图像
- **Gemini 3.1 Pro Preview根据文档类型阈值审查质量**
- **智能迭代**：仅当质量低于阈值时才重新生成
- 几分钟内即可获得出版就绪的输出
- 无需编码、模板或手动绘图

**按文档类型的质量阈值：**
| 文档类型 | 阈值 | 描述 |
|----------|------|------|
| journal | 8.5/10 | 《自然》《科学》等同行评审期刊 |
| conference | 8.0/10 | 会议论文 |
| thesis | 8.0/10 | 博士/硕士论文 |
| grant | 8.0/10 | 基金申请书 |
| preprint | 7.5/10 | arXiv、bioRxiv等 |
| report | 7.5/10 | 技术报告 |
| poster | 7.0/10 | 学术海报 |
| presentation | 6.5/10 | 幻灯片、演讲 |
| default | 7.5/10 | 通用 |

**只需描述您想要的图表，Nano Banana 2便会创建。** 所有图表存储在figures/子文件夹中，并在论文/海报中引用。

## 快速开始：生成任意图表

只需描述即可创建任意科学图表。Nano Banana 2通过**智能迭代**自动处理一切：

```bash
# 为期刊论文生成（最高质量阈值：8.5/10）
python scripts/generate_schematic.py "CONSORT participant flow diagram with 500 screened, 150 excluded, 350 randomized" -o figures/consort.png --doc-type journal

# 为演示文稿生成（较低阈值：6.5/10 - 更快）
python scripts/generate_schematic.py "Transformer encoder-decoder architecture showing multi-head attention" -o figures/transformer.png --doc-type presentation

# 为海报生成（中等阈值：7.0/10）
python scripts/generate_schematic.py "MAPK signaling pathway from EGFR to gene transcription" -o figures/mapk_pathway.png --doc-type poster

# 自定义最大迭代次数（最多2次）
python scripts/generate_schematic.py "Complex circuit diagram with op-amp, resistors, and capacitors" -o figures/circuit.png --iterations 2 --doc-type journal
```

**幕后发生了什么：**
1. **第一次生成**：Nano Banana 2按照科学图表最佳实践创建初始图像
2. **第一次审核**：**Gemini 3.1 Pro Preview**根据文档类型阈值评估质量
3. **决策**：如果质量 >= 阈值 → **完成**（无需更多迭代！）
4. **如果低于阈值**：根据评价改进提示词，重新生成
5. **重复**：直到质量达到阈值或达到最大迭代次数

**智能迭代的优势：**
- ✅ 如果第一次生成足够好，可以节省API调用
- ✅ 对期刊论文有更高的质量标准
- ✅ 演示文稿/海报的周转更快
- ✅ 针对不同用例提供适当质量

**输出**：带版本号的图像以及详细的审核日志，包含质量评分、评价和提前停止信息。

### 配置

设置您的OpenRouter API密钥：
```bash
export OPENROUTER_API_KEY='your_api_key_here'
```

在以下地址获取API密钥：https://openrouter.ai/keys

### AI生成最佳实践

**科学图表的有效提示词：**

✓ **优质提示词**（具体、详细）：
- "显示参与者从筛选（n=500）到随机化再到最终分析的CONSORT流程图"
- "左侧为编码器堆叠、右侧为解码器堆叠的Transformer神经网络架构，显示多头注意力和交叉注意力连接"
- "生物信号级联反应：EGFR受体 → RAS → RAF → MEK → ERK → 细胞核，标注磷酸化步骤"
- "物联网系统框图：传感器 → 微控制器 → WiFi模块 → 云服务器 → 移动应用"

✗ **避免模糊的提示词**：
- "制作流程图"（太笼统）
- "神经网络"（哪种类型？什么组件？）
- "通路图"（什么通路？什么分子？）

**需包含的关键要素：**
- **类型**：流程图、架构图、通路图、电路图等
- **组件**：需包含的具体元素
- **流向/方向**：元素如何连接（从左到右、从上到下）
- **标签**：需包含的关键注释或文本
- **样式**：任何特定的视觉要求

**科学质量指南**（自动应用）：
- 干净的白色/浅色背景
- 高对比度以保证可读性
- 清晰可读的标签（最小10磅）
- 专业字体（无衬线字体）
- 色盲友好颜色（Okabe-Ito调色板）
- 适当间距防止拥挤
- 必要时添加比例尺、图例、坐标轴

## 何时使用本技能

在以下情况下使用本技能：
- 创建神经网络架构图（Transformer、CNN、RNN等）
- 展示系统架构和数据流图
- 绘制研究设计的方法流程图（CONSORT、PRISMA）
- 可视化算法工作流程和处理流水线
- 创建电路图和电气原理图
- 描绘生物通路和分子相互作用
- 生成网络拓扑和层次结构
- 展示概念框架和理论模型
- 设计技术论文中的框图

## 如何使用本技能

**只需用自然语言描述您的图表。** Nano Banana 2会自动生成：

```bash
python scripts/generate_schematic.py "your diagram description" -o output.png
```

**就是这样！** AI会处理：
- ✓ 布局和构图
- ✓ 标签和注释
- ✓ 颜色和样式
- ✓ 质量审核和优化
- ✓ 出版就绪的输出

**适用于所有图表类型：**
- 流程图（CONSORT、PRISMA等）
- 神经网络架构
- 生物通路
- 电路图
- 系统架构
- 框图
- 任何科学可视化

**无需编码、无需模板、无需手动绘图。**

---

# AI生成模式（Nano Banana 2 + Gemini 3.1 Pro Preview审核）

## 智能迭代优化工作流程

AI生成系统使用**智能迭代**——仅当质量低于您文档类型的阈值时才重新生成：

### 智能迭代如何运作

```
┌─────────────────────────────────────────────────────┐
│  1. 使用Nano Banana 2生成图像                     │
│                    ↓                                │
│  2. 使用Gemini 3.1 Pro Preview审核质量             │
│                    ↓                                │
│  3. 评分 >= 阈值？                                  │
│       是 → 完成！（提前停止）                       │
│       否 → 改进提示词，返回第1步                   │
│                    ↓                                │
│  4. 重复直到质量达标或达到最大迭代次数            │
└─────────────────────────────────────────────────────┘
```

### 迭代1：初始生成
**提示词构建：**
```
科学图表指南 + 用户需求
```

**输出：** `diagram_v1.png`

### Gemini 3.1 Pro Preview质量审核

Gemini 3.1 Pro Preview根据以下方面评估图表：
1. **科学准确性**（0-2分）- 正确的概念、符号、关系
2. **清晰度和可读性**（0-2分）- 易于理解，层次清晰
3. **标签质量**（0-2分）- 完整、可读、一致的标签
4. **布局和构图**（0-2分）- 逻辑流程、均衡、无重叠
5. **专业外观**（0-2分）- 出版就绪的质量

**示例审核输出：**
```
评分：8.0

优点：
- 从上到下的流程清晰
- 所有阶段均正确标注
- 专业字体

问题：
- 参与者数量字体略小
- 排除框有轻微重叠

判定：可接受（针对海报，阈值7.0）
```

### 决策点：继续还是停止？

| 如果评分... | 行动 |
|-------------|------|
| >= 阈值 | **停止** - 质量对于此文档类型足够好 |
| < 阈值 | 使用改进的提示词继续下一次迭代 |

**示例：**
- 对于**海报**（阈值7.0）：评分7.5 → **1次迭代后完成！**
- 对于**期刊**（阈值8.5）：评分7.5 → 继续改进

### 后续迭代（仅在需要时）

如果质量低于阈值，系统会：
1. 从Gemini 3.1 Pro Preview的审核中提取具体问题
2. 添加改进指令增强提示词
3. 使用Nano Banana 2重新生成
4. 再次使用Gemini 3.1 Pro Preview审核
5. 重复直到达到阈值或达到最大迭代次数

### 审核日志
所有迭代都会保存为一个JSON审核日志，包含提前停止信息：
```json
{
  "user_prompt": "CONSORT participant flow diagram...",
  "doc_type": "poster",
  "quality_threshold": 7.0,
  "iterations": [
    {
      "iteration": 1,
      "image_path": "figures/consort_v1.png",
      "score": 7.5,
      "needs_improvement": false,
      "critique": "SCORE: 7.5\nSTRENGTHS:..."
    }
  ],
  "final_score": 7.5,
  "early_stop": true,
  "early_stop_reason": "Quality score 7.5 meets threshold 7.0 for poster"
}
```

**注意：**使用智能迭代，如果提前达到质量要求，可能只会看到1次迭代而不是完整的2次迭代！

## 高级AI生成用法

### Python API

```python
from scripts.generate_schematic_ai import ScientificSchematicGenerator

# 初始化生成器
generator = ScientificSchematicGenerator(
    api_key="your_openrouter_key",
    verbose=True
)

# 使用迭代优化生成（最多2次迭代）
results = generator.generate_iterative(
    user_prompt="Transformer architecture diagram",
    output_path="figures/transformer.png",
    iterations=2
)

# 查看结果
print(f"Final score: {results['final_score']}/10")
print(f"Final image: {results['final_image']}")

# 审查每次迭代
for iteration in results['iterations']:
    print(f"Iteration {iteration['iteration']}: {iteration['score']}/10")
    print(f"Critique: {iteration['critique']}")
```

### 命令行选项

```bash
# 基本用法（默认阈值7.5/10）
python scripts/generate_schematic.py "diagram description" -o output.png

# 指定文档类型以获得相应的质量阈值
python scripts/generate_schematic.py "diagram" -o out.png --doc-type journal      # 8.5/10
python scripts/generate_schematic.py "diagram" -o out.png --doc-type conference   # 8.0/10
python scripts/generate_schematic.py "diagram" -o out.png --doc-type poster       # 7.0/10
python scripts/generate_schematic.py "diagram" -o out.png --doc-type presentation # 6.5/10

# 自定义最大迭代次数（1-2次）
python scripts/generate_schematic.py "complex diagram" -o diagram.png --iterations 2

# 详细输出（查看所有API调用和审核）
python scripts/generate_schematic.py "flowchart" -o flow.png -v

# 通过参数提供API密钥
python scripts/generate_schematic.py "diagram" -o out.png --api-key "sk-or-v1-..."

# 组合选项
python scripts/generate_schematic.py "neural network" -o nn.png --doc-type journal --iterations 2 -v
```

### 提示词工程技巧

**1. 明确布局：**
```
✓ "垂直流向，从上到下的流程图"
✓ "左侧编码器、右侧解码器的架构图"
✓ "顺时针流动的环形通路图"
```

**2. 包含定量细节：**
```
✓ "具有输入层（784个节点）、隐藏层（128个节点）、输出层（10个节点）的神经网络"
✓ "显示n=500筛选、n=150排除、n=350随机化的流程图"
✓ "包含1kΩ电阻、10µF电容、5V电源的电路"
```

**3. 指定视觉风格：**
```
✓ "线条简洁的极简框图"
✓ "带有蛋白质结构的详细生物通路"
✓ "带有工程符号的技术原理图"
```

**4. 请求特定标签：**
```
✓ "在所有箭头上标注激活/抑制"
✓ "在每个框中包含层尺寸"
✓ "用时间戳显示时间进程"
```

**5. 提及颜色要求：**
```
✓ "使用色盲友好颜色"
✓ "兼容灰度的设计"
✓ "按功能色编码：蓝色表示输入，绿色表示处理，红色表示输出"
```

## AI生成示例

### 示例1：CONSORT流程图
```bash
python scripts/generate_schematic.py \
  "随机对照试验的CONSORT参与者流程图。 \
   顶部以'评估资格（n=500）'开始。 \
   显示'排除（n=150）'及其原因：年龄<18（n=80），拒绝（n=50），其他（n=20）。 \
   然后'随机分配（n=350）'分为两组： \
   '治疗组（n=175）'和'对照组（n=175）'。 \
   每组显示'失访'（n=15和n=10）。 \
   最终显示'分析'（n=160和n=165）。 \
   使用蓝色框表示过程步骤，橙色表示排除，绿色表示最终分析。" \
  -o figures/consort.png
```

### 示例2：神经网络架构
```bash
python scripts/generate_schematic.py \
  "Transformer编码器-解码器架构图。 \
   左侧：编码器堆叠，包含输入嵌入、位置编码、 \
   多头自注意力、加与归一化、前馈网络、加与归一化。 \
   右侧：解码器堆叠，包含输出嵌入、位置编码、 \
   掩码自注意力、加与归一化、交叉注意力（接收来自编码器的信息）、 \
   加与归一化、前馈网络、加与归一化、线性与softmax。 \
   用虚线显示编码器到解码器的交叉注意力连接。 \
   编码器使用浅蓝色，解码器使用浅红色。 \
   清晰标注所有组件。" \
  -o figures/transformer.png --iterations 2
```

### 示例3：生物通路
```bash
python scripts/generate_schematic.py \
  "MAPK信号通路图。 \
   以细胞膜上的EGFR受体开始（顶部）。 \
   箭头向下到RAS（标注GTP）。 \
   箭头到RAF激酶。 \
   箭头到MEK激酶。 \
   箭头到ERK激酶。 \
   最终箭头指向细胞核，表示基因转录。 \
   每条箭头上标注'磷酸化'或'激活'。 \
   使用圆角矩形表示蛋白质，不同颜色区分。 \
   顶部包含细胞膜边界线。" \
  -o figures/mapk_pathway.png
```

### 示例4：系统架构
```bash
python scripts/generate_schematic.py \
  "物联网系统架构框图。 \
   底层：传感器（温度、湿度、运动）用绿色框。 \
   中层：微控制器（ESP32）用蓝色框。 \
   连接到WiFi模块（橙色框）和显示屏（紫色框）。 \
   顶层：云服务器（灰色框）连接到移动应用（浅蓝色框）。 \
   在所有组件之间显示数据流箭头。 \
   用协议标注连接：I2C、UART、WiFi、HTTPS。" \
  -o figures/iot_architecture.png
```

---

## 命令行用法

生成科学示意图的主要入口点：

```bash
# 基本用法
python scripts/generate_schematic.py "diagram description" -o output.png

# 自定义迭代次数（最多2次）
python scripts/generate_schematic.py "complex diagram" -o diagram.png --iterations 2

# 详细模式
python scripts/generate_schematic.py "diagram" -o out.png -v
```

**注意：**Nano Banana 2 AI生成系统在其迭代优化过程中包含了自动质量审核。每次迭代都会评估科学准确性、清晰度和可访问性。

## 最佳实践总结

### 设计原则

1. **清晰优于复杂** - 简化，移除不必要的元素
2. **一致的风格** - 使用模板和样式文件
3. **色盲无障碍** - 使用Okabe-Ito调色板，冗余编码
4. **合适的字体** - 无衬线字体，最小7-8磅
5. **矢量格式** - 出版时始终使用PDF/SVG

### 技术要求

1. **分辨率** - 优先矢量格式，光栅图像需300+ DPI
2. **文件格式** - LaTeX用PDF，网页用SVG，PNG作为备用
3. **色彩空间** - 数字用RGB，印刷用CMYK（必要时转换）
4. **线宽** - 最小0.5磅，通常1-2磅
5. **文本大小** - 最终尺寸下最小7-8磅

### 整合指南

1. **在LaTeX中使用** - 对生成的图像使用 `\includegraphics{}`
2. **全面标注标题** - 描述所有元素和缩写
3. **在正文中引用** - 在叙述中解释图表
4. **保持一致性** - 论文中所有图表使用相同风格
5. **版本控制** - 将提示词和生成的图像保存在仓库中

## 常见问题排查

### AI生成问题

**问题**：文本或元素重叠
- **解决方案**：AI生成会自动处理间距
- **解决方案**：增加迭代次数以获得更好的优化：`--iterations 2`

**问题**：元素连接不正确
- **解决方案**：在提示词中更具体地说明连接和布局
- **解决方案**：增加迭代次数以获得更好的优化

### 图像质量问题

**问题**：导出质量差
- **解决方案**：AI生成会自动生成高质量图像
- **解决方案**：增加迭代次数以获得更好的结果：`--iterations 2`

**问题**：生成后元素重叠
- **解决方案**：AI生成会自动处理间距
- **解决方案**：增加迭代次数：`--iterations 2` 以获得更好的优化
- **解决方案**：在提示词中更具体地说明布局和间距要求

### 质量检查问题

**问题**：误报重叠检测
- **解决方案**：调整阈值：`detect_overlaps(image_path, threshold=0.98)`
- **解决方案**：在可视化报告中手动审查标记区域

**问题**：生成的图像质量低
- **解决方案**：AI生成默认输出高质量图像
- **解决方案**：增加迭代次数以获得更好的结果：`--iterations 2`

**问题**：色盲模拟显示对比度差
- **解决方案**：在代码中显式切换到Okabe-Ito调色板
- **解决方案**：添加冗余编码（形状、图案、线型）
- **解决方案**：增加颜色饱和度和亮度差异

**问题**：检测到高严重性重叠
- **解决方案**：查看overlap_report.json获取确切位置
- **解决方案**：在这些特定区域增加间距
- **解决方案**：调整参数后重新运行并再次验证

**问题**：可视化报告生成失败
- **解决方案**：检查Pillow和matplotlib安装
- **解决方案**：确保图像文件可读：`Image.open(path).verify()`
- **解决方案**：检查磁盘空间是否足够生成报告

### 可访问性问题

**问题**：灰度下颜色无法区分
- **解决方案**：运行可访问性检查器：`verify_accessibility(image_path)`
- **解决方案**：添加图案、形状或线型作为冗余标识
- **解决方案**：增加相邻元素之间的对比度

**问题**：打印时文本太小
- **解决方案**：运行分辨率验证器：`validate_resolution(image_path)`
- **解决方案**：以最终尺寸设计，使用最小7-8磅字体
- **解决方案**：在分辨率报告中检查物理尺寸

**问题**：可访问性检查持续失败
- **解决方案**：查看accessibility_report.json了解具体失败项目
- **解决方案**：将颜色对比度提高至少20%
- **解决方案**：在定稿前用实际灰度转换进行测试

## 资源与参考

### 详细参考

加载这些文件以获取特定主题的全面信息：

- **`references/best_practices.md`** - 出版标准和可访问性指南

### 外部资源

**Python库**
- Schemdraw文档：https://schemdraw.readthedocs.io/
- NetworkX文档：https://networkx.org/documentation/
- Matplotlib文档：https://matplotlib.org/

**出版标准**
- Nature图表指南：https://www.nature.com/nature/for-authors/final-submission
- Science图表指南：https://www.science.org/content/page/instructions-preparing-initial-manuscript
- CONSORT图表：http://www.consort-statement.org/consort-statement/flow-diagram

## 与其他技能的集成

本技能与以下技能协同工作：

- **科学写作** - 图表遵循图表最佳实践
- **科学可视化** - 共享调色板和样式
- **LaTeX海报** - 为海报展示生成图表
- **研究基金申请** - 提案中的方法示意图
- **同行评审** - 评估图表的清晰度和可访问性

## 快速参考清单

在提交图表之前，请验证：

### 视觉质量
- [ ] 高质量图像格式（AI生成PNG）
- [ ] 无重叠元素（AI自动处理）
- [ ] 所有组件之间有适当间距（AI优化）
- [ ] 干净、专业的对齐
- [ ] 所有箭头正确连接到预期目标

### 可访问性
- [ ] 使用色盲安全调色板（Okabe-Ito）
- [ ] 在灰度下可用（经可访问性检查器测试）
- [ ] 元素之间有足够的对比度（已验证）
- [ ] 在适当时使用冗余编码（形状 + 颜色）
- [ ] 色盲模拟通过所有检查

### 字体和可读性
- [ ] 文本最终尺寸下最小7-8磅
- [ ] 所有元素标签清晰完整
- [ ] 字体族和大小一致
- [ ] 无文本重叠或截断
- [ ] 适用时包含单位

### 出版标准
- [ ] 与稿件中其他图形风格一致
- [ ] 撰写全面的标题，定义所有缩写
- [ ] 在稿件正文中适当引用
- [ ] 符合期刊特定的尺寸要求
- [ ] 以期刊要求的格式导出（PDF/EPS/TIFF）

### 质量验证（必需）
- [ ] 运行 `run_quality_checks()` 并获得PASS状态
- [ ] 审查重叠检测报告（零高严重性重叠）
- [ ] 通过可访问性验证（灰度和色盲）
- [ ] 在目标DPI（印刷300+）下验证分辨率
- [ ] 生成并审查视觉质量报告
- [ ] 所有质量报告与图形文件一起保存

### 文档和版本控制
- [ ] 源文件（.tex、.py）已保存以供将来修改
- [ ] 质量报告存档在 `quality_reports/` 目录中
- [ ] 记录配置参数（颜色、间距、大小）
- [ ] Git提交包含源文件、输出和质量报告
- [ ] README或注释说明如何重新生成图表

### 最终集成检查
- [ ] 图表在编译的稿件中正确显示
- [ ] 交叉引用有效（`\ref{}` 指向正确的图表）
- [ ] 图表编号与正文引用匹配
- [ ] 标题出现在图表相关的正确页面上
- [ ] 无与图表相关的编译警告或错误

## 环境设置

```bash
# 必需的
export OPENROUTER_API_KEY='your_api_key_here'

# 在以下地址获取密钥：https://openrouter.ai/keys
```

## 入门指南

**最简单的用法：**
```bash
python scripts/generate_schematic.py "your diagram description" -o output.png
```

---

使用本技能创建清晰、可访问、出版质量的图表，有效传达复杂的科学概念。由AI驱动的工作流程配合迭代优化，确保图表达到专业标准。
