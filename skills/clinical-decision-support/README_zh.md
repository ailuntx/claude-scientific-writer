# 临床决策支持技能

适用于制药和临床研究环境中医疗专业人员的专业临床决策支持文档。

## 快速开始

此技能可生成三种类型的临床文档：

1. **个体化患者治疗方案** - 针对特定患者的个性化方案
2. **患者队列分析** - 生物标志物分层组分析，包含预后数据
3. **治疗建议报告** - 基于循证医学的临床指南

所有文档均生成为紧凑、专业的 LaTeX/PDF 文件。

## 目录结构

```
clinical-decision-support/
├── SKILL.md                     # 技能主定义
├── README.md                    # 本文件
│
├── references/                  # 临床指南文档
│   ├── patient_cohort_analysis.md
│   ├── treatment_recommendations.md
│   ├── clinical_decision_algorithms.md
│   ├── biomarker_classification.md
│   ├── outcome_analysis.md
│   └── evidence_synthesis.md
│
├── assets/                      # 模板和示例
│   ├── cohort_analysis_template.tex
│   ├── treatment_recommendation_template.tex
│   ├── clinical_pathway_template.tex
│   ├── biomarker_report_template.tex
│   ├── example_gbm_cohort.md
│   ├── recommendation_strength_guide.md
│   └── color_schemes.tex
│
└── scripts/                     # 分析和生成工具
    ├── generate_survival_analysis.py
    ├── create_cohort_tables.py
    ├── build_decision_tree.py
    ├── biomarker_classifier.py
    └── validate_cds_document.py
```

## 使用示例

### 创建患者队列分析
```
> 分析45例NSCLC患者队列，按PD-L1表达分层
  (<1%, 1-49%, ≥50%)，包含ORR、PFS和OS预后
```

### 生成治疗建议
```
> 为HER2阳性转移性乳腺癌创建循证治疗建议，
  采用GRADE方法学
```

### 构建临床路径
```
> 生成急性胸痛管理的临床决策算法，
  使用TIMI风险评分
```

## 主要特性

- **GRADE方法学**：证据质量分级（高/中/低/极低）
- **建议强度**：强推荐（1级） vs 有条件推荐（2级）
- **生物标志物整合**：基因组、表达和分子亚型分类
- **统计分析**：Kaplan-Meier、Cox回归、log-rank检验
- **指南一致性**：NCCN、ASCO、ESMO、AHA/ACC整合
- **专业输出**：0.5英寸页边距、彩色框注、可直接投稿

## 依赖项

Python脚本需要：
- `pandas`、`numpy`、`scipy`：数据分析和统计
- `lifelines`：生存分析（Kaplan-Meier、Cox回归）
- `matplotlib`：可视化
- `pyyaml`（可选）：决策树的YAML输入

安装方式：
```bash
pip install pandas numpy scipy lifelines matplotlib pyyaml
```

## 包含的参考文献

1. **患者队列分析**：分层方法、生物标志物相关性、统计比较
2. **治疗建议**：证据分级、治疗顺序、特殊人群
3. **临床决策算法**：风险评分、决策树、TikZ流程图
4. **生物标志物分类**：基因组改变、分子亚型、伴随诊断
5. **预后分析**：生存方法、疗效评估标准（RECIST）、效应量
6. **证据整合**：指南整合、系统综述、荟萃分析

## 提供的模板

1. **队列分析**：人口统计学表、生物标志物谱、预后、统计、建议
2. **治疗建议**：证据综述、GRADE分级选项、监测、决策算法
3. **临床路径**：带风险分层和紧急编码操作的TikZ流程图
4. **生物标志物报告**：基因组谱系，基于可行性分级和疗法匹配

## 包含的脚本

1. **`generate_survival_analysis.py`**：创建带风险比的Kaplan-Meier曲线
2. **`create_cohort_tables.py`**：生成基线、疗效和安全性表
3. **`build_decision_tree.py`**：将文本/JSON转换为TikZ流程图
4. **`biomarker_classifier.py`**：按PD-L1、HER2、分子亚型对患者进行分层
5. **`validate_cds_document.py`**：检查完整性和合规性的质量控制

## 集成

与现有技能集成：
- **scientific-writing**：引文管理、统计报告
- **clinical-reports**：医学术语、HIPAA合规
- **scientific-schematics**：TikZ流程图

## 版本

版本 1.0 - 初始版本
创建时间：2024年11月
最后更新：2024年11月5日

## 问题或反馈

此技能专为创建临床决策支持文档的制药和临床研究专业人员设计。如有关于使用的问题或改进建议，请联系科学写作开发团队。
