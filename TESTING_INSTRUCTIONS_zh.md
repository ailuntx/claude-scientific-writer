# 测试 Claude Code 插件

## ✅ 设置完成

测试 marketplace 已创建于：
```
/Users/vinayak/Documents/test-marketplace/
```

测试项目已创建于：
```
/Users/vinayak/Documents/test-plugin-project/
```

## 🧪 逐步测试

### 第 1 步：添加测试 marketplace

在 Claude Code（此聊天）中运行：

```
/plugin marketplace add /Users/vinayak/Documents/test-marketplace
```

预期输出：确认 marketplace 已添加。

### 第 2 步：列出可用插件

```
/plugin marketplace list
```

预期输出：应显示 test-marketplace 中的 `claude-scientific-writer`。

### 第 3 步：安装插件

```
/plugin install claude-scientific-writer@test-marketplace
```

预期输出：插件安装确认，可能会提示重启。

### 第 4 步：重启 Claude Code（如果提示）

如果 Claude Code 要求你重启，请现在执行。

### 第 5 步：打开测试项目

在 Claude Code 中打开测试项目目录：
```
/Users/vinayak/Documents/test-plugin-project/
```

或者使用 Cursor 的“Open Folder”并导航到该目录。

### 第 6 步：运行 Init 命令

在测试项目中运行：

```
/scientific-writer:init
```

预期行为：
- 应检查是否存在 CLAUDE.md（目前没有）
- 应创建一个新的 CLAUDE.md 文件
- 应显示一条全面的 onboarding 消息
- CLAUDE.md 文件应出现在测试项目目录中

### 第 7 步：验证 Skills 是否可用

向 Claude 询问：

```
可用的 skills 有哪些？
```

预期输出：应列出 scientific writing skills，包括：
- research-lookup
- peer-review
- citation-management
- clinical-reports
- research-grants
- scientific-slides
- 以及另外 13 个...

### 第 8 步：测试基本功能

尝试一个简单任务：

```
创建一篇关于量子计算应用的简短 scientific abstract（150 words）。
```

预期行为：
- Claude 应使用 scientific-writing skill
- 应创建一个格式正确的 abstract
- 如已配置，可能会使用 research-lookup

### 第 9 步：验证 CLAUDE.md 内容

打开创建的 CLAUDE.md 文件并验证：
- [ ] 文件存在于 `/Users/vinayak/Documents/test-plugin-project/CLAUDE.md`
- [ ] 包含 "Claude Agent System Instructions" 标题
- [ ] 顶部有插件注释
- [ ] 包含全面的 scientific writing instructions
- [ ] 包含 workflow protocols、citation policies 等

## 🔍 故障排除

### 找不到插件
如果找不到插件：
1. 检查 marketplace 路径是否正确：`/Users/vinayak/Documents/test-marketplace`
2. 验证 marketplace.json 是否存在且为有效 JSON
3. 尝试移除并重新添加：`/plugin marketplace remove test-marketplace`

### Skills 没有显示
如果 skills 不可用：
1. 检查插件中是否存在 `skills/` 目录
2. 验证每个 SKILL.md 是否具有有效的 YAML frontmatter
3. 尝试重新安装插件

### Init 命令不工作
如果 `/scientific-writer:init` 不起作用：
1. 检查 `commands/scientific-writer-init.md` 是否存在
2. 验证命令文件中的 YAML frontmatter
3. 检查 `templates/CLAUDE.scientific-writer.md` 是否存在

### 找不到模板
如果 init 命令找不到模板：
1. 验证 `/Users/vinayak/Documents/claude-scientific-writer/templates/CLAUDE.scientific-writer.md` 是否存在
2. 检查文件权限
3. 尝试在插件中使用绝对路径

## 📊 验证清单

完成所有步骤后：

- [ ] 测试 marketplace 已成功添加
- [ ] 插件在 marketplace 列表中可见
- [ ] 插件已成功安装且无错误
- [ ] `/scientific-writer:init` 命令已成功执行
- [ ] CLAUDE.md 已在测试项目中创建
- [ ] skills 查询返回 scientific writing skills
- [ ] 能够创建一个简单的 scientific document
- [ ] 插件按预期工作

## 🎯 成功标准

如果满足以下条件，则插件工作正常：

1. **安装成功** - marketplace 添加或插件安装过程中无错误
2. **命令有效** - `/scientific-writer:init` 创建 CLAUDE.md
3. **Skills 可用** - “可用的 skills 有哪些？” 显示 19 个 skills
4. **功能正常** - 能够使用这些 skills 创建 scientific content
5. **模板正确** - CLAUDE.md 包含完整的 scientific writing instructions

## 📝 备注

- 插件仓库中的 `.claude/` 目录仅用于开发
- 插件使用 `skills/`、`commands/` 和 `templates/` 目录
- 用户在初始化后可以自定义自己的 CLAUDE.md
- 一旦插件安装完成，skills 将在整个项目范围内可用

## 🚀 成功测试后的下一步

如果一切正常：
1. 如有需要，更新 `.claude-plugin/plugin.json` 中的版本
2. 提交并推送更改到 GitHub
3. 考虑发布到公共 marketplace
4. 使用真实场景示例更新文档

---

**准备好测试了吗？** 从上面的第 1 步开始！ 🧪
