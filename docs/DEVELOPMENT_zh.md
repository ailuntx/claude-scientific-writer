# 开发与架构

本文档面向贡献者和维护者。它概述了 Scientific Writer v2.7.0 的包架构、设计决策和开发工作流。

## 架构概览

### 包结构

```
scientific_writer/
├── __init__.py          # Public API exports, version
├── api.py               # Async generate_paper() function
├── cli.py               # CLI entrypoint (cli_main)
├── core.py              # Core utilities (API keys, instructions, data processing)
├── models.py            # Data models (ProgressUpdate, PaperResult, etc.)
└── utils.py             # Helper functions (paper detection, file scanning)
```

### 插件结构

```
claude-scientific-writer/
├── .claude-plugin/          # Plugin metadata
│   └── plugin.json
├── commands/                # Plugin commands
│   └── scientific-writer-init.md
├── skills/                  # All 19+ skills
│   ├── citation-management/
│   ├── clinical-reports/
│   ├── research-lookup/
│   └── ... (16+ more)
├── templates/               # CLAUDE.md template
│   └── CLAUDE.scientific-writer.md
└── scientific_writer/       # Python package
```

### 关键组件

- `api.generate_paper`：异步生成器，流式输出进度并返回一个全面的结果
- `cli.cli_main`：CLI 接口；100% 向后兼容的行为
- `core`：用于 API key 获取、指令加载、输出管理、数据处理的共享逻辑
- `models`：用于 API 响应的类型化 dataclasses
- `utils`：文件扫描、论文检测及辅助函数
- **插件系统**：用于 Claude Code 集成的 commands、skills 和 templates

## 数据模型

- `ProgressUpdate`：实时进度更新（stage、message、timestamp、details）
- `PaperResult`：最终结果，包含 status、files、metadata、citations、token_usage 和 errors
- `PaperMetadata`：title、created_at、topic、word_count
- `PaperFiles`：所有相关路径（final、drafts、references、figures、data、logs）
- `TokenUsage`：token 消耗统计（input_tokens、output_tokens、total_tokens、缓存统计）

所有模型都完全类型化，并且可序列化为字典。

## API 设计

- 异步生成器模式，支持实时更新和最终的完整结果
- 每次调用均为无状态运行
- 通过 `success | partial | failed` 状态进行稳健的错误处理
- 自动检测论文目录并扫描文件

## 本地开发

### 设置

```bash
uv sync
```

环境变量：

- `ANTHROPIC_API_KEY`（必需）
- `OPENROUTER_API_KEY`（可选，用于 research lookup）

### 运行

```bash
# CLI
uv run scientific-writer

# Example API usage
uv run python example_api_usage.py
```

## 测试与质量

- 整个包都使用完整的类型标注
- 按项目默认规则进行 lint/format
- 通过示例用法在本地验证 imports 和 API 签名

## 插件开发

### 在本地测试插件

用于本地插件开发和测试：

1. **创建测试 marketplace**（见 `TESTING_INSTRUCTIONS.md`）：
   ```bash
   cd ..
   mkdir -p test-marketplace/.claude-plugin
   ```

2. **配置 marketplace**，使用指向本地插件的相对路径：
   ```json
   {
     "name": "test-marketplace",
     "plugins": [{
       "name": "claude-scientific-writer",
       "source": "../claude-scientific-writer"
     }]
   }
   ```

3. **在 Claude Code 中添加 marketplace**：
   ```
   /plugin marketplace add ../test-marketplace
   ```

4. **安装插件**：
   ```
   /plugin install claude-scientific-writer@test-marketplace
   ```

5. **在项目中测试**：
   ```
   /scientific-writer:init
   ```

### 插件结构要求

- **`.claude-plugin/plugin.json`** - 插件元数据
- **`commands/`** - 命令定义（需要 YAML frontmatter）
- **`skills/`** - 技能定义（每个都包含 SKILL.md + YAML frontmatter）
- **`templates/`** - 模板文件（CLAUDE.scientific-writer.md）

### 添加新技能

1. 在 `skills/` 中创建目录
2. 添加带有 YAML frontmatter 的 `SKILL.md`：
   ```yaml
   ---
   name: skill-name
   description: Brief description
   allowed-tools: [read_file, write, etc.]
   ---
   ```
3. 按需添加引用、脚本、资源
4. 重新安装插件后测试技能是否可用

## 发布说明

v2.7.0 亮点：

- **专注于 Claude Code 插件** - 针对 IDE 集成进行了优化
- 通过 `/scientific-writer:init` 安装插件
- 所有 19+ 个技能都可通过插件访问
- 精简的 IDE 工作流

v2.0 亮点：

- 通过 `generate_paper` 提供编程式 API
- 进度流式输出和完整的 JSON 结果
- 模块化包结构与入口点
- 100% CLI 向后兼容

详见 `CHANGELOG.md`。

## 迁移指南

### v1.x -> v2.0

- CLI 保持不变（`scientific-writer`）
- 新的包结构替代了单文件脚本
- 如需编程式使用，请从 `scientific_writer` 导入

示例：

```python
from scientific_writer import generate_paper
```

### CLI/API -> 插件（v2.7.0）

为了获得最佳 IDE 体验：
- 安装为 Claude Code 插件（推荐）
- 在项目中使用 `/scientific-writer:init`
- 直接在 IDE 中访问所有技能
- 大多数工作流不再需要 CLI

## 贡献

1. Fork 并创建功能分支
2. 使用 `uv sync` 安装依赖
3. 进行更改并保持提交清晰
4. 本地测试（CLI、API，以及适用时的插件）
5. 确保所有示例都能运行
6. 如有需要，更新文档
7. 提交一个描述简洁的 pull request

## 项目链接

- `README.md` — 入口点和快速开始
- `Docs/API.md` — 完整 API 参考
- `Docs/TROUBLESHOOTING.md` — 故障排除
- `Docs/SKILLS.md` — 技能概览
- `CHANGELOG.md` — 发布历史
- `CLAUDE.md` — 系统指令（保留在根目录）
