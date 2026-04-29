---
name: infographics
description: "Create professional infographics using Nano Banana Pro AI with smart iterative refinement. Uses Gemini 3 Pro for quality review. Integrates research-lookup and web search for accurate data. Supports 10 infographic types, 8 industry styles, and colorblind-safe palettes."
allowed-tools: [Read, Write, Edit, Bash]
---

# 信息图

## 概述

信息图是信息、数据或知识的可视化呈现，旨在快速清晰地展示复杂内容。**此技能使用 Nano Banana Pro AI 生成信息图，结合 Gemini 3 Pro 质量审查和 Perplexity Sonar 进行研究。**

**工作原理：**
- （可选）**研究阶段**：使用 Perplexity Sonar 收集准确的事实和数据
- 用自然语言描述您的信息图
- Nano Banana Pro 自动生成出版级质量的信息图
- **Gemini 3 Pro 根据文档类型阈值审查质量**
- **智能迭代**：仅在质量低于阈值时重新生成
- 几分钟内输出专业成品
- 无需设计技能

**各文档类型的质量阈值：**
| 文档类型 | 阈值 | 描述 |
|---------------|-----------|-------------|
| marketing | 8.5/10 | 营销材料 - 必须具有吸引力 |
| report | 8.0/10 | 商业报告 - 专业质量 |
| presentation | 7.5/10 | 幻灯片、演讲 - 清晰且引人入胜 |
| social | 7.0/10 | 社交媒体内容 |
| internal | 7.0/10 | 内部使用 |
| draft | 6.5/10 | 工作草稿 |
| default | 7.5/10 | 通用目的 |

**只需描述您想要什么，Nano Banana Pro 就会创建它。**

## 快速开始

只需描述即可生成任何信息图：

```bash
# 生成列表型信息图（默认阈值 7.5/10）
python skills/infographics/scripts/generate_infographic.py \
  "5 benefits of regular exercise" \
  -o figures/exercise_benefits.png --type list

# 为营销生成（最高阈值：8.5/10）
python skills/infographics/scripts/generate_infographic.py \
  "Product features comparison" \
  -o figures/product_comparison.png --type comparison --doc-type marketing

# 使用企业风格生成
python skills/infographics/scripts/generate_infographic.py \
  "Company milestones 2010-2025" \
  -o figures/timeline.png --type timeline --style corporate

# 使用色盲安全调色板生成
python skills/infographics/scripts/generate_infographic.py \
  "Heart disease statistics worldwide" \
  -o figures/health_stats.png --type statistical --palette wong

# 带研究功能生成，获取准确最新数据
python skills/infographics/scripts/generate_infographic.py \
  "Global AI market size and growth projections" \
  -o figures/ai_market.png --type statistical --research
```

**后台执行流程：**
1. **（可选）研究**：Perplexity Sonar 收集准确的事实、统计数据和数据
2. **生成 1**：Nano Banana Pro 根据设计最佳实践创建初始信息图
3. **审查 1**：**Gemini 3 Pro** 根据文档类型阈值评估质量
4. **决策**：如果质量 >= 阈值 → **完成**（无需更多迭代！）
5. **如果低于阈值**：根据批评改进提示词，重新生成
6. **重复**：直到质量达到阈值或达到最大迭代次数

**智能迭代的优势：**
- ✅ 如果首次生成足够好，可节省 API 调用
- ✅ 营销材料更高的质量标准
- ✅ 草稿/内部使用更快的周转时间
- ✅ 根据不同使用场景设置适当的质量

**输出**：带版本号的图像以及详细的审查日志，包含质量分数、批评和提前停止信息。

## 何时使用此技能

在以下情况下使用 **infographics** 技能：
- 以可视化格式呈现数据或统计数据
- 为项目里程碑或历史创建时间线可视化
- 解释流程、工作流程或分步指南
- 并排比较选项、产品或概念
- 以引人入胜的可视化格式总结要点
- 创建地理或基于地图的数据可视化
- 构建层级或组织结构图
- 设计社交媒体内容或营销材料

**请改用 scientific-schematics：**
- 技术流程图和电路图
- 生物途径和分子图
- 神经网络架构图
- CONSORT/PRISMA 方法流程图

---

## 研究集成

### 自动数据收集（`--research`）

创建需要准确、最新数据的信息图时，使用 `--research` 标志自动使用 **Perplexity Sonar Pro** 收集事实和统计数据。

