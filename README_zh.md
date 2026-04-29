# Claude 科学写作助手

[![PyPI version](https://img.shields.io/pypi/v/scientific-writer.svg)](https://pypi.org/project/scientific-writer/)
[![Total Downloads](https://static.pepy.tech/badge/scientific-writer)](https://pepy.tech/project/scientific-writer)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> 🚀 **在寻找更高级的功能？** 如需端到端科学写作、深度科学检索、高级图像生成和企业级解决方案，请访问 **[www.k-dense.ai](https://www.k-dense.ai)**

**一款深度研究与写作工具**，将 AI 驱动的深度研究能力与格式精良的写作输出相结合。可生成可直接发表的科学论文、报告、海报、资助申请、文献综述以及更多学术文档——全部基于实时文献检索和经过验证的引用。

Scientific Writer 在写作前会进行全面研究，确保每一项论断都由真实、可验证的来源支持。其功能包括通过 Perplexity Sonar Pro Search 进行实时研究查询、智能论文检测、全面文档转换，以及借助 Nano Banana Pro 的 AI 图表生成。你可以将其作为 claude code 插件、python 包或原生 CLI 使用

## 快速开始

### 前提条件
- Python 3.10-3.12
- ANTHROPIC_API_KEY（必需），OPENROUTER_API_KEY（可选，用于研究查询）

### 安装选项

#### 选项 1：Claude Code 插件（推荐）⭐
使用 Scientific Writer 最简单的方式是作为 Claude Code 插件。请参见上方的 [插件安装](#-use-as-a-claude-code-plugin-recommended) 部分。

#### 选项 2：从 PyPI 安装（CLI/API 使用）
```bash
pip install scientific-writer
```

#### 选项 3：使用 uv 从源码安装
```bash
git clone https://github.com/K-Dense-AI/claude-scientific-writer.git
cd claude-scientific-writer
uv sync
```

### 配置 API 密钥
```bash
# .env 文件（推荐）
echo "ANTHROPIC_API_KEY=your_key" > .env
echo "OPENROUTER_API_KEY=your_openrouter_key" >> .env
# 或在 shell 中导出
export ANTHROPIC_API_KEY='your_key'
```

### 使用选项

#### 作为插件使用（推荐）
安装插件并运行 `/scientific-writer:init` 后，只需向 Claude 提出请求：
```bash
> 创建一篇关于 CRISPR 基因编辑的 Nature 论文。提供 experimental_data.csv 
  （5 个细胞系的效率），包含 Western_blot.png 和 flow_cytometry.png 
  展示 87% 的编辑效率（p<0.001）。与文献基准进行比较。

> 生成一份 NSF 资助申请，展示来自 quantum_results.csv 的初步数据 
  （99.2% 门控保真度）、circuit_topology.png 和 error_rates.csv。 
  包含带有 milestones_budget.xlsx 的 5 年时间线。

> @research-lookup 查找关于 mRNA 疫苗有效性的论文（2022-2024）。与我们的 trial_outcomes.csv 
  （n=500，94% 有效性）和 antibody_titers.png 进行比较。
```

#### 使用 CLI
```bash
# 如果通过 pip 安装
scientific-writer

# 如果使用 uv 从源码安装
uv run scientific-writer
```

#### 使用 Python API
```python
import asyncio
from scientific_writer import generate_paper

async def main():
    # 带有具体数据和图表的详细提示词
    async for update in generate_paper(
        query=(
            "创建一篇关于 CRISPR 基因编辑的 Nature 论文。 "
            "提供 editing_efficiency.csv（5 个细胞系，每个 n=200 个细胞）。 "
            "包含 Western blot（protein_knockout.png）展示目标蛋白耗竭， "
            "流式细胞术数据（editing_percentages.png）显示 HEK293 中 87% 的效率， "
            "以及 off_target_analysis.csv 显示 <0.1% 的脱靶效应。 "
            "将结果与已发表的 Cas9 基准（通常 70-75% 的效率）进行比较。"
        ),
        data_files=[
            "editing_efficiency.csv",
            "protein_knockout.png",
            "editing_percentages.png",
            "off_target_analysis.csv"
        ]
    ):
        if update["type"] == "progress":
            print(f"[{update['stage']}] {update['message']}")
        else:
            print(f"✓ PDF: {update['files']['pdf_final']}")
            print(f"  Figures: {len(update.get('figures', []))} included")

asyncio.run(main())
```

## 🎯 作为 Claude Code 插件使用（推荐）

**Scientific Writer 最适合用作 Claude Code（Cursor）插件**，可在你的 IDE 中直接无缝访问所有科学写作能力。无需 CLI！

### 快速开始 - 插件安装

1. **在 Claude Code 中添加插件市场**：
   ```bash
   /plugin marketplace add https://github.com/K-Dense-AI/claude-scientific-writer
   ```

2. **安装插件**：
   ```bash
   /plugin install claude-scientific-writer
   ```

3. **按提示重启 Claude Code**。

4. **在你的项目中初始化**：
   ```bash
   /scientific-writer:init
   ```
   这会创建一个 `CLAUDE.md` 文件，内含全面的科学写作说明，并使全部 19+ 项技能可用。

5. **立即开始使用**：
   ```bash
   # 使用数据和图表创建论文
   > 创建一篇关于 CRISPR 基因编辑的 Nature 论文。提供 knockout_efficiency.csv 
     （测试了 5 个细胞系），包含 Western blot（protein_levels.png）和 flow 
     cytometry 数据（editing_rates.png）。突出 HEK293 细胞中 87% 的效率。
   
   > 为量子计算撰写 NSF 资助申请。展示 gate_fidelity.csv 的初步结果 
     （99.2% 保真度），包含 circuit_diagram.png 和 
     error_analysis.png。与当前 95% 的 state-of-art 相比进行强调。
   
   > 生成会议海报。展示 clinical_trial.csv 
     （n=150）、survival_curves.png、biomarker_heatmap.png 和 mechanism_diagram.svg 的结果。
   
   # 使用特定技能并结合研究数据
   > @research-lookup 查找关于 mRNA 疫苗有效性的论文（2022-2024）。与我们的 trial_data.csv 
     （94% 有效性）和 antibody_titers.xlsx 进行比较。
   
   > @peer-review 评估这篇稿件。参考 methods.csv 中的样本量 
     （n=30）和 effect_sizes.png。评估统计功效是否充足。
   
   > @clinical-reports 为自身免疫疾病创建病例报告。包含 patient_labs.xlsx 
     （6 个月数据）、MRI_scans/ 文件夹、以及显示治疗反应的 treatment_timeline.csv。
   ```

### 为什么使用插件？

- ✅ **无需 CLI** - 所有功能都可直接在 Claude Code 中使用
- ✅ **即时访问** - 立刻可用全部 19+ 项技能
- ✅ **IDE 集成** - 文件在你的项目中创建并编辑
- ✅ **上下文感知** - 技能能理解你的项目结构
- ✅ **无缝工作流** - 无需在工具之间切换

### 可用技能

安装为插件后，你将可立即使用：
- `scientific-schematics` - 使用 Nano Banana Pro 生成 AI 图表（CONSORT、神经网络、通路）
- `research-lookup` - 实时文献检索
- `peer-review` - 系统化稿件评估
- `citation-management` - BibTeX 和参考文献处理
- `clinical-reports` - 医学文档标准
- `research-grants` - NSF、NIH、DOE 申请支持
- `scientific-slides` - 研究演示文稿
- `latex-posters` - 会议海报生成
- `hypothesis-generation` - 科学假设开发
- `market-research-reports` - 带有可视化的全面 50+ 页市场分析报告
- 以及 10+ 个更多专门技能...

请参见下方的 [插件测试指南](#plugin-testing-local-development)，了解本地开发说明。

## 功能

### 📝 文档生成
- **科学论文**，采用 IMRaD 结构（Nature、Science、NeurIPS 等）
- **临床报告**（病例报告、诊断报告、试验报告、患者文档）
- **研究海报**，使用 LaTeX（beamerposter、tikzposter、baposter）
- **资助申请**（NSF、NIH、DOE、DARPA），带机构特定格式
- **文献综述**，带系统化引用管理
- **科学示意图**，由 Nano Banana Pro 驱动（CONSORT 图、神经架构、生物通路、电路图）

### 🤖 AI 驱动能力
- **实时研究检索**，使用 Perplexity Sonar Pro Search（通过 OpenRouter）
- **AI 图表生成**，使用 Nano Banana Pro——可从自然语言描述创建任意科学图表
- **智能论文检测**——自动识别对已有论文的引用
- **同行评审反馈**，采用量化 ScholarEval 框架（8 维评分）
- **迭代编辑**，提供具上下文感知的修改建议

### 🔧 对开发者友好
- **程序化 API** - 带类型提示的完整异步 Python API
- **CLI 界面** - 带进度跟踪的交互式命令行工具
- **进度流式输出** - 生成过程中实时更新
- **全面结果** - 包含元数据、文件路径、引用的 JSON 输出

### 📦 数据与文件集成
- **自动数据处理** - 将文件放入 `data/`，自动分类到 `figures/` 或 `data/`
- **文档转换** - 使用 MarkItDown 将 PDF、DOCX、PPTX、XLSX 转换为 Markdown
- **参考文献管理** - 自动生成 BibTeX 并格式化引用
- **图像集成** - 自动引用并组织图像

## 典型工作流

### CLI 使用
1. 将图表和数据放入项目根目录的 `data/` 中（图像 → `figures/`，文件 → `data/`，自动处理）
2. 运行 `scientific-writer` 并描述你的需求
3. 跟随进度更新；输出保存到 `writing_outputs/<timestamp>_<topic>/`

```bash
# 使用图表和数据开始一篇新论文
> 创建一篇关于 CRISPR 基因编辑的 Nature 论文。在结果部分包含 experimental_results.csv，显示 5 个细胞系的敲除效率。引用 figure1.png（Western blot）和 figure2.png（流式细胞术数据）。讨论在 HEK293 细胞中观察到的 87% 效率提升。

# 继续用额外研究结果编辑
> 添加一个方法部分，描述用于生成 results_table.csv 中数据的实验设置。引用 microscopy_images/ 文件夹中显示的转染、筛选和验证流程。

# 带初步数据的资助申请
> 为量子计算研究撰写 NSF 申请。展示 quantum_fidelity.csv 中的初步结果，显示 99.2% 的门控保真度。包含 circuit_diagram.png 和 error_rates.png 图表。强调与当前 state-of-art（95% 保真度）相比的突破性结果。

# 带完整图表的研究海报
> 从我的论文生成一张会议海报。以 dose_response_graph.png 作为中心图。包含 mechanism_schematic.png、compare_treatments.png 和 statistical_analysis.png。突出结果中所示主要终点的 p<0.001 显著性。

# 含患者数据的临床病例报告
> 为罕见疾病表现创建一份临床病例报告。引用 patient_timeline.csv，显示 6 个月内症状进展。包含 diagnostic_images/（CT 扫描、MRI）。讨论 lab_values.xlsx 中显示的升高生物标志物以及在 follow_up_data.csv 中记录的治疗反应。

# 文献综述与荟萃分析
> 创建一篇关于医疗保健中机器学习的文献综述。引用 studies_comparison.csv 中覆盖 50 篇论文的比较。包含显示合并效应量的 forest_plot.png 和来自偏倚分析的 quality_assessment.png。综合结果，展示诊断准确性（AUC 0.89）、治疗预测（准确率 82%）以及风险分层结果。
```

### API 使用
```python
import asyncio
from scientific_writer import generate_paper

async def main():
    async for update in generate_paper(
        query="创建一篇关于 transformers 的 NeurIPS 论文",
        data_files=["results.csv", "figure.png"],
        output_dir="./my_papers",
        track_token_usage=True  # 可选：跟踪 token 消耗
    ):
        if update["type"] == "progress":
            print(f"[{update['stage']}] {update['message']}")
        else:
            print(f"✓ PDF: {update['files']['pdf_final']}")
            # 当 track_token_usage=True 时可获得 token 使用情况
            if "token_usage" in update:
                print(f"  使用的 Tokens: {update['token_usage']['total_tokens']:,}")

asyncio.run(main())
```

## 快速参考

### 常用命令

| 任务 | 命令示例 |
|------|----------------|
| **科学论文** | `> 创建一篇关于 CRISPR 基因编辑的 Nature 论文。提供 results.csv 中的敲除效率数据（测试了 5 个细胞系）。包含 Western blot（figure1.png）和 flow cytometry（figure2.png），显示 HEK293 细胞中 87% 的效率。与已发表基准进行比较。` |
| **临床报告** | `> 为罕见线粒体疾病创建一份临床病例报告。包含 patient_timeline.csv（6 个月进展）、diagnostic_scans/ 文件夹（MRI、CT 图像）以及 lab_values.xlsx，显示升高的乳酸（8.2 mmol/L）和肌酸激酶（450 U/L）。描述治疗反应。` |
| **资助申请** | `> 为量子纠错研究撰写 NSF 申请。展示 gate_fidelity.csv 的初步数据，显示 99.2% 的保真度（对比 95% 的 state-of-art）。包含 circuit_topology.png、error_rates_comparison.png，以及针对 100 量子比特系统的 scalability_projections.csv。` |
| **研究海报** | `> 生成一张 A0 会议海报。突出 efficacy_study.csv 中的发现（n=150 名患者，40% 反应率）。展示 mechanism_diagram.png、survival_curves.png、biomarker_heatmap.png 和 statistical_forest_plot.png（主要终点 p<0.001）。` |
| **文献综述** | `> 创建一篇关于 AI 在药物发现中的系统综述。引用 studies_database.csv（127 篇论文，2020-2024）。包含 success_rates_meta.png（合并 OR=2.3，95% CI 1.8-2.9）、publication_trends.png，以及显示肿瘤学占主导地位（45% 研究）的 therapeutic_areas_breakdown.csv。` |
| **同行评审** | `> 使用 ScholarEval 评估这篇稿件。参考图表（power_analysis.png 显示 n=30，功效不足），审查 results_table.csv 中的统计结果，依据 CONSORT 标准评估方法学，核实引用是否与论断一致。` |
| **假设论文** | `> 生成关于抗衰老干预的研究假设。引用 transcriptomics_data.csv（跨组织的 15,000 个基因）、pathway_enrichment.png 和 longevity_correlations.csv。提出 5 个可检验假设，连接 NAD+ 代谢、细胞衰老和寿命延长。` |
| **继续编辑** | `> 添加方法部分，描述用于生成 binding_assay.csv 数据的协议。包含设备规格、所用统计检验（stats_summary.csv 中的 t 检验）以及来自 power_calculation.xlsx 的样本量依据` |
| **查找已有论文** | `> 找到那篇 CRISPR 论文，并补充对 off_target_analysis.csv 中所示局限性以及不同细胞类型间效率变化（efficiency_variation.png）的讨论` |

### 研究检索示例

```bash
# 近期研究与数据整合（自动触发研究检索）
> 创建一篇关于量子计算最新进展（2024 年）的论文。将已发表数值与我们的 gate_fidelity_results.csv（2 量子比特门 99.2%）进行比较。包含我们的 error_correction_benchmarks.png，并引用实现 >98% 保真度的论文。讨论我们的 topology_diagram.png 与 Google 和 IBM 的最新架构之间的关系。

# 带实验背景的事实核验
> CAR-T 疗法在 B 细胞淋巴瘤中的当前成功率是多少？与我们的 clinical_trial_outcomes.csv（n=45 名患者，62% 完全缓解）进行比较。包含我们的 response_timeline.png 和 cytokine_profiles.csv。我们的结果与已发表的 JULIET 和 ZUMA 试验相比如何？

# 以数据驱动为重点的文献检索
> 查找 10 篇关于 transformer 效率优化的近期论文（2023-2024）。将它们报告的 FLOPS 和内存使用与我们的 benchmark_results.csv 进行比较，该文件测试了 GPT-4、Claude 和 Llama 模型。结合我们的 latency_comparison.png 和 throughput_scaling.csv 作为背景。

# 带新数据的荟萃分析
> 搜索关于二甲双胍在衰老中的 RCT（过去 5 年）。将已发表的疗效数据与我们的 mouse_longevity_study.csv（寿命延长 18%，n=120）进行比较。包含我们的 survival_curves.png、biomarker_changes.xlsx（AMPK、mTOR、NAD+ 水平）以及 dose_response.png。我们的发现与人体试验结果如何一致？

# 比较分析
> 查找 2022-2024 年关于 CRISPR base editors 与 prime editors 的论文。将其报告的效率和特异性与我们的 editing_efficiency.csv（5 个靶点，3 个细胞系）进行比较。包含我们的 off_target_analysis.png 和 on_target_rates.csv。讨论我们的 89% 靶向率是否具有竞争力。
```

### 文档类型

| 类型 | 带数据/图表的示例 |
|------|---------|
| **论文** | `> 创建一篇关于神经可塑性的 Nature 论文。提供 electrophysiology_data.csv（n=30 个神经元），包含 LTP_traces.png、calcium_imaging_timelapse/ 文件夹，以及显示 156% 增强（p<0.001）的 synaptic_strength.csv。` |
| **临床报告** | `> 为自身免疫性脑炎撰写病例报告。包含 MRI_series/（FLAIR、T2 序列）、CSR_results.xlsx（寡克隆带、IgG 升高）、EEG_recordings.png，以及显示 8 周内免疫治疗反应的 treatment_timeline.csv。` |
| **资助** | `> 关于光遗传学的 NSF 申请。提供 pilot_data/，其中包含 behavioral_results.csv（n=24 只小鼠）、neural_activation_maps.png、circuit_tracing.tif，以及显示 78% 行为改变成功率的 projection_analysis.csv。包含带有 milestones.xlsx 的 5 年时间线。` |
| **海报** | `> 为 ASCO 会议制作一张 A0 海报。展示 trial_demographics.csv（n=200）、primary_outcome_kaplan_meier.png、adverse_events_heatmap.png、biomarker_correlations.csv、mechanism_schematic.png。突出 8.5 个月中位 PFS 改善。` |
| **综述** | `> 免疫治疗联合方案的系统综述。引用来自 85 项试验的 extracted_data.csv，包含用于荟萃分析的 forest_plot_OS.png 和 forest_plot_PFS.png、risk_of_bias_summary.png、比较 12 种方案的 network_meta_analysis.csv。` |
| **示意图** | `> 使用 Nano Banana Pro 为 RCT 生成 CONSORT 图。使用 enrollment_data.csv（筛查 n=450，随机分配 312），展示分配流程图。创建展示 encoder-decoder 的 transformer 架构图。为 MAPK 信号通路生成生物通路图。` |

### 文件处理

```bash
# 1. 将所有研究文件放入 data/ 文件夹
cp experimental_data.csv ~/Documents/claude-scientific-writer/data/
cp western_blot.png ~/Documents/claude-scientific-writer/data/
cp flow_cytometry.png ~/Documents/claude-scientific-writer/data/
cp statistical_summary.xlsx ~/Documents/claude-scientific-writer/data/
cp methods_diagram.svg ~/Documents/claude-scientific-writer/data/

# 2. 文件会按类型自动分类：
#    图像（png, jpg, svg, tif, pdf figures）→ figures/
#    数据文件（csv, json, txt, xlsx, tsv）→ data/
#    文档（pdf, docx, pptx）→ 转换为 markdown

# 3. 在提示词中明确引用文件，并提供具体细节
> 创建一篇关于深度学习优化的 NeurIPS 论文。包含 training_curves.csv，显示 5 种模型架构在 50 个 epoch 后收敛。引用 accuracy_comparison.png（我们的方法：94.2% 对比基线：89.1%）、展示优化轨迹的 loss_landscapes.png，以及已测试 100 种配置的 hyperparameter_grid.csv。在方法中包含 architecture_diagram.svg。讨论基准结果中显示的 5.1% 准确率提升和 30% 更快收敛。

# 4. 为多个相关文件引用文件夹
> 撰写一份放射学病例报告。包含 CT_scans/ 文件夹（20 张切片，显示肿瘤进展）、lab_results/（每周血检 CSV）以及记录病灶测量的 treatment_response.xlsx。时间线请引用 imaging_timeline.csv 中的日期。

# 5. 结合数据文件进行完整展示
> 生成一份资助申请，展示以下初步数据：dose_response.csv（6 个剂量，4 次重复）、survival_analysis.csv（Kaplan-Meier 数据，n=80 只小鼠）、mechanism_pathway.png、gene_expression.csv（RNA-seq，15,000 个基因）以及 protein_validation.xlsx（Western blot 定量）。包含来自 project_costs.xlsx 的预算。
```

### API 快速开始

```python
import asyncio
from scientific_writer import generate_paper

# 简单用法，带详细提示词
async for update in generate_paper(
    "创建一篇关于 CRISPR base editing 的 Nature 论文。展示来自 "
    "results.csv 的编辑效率（5 个细胞系，每行 n=200）。包含 Western blots（protein_expression.png）、 "
    "flow cytometry（editing_rates.png）以及脱靶分析（specificity_heatmap.png）。 "
    "突出 89% 的靶向内效率以及 <0.1% 的脱靶效应。"
):
    if update["type"] == "result":
        print(f"PDF: {update['files']['pdf_final']}")

# 使用多个数据文件和具体说明
async for update in generate_paper(
    query=(
        "为机器人学强化学习创建一篇 ICML 论文。 "
        "展示 training_metrics.csv（100 万 timesteps，5 个环境）。 "
        "包含 learning_curves.png，对比我们的方法（reward: 450）与基线（320）， "
        "100 个测试 episode 的 success_rates.csv、policy_visualizations.png， "
        "以及测试 8 种超参数配置的 ablation_study.xlsx。 "
        "在方法中包含 robot_architecture.svg 图和 trajectory_examples.png。 "
        "强调相较于 SAC 提升 40%，相较于 TD3 提升 25%。"
    ),
    data_files=[
        "training_metrics.csv",
        "learning_curves.png", 
        "success_rates.csv",
        "policy_visualizations.png",
        "ablation_study.xlsx",
        "robot_architecture.svg",
        "trajectory_examples.png"
    ],
    output_dir="./papers"
):
    if update["type"] == "progress":
        print(f"[{update['stage']}] {update['message']}")
    elif update["type"] == "result":
        print(f"✓ Paper completed!")
        print(f"  PDF: {update['files']['pdf_final']}")
        print(f"  LaTeX: {update['files']['tex_final']}")
        print(f"  Figures: {len(update.get('figures', []))} included")

# 含全面数据的临床试验报告
async for update in generate_paper(
    query=(
        "生成一份新型免疫治疗的 2 期临床试验报告。 "
        "展示 patient_demographics.csv（n=120，按年龄/分期分层）、"
        "primary_endpoint_PFS.csv（中位数 12.3 个月，HR=0.65，p=0.003）、"
        "secondary_outcomes.xlsx（ORR 45%，DCR 78%）、"
        "用于 OS 和 PFS 的 kaplan_meier_curves.png、"
        "adverse_events.csv（3 级以上：23%）、"
        "biomarker_analysis.csv（PD-L1、TMB 相关性）、"
        "以及 response_waterfall.png。基于 enrollment_flow.csv 包含 CONSORT 图。"
    ),
    data_files=[
        "patient_demographics.csv",
        "primary_endpoint_PFS.csv", 
        "secondary_outcomes.xlsx",
        "kaplan_meier_curves.png",
        "adverse_events.csv",
        "biomarker_analysis.csv",
        "response_waterfall.png",
        "enrollment_flow.csv"
    ]
):
    if update["type"] == "result":
        print(f"Trial report: {update['files']['pdf_final']}")
```

## 插件测试（本地开发）

对于正在开发插件或进行本地测试的开发者：

### 设置本地市场

1. **在父目录中创建测试市场**：
   ```bash
   cd ..
   mkdir -p test-marketplace/.claude-plugin
   ```

2. **创建市场配置**（`test-marketplace/.claude-plugin/marketplace.json`）：
   
   可从 `test-marketplace-example.json` 复制示例，或创建：
   
   ```json
   {
     "name": "test-marketplace",
     "owner": { "name": "K-Dense" },
     "plugins": [
       {
         "name": "claude-scientific-writer",
         "source": "../claude-scientific-writer",
         "description": "Scientific writing skills and CLAUDE.md initializer"
       }
     ]
   }
   ```
   
   **注意**：请将 `source` 路径更新为与你本地目录结构匹配的路径（相对于 test-marketplace 目录）。

### 安装与测试

3. **在 Claude Code 中添加测试市场**：
   ```bash
   /plugin marketplace add ../test-marketplace
   ```
   
   （使用与你的 test-marketplace 目录相对应的正确相对或绝对路径）

4. **安装插件**：
   ```bash
   /plugin install claude-scientific-writer@test-marketplace
   ```

5. **按提示重启 Claude Code**。

6. **测试插件**：
   - 打开任意项目目录
   - 运行 `/scientific-writer:init`
   - 验证 CLAUDE.md 已创建
   - 测试技能：“有哪些可用技能？”
   - 尝试创建文档：“创建一篇关于量子计算的简短科学摘要”

### 验证插件结构

你的插件应具有以下结构：
```
claude-scientific-writer/
├── .claude-plugin/
│   └── plugin.json          # 插件元数据
├── commands/
│   └── scientific-writer-init.md  # /scientific-writer:init 命令
├── skills/                  # 全部 20 项技能
│   ├── citation-management/
│   ├── clinical-decision-support/
│   ├── clinical-reports/
│   ├── document-skills/
│   ├── hypothesis-generation/
│   ├── latex-posters/
│   ├── literature-review/
│   ├── market-research-reports/
│   ├── markitdown/
│   ├── paper-2-web/
│   ├── peer-review/
│   ├── research-grants/
│   ├── research-lookup/
│   ├── scholar-evaluation/
│   ├── scientific-critical-thinking/
│   ├── scientific-schematics/
│   ├── scientific-slides/
│   ├── scientific-writing/
│   ├── treatment-plans/
│   └── venue-templates/
├── templates/
│   └── CLAUDE.scientific-writer.md  # CLAUDE.md 模板
└── ... (现有 Python 包文件)
```

### 插件安装故障排查

- **技能未显示**：验证每个 `SKILL.md` 都有有效的 YAML frontmatter（name、description、allowed-tools）
- **命令不工作**：检查 `commands/scientific-writer-init.md` 是否存在并具有正确的 frontmatter
- **模板未找到**：确保 `templates/CLAUDE.scientific-writer.md` 存在
- **市场未加载**：验证 `marketplace.json` 语法以及到插件的相对路径

## 📄 示例输出

想看看 Scientific Writer 能生成什么？请查看 [`docs/examples/`](docs/examples/) 目录中的真实示例！

| 文档类型 | 示例 | 描述 |
|--------------|-------------|---------|
| **研究论文** | 即将推出 | 带有 IMRaD 结构的完整科学论文 |
| **资助申请** | [NSF Proposal](docs/examples/grants/v6_draft.pdf) | 包含预算和时间线的完整 NSF 申请 |
| **研究海报** | [Conference Poster](docs/examples/poster/poster.pdf) | LaTeX 生成的学术海报 |
| **演示幻灯片** | [AI Scientist Talk](docs/examples/slides/ai_scientist_talk.pdf) | 专业研究演示 |
| **临床报告** | [Treatment Plan](docs/examples/treatment_plan/GERD.pdf) | 患者治疗文档 |
| **临床决策支持** | [Breast Cancer](docs/examples/clinical_decision_support/breast_cancer.pdf) | 基于证据的临床建议 |
| **假设生成** | [AI Weather Prediction](docs/examples/hypotheses_generation/AI_in_weather.pdf) | 研究假设开发 |
| **市场研究** | [Agentic AI Report](docs/examples/market%20research%20reports/agentic_ai_life_sciences.pdf) | 行业分析和市场洞察 |

**🎯 浏览这些示例**，在开始自己的项目之前查看格式、结构和质量！

## 文档

### 用户指南
- [📖 完整功能指南](docs/FEATURES.md) - 全面概述所有能力
- [🔧 API 参考](docs/API.md) - 完整的程序化 API 文档
- [🎯 技能概览](docs/SKILLS.md) - 所有可用技能和工具
- [🐛 故障排查](docs/TROUBLESHOOTING.md) - 常见问题与解决方案

### 开发者资源
- [💻 开发指南](docs/DEVELOPMENT.md) - 贡献与开发设置
- [📦 发布指南](docs/RELEASING.md) - 版本管理与发布
- [📋 更新日志](CHANGELOG.md) - 版本历史与更新
- [🤖 系统说明](CLAUDE.md) - 代理指令（高级）

## 版本管理与发布（简版）
使用 `uv` 和辅助脚本：
- 升级版本（保持 pyproject + __init__ 同步）：`uv run scripts/bump_version.py [patch|minor|major]`
- 构建并发布：`uv run scripts/publish.py`（或 `--bump patch|minor|major`）
有关前提条件、dry run、打标签和验证，请参见 [docs/RELEASING.md](docs/RELEASING.md)。

## 迁移（v1.x -> v2.0）
- CLI 保持不变（scientific-writer）。
- 新的程序化 API：from scientific_writer import generate_paper。
- 旧的单文件脚本已替换为正式包；CLI 用户无需任何操作。

## 许可证
MIT - 见 LICENSE。

## 支持
- 在 GitHub 上提交 issue
- 有关常见问题，请参见 [docs/TROUBLESHOOTING.md](docs/TROUBLESHOOTING.md)

## 💬 加入我们的社区！

**想与其他研究人员交流、分享技巧并实时获得帮助？** 加入我们充满活力的 Slack 社区吧！🎉

无论你是在撰写第一篇论文、探索高级功能，还是只是想聊聊科学写作和 AI，我们都很欢迎你！获取更快的支持，分享你的成功故事，并与其他用户协作。

👉 **[加入 K-Dense Slack 社区](https://join.slack.com/t/k-densecommunity/shared_invite/zt-3iajtyls1-EwmkwIZk0g_o74311Tkf5g)** 👈

我们很期待见到你！🚀

## ⭐ 展示你的支持

如果你觉得这个项目对你的研究或工作有帮助，请考虑在 GitHub 上给它点个星标！这有助于更多人发现这个工具，并激励持续开发。谢谢！🙏

![GitHub stars](https://img.shields.io/github/stars/K-Dense-AI/claude-scientific-writer?style=social)

## 星标历史

[![Star History Chart](https://api.star-history.com/svg?repos=K-Dense-AI/claude-scientific-writer&type=Date)](https://star-history.com/#K-Dense-AI/claude-scientific-writer&Date)
