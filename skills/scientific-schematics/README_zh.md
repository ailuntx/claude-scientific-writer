# 科学示意图生成器 - Nano Banana Pro

**通过自然语言描述生成任意科学示意图。**

Nano Banana Pro 自动创建符合发表质量的示意图——无需编码、无需模板、无需手动绘制。

## 快速开始

### 生成任意示意图

```bash
# 设置您的 OpenRouter API 密钥
export OPENROUTER_API_KEY='your_api_key_here'

# 生成任意科学示意图
python scripts/generate_schematic.py "CONSORT 参与者流程图" -o figures/consort.png

# 神经网络架构
python scripts/generate_schematic.py "Transformer 编码器-解码器架构" -o figures/transformer.png

# 生物通路
python scripts/generate_schematic.py "MAPK 信号通路" -o figures/pathway.png
```

### 您将获得

- **最多两次迭代**（v1, v2），逐步优化
- **每次迭代后自动质量评审**
- **详细的评审日志**，包含分数和评价（JSON 格式）
- **符合发表标准的图像**，遵循科学规范

## 功能特性

### 迭代优化流程

1. **生成 1**：根据您的描述创建初始示意图
2. **评审 1**：AI 评估清晰度、标签、准确性、可访问性
3. **生成 2**：基于评价进行改进
4. **评审 2**：第二次评估并提供具体反馈
5. **生成 3**：最终优化版本

### 自动质量标准

所有示意图自动遵循：
- 干净的白色/浅色背景
- 高对比度以确保可读性
- 清晰的标签（最小 10pt 字体）
- 专业的排版
- 色盲友好型颜色
- 元素间适当的间距
- 在适当时包含比例尺、图例、坐标轴
- **无图号**——示意图不包含“图 1:”或类似标签（由文档/LaTeX 添加）

## 安装

### 用于 AI 生成

```bash
# 获取 OpenRouter API 密钥
# 访问：https://openrouter.ai/keys

# 设置环境变量
export OPENROUTER_API_KEY='sk-or-v1-...'

# 或添加到 .env 文件
echo "OPENROUTER_API_KEY=sk-or-v1-..." >> .env

# 安装 Python 依赖（如果尚未安装）
pip install requests
```

## 使用示例

### 示例 1：CONSORT 流程图

```bash
python scripts/generate_schematic.py \
  "RCT 的 CONSORT 参与者流程图。\
   评估资格（n=500）。\
   排除（n=150）：年龄<18（n=80），拒绝（n=50），其他（n=20）。\
   随机化（n=350）分为治疗组（n=175）和对照组（n=175）。\
   失访：分别为 15 和 10。\
   最终分析：160 和 165。" \
  -o figures/consort.png
```

**输出：**
- `figures/consort_v1.png` - 初始生成
- `figures/consort_v2.png` - 第一次评审后
- `figures/consort_v3.png` - 最终版本
- `figures/consort.png` - 最终版本的副本
- `figures/consort_review_log.json` - 详细评审日志

### 示例 2：神经网络架构

```bash
python scripts/generate_schematic.py \
  "Transformer 架构，左侧为编码器（输入嵌入、\
   位置编码、多头注意力、前馈网络），右侧为解码器（掩码注意力、\
   交叉注意力、前馈网络）。\
   显示从编码器到解码器的交叉注意力连接。" \
  -o figures/transformer.png \
  --iterations 2
```

### 示例 3：生物通路

```bash
python scripts/generate_schematic.py \
  "MAPK 信号通路：EGFR 受体 → RAS → RAF → MEK → ERK → 细胞核。\
   用磷酸化标记每个步骤。为每种激酶使用不同颜色。" \
  -o figures/mapk.png
```

### 示例 4：系统架构

```bash
python scripts/generate_schematic.py \
  "物联网系统框图：传感器（底部）→ 微控制器 → \
   WiFi 模块和显示器（中部）→ 云服务器 → 移动应用（顶部）。\
   用协议标记所有连接。" \
  -o figures/iot_system.png
```

## 命令行选项

```bash
python scripts/generate_schematic.py [选项] "描述" -o 输出.png

选项：
  --iterations N           AI 优化迭代次数（默认：2，最大：2）
  --api-key KEY           OpenRouter API 密钥（或使用环境变量）
  -v, --verbose           详细输出
  -h, --help              显示帮助信息
```

## Python API