```bash
# 研究并生成统计信息图
python skills/infographics/scripts/generate_infographic.py \
  "Global renewable energy adoption rates by country" \
  -o figures/renewable_energy.png --type statistical --research

# 为时间线信息图进行研究
python skills/infographics/scripts/generate_infographic.py \
  "History of artificial intelligence breakthroughs" \
  -o figures/ai_history.png --type timeline --research

# 为比较信息图进行研究
python skills/infographics/scripts/generate_infographic.py \
  "Electric vehicles vs hydrogen vehicles comparison" \
  -o figures/ev_hydrogen.png --type comparison --research
```

### 研究提供的内容

研究阶段自动完成：

1. **收集关键事实**：关于主题的 5-8 个相关事实和统计数据
2. **提供背景**：准确呈现所需的背景信息
3. **查找数据点**：具体数字、百分比和日期
4. **引用来源**：提及主要研究或来源
5. **优先近期**：聚焦 2023-2026 年的信息

### 何时使用研究

**启用研究（`--research`）适用于：**
- 需要准确数字的统计信息图
- 市场数据、行业统计数据或趋势
- 科学或医学信息
- 当前事件或最新发展
- 任何准确性至关重要的主题

**跳过研究适用于：**
- 简单的概念信息图
- 内部流程文档
- 您在提示词中提供所有数据的主题
- 速度优先的生成

### 研究输出

启用研究后，将创建额外的文件：
- `{name}_research.json` - 原始研究数据和来源
- 研究内容会自动整合到信息图提示词中

---

## 信息图类型

### 1. 统计/数据驱动（`--type statistical`）

最适合：展示数字、百分比、调查结果和定量数据。

**关键元素：** 图表（柱状、饼图、折线、环形）、大号数字展示、数据比较、趋势指标。

```bash
python skills/infographics/scripts/generate_infographic.py \
  "Global internet usage 2025: 5.5 billion users (68% of population), \
   Asia Pacific 53%, Europe 15%, Americas 20%, Africa 12%" \
  -o figures/internet_stats.png --type statistical --style technology
```

---

### 2. 时间线（`--type timeline`）

最适合：历史事件、项目里程碑、公司历史、概念演变。

**关键元素：** 时间顺序流、日期标记、事件节点、连接线。

```bash
python skills/infographics/scripts/generate_infographic.py \
  "History of AI: 1950 Turing Test, 1956 Dartmouth Conference, \
   1997 Deep Blue, 2016 AlphaGo, 2022 ChatGPT" \
  -o figures/ai_history.png --type timeline --style technology
```

---

### 3. 流程/操作指南（`--type process`）

最适合：分步说明、工作流程、程序、教程。

**关键元素：** 编号步骤、方向箭头、操作图标、清晰流程。

```bash
python skills/infographics/scripts/generate_infographic.py \
  "How to start a podcast: 1. Choose your niche, 2. Plan content, \
   3. Set up equipment, 4. Record episodes, 5. Publish and promote" \
  -o figures/podcast_process.png --type process --style marketing
```

---

### 4. 比较（`--type comparison`）

最适合：产品比较、优缺点、之前/之后、选项评估。

**关键元素：** 并排布局、匹配类别、对勾/叉号指示。

```bash
python skills/infographics/scripts/generate_infographic.py \
  "Electric vs Gas Cars: Fuel cost (lower vs higher), \
   Maintenance (less vs more), Range (improving vs established)" \
  -o figures/ev_comparison.png --type comparison --style nature
```

---

### 5. 列表/信息型（`--type list`）

最适合：提示、事实、要点、摘要、快速参考指南。

**关键元素：** 编号或项目符号点、图标、清晰层级。

```bash
python skills/infographics/scripts/generate_infographic.py \
  "7 Habits of Highly Effective People: Be Proactive, \
   Begin with End in Mind, Put First Things First, Think Win-Win, \
   Seek First to Understand, Synergize, Sharpen the Saw" \
  -o figures/habits.png --type list --style corporate
```

---

### 6. 地理（`--type geographic`）

最适合：区域数据、人口统计、基于位置的统计数据、全球趋势。

**关键元素：** 地图可视化、颜色编码、数据叠加、图例。

```bash
python skills/infographics/scripts/generate_infographic.py \
  "Renewable energy adoption by region: Iceland 100%, Norway 98%, \
   Germany 50%, USA 22%, India 20%" \
  -o figures/renewable_map.png --type geographic --style nature
```

