# 安装与配置

## 系统要求

### 硬件要求
- **GPU**：需要 NVIDIA A6000（48GB 最低）用于生成带有对话头部功能的视频
- **CPU**：推荐多核处理器用于 PDF 处理和文档转换
- **RAM**：最低 16GB，推荐 32GB 用于大型论文

### 软件要求
- **Python**：3.11 或更高版本
- **Conda**：用于依赖隔离的环境管理器
- **LibreOffice**：用于文档格式转换（PDF 转 PPTX 等）
- **Poppler 工具**：用于 PDF 处理和操作

## 安装步骤

### 1. 克隆仓库
```bash
git clone https://github.com/YuhangChen1/Paper2All.git
cd Paper2All
```

### 2. 创建 Conda 环境
```bash
conda create -n paper2all python=3.11
conda activate paper2all
```

### 3. 安装依赖
```bash
pip install -r requirements.txt
```

### 4. 安装系统依赖

**Ubuntu/Debian：**
```bash
sudo apt-get install libreoffice poppler-utils
```

**macOS：**
```bash
brew install libreoffice poppler
```

**Windows：**
- 从 https://www.libreoffice.org/ 下载并安装 LibreOffice
- 从 https://github.com/oschwartz10612/poppler-windows 下载并安装 Poppler

## API 配置

在项目根目录创建 `.env` 文件，并添加以下凭证：

### 必需的 API 密钥

**选项 1：OpenAI API**
```
OPENAI_API_KEY=your_openai_api_key_here
```

**选项 2：OpenRouter API**（OpenAI 的替代方案）
```
OPENROUTER_API_KEY=your_openrouter_api_key_here
```

### 可选的 API 密钥

**Google Search API**（用于自动发现图标）
```
GOOGLE_API_KEY=your_google_api_key_here
GOOGLE_CSE_ID=your_custom_search_engine_id_here
```

## 模型配置

系统支持多个 LLM 后端：

### 支持的模型
- GPT-4（推荐，质量最佳）
- GPT-4.1（最新版本）
- GPT-3.5-turbo（更快，成本更低）
- 通过 OpenRouter 的 Claude 模型
- 其他 OpenRouter 支持的模型

### 模型选择

使用 `--model-choice` 参数或 `--model_name_t` 和 `--model_name_v` 参数指定模型：
- 模型选择 1：所有组件使用 GPT-4
- 模型选择 2：所有组件使用 GPT-4.1
- 自定义：为文本和视觉处理指定不同的模型

## 验证

测试安装：

```bash
python pipeline_all.py --help
```

如果成功，您应该看到包含所有可用选项的帮助菜单。

## 故障排除

### 常见问题

**1. 找不到 LibreOffice**
- 确保 LibreOffice 已安装并在系统 PATH 中
- 尝试运行 `libreoffice --version` 进行验证

**2. 找不到 Poppler 工具**
- 使用 `pdftoppm -v` 验证安装
- 如需要，将 Poppler bin 目录添加到 PATH

**3. 视频生成的 GPU/CUDA 错误**
- 确保 NVIDIA 驱动是最新版本
- 验证 CUDA 工具包已安装
- 使用 `nvidia-smi` 检查 GPU 内存

**4. API 密钥错误**
- 验证 `.env` 文件在项目根目录
- 检查 API 密钥是否有效且有足够的配额
- 确保 `.env` 中密钥周围没有多余的空格或引号

## 目录结构

安装后，组织您的工作空间：

```
Paper2All/
├── .env                  # API 凭证
├── input/               # 在此放置论文文件
│   └── paper_name/      # 每篇论文在各自的目录中
│       └── main.tex     # LaTeX 源文件或 PDF
├── output/              # 生成的输出
│   └── paper_name/
│       ├── website/     # 生成的网站文件
│       ├── video/       # 生成的视频文件
│       └── poster/     # 生成的海报文件
└── ...
```
