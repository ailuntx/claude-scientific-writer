# 数据充实

充实: $ARGUMENTS

## 开始之前

告知用户，根据所请求的行数和字段数量，充实过程可能需要几分钟。

## 步骤 1: 启动充实任务

使用以下命令模式之一（替换用户的实际数据）：

针对内联数据：

```bash
parallel-cli enrich run --data '[{"company": "Google"}, {"company": "Microsoft"}]' --intent "CEO name and founding year" --target "output.json" --no-wait --json
```

针对 CSV 文件：

```bash
parallel-cli enrich run --source-type csv --source "input.csv" --target "/tmp/output.json" --source-columns '[{"name": "company", "description": "Company name"}]' --intent "CEO name and founding year" --no-wait --json
```

如果这是对之前研究或充实任务的**后续操作**，并且你知道 `interaction_id`，请添加上下文链：

```bash
parallel-cli enrich run --data '...' --intent "..." --target "output.json" --no-wait --json --previous-interaction-id "$INTERACTION_ID"
```

通过跨请求链接 `interaction_id` 值，每个后续操作会自动获得之前轮次的完整上下文，这样你就可以对早期研究中发现的实体进行充实，而无需重复已找到的内容。

**重要：** 始终包含 `--no-wait`，以便命令立即返回而非阻塞。

解析输出以提取 `taskgroup_id`、`interaction_id` 和监控 URL。立即告知用户：
- 充实任务已启动
- 他们可以跟踪进度的监控 URL

告诉他们可以后台轮询步骤，以便在任务运行时继续工作。

## 步骤 2: 轮询结果

根据充实任务选择一个简短且描述性的文件名（例如 `companies-ceos`、`startups-funding`）。使用小写字母和连字符，不含空格。

```bash
parallel-cli enrich poll "$TASKGROUP_ID" --timeout 540 --json --output "$FILENAME.json"
```

`enrich run` 上的 `--target` 标志不会延续到轮询步骤——你必须在此处传递 `--output` 以保存结果。始终使用 `--json` 以获取结构化的 JSON 输出。

注意：
- 使用 `--timeout 540`（9 分钟）以保持在工具执行限制内

### 如果轮询超时

大型数据集的充实可能需要 9 分钟以上。如果轮询在没有完成的情况下退出：
1. 告知用户充实任务仍在服务器端运行
2. 重新运行相同的 `parallel-cli enrich poll` 命令以继续等待

## 响应格式

**步骤 1 完成后：** 分享监控 URL（用于跟踪进度）。

**步骤 2 完成后：**
1. 报告已充实的行数
2. 预览输出 JSON 的前几行
3. 告知用户输出 JSON 文件的完整路径（`$FILENAME.json`）
4. 分享 `interaction_id`，并告知用户可以基于本次充实提出后续问题

任务完成后请勿重新分享监控 URL——结果已在输出文件中。

**记住 `interaction_id`**——如果用户提出的后续问题与本次充实相关，请在下一个研究或充实命令中使用它作为 `--previous-interaction-id`。