---

### 7. 层级/金字塔（`--type hierarchical`）

最适合：组织结构、优先级、重要性排名。

**关键元素：** 金字塔或树形结构、清晰层级、大小递进。

```bash
python skills/infographics/scripts/generate_infographic.py \
  "Maslow's Hierarchy: Physiological, Safety, Love/Belonging, \
   Esteem, Self-Actualization" \
  -o figures/maslow.png --type hierarchical --style education
```

---

### 8. 解剖/视觉隐喻（`--type anatomical`）

最适合：使用熟悉的视觉隐喻解释复杂系统。

**关键元素：** 中央隐喻图像、标注部分、连接线。

```bash
python skills/infographics/scripts/generate_infographic.py \
  "Business as a human body: Brain=Leadership, Heart=Culture, \
   Arms=Sales, Legs=Operations, Skeleton=Systems" \
  -o figures/business_body.png --type anatomical --style corporate
```

---

### 9. 简历/职业（`--type resume`）

最适合：个人品牌、简历、作品集亮点、职业成就。

**关键元素：** 照片区域、技能可视化、时间线、联系方式。

```bash
python skills/infographics/scripts/generate_infographic.py \
  "UX Designer resume: Skills - User Research 95%, Wireframing 90%, \
   Prototyping 85%. Experience - 2020-2022 Junior, 2022-2025 Senior" \
  -o figures/resume.png --type resume --style technology
```

---

### 10. 社交媒体（`--type social`）

最适合：Instagram、LinkedIn、Twitter/X 帖子、可分享图形。

**关键元素：** 大标题、最少文字、最大冲击力、鲜艳色彩。

```bash
python skills/infographics/scripts/generate_infographic.py \
  "Save Water, Save Life: 2.2 billion people lack safe drinking water. \
   Tips: shorter showers, fix leaks, full loads only" \
  -o figures/water_social.png --type social --style marketing
```

---

## 样式预设

### 行业风格（`--style`）

| 风格 | 颜色 | 最适合 |
|-------|--------|----------|
| `corporate` | 深蓝、钢蓝、金色 | 商业报告、金融 |
| `healthcare` | 医疗蓝、青色、浅青色 | 医疗、健康 |
| `technology` | 科技蓝、板岩紫、紫色 | 软件、数据、AI |
| `nature` | 森林绿、薄荷绿、土棕色 | 环境、有机 |
| `education` | 学术蓝、浅蓝色、珊瑚色 | 学习、学术 |
| `marketing` | 珊瑚色、青色、黄色 | 社交媒体、活动 |
| `finance` | 深蓝、金色、绿/红色 | 投资、银行 |
| `nonprofit` | 暖橙色、鼠尾草色、沙色 | 社会事业、慈善 |

```bash
# 企业风格
python skills/infographics/scripts/generate_infographic.py \
  "Q4 Results" -o q4.png --type statistical --style corporate

# 医疗保健风格
python skills/infographics/scripts/generate_infographic.py \
  "Patient Journey" -o journey.png --type process --style healthcare
```

---

## 色盲安全调色板

### 可用调色板（`--palette`）

| 调色板 | 颜色 | 描述 |
|---------|--------|-------------|
| `wong` | 橙色、天蓝色、绿色、蓝色、朱红色 | 最广泛推荐 |
| `ibm` | 靛青色、靛蓝、洋红色、橙色、金色 | IBM 的无障碍调色板 |
| `tol` | 12 色扩展调色板 | 适用于多类别 |

```bash
# Wong 色盲安全调色板
python skills/infographics/scripts/generate_infographic.py \
  "Survey results by category" -o survey.png --type statistical --palette wong
```

---

## 智能迭代改进

### 工作原理

```
┌─────────────────────────────────────────────────────┐
│  1. Generate infographic with Nano Banana Pro       │
│                    ↓                                │
│  2. Review quality with Gemini 3 Pro                │
│                    ↓                                │
│  3. Score >= threshold?                             │
│       YES → DONE! (early stop)                      │
│       NO  → Improve prompt, go to step 1            │
│                    ↓                                │
│  4. Repeat until quality met OR max iterations      │
└─────────────────────────────────────────────────────┘
```

### 质量审查标准

Gemini 3 Pro 从以下方面评估每个信息图：

1. **视觉层级与布局**（0-2 分）
   - 清晰的视觉层级
   - 逻辑阅读流程
   - 平衡的构图

