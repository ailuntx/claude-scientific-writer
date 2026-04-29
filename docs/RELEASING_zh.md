# 发布：版本管理与发布

本指南涵盖该包的版本号递增以及发布到 PyPI。它将所有要点整合为一份简明文档。

## 要求

- 已安装 uv（环境和构建管理器）
- 已通过环境变量或 ~/.pypirc 配置 PyPI token
  - 环境变量：`export UV_PUBLISH_TOKEN="pypi-***"`
  - 或 `~/.pypirc`：
    ```ini
    [pypi]
    username = __token__
    password = pypi-***
    ```

## 提升版本号（semver）

使用辅助脚本来递增 patch、minor 或 major，并保持 `pyproject.toml` 和 `scientific_writer/__init__.py` 同步：

```bash
uv run scripts/bump_version.py patch   # X.Y.Z -> X.Y.(Z+1)
uv run scripts/bump_version.py minor   # X.Y.Z -> X.(Y+1).0
uv run scripts/bump_version.py major   # X.Y.Z -> (X+1).0.0
```

递增后，审查变更并更新 `CHANGELOG.md`；然后提交。

## 发布到 PyPI

使用 uv 构建并发布。你也可以选择在一个命令中同时递增版本并发布。

```bash
# 仅构建（dry run）
uv run scripts/publish.py --dry-run

# 发布当前版本
uv run scripts/publish.py

# 一步完成递增版本并发布
uv run scripts/publish.py --bump patch   # or minor | major
```

发布脚本将验证元数据，构建 sdist 和 wheel，创建并推送 git tag（`vX.Y.Z`），并通过 `uv publish` 发布。

## 验证

发布前的本地验证（可选）：

```bash
uv run scripts/verify_package.py
```

发布后的基本 smoke 检查：

```bash
pip install scientific-writer==X.Y.Z
python -c "from scientific_writer import generate_paper; print('ok')"
uvx scientific-writer --help
```

## CLI 入口点

- 已安装命令：`scientific-writer`
- 一次性使用：`uvx scientific-writer`
- 工具：`uv tool install scientific-writer` 然后 `uv tool run scientific-writer`

## 注意

- 语义化版本：破坏性变更 → major；新功能 → minor；修复 → patch。
- 如果 tag 已经存在，删除/重新创建它，或者使用 `--skip-tag` 跳过打 tag。
- 如果你的工作区有未提交更改，提交它们，或者使用 `--skip-git-check`（不推荐）。
