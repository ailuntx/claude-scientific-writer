# 文件格式支持

本文档提供有关 MarkItDown 支持的每种文件格式的详细信息。

## 文档格式

### PDF (.pdf)

**功能**：
- 文本提取
- 表格检测
- 元数据提取
- 扫描文档的 OCR（需要依赖项）

**依赖项**：
```bash
pip install 'markitdown[pdf]'
```

**最适用于**：
- 科学论文
- 报告
- 书籍
- 表单

**限制**：
- 复杂布局可能无法保留完美的格式
- 扫描的 PDF 需要配置 OCR
- 某些 PDF 功能（注释、表单）可能无法转换

**示例**：
```python
from markitdown import MarkItDown

md = MarkItDown()
result = md.convert("research_paper.pdf")
print(result.text_content)
```

**使用 Azure Document Intelligence 增强**：
```python
md = MarkItDown(docintel_endpoint="https://YOUR-ENDPOINT.cognitiveservices.azure.com/")
result = md.convert("complex_layout.pdf")
```

---

### Microsoft Word (.docx)

**功能**：
- 文本提取
- 表格转换
- 标题层级
- 列表格式
- 基本文本格式（粗体、斜体）

**依赖项**：
```bash
pip install 'markitdown[docx]'
```

**最适用于**：
- 科学论文
- 报告
- 文档
- 手稿

**保留的元素**：
- 标题（转换为 Markdown 标题）
- 表格（转换为 Markdown 表格）
- 列表（无序和有序）
- 基本格式（粗体、斜体）
- 段落

**示例**：
```python
result = md.convert("manuscript.docx")
```

---

### PowerPoint (.pptx)

**功能**：
- 幻灯片内容提取
- 演讲者备注
- 表格提取
- 图片描述（使用 AI）

**依赖项**：
```bash
pip install 'markitdown[pptx]'
```

**最适用于**：
- 演示文稿
- 讲座幻灯片
- 会议演讲

**输出格式**：
```markdown
# Slide 1: Title

Content from slide 1...

**Notes**: Speaker notes appear here

---

# Slide 2: Next Topic

...
```

**使用 AI 图片描述**：
```python
from openai import OpenAI

client = OpenAI()
md = MarkItDown(llm_client=client, llm_model="gpt-4o")
result = md.convert("presentation.pptx")
```

---

### Excel (.xlsx, .xls)

**功能**：
- 工作表提取
- 表格格式
- 数据保留
- 公式值（计算后）

**依赖项**：
```bash
pip install 'markitdown[xlsx]'  # 现代 Excel
pip install 'markitdown[xls]'   # 旧版 Excel
```

**最适用于**：
- 数据表格
- 研究数据
- 统计结果
- 实验数据

**输出格式**：
```markdown
# Sheet: Results

| Sample | Control | Treatment | P-value |
|--------|---------|-----------|---------|
| 1      | 10.2    | 12.5      | 0.023   |
| 2      | 9.8     | 11.9      | 0.031   |
```

**示例**：
```python
result = md.convert("experimental_data.xlsx")
```

---

## 图片格式

### 图片 (.jpg, .jpeg, .png, .gif, .webp)

**功能**：
- EXIF 元数据提取
- OCR 文本提取
- AI 驱动的图片描述

**依赖项**：
```bash
pip install 'markitdown[all]'  # 包含图片支持
```

**最适用于**：
- 扫描文档
- 图表
- 科学图表
- 带有文字的照片

**无 AI 的输出**：
```markdown
![Image](image.jpg)

**EXIF Data**:
- Camera: Canon EOS 5D
- Date: 2024-01-15
- Resolution: 4000x3000
```

**使用 AI 的输出**：
```python
from openai import OpenAI

client = OpenAI()
md = MarkItDown(
    llm_client=client,
    llm_model="gpt-4o",
    llm_prompt="Describe this scientific diagram in detail"
)
result = md.convert("graph.png")
```

**用于文本提取的 OCR**：
需要 Tesseract OCR：
```bash
# macOS
brew install tesseract

# Ubuntu
sudo apt-get install tesseract-ocr
```

---

## 音频格式

### 音频 (.wav, .mp3)

**功能**：
- 元数据提取
- 语音转文字转录
- 时长和技术信息

**依赖项**：
```bash
pip install 'markitdown[audio-transcription]'
```

**最适用于**：
- 讲座录音
- 访谈
- 播客
- 会议录音

**输出格式**：
```markdown
# Audio: interview.mp3

**Metadata**:
- Duration: 45:32
- Bitrate: 320kbps
- Sample Rate: 44100Hz

**Transcription**:
[Transcribed text appears here...]
```

**示例**：
```python
result = md.convert("lecture.mp3")
```

---

## 网页格式

### HTML (.html, .htm)

**功能**：
- 干净的 HTML 到 Markdown 转换
- 链接保留
- 表格转换
- 列表格式