```python
from scripts.generate_schematic_ai import ScientificSchematicGenerator

# 初始化
generator = ScientificSchematicGenerator(
    api_key="your_key",
    verbose=True
)

# 通过迭代优化生成
results = generator.generate_iterative(
    user_prompt="CONSORT 流程图",
    output_path="figures/consort.png",
    iterations=2
)

# 访问结果
print(f"最终分数：{results['final_score']}/10")
print(f"最终图像：{results['final_image']}")

# 评审迭代
for iteration in results['iterations']:
    print(f"迭代 {iteration['iteration']}：{iteration['score']}/10")
    print(f"评价：{iteration['critique']}")
```

## 提示工程技巧

### 明确布局
✓ "垂直流向的流程图，从上到下"  
✓ "左侧编码器、右侧解码器的架构图"  
✗ "做个图"（太模糊）

### 包含定量细节
✓ "神经网络：输入（784），隐藏层（128），输出（10）"  
✓ "流程图：n=500 筛选，n=150 排除，n=350 随机化"  
✗ "一些数字"（不具体）

### 指定视觉风格
✓ "简洁的框图，线条清晰"  
✓ "详细的生物通路图，包含蛋白质结构"  
✓ "技术示意图，使用工程符号"

### 请求特定标签
✓ "用激活/抑制标记所有箭头"  
✓ "在每个框中包含层维度"  
✓ "用时间戳显示时间进程"

### 提及颜色要求
✓ "使用色盲友好型颜色"  
✓ "灰度兼容设计"  
✓ "按功能颜色编码：蓝色=输入，绿色=处理，红色=输出"

## 评审日志格式

每次生成都会产生一个 JSON 评审日志：

```json
{
  "user_prompt": "CONSORT 参与者流程图...",
  "iterations": [
    {
      "iteration": 1,
      "image_path": "figures/consort_v1.png",
      "prompt": "完整生成提示...",
      "critique": "分数：7/10。问题：字体太小...",
      "score": 7.0,
      "success": true
    },
    {
      "iteration": 2,
      "image_path": "figures/consort_v2.png",
      "score": 8.5,
      "critique": "改进很大。剩余问题..."
    },
    {
      "iteration": 3,
      "image_path": "figures/consort_v3.png",
      "score": 9.5,
      "critique": "优秀。符合发表要求。"
    }
  ],
  "final_image": "figures/consort_v3.png",
  "final_score": 9.5,
  "success": true
}
```

## 为什么使用 Nano Banana Pro

**只需描述您想要的内容——Nano Banana Pro 为您创建：**

- ✓ **快速**：几分钟内出结果
- ✓ **简单**：自然语言描述（无需编码）
- ✓ **高质量**：自动评审和优化
- ✓ **通用**：适用于所有图表类型
- ✓ **符合发表要求**：立即获得高质量输出

**只需描述您的示意图，即可自动生成。**

## 故障排除

### API 密钥问题

```bash
# 检查密钥是否设置
echo $OPENROUTER_API_KEY

# 临时设置
export OPENROUTER_API_KEY='your_key'

# 永久设置（添加到 ~/.bashrc 或 ~/.zshrc）
echo 'export OPENROUTER_API_KEY="your_key"' >> ~/.bashrc
```

### 导入错误

```bash
# 安装 requests 库
pip install requests

# 或使用包管理器
pip install -r requirements.txt
```

### 生成失败

```bash
# 使用详细模式查看详细错误
python scripts/generate_schematic.py "diagram" -o out.png -v

# 检查 API 状态
curl https://openrouter.ai/api/v1/models
```

### 低质量分数

如果迭代分数持续低于 7/10：
1. 使您的提示更具体
2. 包含更多关于布局和标签的细节
3. 明确指定视觉要求
4. 增加迭代次数：`--iterations 2`

## 测试

运行验证测试：

```bash
python test_ai_generation.py
```

测试内容包括：
- 文件结构
- 模块导入
- 类初始化
- 错误处理
- 提示工程
- 包装脚本

## 成本考虑

所用模型的 OpenRouter 定价：
- **Nano Banana Pro**：约 $2/M 输入令牌，约 $12/M 输出令牌

每个示意图的典型成本：
- 简单示意图（1 次迭代）：约 $0.05-0.15
- 复杂示意图（2 次迭代）：约 $0.10-0.30

## 示例库

查看完整的 SKILL.md 获取大量示例，包括：
- CONSORT 流程图
- 神经网络架构（Transformers、CNNs、RNNs）
- 生物通路
- 电路图
- 系统架构
- 框图

## 支持

如有问题或疑问：
1. 查看 SKILL.md 获取详细文档
2. 运行 test_ai_generation.py 验证设置
3. 使用详细模式（-v）查看详细错误
4. 查看 review_log.json 获取质量反馈

## 许可证

属于 scientific-writer 包的一部分。请查看主仓库获取许可证信息。