2. **排版与可读性**（0-2 分）
   - 可读的文本
   - 醒目的标题
   - 无重叠

3. **数据可视化**（0-2 分）
   - 突出的数字
   - 清晰的图表/图标
   - 适当的标签

4. **颜色与无障碍**（0-2 分）
   - 专业颜色
   - 足够的对比度
   - 色盲友好

5. **整体效果**（0-2 分）
   - 专业外观
   - 无视觉错误
   - 达成沟通目标

### 审查日志

每次生成都会产生 JSON 格式的审查日志：
```json
{
  "user_prompt": "5 benefits of exercise...",
  "infographic_type": "list",
  "style": "healthcare",
  "doc_type": "marketing",
  "quality_threshold": 8.5,
  "iterations": [
    {
      "iteration": 1,
      "image_path": "figures/exercise_v1.png",
      "score": 8.7,
      "needs_improvement": false,
      "critique": "SCORE: 8.7\nSTRENGTHS:..."
    }
  ],
  "final_score": 8.7,
  "early_stop": true,
  "early_stop_reason": "Quality score 8.7 meets threshold 8.5"
}
```

---

## 命令行参考

```bash
python skills/infographics/scripts/generate_infographic.py [OPTIONS] PROMPT

Arguments:
  PROMPT                    Description of the infographic content

Options:
  -o, --output PATH         Output file path (required)
  -t, --type TYPE           Infographic type preset
  -s, --style STYLE         Industry style preset
  -p, --palette PALETTE     Colorblind-safe palette
  -b, --background COLOR   Background color (default: white)
  --doc-type TYPE           Document type for quality threshold
  --iterations N            Maximum refinement iterations (default: 3)
  --api-key KEY            OpenRouter API key
  -v, --verbose            Verbose output
  --list-options           List all available options
```

### 列出所有选项

```bash
python skills/infographics/scripts/generate_infographic.py --list-options
```

---

## 配置

### API 密钥设置

设置您的 OpenRouter API 密钥：
```bash
export OPENROUTER_API_KEY='your_api_key_here'
```

获取 API 密钥：https://openrouter.ai/keys

---

## 提示工程技巧

### 内容要具体

✓ **好的提示词**（具体、详细）：
```
"5 benefits of meditation: reduces stress, improves focus, 
better sleep, lower blood pressure, emotional balance"
```

✗ **避免模糊的提示词**：
```
"meditation infographic"
```

### 包含数据点

✓ **好的**：
```
"Market growth from $10B (2020) to $45B (2025), CAGR 35%"
```

✗ **模糊的**：
```
"market is growing"
```

### 指定视觉元素

✓ **好的**：
```
"Timeline showing 5 milestones with icons for each event"
```

---

## 参考文件

获取详细指导，请加载这些参考文件：

- **`references/infographic_types.md`**：所有 10+ 种类型的扩展模板
- **`references/design_principles.md`**：视觉层级、布局、排版
- **`references/color_palettes.md`**：完整调色板规格

---

## 问题排查

### 常见问题

**问题**：信息图中的文字不可读
- **解决方案**：减少文字内容；使用 `--type` 指定布局类型

**问题**：颜色冲突或不可访问
- **解决方案**：使用 `--palette wong` 获取色盲安全颜色

**问题**：质量分数太低
- **解决方案**：使用 `--iterations 3` 增加迭代次数；使用更具体的提示词

**问题**：生成的信息图类型不正确
- **解决方案**：始终指定 `--type` 标志以获得一致的结果

---

## 与其他技能集成

此技能可与以下技能协同工作：

- **scientific-schematics**：技术图表和流程图
- **market-research-reports**：商业报告用信息图
- **scientific-slides**：演示文稿用信息图元素
- **generate-image**：非信息图视觉内容

---

## 快速参考检查清单

生成前：
- [ ] 清晰、具体的内容描述
- [ ] 已选择信息图类型（`--type`）
- [ ] 风格适合受众（`--style`）
- [ ] 已指定输出路径（`-o`）
- [ ] 已配置 API 密钥

生成后：
- [ ] 检查生成的图像
- [ ] 查看审查日志中的分数
- [ ] 如需要，使用更具体的提示词重新生成

---

使用此技能，利用 Nano Banana Pro AI 的强大功能和智能质量审查，创建专业、无障碍且视觉吸引人的信息图。
