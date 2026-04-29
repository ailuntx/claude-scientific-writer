# 科学图表 - 快速参考

**工作原理：** 描述您的图表 → Nano Banana Pro 自动生成

## 设置（一次性）

```bash
# 从 https://openrouter.ai/keys 获取 API 密钥
export OPENROUTER_API_KEY='sk-or-v1-your_key_here'

# 添加到 shell 配置文件中以持久化
echo 'export OPENROUTER_API_KEY="sk-or-v1-your_key"' >> ~/.bashrc  # 或 ~/.zshrc
```

## 基本用法

```bash
# 描述您的图表，Nano Banana Pro 会创建它
python scripts/generate_schematic.py "您的图表描述" -o output.png

# 就是这么简单！自动完成：
# - 迭代优化（3轮）
# - 质量审查和改进
# - 出版级输出
```

## 常用示例

### CONSORT 流程图
```bash
python scripts/generate_schematic.py \
  "CONSORT 流程：筛选 n=500，排除 n=150，随机化 n=350" \
  -o consort.png
```

### 神经网络
```bash
python scripts/generate_schematic.py \
  "带编码器和解码器堆栈的 Transformer 架构" \
  -o transformer.png
```

### 生物通路
```bash
python scripts/generate_schematic.py \
  "MAPK 通路：EGFR → RAS → RAF → MEK → ERK" \
  -o mapk.png
```

### 电路图
```bash
python scripts/generate_schematic.py \
  "带 1kΩ 电阻器和 10µF 电容器的运算放大器电路" \
  -o circuit.png
```

## 命令选项

| 选项 | 描述 | 示例 |
|--------|-------------|---------|
| `-o, --output` | 输出文件路径 | `-o figures/diagram.png` |
| `--iterations N` | 优化次数（1-2） | `--iterations 2` |
| `-v, --verbose` | 显示详细输出 | `-v` |
| `--api-key KEY` | 提供 API 密钥 | `--api-key sk-or-v1-...` |

## 提示技巧

### ✓ 好的提示（具体）
- "CONSORT 流程图，含筛选（n=500）、排除（n=150）、随机化（n=350）"
- "Transformer 架构：左侧编码器6层，右侧解码器，交叉注意力连接"
- "MAPK 信号通路：受体 → RAS → RAF → MEK → ERK → 细胞核，标注每个磷酸化"

### ✗ 避免（太模糊）
- "画个流程图"
- "神经网络"
- "通路图"

## 输出文件

对于输入 `diagram.png`，您会得到：
- `diagram_v1.png` - 第一次迭代
- `diagram_v2.png` - 第二次迭代  
- `diagram_v3.png` - 最终迭代
- `diagram.png` - 最终版本的副本
- `diagram_review_log.json` - 质量评分和批评

## 审查日志

```json
{
  "iterations": [
    {
      "iteration": 1,
      "score": 7.0,
      "critique": "好的开始。字体太小了..."
    },
    {
      "iteration": 2,
      "score": 8.5,
      "critique": "改进很大。轻微的间距问题..."
    },
    {
      "iteration": 3,
      "score": 9.5,
      "critique": "很棒。可以出版了。"
    }
  ],
  "final_score": 9.5
}
```

## Python API

```python
from scripts.generate_schematic_ai import ScientificSchematicGenerator

# 初始化
gen = ScientificSchematicGenerator(api_key="your_key")

# 生成
results = gen.generate_iterative(
    user_prompt="图表描述",
    output_path="output.png",
    iterations=2
)

# 检查质量
print(f"评分: {results['final_score']}/10")
```

## 故障排除

### 找不到 API 密钥
```bash
# 检查是否已设置
echo $OPENROUTER_API_KEY

# 设置它
export OPENROUTER_API_KEY='your_key'
```

### 导入错误
```bash
# 安装 requests
pip install requests
```

### 质量评分低
- 使提示更具体
- 包含布局细节（从左到右，从上到下）
- 指定标签要求
- 增加迭代次数：`--iterations 2`

## 测试

```bash
# 验证安装
python test_ai_generation.py

# 应显示："6/6 测试通过"
```

## 费用

每个图表的典型费用（最多2次迭代）：
- 简单（1次迭代）：$0.05-0.15
- 复杂（2次迭代）：$0.10-0.30

## Nano Banana Pro 工作原理

**只需用自然语言描述您想要的图表：**
- ✓ 无需编码
- ✓ 无需模板
- ✓ 无需手动绘图
- ✓ 自动质量审查
- ✓ 出版级输出
- ✓ 适用于任何类型的图表
- ✓ 不包含图号（图号在文档/LaTeX 中单独添加）

**只需描述您想要的内容，它会自动生成。**

## 获取帮助

```bash
# 显示帮助
python scripts/generate_schematic.py --help

# 调试用详细模式
python scripts/generate_schematic.py "图表" -o out.png -v
```

## 快速启动检查清单

- [ ] 设置 `OPENROUTER_API_KEY` 环境变量
- [ ] 运行 `python test_ai_generation.py`（应通过 6/6）
- [ ] 尝试：`python scripts/generate_schematic.py "测试图表" -o test.png`
- [ ] 查看输出文件（test_v1.png、v2、v3、review_log.json）
- [ ] 阅读 SKILL.md 获取详细文档
- [ ] 查看 README.md 获取示例

## 资源

- 完整文档：`SKILL.md`
- 详细指南：`README.md`
- 实现细节：`IMPLEMENTATION_SUMMARY.md`
- 示例脚本：`example_usage.sh`
- 获取 API 密钥：https://openrouter.ai/keys
