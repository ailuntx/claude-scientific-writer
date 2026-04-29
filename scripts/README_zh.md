# 包管理脚本

此目录包含用于管理 scientific-writer 包的自动化脚本。

## 版本管理

### 提升版本号

按照语义化版本控制递增包版本：

```bash
# 提升补丁版本 (2.0.0 -> 2.0.1)
uv run scripts/bump_version.py patch

# 提升次版本 (2.0.0 -> 2.1.0)
uv run scripts/bump_version.py minor

# 提升主版本 (2.0.0 -> 3.0.0)
uv run scripts/bump_version.py major
```

脚本会自动更新以下文件中的版本号：
- `pyproject.toml`
- `scientific_writer/__init__.py`

提升版本后：
1. 使用 `git diff` 查看更改
2. 更新 `CHANGELOG.md`
3. 提交版本更改
4. 创建 git tag
5. 发布到 PyPI

## 发布到 PyPI

### 前提条件

使用以下任一方式设置 PyPI 凭据：

**选项 1：环境变量（推荐）**
```bash
export UV_PUBLISH_TOKEN="pypi-your-token-here"
```

**选项 2：`.pypirc` 文件**
创建 `~/.pypirc`：
```ini
[pypi]
username = __token__
password = pypi-your-token-here
```

### 发布包

```bash
# 发布当前版本
uv run scripts/publish.py

# 提升补丁版本并发布
uv run scripts/publish.py --bump patch

# 提升次版本并发布
uv run scripts/publish.py --bump minor

# 试运行（仅构建，不发布）
uv run scripts/publish.py --dry-run

# 跳过创建 git tag
uv run scripts/publish.py --skip-tag

# 跳过 git 状态检查（谨慎使用）
uv run scripts/publish.py --skip-git-check
```

发布脚本会：
1. 验证 git 工作目录是否干净（除非使用 `--skip-git-check`）
2. 可选地提升版本号（如果指定了 `--bump`）
3. 验证包元数据
4. 清理旧的构建产物
5. 使用 `uv build` 构建 wheel 和源码分发包
6. 创建 git tag `vX.Y.Z`（除非使用 `--skip-tag` 或 `--dry-run`）
7. 使用 `uv publish` 发布到 PyPI（除非使用 `--dry-run`）

## 完整工作流示例

```bash
# 1. 提升版本号
uv run scripts/bump_version.py patch

# 2. 更新 changelog
nano CHANGELOG.md

# 3. 提交更改
git add -A
git commit -m "将版本提升到 2.0.1"

# 4. 发布（这将创建并推送 git tag）
uv run scripts/publish.py

# 或者一次性完成：
uv run scripts/publish.py --bump patch
# （然后手动更新 CHANGELOG.md 并提交）
```

## 包安装

发布后，用户可以安装该包：

```bash
# 使用 pip
pip install scientific-writer

# 使用 uv
uv pip install scientific-writer

# 使用 uv tool（用于 CLI）
uv tool install scientific-writer

# 使用 uvx（一次性 CLI 用法）
uvx scientific-writer
```

## 验证包结构

API 和 CLI 都已正确暴露：

**API 用法：**
```python
from scientific_writer import generate_paper
# 或
from scientific_writer.api import generate_paper
```

**CLI 用法：**
```bash
scientific-writer
# 或
uvx scientific-writer
```

## 故障排除

### "No module named 'uv'"
安装 uv：`curl -LsSf https://astral.sh/uv/install.sh | sh`

### "PyPI credentials not found"
设置 `UV_PUBLISH_TOKEN` 环境变量，或创建 `~/.pypirc`

### "Working directory has uncommitted changes"
要么提交/暂存更改，要么使用 `--skip-git-check` 标志

### 构建失败
确保你位于项目根目录，并且 `pyproject.toml` 存在
