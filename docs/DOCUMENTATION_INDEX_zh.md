# 完整文档索引

**Scientific Writer v2.7.0** - 全面的文档导航指南。

---

## 📚 文档结构

### 核心文档（从这里开始）

| 文档 | 用途 | 适用对象 | 最后更新 |
|----------|---------|----------|--------------|
| [README.md](../README.md) | 主要入口，快速开始，功能概览 | 所有人 | v2.7.0 |
| [docs/README.md](README.md) | 带导航指南的文档中心 | 所有人 | v2.7.0 |
| [CHANGELOG.md](../CHANGELOG.md) | 版本历史和发布说明 | 所有人 | v2.7.0 |

### 用户指南

| 文档 | 内容 | 何时阅读 |
|----------|---------|--------------|
| [FEATURES.md](FEATURES.md) | 完整功能指南（文档生成、AI 能力、文件集成） | 了解可实现的内容时 |
| [SKILLS.md](SKILLS.md) | 全部 19+ 项技能及示例 | 学习可用能力时 |
| [API.md](API.md) | 带代码示例的程序化 API 参考 | 使用 Python API 时 |
| [TROUBLESHOOTING.md](TROUBLESHOOTING.md) | 常见问题与解决方案 | 遇到问题时 |

### 开发者资源

| 文档 | 内容 | 适用对象 |
|----------|---------|----------|
| [DEVELOPMENT.md](DEVELOPMENT.md) | 架构、插件开发、贡献 | 贡献者、维护者 |
| [RELEASING.md](RELEASING.md) | 版本管理、PyPI 发布 | 维护者 |
| [example_api_usage.py](../example_api_usage.py) | 可运行的 Python 示例 | API 用户 |
| [TESTING_INSTRUCTIONS.md](../TESTING_INSTRUCTIONS.md) | 插件测试指南 | 插件开发者 |

### 系统文档

| 文档 | 内容 | 适用对象 |
|----------|---------|----------|
| [CLAUDE.md](../CLAUDE.md) | 面向 AI agent 的系统指令 | 高级用户、开发者 |

---

## 🎯 按使用场景快速导航

### 我想安装并使用 Scientific Writer

