---
name: docx
description: "文档工具包（.docx）。创建/编辑文档、修订追踪、评论、格式保留、文本提取，用于专业文档处理。"
license: 专有。LICENSE.txt 包含完整条款
---

# DOCX 创建、编辑和分析

## 概述

.docx 文件是包含 XML 文件和资源的 ZIP 存档。使用文本提取、原始 XML 访问或修订流程来创建、编辑或分析 Word 文档。将此技能应用于专业文档处理、修订追踪和内容操作。

## 使用科学示意图增强视觉效果

**使用此技能创建文档时，请始终考虑添加科学图表和示意图以增强视觉传达。**

如果您的文档尚不包含示意图或图表：
- 使用 **scientific-schematics** 技能生成 AI 驱动的出版物级质量图表
- 只需用自然语言描述您想要的图表
- Nano Banana Pro 将自动生成、审阅和改进示意图

**对于新文档：** 应默认生成科学示意图，以直观呈现文本中描述的关键概念、工作流程、架构或关系。

**如何生成示意图：**
```bash
python scripts/generate_schematic.py "您的图表描述" -o figures/output.png
```

AI 将自动：
- 创建具有正确格式的出版物级质量图像
- 通过多次迭代审阅和改进
- 确保可访问性（适合色盲、高对比度）
- 将输出保存在 figures/ 目录中

**何时添加示意图：**
- 文档工作流程图
- 流程图
- 系统架构图
- 数据流图
- 组织结构图
- 任何受益于可视化的复杂概念

有关创建示意图的详细指南，请参阅 scientific-schematics 技能文档。

---

## 工作流决策树

### 读取/分析内容
使用下面的"文本提取"或"原始 XML 访问"部分

### 创建新文档
使用"创建新 Word 文档"工作流

### 编辑现有文档
- **您自己的文档 + 简单更改**
  使用"基本 OOXML 编辑"工作流

- **其他人的文档**
  使用**"修订工作流"**（推荐默认）

- **法律、学术、商业或政府文档**
  使用**"修订工作流"**（必需）

## 读取和分析内容

### 文本提取
要读取文档的文本内容，使用 pandoc 将文档转换为 markdown。Pandoc 提供了出色的支持来保留文档结构，并能显示修订追踪：

```bash
# 将文档转换为带修订追踪的 markdown
pandoc --track-changes=all 文档路径.docx -o output.md
# 选项：--track-changes=accept/reject/all
```

### 原始 XML 访问
原始 XML 访问适用于：评论、复杂格式、文档结构、嵌入媒体和元数据。对于这些功能，请解压文档并读取其原始 XML 内容。

#### 解压文件
`python ooxml/scripts/unpack.py <office_file> <output_directory>`

#### 关键文件结构
* `word/document.xml` - 主文档内容
* `word/comments.xml` - 文档中引用的评论
* `word/media/` - 嵌入的图片和媒体文件
* 修订追踪使用 `<w:ins>`（插入）和 `<w:del>`（删除）标签

## 创建新 Word 文档

从零开始创建新 Word 文档时，使用 **docx-js**，它允许您使用 JavaScript/TypeScript 创建 Word 文档。

### 工作流
1. **必须 - 阅读整个文件**：从头到尾完整阅读 [`docx-js.md`](docx-js.md)（约 500 行）。**阅读此文件时切勿设置任何范围限制。** 在继续创建文档之前，请阅读完整文件内容以了解详细语法、关键格式规则和最佳实践。
2. 使用 Document、Paragraph、TextRun 组件创建 JavaScript/TypeScript 文件（您可以假设所有依赖已安装，如果没有，请参阅下面的依赖部分）
3. 使用 Packer.toBuffer() 导出为 .docx

## 编辑现有 Word 文档

编辑现有 Word 文档时，使用 **Document 库**（用于 OOXML 操作的 Python 库）。该库自动处理基础架构设置，并提供文档操作方法。对于复杂场景，您可以直接通过该库访问底层 DOM。

### 工作流
1. **必须 - 阅读整个文件**：从头到尾完整阅读 [`ooxml.md`](ooxml.md)（约 600 行）。**阅读此文件时切勿设置任何范围限制。** 阅读完整文件内容以了解 Document 库 API 和直接编辑文档文件的 XML 模式。
2. 解压文档：`python ooxml/scripts/unpack.py <office_file> <output_directory>`
3. 使用 Document 库创建并运行 Python 脚本（请参阅 ooxml.md 中的"Document 库"部分）
4. 打包最终文档：`python ooxml/scripts/pack.py <input_directory> <office_file>`

Document 库同时提供用于常见操作的高级方法和用于复杂场景的直接 DOM 访问。

## 文档审阅的修订工作流

此工作流允许在 OOXML 中实施之前，使用 markdown 规划全面的修订追踪。**关键**：要实现完整的修订追踪，请系统性地实施所有更改。

**分批策略**：将相关更改分组为 3-10 个更改一批。这使调试易于管理，同时保持效率。在进入下一批之前测试每一批。

**原则：最小化、精确编辑**
实施修订追踪时，只标记实际更改的文本。重复未更改的文本会使编辑更难以审阅，且显得不专业。将替换分解为：[未更改文本] + [删除] + [插入] + [未更改文本]。通过从原始内容中提取 `<w:r>` 元素并重用它来保留未更改文本的原始运行 RSID。

