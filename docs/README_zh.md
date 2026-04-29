# Scientific Writer 文档

欢迎来到 Scientific Writer 文档！**Scientific Writer 是一款深度研究和写作工具**，将 AI 驱动的深度研究能力与多种格式良好的书面输出相结合——从科学论文和资助申请，到临床报告和会议演示。

本指南将帮助你浏览可用资源。

## 📚 文档概览

> 💡 **新！** 查看 [完整文档索引](DOCUMENTATION_INDEX.md)，获取包含学习路径和快速参考的全面导航指南。

### 面向新用户

从这里开始，快速上手：

1. **[主 README](../README.md)** - 快速开始、安装和基本用法
2. **[完整功能指南](FEATURES.md)** - 所有能力的全面概览
3. **[技能概览](SKILLS.md)** - 可用技能及其用途
4. **[插件安装](../README.md#-use-as-a-claude-code-plugin-recommended)** - Claude Code 插件设置（推荐）

### 面向开发者

将 Scientific Writer 集成到你的 Python 项目中：

1. **[API 参考](API.md)** - 完整的程序化 API 文档
2. **[开发指南](DEVELOPMENT.md)** - 贡献与开发环境设置
3. **[发布指南](RELEASING.md)** - 版本管理与发布工作流

### 故障排查

遇到问题？查看这些资源：

1. **[故障排查指南](TROUBLESHOOTING.md)** - 常见问题及解决方案
2. **[更新日志](../CHANGELOG.md)** - 版本历史和破坏性变更

## 🎯 使用模式

Scientific Writer 可通过三种方式使用：

1. **🌟 Claude Code 插件（推荐）** - 直接在你的 IDE 中使用
   - 一条命令即可完成设置：`/scientific-writer:init`
   - 所有 19+ 项技能可立即使用
   - 无需 CLI
   - 参见：[插件安装指南](../README.md#-use-as-a-claude-code-plugin-recommended)

2. **💻 命令行界面（CLI）** - 交互式科学写作
   - 运行：`scientific-writer` 或 `uv run scientific-writer`
   - 功能完整的交互模式
   - 参见：[CLI 快速开始](../README.md#use-the-cli)

3. **🔧 Python API** - 程序化集成
   - 导入：`from scientific_writer import generate_paper`
   - 支持带进度流式传输的异步 API
   - 参见：[API 参考](API.md)

## 🎯 按任务快速导航

### 我想生成一个……

| 文档类型 | 从这里开始 |
|--------------|------------|
| **科学论文** | [README 快速开始](../README.md#quick-start) → [功能：科学论文](FEATURES.md#scientific-papers) |
| **资助申请** | [功能：资助申请](FEATURES.md#grant-proposals) → [技能：研究资助](SKILLS.md#5-research-grants) |
| **研究海报** | [功能：研究海报](FEATURES.md#research-posters) → [技能：LaTeX 海报](SKILLS.md#6-latex-research-posters) |
| **文献综述** | [功能：文献综述](FEATURES.md#literature-reviews) → [技能：文献综述](SKILLS.md#2-literature-review) |
| **科学图示** | [功能：科学示意图](FEATURES.md#scientific-schematics) → [技能：科学示意图](SKILLS.md#6-scientific-schematics-and-diagrams) |

### 我想要……

| 任务 | 文档 |
|------|---------------|
| **使用 Python API** | [API 参考](API.md) → [README：API 用法](../README.md#api-usage) |
| **了解研究检索** | [功能：实时研究检索](FEATURES.md#real-time-research-lookup) → [API：研究检索](API.md#research-lookup) |
| **自动检测现有论文** | [功能：智能论文检测](FEATURES.md#intelligent-paper-detection) |
| **处理数据文件** | [功能：数据与文件集成](FEATURES.md#data--file-integration) → [README：文件处理](../README.md#file-handling) |
| **转换文档** | [功能：文档转换](FEATURES.md#document-conversion) → [技能：MarkItDown](SKILLS.md#7-markitdown---universal-file-to-markdown-converter) |
| **获取同行评审** | [功能：使用 ScholarEval 的同行评审](FEATURES.md#peer-review-with-scholareval) → [技能：学者评估](SKILLS.md#4-scholar-evaluation) |
| **修复问题** | [故障排查指南](TROUBLESHOOTING.md) |
| **贡献代码** | [开发指南](DEVELOPMENT.md) |

## 📖 完整文档索引

### 用户文档

1. **[README.md](../README.md)** - 主包文档
   - 快速开始
   - 安装
   - 功能概览
   - 基本用法（CLI 和 API）
   - 快速参考
   - 示例

2. **[FEATURES.md](FEATURES.md)** - 完整功能指南
   - 文档生成（论文、海报、资助申请、综述、示意图）
   - AI 驱动能力（研究检索、同行评审、编辑）
   - 智能论文检测
   - 数据与文件集成
   - 文档转换
   - 开发者功能

3. **[API.md](API.md)** - 程序化 API 参考
   - API 函数
   - 数据模型
   - 使用模式
   - 高级功能
   - 环境变量
   - 错误处理
   - 最佳实践

4. **[SKILLS.md](SKILLS.md)** - 可用技能与能力
   - 写作技能（科学写作、文献综述、同行评审、学者评估、资助申请、海报、示意图）
   - 文档处理技能（MarkItDown、DOCX、PDF、PPTX、XLSX）
   - 使用示例

5. **[TROUBLESHOOTING.md](TROUBLESHOOTING.md)** - 常见问题与解决方案
   - 安装问题
   - LaTeX 编译错误
   - API 密钥问题
   - 运行时错误
   - 性能问题

### 开发者文档

6. **[DEVELOPMENT.md](DEVELOPMENT.md)** - 开发与贡献
   - 配置开发环境
   - 代码结构
   - 测试
   - 贡献指南

7. **[RELEASING.md](RELEASING.md)** - 版本管理与发布
   - 版本控制策略
   - 发布流程
   - 发布到 PyPI
   - Git 标签

8. **[CHANGELOG.md](../CHANGELOG.md)** - 版本历史
   - 发布说明
   - 破坏性变更
   - 新功能
   - 错误修复

### 高级

9. **[CLAUDE.md](../CLAUDE.md)** - 为代理提供的系统指令
   - 代理行为准则
   - 技能集成
   - 工具使用模式

## 🔍 搜索提示

查找特定信息时：

### 按主题
- **API 用法**：在 [API.md](API.md) 中搜索
- **CLI 命令**：在 [README.md](../README.md) 和 [FEATURES.md](FEATURES.md) 中搜索
- **技能/能力**：在 [SKILLS.md](SKILLS.md) 中搜索
- **错误/问题**：在 [TROUBLESHOOTING.md](TROUBLESHOOTING.md) 中搜索
- **最近变更**：查看 [CHANGELOG.md](../CHANGELOG.md)

### 按关键词
- `generate_paper()` → [API.md](API.md)
- `scientific-writer` → [README.md](../README.md)
- `NSF`/`NIH`/`DOE`/`DARPA` → [SKILLS.md](SKILLS.md#5-research-grants)
- `CONSORT`/`circuit`/`pathway` → [SKILLS.md](SKILLS.md#6-scientific-schematics-and-diagrams)
- `MarkItDown` → [SKILLS.md](SKILLS.md#7-markitdown---universal-file-to-markdown-converter)
- `ScholarEval` → [SKILLS.md](SKILLS.md#4-scholar-evaluation)
- `data files` → [FEATURES.md](FEATURES.md#automatic-data-handling)
- `research lookup` → [FEATURES.md](FEATURES.md#real-time-research-lookup)

## 💡 获取帮助

如果你找不到想要的内容：

1. **查看 [故障排查指南](TROUBLESHOOTING.md)**
2. **搜索 [更新日志](../CHANGELOG.md)** 了解最近更新
3. **查看 [技能概览](SKILLS.md)** 以了解全部能力
4. **在 GitHub 上提交 issue** 并附上你的问题

## 🚀 快速链接

- [安装](../README.md#install)
- [CLI 快速开始](../README.md#use-the-cli)
- [API 快速开始](../README.md#use-the-python-api)
- [常用命令](../README.md#common-commands)
- [示例代码](../example_api_usage.py)
- [PyPI 包](https://pypi.org/project/scientific-writer/)

---

**最后更新**：2025 年 1 月 22 日（v2.7.0）
