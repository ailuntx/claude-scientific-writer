---
description: 使用 Scientific Writer 初始化当前项目——一个将 AI 驱动研究与格式良好的书面输出相结合的深度研究和写作工具。
---

# Scientific Writer 项目设置

当用户运行 `/scientific-writer:init` 时，请执行以下操作：

## ⚠️ 关键规则：绝不要读取模板文件

**在整个过程中，绝对不要对模板文件使用 read_file 工具。模板文件有 1362 行，读取它会浪费时间和 token。只使用终端命令（`cp`、`cat`、`mv`）来处理该文件。**

## 第 1 步：检查是否存在 CLAUDE.md

1. 检查当前工作目录中是否存在 `CLAUDE.md` 文件。
   
2. 如果存在：
   - 询问用户希望如何处理：
     - a) **备份** 现有文件为 `CLAUDE.md.bak`，并用 Scientific Writer 配置替换它，或
     - b) **合并** Scientific Writer 设置到现有文件中（追加到末尾），或
     - c) **取消** 操作。
   
3. 在继续之前等待用户回复。

## 第 2 步：定位模板文件路径

**关键：不要使用 read_file 工具。不要读取模板内容。只定位文件路径。**

查找 Scientific Writer 模板文件的路径。可使用以下方法之一：

1. **使用 glob_file_search** 在 templates 目录中查找 `CLAUDE.scientific-writer.md`
2. **使用 list_dir** 检查文件是否存在于已知位置
3. **直接尝试以下路径**（按顺序）：
   - `/Users/vinayak/Documents/claude-scientific-writer/templates/CLAUDE.scientific-writer.md`
   - `~/.claude/plugins/*/claude-scientific-writer/templates/CLAUDE.scientific-writer.md`

一旦获得路径，立即继续执行第 3 步。**不要读取或验证文件内容。**

## 第 3 步：创建或更新 CLAUDE.md

**以下所有选项都必须仅使用终端命令。不要读取模板文件内容。**

根据用户的选择（如果不存在现有文件，则创建新文件）：

### 选项 A：替换（带备份）
使用终端命令执行以下操作：
1. 将现有 `CLAUDE.md` 重命名为 `CLAUDE.md.bak`：
   ```bash
   mv CLAUDE.md CLAUDE.md.bak
   ```
2. 将模板文件复制为 `CLAUDE.md`：
   ```bash
   cp {template_path} CLAUDE.md
   ```
3. 输出：`"✅ 已将现有 CLAUDE.md 备份到 CLAUDE.md.bak，并创建新的 Scientific Writer 配置"`

### 选项 B：合并
使用终端命令执行以下操作：
1. 向现有 `CLAUDE.md` 追加分隔符：
   ```bash
   echo -e "\n\n---\n\n# Scientific Writer Configuration (Added by Plugin)\n" >> CLAUDE.md
   ```
2. 直接将模板文件内容追加进去（无需读取）：
   ```bash
   cat {template_path} >> CLAUDE.md
   ```
3. 输出：`"✅ 已将 Scientific Writer 配置合并到现有 CLAUDE.md 中"`

### 选项 C：创建新文件（默认）
如果不存在现有文件，使用终端命令执行以下操作：
1. 将模板文件复制为 `CLAUDE.md`：
   ```bash
   cp {template_path} CLAUDE.md
   ```
2. 输出：`"✅ 已使用 Scientific Writer 配置创建 CLAUDE.md"`

## 第 4 步：总结已安装内容

写入文件后，提供简要摘要：

```
🎉 Scientific Writer 已在此项目中初始化！

📋 包含内容：
- 一个将 AI 驱动研究与格式良好的书面输出相结合的深度研究和写作工具
- 完整的 scientific writing 工作流，包含实时文献检索和经过验证的引用
- 19+ 个面向学术写作的 specialized skills：
  • research-lookup: 实时文献搜索
  • peer-review: 系统性稿件评估
  • citation-management: BibTeX 和参考文献处理
  • clinical-reports: 医疗文档标准
  • research-grants: NSF、NIH、DOE 提案支持
  • scientific-slides: 研究演示
  • latex-posters: 会议海报生成
  • 以及另外 12 个 specialized skills...

📝 支持的文档类型：
- 科学论文（Nature、Science、NeurIPS、IEEE 等）
- 临床报告（病例报告、试验文档）
- 资助提案（NSF、NIH、DOE、DARPA）
- 研究海报和演示文稿
- 文献综述和系统综述

🚀 开始使用：
1. 你的 CLAUDE.md 文件已配置在：{path to CLAUDE.md}
2. 所有 skills 都会自动在此项目中可用
3. 可以使用如下提示开始：
   - “基于 [topic] 创建一篇 Nature 论文”
   - “为 [research] 生成一份 NSF 资助提案”
   - “使用 peer-review 标准审阅这份稿件”
   - “基于 [topic] 创建会议幻灯片”

💡 提示：
- research-lookup skill 会自动查找真实论文和引用
- 所有文档默认使用 LaTeX 格式（可直接发表）
- 论文生成后会自动执行同行评审
- 你可以编辑 CLAUDE.md 文件来自定义行为

📚 文档：
- Skill 详情：浏览 skills/ 目录
- 完整文档：https://github.com/K-Dense-AI/claude-scientific-writer

祝你写作愉快！🔬📄
```

## 第 5 步：最终提醒

提醒用户：
- `CLAUDE.md` 文件可以随时手动打开和编辑
- 目前此项目中可用的 19 个 skills 都已启用
- 他们可以询问“有哪些 skills 可用？”来查看完整列表
- 他们可以在提示中引用特定 skills，例如 `@research-lookup`

## 错误处理

如果在文件创建过程中发生任何错误：
- 向用户报告具体错误
- 建议手动步骤（例如，手动创建文件）
- 提供可尝试的模板路径：
  - `/Users/vinayak/Documents/claude-scientific-writer/templates/CLAUDE.scientific-writer.md`（本地开发）
  - `~/.claude/plugins/*/claude-scientific-writer/templates/CLAUDE.scientific-writer.md`（已安装的插件）
- 如果仍然找不到模板，提供创建一个带有最少 scientific writing 指令的基础 CLAUDE.md 的选项
