# MarkItDown 技能 - 创建总结

## 概述

为 Claude Scientific Writer 创建了一个全面使用 Microsoft MarkItDown 工具的技能。该技能支持将 15+ 种文件格式转换为 Markdown，针对 LLM 处理和科学工作流程进行了优化。

## 创建内容

### 核心文档

1. **SKILL.md**（主技能文件）
   - MarkItDown 完整指南
   - 快速入门示例
   - 所有支持的格式
   - 高级功能（AI、Azure DI）
   - 最佳实践
   - 用例和示例

2. **README.md**
   - 技能概述
   - 关键功能
   - 快速参考
   - 集成指南

3. **QUICK_REFERENCE.md**
   - 常见任务速查表
   - 快速语法参考
   - 常用命令
   - 故障排除技巧

4. **INSTALLATION_GUIDE.md**
   - 分步安装指南
   - 系统依赖项
   - 虚拟环境设置
   - 可选功能
   - 故障排除

### 参考文档

位于 `references/`：

1. **api_reference.md**
   - 完整的 API 文档
   - 类和方法参考
   - 自定义转换器开发
   - 插件系统
   - 错误处理
   - 重大变更指南

2. **file_formats.md**
   - 详细的格式特定指南
   - 15+ 种支持的格式
   - 格式功能和限制
   - 每种格式的最佳实践
   - 示例输出

### 实用脚本

位于 `scripts/`：

1. **batch_convert.py**
   - 并行批量转换
   - 多格式支持
   - 递归目录搜索
   - 进度跟踪
   - 错误报告
   - 命令行界面

2. **convert_with_ai.py**
   - AI 增强的转换
   - 预定义提示类型（科学、医学、数据可视化等）
   - 自定义提示支持
   - 多模型支持
   - OpenRouter 集成（高级视觉模型）

3. **convert_literature.py**
   - 科学文献转换
   - 从文件名提取元数据
   - 按年份组织
   - 自动索引生成
   - JSON 目录创建
   - 前言支持

### 资源

位于 `assets/`：

1. **example_usage.md**
   - 20+ 个实际示例
   - 基础转换
   - 科学工作流程
   - AI 增强处理
   - 批量操作
   - 错误处理模式
   - 集成示例

### 许可证

- **LICENSE.txt** - 来自 Microsoft 的 MIT 许可证

## 技能结构

```
.claude/skills/markitdown/
├── SKILL.md                    # 主技能文档
├── README.md                   # 技能概述
├── QUICK_REFERENCE.md          # 快速参考指南
├── INSTALLATION_GUIDE.md       # 安装说明
├── SKILL_SUMMARY.md           # 本文件
├── LICENSE.txt                 # MIT 许可证
├── references/
│   ├── api_reference.md       # 完整 API 文档
│   └── file_formats.md        # 格式特定指南
├── scripts/
│   ├── batch_convert.py       # 批量转换实用工具
│   ├── convert_with_ai.py     # AI 增强转换
│   └── convert_literature.py  # 文献转换
└── assets/
    └── example_usage.md       # 实际示例
```

## 功能

### 文件格式支持

- **文档**：PDF、DOCX、PPTX、XLSX、XLS、EPUB
- **图片**：JPEG、PNG、GIF、WebP（带 OCR）
- **音频**：WAV、MP3（带转录）
- **网页**：HTML、YouTube URL
- **数据**：CSV、JSON、XML
- **归档**：ZIP 文件
- **邮件**：Outlook MSG 文件

### 高级功能

1. **通过 OpenRouter 实现 AI 增强**
   - 通过 OpenRouter 访问 100+ 个 AI 模型
   - 多个预设提示（科学、医学、数据可视化）
   - 自定义提示支持
   - 默认：高级视觉模型（最适合科学视觉）
   - 为每项任务选择最佳模型

2. **Azure 集成**
   - 用于复杂 PDF 的 Azure Document Intelligence
   - 增强的布局理解
   - 更好的表格提取

3. **批量处理**
   - 可配置工作器的并行转换
   - 递归目录处理
   - 进度跟踪和错误报告
   - 格式特定组织

4. **科学工作流程**
   - 带元数据的文献转换
   - 自动索引生成
   - 按年份组织
   - 引用友好的输出

## 与 Scientific Writer 的集成

该技能已添加到 Scientific Writer 的技能目录中：

- **位置**：`.claude/skills/markitdown/`
- **技能编号**：文档操作技能 #5
- **SKILLS.md**：已更新完整的技能描述

### 使用示例

