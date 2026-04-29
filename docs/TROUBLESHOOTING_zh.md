# 故障排除指南

本文档提供了在使用 Claude Scientific Writer 时可能遇到的常见问题解决方案。

## 目录
- [Windows：Claude Code 未找到错误](#windows-claude-code-未找到错误)
- [API 密钥问题](#api-密钥问题)
- [安装问题](#安装问题)
- [LaTeX 编译问题](#latex-编译问题)
- [常规问题](#常规问题)

---

## Windows：Claude Code 未找到错误

### 问题
在 Windows 上运行 scientific writer 时，您可能会遇到此错误：
```
Error: Claude Code not found at: C:\Users\<username>\AppData\Roaming\npm\claude.CMD Please try again or type 'exit' to quit.
```

即使 `claude.CMD` 存在于指定路径并且直接调用时可正常工作，`claude-agent-sdk` 仍可能无法正确定位或执行它。

### 解决方案

#### 1. 验证 Claude Code CLI 安装
首先，测试 Claude Code 是否能直接从命令提示符运行：
```cmd
claude
```

如果这不能正常工作，请重新安装 Claude Code CLI：
```cmd
npm uninstall -g @anthropic-ai/claude-code
npm install -g @anthropic-ai/claude-code
```

#### 2. 检查 PATH 配置
验证 npm 的全局 bin 目录是否在系统 PATH 中：

```cmd
where claude
echo %PATH%
```

输出中应包含 `C:\Users\<username>\AppData\Roaming\npm`。 

**将 npm 添加到 PATH（如果缺失）：**
1. 按下 `Win + X` 并选择 "System"
2. 点击 "Advanced system settings"
3. 点击 "Environment Variables"
4. 在 "User variables" 或 "System variables" 下找到 "Path" 并点击 "Edit"
5. 点击 "New" 并添加：`C:\Users\<username>\AppData\Roaming\npm`
6. 点击 "OK" 保存

#### 3. 重启终端
在更改 PATH 之后，**完全关闭并重新打开**命令提示符或 PowerShell 窗口，以重新加载环境变量。

#### 4. 以管理员身份运行
Windows 权限有时会干扰 `.CMD` 文件执行。尝试以管理员身份运行终端：
1. 右键单击 Command Prompt 或 PowerShell
2. 选择 "Run as administrator"
3. 导航到您的项目目录
4. 再次运行 scientific writer

#### 5. 使用 Node.js Command Prompt
如果您通过 Windows 安装程序安装了 Node.js，请尝试使用随附的 "Node.js command prompt"，而不是常规命令提示符。

#### 6. 替代方案：Windows Subsystem for Linux (WSL)
如果上述步骤都无法解决问题，请考虑使用 [WSL](https://learn.microsoft.com/en-us/windows/wsl/install)：

```bash
# 在 PowerShell 中（以管理员身份）
wsl --install
```

然后在您的 WSL 环境中安装 Node.js 和 scientific writer，Claude Code CLI 通常在那里兼容性问题更少。

#### 7. 直接尝试使用 npx
如果 Claude Code 可以从命令行运行，但 SDK 找不到它，请尝试使用 `npx` 运行它：

```cmd
npx @anthropic-ai/claude-code --version
```

如果这可以工作，您可能遇到了与 Python/SDK 启动进程方式相关的 PATH 解析问题。

#### 8. 检查是否存在多个 Node.js 安装
多个 Node.js 安装可能会导致 PATH 冲突：

```cmd
where node
where npm
npm config get prefix
```

如果您看到多个路径，这可能就是导致问题的原因。

#### 9. 尝试虚拟环境
创建一个新的 Python 虚拟环境以隔离安装：

```cmd
python -m venv venv
venv\Scripts\activate
pip install -e .
```

然后在该虚拟环境中运行 scientific writer。

### 已知问题：Windows 上的 SDK 兼容性（无管理员权限）

**如果您已确认：**
- ✅ 直接调用时 `claude` 可用（`claude --version` 显示版本 2.0.28 或类似）
- ✅ npm 全局路径在您的 PATH 中（`C:\Users\<username>\AppData\Roaming\npm`）
- ✅ 包已正确安装（`npm list -g @anthropic-ai/claude-code` 可显示它）
- ✅ 已尝试 CMD 和 PowerShell
- ❌ 没有管理员权限来修改系统设置

**这似乎是 `claude-agent-sdk` 在 Windows 上的子进程执行问题。**

该 SDK 可能使用了一种进程启动方式，无法在非管理员环境下正确解析 Windows 上的 `.CMD` 文件。这是一个 **上游 SDK 问题**。

**临时解决方法：**

1. **在无管理员权限下使用 WSL**：如果您的 IT 部门已启用，您可以作为普通用户安装 WSL：
   ```powershell
   wsl --install --distribution Ubuntu
   ```
   然后在 WSL 中设置项目，那里 SDK 的兼容性更好。

2. **尝试 Git Bash**：如果您安装了 Git for Windows，请尝试从 Git Bash 而不是 CMD/PowerShell 运行 scientific writer，因为它提供了更接近 Unix 的环境。

3. **请求 IT 协助**：请您的 IT 部门：
   - 授予您临时管理员权限以安装软件
   - 将工具安装到系统范围的位置
   - 如果尚未启用，则启用 WSL

4. **使用您的个人电脑**：作为短期变通方案，在您有管理员权限的设备上运行该工具（正如您提到在 Mac 上尝试过的那样）。

5. **报告 SDK 问题**：这很可能是 `claude-agent-sdk` 中的一个 bug。请考虑在 [Claude Agent SDK repository](https://github.com/anthropics/claude-agent-sdk) 上附带您的诊断信息提交 issue。

### 其他诊断
如果问题仍然存在，请收集以下信息以便进一步排查：

```cmd
# 检查 Claude 版本
claude --version

# 检查 npm 全局包
npm list -g @anthropic-ai/claude-code

# 检查 Node.js 版本
node --version

# 检查 npm 版本
npm --version

# 检查 npm 将全局包安装到哪里
npm config get prefix

# 检查 Python 版本
python --version

# 尝试 npx
npx @anthropic-ai/claude-code --version

# 检查是否存在多个 Node 安装
where node
where npm
```

在 GitHub 或 SDK repository 上报告问题时，请分享这些信息。

---

## API 密钥问题

### 问题："ANTHROPIC_API_KEY 环境变量未设置"

#### 解决方案 1：创建 .env 文件
在项目根目录中创建一个 `.env` 文件：
```bash
ANTHROPIC_API_KEY=your_api_key_here
```

#### 解决方案 2：在 shell 中导出
**Linux/macOS：**
```bash
export ANTHROPIC_API_KEY='your_api_key_here'
```

将其添加到 `~/.bashrc`、`~/.zshrc` 或 `~/.bash_profile` 以使其永久生效。

**Windows（PowerShell）：**
```powershell
$env:ANTHROPIC_API_KEY='your_api_key_here'
```

**Windows（Command Prompt）：**
```cmd
set ANTHROPIC_API_KEY=your_api_key_here
```

### 获取您的 API 密钥
1. 访问 [console.anthropic.com](https://console.anthropic.com/)
2. 登录或创建账户
3. 导航到 "API Keys"
4. 创建一个新密钥或复制已有密钥

---

## 安装问题

### 问题："Module not found" 错误

#### 解决方案：安装依赖
使用 uv（推荐）：
```bash
uv pip install -e .
```

使用 pip：
```bash
pip install -e .
```

### 问题：Python 版本不兼容

此项目要求 **Python 3.10 或更高版本**。

检查您的 Python 版本：
```bash
python --version
# 或
python3 --version
```

如果您需要升级，请访问 [python.org](https://www.python.org/downloads/)。

### 问题：安装时权限被拒绝

**Linux/macOS：**
```bash
# 使用 --user 标志
pip install --user -e .

# 或使用虚拟环境（推荐）
python -m venv venv
source venv/bin/activate
pip install -e .
```

**Windows：**
以管理员身份运行终端，或使用虚拟环境：
```cmd
python -m venv venv
venv\Scripts\activate
pip install -e .
```

---

## LaTeX 编译问题

### 问题：LaTeX 编译失败

#### 安装 LaTeX 发行版

**macOS：**
```bash
brew install --cask mactex
# 或安装更小体积的 BasicTeX
brew install --cask basictex
```

**Ubuntu/Debian：**
```bash
sudo apt-get update
sudo apt-get install texlive-full
# 或进行最小安装
sudo apt-get install texlive-latex-base texlive-latex-extra
```

**Windows：**
下载并安装 [MiKTeX](https://miktex.org/download) 或 [TeX Live](https://www.tug.org/texlive/windows.html)。

#### 缺少 LaTeX 包

如果您看到 "LaTeX Error: File `package.sty' not found":

**MiKTeX（Windows）：**
MiKTeX 通常会自动安装包。如果没有：
1. 打开 MiKTeX Console
2. 转到 "Packages"
3. 搜索缺失的包
4. 点击 "+" 安装

**TeX Live（Linux/macOS）：**
```bash
sudo tlmgr install <package-name>
```

#### 常见必需包
```bash
# 如果使用 tlmgr
sudo tlmgr install amsmath graphicx hyperref natbib geometry fancyhdr
```

---

## 常规问题

### 问题：访问文件时出现 "Permission denied"

检查文件权限：
```bash
# Linux/macOS
ls -l <file_path>
chmod +r <file_path>  # 添加读取权限
```

### 问题：脚本卡住或没有响应

1. **检查您的互联网连接** - 该工具需要连接到 Anthropic 的 API
2. **验证 API 密钥** - 确保您的 API 密钥有效并且有足够额度
3. **尝试 Ctrl+C** - 中断后重试
4. **检查 API 状态** - 访问 [status.anthropic.com](https://status.anthropic.com/)

### 问题：未创建输出目录

确保您在项目目录中有写入权限：
```bash
# 检查权限
ls -ld /path/to/claude-scientific-writer

# 如有需要，修复（Linux/macOS）
chmod u+w /path/to/claude-scientific-writer
```

### 问题：数据文件未被处理

1. 确保文件位于项目根目录下的 `data/` 文件夹中
2. 检查您是否有一个活动论文（无论是继续还是新建）
3. 验证文件权限允许读取
4. 检查控制台输出中的任何错误消息

### 问题：找不到已有论文

1. 论文必须位于 `writing_outputs/` 目录中
2. 论文目录应遵循格式：`YYYYMMDD_HHMMSS_topic_description`
3. 在引用论文时使用其主题中的关键词
4. 尝试使用明确的继续关键词，例如 "continue"、"update"、"the paper"

---

## 获取更多帮助

如果您已经尝试了上述解决方案但仍然遇到问题：

1. **查看 GitHub Issues**: [github.com/your-repo/issues](https://github.com)
2. **创建新 Issue**: 包含：
   - 操作系统及版本
   - Python 版本（`python --version`）
   - Node.js 版本（`node --version`）
   - Claude Code 版本（`claude --version`）
   - 完整错误信息和堆栈跟踪
   - 复现问题的步骤
3. **查看 README**: [README.md](../README.md)
4. **查看 Skills 文档**: [SKILLS.md](SKILLS.md)

---

## 为本指南做贡献

发现了这里未列出的问题解决方案？欢迎贡献！

1. Fork 仓库
2. 将您的解决方案添加到本文档中
3. 提交 pull request

您的贡献有助于社区！ 🙏