**作为 Claude Code 插件（推荐）：**
1. 开始：[插件安装指南](../README.md#-use-as-a-claude-code-plugin-recommended)
2. 参考：[技能概览](SKILLS.md)
3. 排查：[插件问题](TROUBLESHOOTING.md)

**作为 CLI 工具：**
1. 开始：[安装](../README.md#installation-options) → [CLI 使用](../README.md#use-the-cli)
2. 参考：[常用命令](../README.md#common-commands)
3. 排查：[CLI 问题](TROUBLESHOOTING.md)

**作为 Python API：**
1. 开始：[API 快速开始](../README.md#use-the-python-api)
2. 参考：[API 文档](API.md)
3. 示例：[example_api_usage.py](../example_api_usage.py)

### 我想生成特定文档

| 文档类型 | 入门 | 详细指南 | 示例 |
|--------------|----------------|----------------|----------|
| **研究论文** | [快速开始](../README.md#quick-start) | [功能：论文](FEATURES.md#scientific-papers) | [README 示例](../README.md#common-commands) |
| **资助提案** | [资助命令](../README.md#common-commands) | [技能：资助](SKILLS.md#5-research-grants) | [功能：资助提案](FEATURES.md#grant-proposals) |
| **研究海报** | [海报命令](../README.md#common-commands) | [技能：海报](SKILLS.md#8-latex-research-posters) | [功能：海报](FEATURES.md#research-posters) |
| **临床报告** | [临床命令](../README.md#common-commands) | [技能：临床](SKILLS.md#6-clinical-reports) | [功能：临床](FEATURES.md#document-generation) |
| **文献综述** | [综述命令](../README.md#common-commands) | [技能：文献](SKILLS.md#2-literature-review) | [功能：综述](FEATURES.md#literature-reviews) |
| **演示文稿** | [幻灯片示例](../README.md#common-commands) | [技能：幻灯片](SKILLS.md#9-scientific-slides-and-presentations) | [CLAUDE.md：演示文稿](../CLAUDE.md) |

### 我想使用特定功能

| 功能 | 文档 | 涉及的技能 |
|---------|---------------|-----------------|
| **研究检索** | [功能：研究检索](FEATURES.md#real-time-research-lookup) | [research-lookup](SKILLS.md#research-lookup) |
| **同行评审** | [功能：同行评审](FEATURES.md#peer-review-with-scholareval) | [peer-review](SKILLS.md#3-peer-review), [scholar-evaluation](SKILLS.md#4-scholar-evaluation) |
| **引用管理** | [技能：引用](SKILLS.md#citation-management) | [citation-management](SKILLS.md) |
| **文档转换** | [功能：转换](FEATURES.md#document-conversion) | [markitdown](SKILLS.md#12-markitdown---universal-file-to-markdown-converter) |
| **科学示意图** | [功能：示意图](FEATURES.md#scientific-schematics) | [scientific-schematics](SKILLS.md#10-scientific-schematics-and-diagrams) |

### 我想开发或贡献

**插件开发：**
1. [插件结构](DEVELOPMENT.md#plugin-structure)
2. [本地测试](DEVELOPMENT.md#testing-plugin-locally)
3. [测试指南](../TESTING_INSTRUCTIONS.md)

**Python 包开发：**
1. [架构](DEVELOPMENT.md#architecture-overview)
2. [设置](DEVELOPMENT.md#local-development)
3. [贡献](DEVELOPMENT.md#contributing)

**发布：**
1. [版本管理](RELEASING.md#bump-the-version-semver)
2. [发布到 PyPI](RELEASING.md#publish-to-pypi)
3. [验证](RELEASING.md#verify)

---

## 🔗 外部资源

- **GitHub 仓库**: https://github.com/K-Dense-AI/claude-scientific-writer
- **PyPI 包**: https://pypi.org/project/scientific-writer/
- **社区 Slack**: [加入 K-Dense 社区](https://join.slack.com/t/k-densecommunity/shared_invite/zt-3iajtyls1-EwmkwIZk0g_o74311Tkf5g)
- **问题跟踪**: https://github.com/K-Dense-AI/claude-scientific-writer/issues

---

## 📊 文档健康检查

### 完整性

- ✅ 安装指南（插件、CLI、API）
- ✅ 使用示例（所有文档类型）
- ✅ API 参考（包含完整示例）
- ✅ 技能文档（19+ 项技能）
- ✅ 故障排除指南
- ✅ 开发指南
- ✅ 发布流程
- ✅ 更新日志

### 准确性

- ✅ 版本号已更新（v2.7.0）
- ✅ 链接已验证
- ✅ 示例已测试
- ✅ 前置条件为最新

### 覆盖范围

- ✅ 已记录全部三种使用模式（插件、CLI、API）
- ✅ 涵盖所有主要功能
- ✅ 已记录所有技能
- ✅ 已处理常见问题

---

## 🎓 学习路径

### 初学者路径（首次使用者）

1. 阅读：[主 README](../README.md)（5 分钟）
2. 安装：按照 [插件安装](../README.md#-use-as-a-claude-code-plugin-recommended)（2 分钟）
3. 尝试：创建你的第一份文档（10 分钟）
4. 探索：浏览 [技能概览](SKILLS.md)（10 分钟）

### 中级路径（常规用户）

1. 掌握：[常用命令](../README.md#common-commands)
2. 学习：[研究检索](FEATURES.md#real-time-research-lookup)
3. 使用：[同行评审](FEATURES.md#peer-review-with-scholareval)
4. 优化：[文件集成](FEATURES.md#data--file-integration)

### 高级路径（进阶用户）

1. API：阅读 [API 参考](API.md)
2. 定制：理解 [系统指令](../CLAUDE.md)
3. 扩展：学习 [插件开发](DEVELOPMENT.md)
4. 贡献：遵循 [贡献指南](DEVELOPMENT.md#contributing)

---

## 📝 文档约定

### 文件组织

```
claude-scientific-writer/
├── README.md                    # 主要入口
├── CHANGELOG.md                 # 版本历史
├── CLAUDE.md                    # 系统指令
├── TESTING_INSTRUCTIONS.md      # 插件测试
├── example_api_usage.py         # API 示例
├── docs/
│   ├── README.md                # 文档中心
│   ├── DOCUMENTATION_INDEX.md   # 本文件
│   ├── API.md                   # API 参考
│   ├── FEATURES.md              # 功能指南
│   ├── SKILLS.md                # 技能参考
│   ├── TROUBLESHOOTING.md       # 问题解决
│   ├── DEVELOPMENT.md           # 开发者指南
│   ├── RELEASING.md             # 发布流程
│   └── examples/                # 示例输出
└── skills/                      # 19+ 个技能目录
```

### 链接格式

- **内部链接**：相对路径（例如 `[text](../README.md)`）
- **外部链接**：完整 URL（例如 `https://github.com/...`）
- **锚点**：小写并使用连字符（例如 `#quick-start`）

### 版本引用

- 引用功能时始终注明版本（例如 "v2.7.0"）
- 当前版本使用 "Latest"，旧版本使用 "Previous"
- 在发布期间更新版本号

---

## 🔄 维护计划

### 定期更新（每次发布）

- [ ] 更新所有文档中的版本号
- [ ] 在 CHANGELOG.md 中更新新功能
- [ ] 审阅并更新 README.md 示例
- [ ] 验证所有链接仍然有效
- [ ] 更新“最后更新”日期

### 季度审查

- [ ] 检查过时信息
- [ ] 根据用户反馈添加新示例
- [ ] 审阅并更新故障排除指南
- [ ] 如果界面发生变化，更新截图
- [ ] 审阅文档完整性

### 年度更新

- [ ] 如有需要，进行重大文档重组
- [ ] 根据使用模式更新学习路径
- [ ] 全面检查链接
- [ ] 更新外部资源链接
- [ ] 审阅并更新约定

---

## 💬 反馈

发现文档有问题？请：

1. **检查**：[故障排除指南](TROUBLESHOOTING.md)
2. **搜索**：[GitHub Issues](https://github.com/K-Dense-AI/claude-scientific-writer/issues)
3. **报告**：创建一个带有 “documentation” 标签的新 issue
4. **讨论**：加入我们的 [Slack 社区](https://join.slack.com/t/k-densecommunity/shared_invite/zt-3iajtyls1-EwmkwIZk0g_o74311Tkf5g)

---

**最后更新**: 2025 年 1 月 22 日 (v2.7.0)

**文档状态**: ✅ 完整且最新