```
> 将文献文件夹中的所有 PDF 转换为 Markdown
> 使用 AI 生成的描述将此 PowerPoint 演示文稿转换为 Markdown
> 从此 Excel 文件中提取表格
> 转录此讲座录音
```

## 脚本使用

### 批量转换
```bash
python scripts/batch_convert.py input_dir/ output_dir/ --extensions .pdf .docx --workers 4
```

### AI 增强转换
```bash
export OPENROUTER_API_KEY="sk-or-v1-..."
python scripts/convert_with_ai.py paper.pdf output.md \
  --model anthropic/claude-sonnet-4.5 \
  --prompt-type scientific
```

### 文献转换
```bash
python scripts/convert_literature.py papers/ markdown/ --organize-by-year --create-index
```

## 关键功能

1. **Token 高效输出**：针对 LLM 处理优化的 Markdown
2. **全面的格式支持**：15+ 种文件类型
3. **AI 增强**：通过 OpenAI 提供详细的图片描述
4. **OCR 支持**：从扫描文档中提取文本
5. **音频转录**：音频文件的语音转文本
6. **YouTube 支持**：视频转录提取
7. **插件系统**：可扩展架构
8. **批量处理**：高效的并行转换
9. **错误处理**：强大的错误管理
10. **科学重点**：针对研究工作流程优化

## 安装

```bash
# 完整安装
pip install 'markitdown[all]'

# 选择性安装
pip install 'markitdown[pdf,docx,pptx,xlsx]'
```

## 快速入门

```python
from markitdown import MarkItDown

# 基础用法
md = MarkItDown()
result = md.convert("document.pdf")
print(result.text_content)

# 通过 OpenRouter 使用 AI
from openai import OpenAI
client = OpenAI(
    api_key="your-openrouter-api-key",
    base_url="https://openrouter.ai/api/v1"
)
md = MarkItDown(
    llm_client=client,
    llm_model="anthropic/claude-sonnet-4.5"  # 或 openai/gpt-4o
)
result = md.convert("presentation.pptx")
```

## 文档文件

| 文件 | 用途 | 行数 |
|------|---------|-------|
| SKILL.md | 主文档 | 400+ |
| api_reference.md | API 文档 | 500+ |
| file_formats.md | 格式指南 | 600+ |
| example_usage.md | 实际示例 | 500+ |
| batch_convert.py | 批量转换 | 200+ |
| convert_with_ai.py | AI 转换 | 200+ |
| convert_literature.py | 文献转换 | 250+ |
| QUICK_REFERENCE.md | 快速参考 | 300+ |
| INSTALLATION_GUIDE.md | 安装指南 | 300+ |

**总计**：约 3,000+ 行文档和代码

## 用例

1. **文献综述**：将研究论文转换为 Markdown 以便分析
2. **数据提取**：从 Excel/PDF 中提取表格进行处理
3. **演示文稿处理**：使用 AI 描述转换幻灯片
4. **文档分析**：为 LLM 消费准备文档
5. **讲座转录**：将录音转换为文本
6. **YouTube 分析**：提取视频转录
7. **归档处理**：批量转换文档集合

## 下一步

1. 安装 MarkItDown：`pip install 'markitdown[all]'`
2. 阅读 `QUICK_REFERENCE.md` 了解常见任务
3. 尝试 `scripts/` 目录中的示例脚本
4. 探索 `SKILL.md` 了解全面指南
5. 查看 `example_usage.md` 了解实际示例

## 资源

- **MarkItDown GitHub**：https://github.com/microsoft/markitdown
- **PyPI**：https://pypi.org/project/markitdown/
- **OpenRouter**：https://openrouter.ai（AI 模型访问）
- **OpenRouter API 密钥**：https://openrouter.ai/keys
- **OpenRouter 模型**：https://openrouter.ai/models
- **许可证**：MIT（Microsoft Corporation）
- **Python**：需要 3.10+
- **技能位置**：`.claude/skills/markitdown/`

## 成功标准

✅ 综合技能文档已创建  
✅ 完整的 API 参考已提供  
✅ 格式特定指南已包含  
✅ 实用脚本已实现  
✅ 实际示例已记录  
✅ 安装指南已创建  
✅ 快速参考指南已添加  
✅ 与 Scientific Writer 的集成完成  
✅ SKILLS.md 已更新  
✅ 脚本已设为可执行  
✅ MIT 许可证已包含  

## 技能状态

**状态**：✅ 完成并可用

MarkItDown 技能已完全集成到 Claude Scientific Writer 中，可以立即使用。所有文档、脚本和示例都已就位。