**最适用于**：
- 网页
- 文档
- 博客文章
- 在线文章

**输出格式**：保留链接和结构的干净 Markdown

**示例**：
```python
result = md.convert("webpage.html")
```

---

### YouTube 链接

**功能**：
- 获取视频转录
- 提取视频元数据
- 字幕下载

**依赖项**：
```bash
pip install 'markitdown[youtube-transcription]'
```

**最适用于**：
- 教育视频
- 讲座
- 演讲
- 教程

**示例**：
```python
result = md.convert("https://www.youtube.com/watch?v=VIDEO_ID")
```

---

## 数据格式

### CSV (.csv)

**功能**：
- 自动表格转换
- 分隔符检测
- 表头保留

**输出格式**：Markdown 表格

**示例**：
```python
result = md.convert("data.csv")
```

**输出**：
```markdown
| Column1 | Column2 | Column3 |
|---------|---------|---------|
| Value1  | Value2  | Value3  |
```

---

### JSON (.json)

**功能**：
- 结构化表示
- 格式化输出
- 嵌套数据可视化

**最适用于**：
- API 响应
- 配置文件
- 数据导出

**示例**：
```python
result = md.convert("data.json")
```

---

### XML (.xml)

**功能**：
- 结构保留
- 属性提取
- 格式化输出

**最适用于**：
- 配置文件
- 数据交换
- 结构化文档

**示例**：
```python
result = md.convert("config.xml")
```

---

## 压缩包格式

### ZIP (.zip)

**功能**：
- 遍历压缩包内容
- 单独转换每个文件
- 在输出中保持目录结构

**最适用于**：
- 文档集合
- 项目压缩包
- 批量转换

**输出格式**：
```markdown
# Archive: documents.zip

## File: document1.pdf
[Content from document1.pdf...]

---

## File: document2.docx
[Content from document2.docx...]
```

**示例**：
```python
result = md.convert("archive.zip")
```

---

## 电子书格式

### EPUB (.epub)

**功能**：
- 完整文本提取
- 章节结构
- 元数据提取

**最适用于**：
- 电子书
- 数字出版物
- 长篇内容

**输出格式**：保留章节结构的 Markdown

**示例**：
```python
result = md.convert("book.epub")
```

---

## 其他格式

### Outlook 邮件 (.msg)

**功能**：
- 邮件内容提取
- 附件列表
- 元数据（发件人、收件人、主题、日期）

**依赖项**：
```bash
pip install 'markitdown[outlook]'
```

**最适用于**：
- 邮件归档
- 通信记录

**示例**：
```python
result = md.convert("message.msg")
```

---

## 格式特定技巧

### PDF 最佳实践

1. **对于复杂布局，使用 Azure Document Intelligence**：
   ```python
   md = MarkItDown(docintel_endpoint="endpoint_url")
   ```

2. **对于扫描的 PDF，确保配置好 OCR**：
   ```bash
   brew install tesseract  # macOS
   ```

3. **转换前拆分非常大的 PDF** 以获得更好的性能

### PowerPoint 最佳实践

1. **使用 AI 处理视觉内容**：
   ```python
   md = MarkItDown(llm_client=client, llm_model="gpt-4o")
   ```

2. **检查演讲者备注** - 它们包含在输出中

3. **复杂的动画不会被捕获** - 仅静态内容

### Excel 最佳实践

1. **大型电子表格** 可能需要较长时间转换

2. **公式会转换为其计算值**

3. **多个工作表** 都包含在输出中

4. **图表会变成文本描述**（使用 AI 获得更好的描述）

### 图片最佳实践

1. **使用 AI 获得有意义的描述**：
   ```python
   md = MarkItDown(
       llm_client=client,
       llm_model="gpt-4o",
       llm_prompt="Describe this scientific figure in detail"
   )
   ```

2. **对于文字密集的图片，确保安装 OCR 依赖项**

3. **高分辨率图片** 可能需要更长的处理时间

### 音频最佳实践

1. **清晰的音频** 能产生更好的转录

2. **长录音** 可能需要相当长的时间

3. **考虑拆分长音频文件** 以加快处理速度

---

## 不支持的格式

如果需要转换不支持的格式：

1. **创建自定义转换器**（参见 `api_reference.md`）
2. **在 GitHub 上寻找插件** (#markitdown-plugin)
3. **预先转换为支持的格式**（例如，将 .rtf 转换为 .docx）

---

## 格式检测

MarkItDown 自动从以下内容检测格式：

1. **文件扩展名**（主要方法）
2. **MIME 类型**（后备）
3. **文件签名**（魔数，后备）

**覆盖检测**：
```python
# 强制指定格式
result = md.convert("file_without_extension", file_extension=".pdf")

# 使用流
with open("file", "rb") as f:
    result = md.convert_stream(f, file_extension=".pdf")
```