示例 - 将句子中的"30 天"改为"60 天"：
```python
# 差 - 替换整个句子
'<w:del><w:r><w:delText>期限为 30 天。</w:delText></w:r></w:del><w:ins><w:r><w:t>期限为 60 天。</w:t></w:r></w:ins>'

# 好 - 只标记更改的部分，为未更改文本保留原始 <w:r>
'<w:r w:rsidR="00AB12CD"><w:t>期限为 </w:t></w:r><w:del><w:r><w:delText>30</w:delText></w:r></w:del><w:ins><w:r><w:t>60</w:t></w:r></w:ins><w:r w:rsidR="00AB12CD"><w:t> 天。</w:t></w:r>'
```

### 修订追踪工作流

1. **获取 markdown 表示**：将文档转换为保留修订追踪的 markdown：
   ```bash
   pandoc --track-changes=all 文档路径.docx -o current.md
   ```

2. **识别并分组更改**：审阅文档并识别所有需要的更改，将其组织成逻辑批次：

   **定位方法**（用于在 XML 中查找更改）：
   - 节/标题编号（例如"第 3.2 节"、"第四条"）
   - 段落标识符（如果已编号）
   - 具有唯一周围文本的 Grep 模式
   - 文档结构（例如"第一段"、"签名块"）
   - **不要使用 markdown 行号** - 它们无法映射到 XML 结构

   **批次组织**（每批分组 3-10 个相关更改）：
   - 按节："第一批：第 2 节修正"、"第二批：第 5 节更新"
   - 按类型："第一批：日期更正"、"第二批：当事方名称更改"
   - 按复杂性：从简单的文本替换开始，然后处理复杂的结构更改
   - 按顺序："第一批：第 1-3 页"、"第二批：第 4-6 页"

3. **阅读文档并解压**：
   - **必须 - 阅读整个文件**：从头到尾完整阅读 [`ooxml.md`](ooxml.md)（约 600 行）。**阅读此文件时切勿设置任何范围限制。** 请特别注意"Document 库"和"修订追踪模式"部分。
   - **解压文档**：`python ooxml/scripts/unpack.py <file.docx> <dir>`
   - **记下建议的 RSID**：解压脚本将建议一个用于您的修订追踪的 RSID。在步骤 4b 中复制此 RSID 以供使用。

4. **分批实施更改**：逻辑性地分组更改（按节、按类型或按邻近），并在单个脚本中一起实施。这种方法：
   - 使调试更容易（批次越小越容易隔离错误）
   - 允许增量进度
   - 保持效率（3-10 个更改的批次大小效果良好）

   **建议的批次分组**：
   - 按文档节（例如"第 3 节更改"、"定义"、"终止条款"）
   - 按更改类型（例如"日期更改"、"当事方名称更新"、"法律术语替换"）
   - 按邻近（例如"第 1-3 页的更改"、"文档前半部分的更改"）

   对于每批相关更改：

   **a. 将文本映射到 XML**：在 `word/document.xml` 中 grep 文本，以验证文本如何拆分到 `<w:r>` 元素中。

   **b. 创建并运行脚本**：使用 `get_node` 查找节点，实施更改，然后 `doc.save()`。请参阅 ooxml.md 中的 **"Document 库"** 部分获取模式。

   **注意**：在编写脚本之前，始终立即 grep `word/document.xml` 以获取当前行号并验证文本内容。每运行一次脚本后行号都会更改。

5. **打包文档**：所有批次完成后，将解压的目录转回 .docx：
   ```bash
   python ooxml/scripts/pack.py unpacked reviewed-document.docx
   ```

6. **最终验证**：对完整文档进行全面检查：
   - 将最终文档转换为 markdown：
     ```bash
     pandoc --track-changes=all reviewed-document.docx -o verification.md
     ```
   - 验证所有更改已正确应用：
     ```bash
     grep "原始短语" verification.md  # 不应找到它
     grep "替换短语" verification.md  # 应该找到它
     ```
   - 检查没有引入意外更改

## 将文档转换为图像

要直观地分析 Word 文档，请使用两步流程将其转换为图像：

1. **将 DOCX 转换为 PDF**：
   ```bash
   soffice --headless --convert-to pdf document.docx
   ```

2. **将 PDF 页面转换为 JPEG 图像**：
   ```bash
   pdftoppm -jpeg -r 150 document.pdf page
   ```
   这将创建 `page-1.jpg`、`page-2.jpg` 等文件。

选项：
- `-r 150`：设置分辨率为 150 DPI（根据质量/大小平衡调整）
- `-jpeg`：输出 JPEG 格式（如果喜欢 PNG 可使用 `-png`）
- `-f N`：要转换的首页（例如 `-f 2` 从第 2 页开始）
- `-l N`：要转换的末页（例如 `-l 5` 在第 5 页停止）
- `page`：输出文件的前缀

特定范围的示例：
```bash
pdftoppm -jpeg -r 150 -f 2 -l 5 document.pdf page  # 仅转换第 2-5 页
```

## 代码风格指南
**重要**：生成 DOCX 操作代码时：
- 编写简洁的代码
- 避免冗长的变量名和冗余操作
- 避免不必要的 print 语句

## 依赖项

所需依赖项（如果不可用则安装）：

- **pandoc**：`sudo apt-get install pandoc`（用于文本提取）
- **docx**：`npm install -g docx`（用于创建新文档）
- **LibreOffice**：`sudo apt-get install libreoffice`（用于 PDF 转换）
- **Poppler**：`sudo apt-get install poppler-utils`（用于 pdftoppm 将 PDF 转换为图像）
- **defusedxml**：`pip install defusedxml`（用于安全 XML 解析）
