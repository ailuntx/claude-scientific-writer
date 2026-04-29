# MarkItDown 安装指南

## 前置要求

- Python 3.10 或更高版本
- pip 包管理器
- 虚拟环境（推荐）

## 基本安装

### 安装所有功能（推荐）

```bash
pip install 'markitdown[all]'
```

这将安装所有文件格式和功能的支持。

### 安装特定功能

如果您只需要某些文件格式，可以安装特定的依赖：

```bash
# 仅支持 PDF
pip install 'markitdown[pdf]'

# Office 文档
pip install 'markitdown[docx,pptx,xlsx]'

# 多种格式
pip install 'markitdown[pdf,docx,pptx,xlsx,audio-transcription]'
```

### 从源码安装

```bash
git clone https://github.com/microsoft/markitdown.git
cd markitdown
pip install -e 'packages/markitdown[all]'
```

## 可选依赖

| 功能 | 安装命令 | 使用场景 |
|---------|--------------|----------|
| 所有格式 | `pip install 'markitdown[all]'` | 全部功能 |
| PDF | `pip install 'markitdown[pdf]'` | PDF 文档 |
| Word | `pip install 'markitdown[docx]'` | DOCX 文件 |
| PowerPoint | `pip install 'markitdown[pptx]'` | PPTX 文件 |
| Excel（新） | `pip install 'markitdown[xlsx]'` | XLSX 文件 |
| Excel（旧） | `pip install 'markitdown[xls]'` | XLS 文件 |
| Outlook | `pip install 'markitdown[outlook]'` | MSG 文件 |
| Azure DI | `pip install 'markitdown[az-doc-intel]'` | 增强型 PDF |
| 音频 | `pip install 'markitdown[audio-transcription]'` | WAV/MP3 |
| YouTube | `pip install 'markitdown[youtube-transcription]'` | YouTube 视频 |

## 系统依赖

### OCR 支持（用于扫描文档和图像）

#### macOS
```bash
brew install tesseract
```

#### Ubuntu/Debian
```bash
sudo apt-get update
sudo apt-get install tesseract-ocr
```

#### Windows
从以下地址下载：https://github.com/UB-Mannheim/tesseract/wiki

### Poppler 工具（用于高级 PDF 操作）

#### macOS
```bash
brew install poppler
```

#### Ubuntu/Debian
```bash
sudo apt-get install poppler-utils
```

## 验证

测试您的安装：

```bash
# 检查版本
python -c "import markitdown; print('MarkItDown installed successfully')"

# 测试基本转换
echo "Test" > test.txt
markitdown test.txt
rm test.txt
```

## 虚拟环境设置

### 使用 venv

```bash
# 创建虚拟环境
python -m venv markitdown-env

# 激活（macOS/Linux）
source markitdown-env/bin/activate

# 激活（Windows）
markitdown-env\Scripts\activate

# 安装
pip install 'markitdown[all]'
```

### 使用 conda

```bash
# 创建环境
conda create -n markitdown python=3.12

# 激活
conda activate markitdown

# 安装
pip install 'markitdown[all]'
```

### 使用 uv

```bash
# 创建虚拟环境
uv venv --python=3.12 .venv

# 激活
source .venv/bin/activate

# 安装
uv pip install 'markitdown[all]'
```

## AI 增强设置（可选）

使用 OpenRouter 进行 AI 驱动的图像描述：

### OpenRouter API

OpenRouter 提供通过单一 API 访问多个 AI 模型（GPT-4、Claude、Gemini 等）的统一访问。

```bash
# 安装 OpenAI SDK（必需，已包含在 markitdown 中）
pip install openai

# 从 https://openrouter.ai/keys 获取 API 密钥

# 设置 API 密钥
export OPENROUTER_API_KEY="sk-or-v1-..."

# 添加到 shell 配置文件中以持久化
echo 'export OPENROUTER_API_KEY="sk-or-v1-..."' >> ~/.bashrc  # Linux
echo 'export OPENROUTER_API_KEY="sk-or-v1-..."' >> ~/.zshrc   # macOS
```

**为什么选择 OpenRouter？**
- 通过一个 API 访问 100+ 个 AI 模型
- 可在 GPT-4、Claude、Gemini 等之间选择
- 有竞争力的定价
- 无供应商锁定
- 简单的 OpenAI 兼容接口

**图像描述的热门模型：**
- `anthropic/claude-sonnet-4.5` - **推荐** - 最适合科学视觉
- `anthropic/claude-opus-4.5` - 卓越的技术分析
- `openai/gpt-4o` - 良好的视觉理解
- `google/gemini-pro-vision` - 成本效益选项

请参阅 https://openrouter.ai/models 获取完整的模型列表和定价。

## Azure 文档智能设置（可选）

用于增强型 PDF 转换：

1. 在 Azure 门户中创建 Azure 文档智能资源
2. 获取端点和密钥
3. 设置环境变量：

```bash
export AZURE_DOCUMENT_INTELLIGENCE_KEY="your-key"
export AZURE_DOCUMENT_INTELLIGENCE_ENDPOINT="https://your-endpoint.cognitiveservices.azure.com/"
```

## Docker 安装（替代方案）

```bash
# 克隆仓库
git clone https://github.com/microsoft/markitdown.git
cd markitdown

# 构建镜像
docker build -t markitdown:latest .

# 运行
docker run --rm -i markitdown:latest < input.pdf > output.md
```

## 故障排除

### 导入错误
```
ModuleNotFoundError: No module named 'markitdown'
```

**解决方案**：确保您在正确的虚拟环境中且 markitdown 已安装：
```bash
pip install 'markitdown[all]'
```

### 缺少功能
```
Error: PDF conversion not supported
```

**解决方案**：安装特定功能：
```bash
pip install 'markitdown[pdf]'
```

### OCR 不工作

**解决方案**：安装 Tesseract OCR（请参阅上面的系统依赖）

### 权限错误

**解决方案**：使用虚拟环境或使用 `--user` 标志安装：
```bash
pip install --user 'markitdown[all]'
```

## 升级

```bash
# 升级到最新版本
pip install --upgrade 'markitdown[all]'

# 检查版本
pip show markitdown
```

## 卸载

```bash
pip uninstall markitdown
```

## 下一步

安装后：
1. 阅读 `QUICK_REFERENCE.md` 了解基本用法
2. 查看 `SKILL.md` 获取综合指南
3. 尝试 `scripts/` 目录中的示例脚本
4. 查看 `assets/example_usage.md` 获取实际示例

## 技能脚本设置

要使用技能脚本：

```bash
# 导航到脚本目录
cd /Users/vinayak/Documents/claude-scientific-writer/.claude/skills/markitdown/scripts

# 脚本已经是可执行的，直接运行
python batch_convert.py --help
python convert_with_ai.py --help
python convert_literature.py --help
```

## 测试安装

创建测试文件以验证一切正常：

```python
# test_markitdown.py
from markitdown import MarkItDown

def test_basic():
    md = MarkItDown()
    # 创建简单的测试文件
    with open("test.txt", "w") as f:
        f.write("Hello MarkItDown!")
    
    # 转换它
    result = md.convert("test.txt")
    print("✓ 基本转换正常工作")
    print(result.text_content)
    
    # 清理
    import os
    os.remove("test.txt")

if __name__ == "__main__":
    test_basic()
```

运行它：
```bash
python test_markitdown.py
```

## 获取帮助

- **文档**：请参阅 `SKILL.md` 和 `README.md`
- **GitHub 问题**：https://github.com/microsoft/markitdown/issues
- **示例**：`assets/example_usage.md`
- **API 参考**：`references/api_reference.md`
