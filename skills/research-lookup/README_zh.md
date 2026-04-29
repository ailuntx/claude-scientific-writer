# 研究查询技能

提供实时研究信息查询，并智能路由后端：**parallel-cli search**（主要，快速）和 **Parallel Chat API**（仅限深度研究）。

## 设置

1. **安装 parallel-cli**（主后端 — 必需）：
   ```bash
   curl -fsSL https://parallel.ai/install.sh | bash
   # 或：
   uv tool install "parallel-web-tools[cli]"
   ```

2. **认证：**
   ```bash
   parallel-cli auth
   # 或直接设置：
   export PARALLEL_API_KEY="your_parallel_api_key"
   ```

3. **测试设置：**
   ```bash
   parallel-cli search "test query" --json --max-results 3
   ```

## 使用

### 命令行使用

```bash
# 一般研究（parallel-cli search — 快速，默认）
parallel-cli search "Recent advances in CRISPR gene editing 2025" \
  --json --max-results 10 --excerpt-max-chars-total 27000 \
  -o sources/research_crispr.json

# 学术重点搜索（包含学术域名）
parallel-cli search "find papers on CRISPR off-target effects" \
  --json --max-results 10 \
  --include-domains "scholar.google.com,arxiv.org,pubmed.ncbi.nlm.nih.gov,nature.com,science.org,cell.com,pnas.org,nih.gov" \
  -o sources/research_crispr-academic.json

# 通过 research_lookup.py 进行深度研究（Parallel Chat API — 慢速）
python scripts/research_lookup.py "comprehensive review of mRNA vaccines" --force-backend parallel-chat

# 自动路由的研究（识别学术或一般查询）
python scripts/research_lookup.py "your research query" -o sources/research_topic.md
```

### 集成

研究查询工具会在以下情况自动可用：

1. **提出研究问题：** “研究量子计算的最新进展”
2. **请求文献综述：** “查找关于气候变化影响的最新研究”
3. **需要引用：** “关于Transformer注意力机制的最新论文有哪些？”
4. **想要技术信息：** “流式细胞术的标准方案”

## 后端路由

| 查询类型 | 后端 | 速度 |
|------------|---------|-------|
| 一般研究 | parallel-cli search | 快速（2-10秒） |
| 学术论文查询（包含：“找论文”、“doi”、“同行评审”等） | parallel-cli search + 学术域名 | 快速（2-10秒） |
| 深度/详尽研究（明确请求） | Parallel Chat API | 慢速（60秒-5分钟） |

## 论文质量优先级

查找论文时，按以下顺序优先考虑：

### 期刊/会议质量层级

- **第一层（最高）：** Nature、Science、Cell、NEJM、Lancet、JAMA、PNAS
- **第二层（高）：** 高影响力期刊（IF>10），顶级会议（NeurIPS、ICML、ICLR）
- **第三层（良好）：** 受尊敬的专业期刊（IF 5-10）

### 基于引用的排名

| 论文年龄 | 引用阈值 | 分类 |
|-----------|-------------------|----------------|
| 0-3年 | 20+ 引用 | 值得关注 |
| 0-3年 | 100+ 引用 | 高度影响力 |
| 3-7年 | 100+ 引用 | 重要 |
| 7年以上 | 500+ 引用 | 开创性/奠基性 |

## 故障排除

**“parallel-cli 未找到”**
- 安装: `curl -fsSL https://parallel.ai/install.sh | bash`

**“认证错误”**
- 运行 `parallel-cli auth` 或设置 `PARALLEL_API_KEY`

**“没有相关结果”**
- 尝试更具体的查询或添加 `-q "关键词"` 标志
- 包含时间范围（例如，`--after-date 2024-01-01`）
- 使用 `--include-domains` 限制为高质量来源

**“速率限制已超出”**
- 在请求之间添加延迟
- 检查你的 Parallel 账户限制

## 与科学写作的集成

1. **文献综述：** 引言部分的最新研究
2. **方法验证：** 对照当前标准验证方案
3. **结果背景：** 将发现与近期的类似研究进行比较
4. **讨论支持：** 论证的最新证据
5. **引文管理：** 正确格式化的参考文献

始终将结果保存到 `sources/`，以实现可重复性并避免重复查询。
