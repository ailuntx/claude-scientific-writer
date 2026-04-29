# 临床报告技能

## 概述

综合技能用于撰写临床报告，包括病例报告、诊断报告、临床试验报告和患者文档。提供模板、监管合规性和验证工具的全面支持。

## 包含内容

### 📋 四大报告类型

1. **临床病例报告** - 符合CARE指南的医学期刊发表病例报告
2. **诊断报告** - 放射学（ACR）、病理学（CAP）和实验室报告
3. **临床试验报告** - SAE报告、临床研究报告（ICH-E3）、DSMB报告
4. **患者文档** - SOAP笔记、病历记录、出院小结、会诊记录

### 📚 参考文件（8份综合指南）

- `case_report_guidelines.md` - CARE指南、去标识化、期刊要求
- `diagnostic_reports_standards.md` - ACR、CAP、CLSI标准、结构化报告系统
- `clinical_trial_reporting.md` - ICH-E3、CONSORT、SAE报告、MedDRA编码
- `patient_documentation.md` - SOAP笔记、病历记录、出院小结标准
- `regulatory_compliance.md` - HIPAA、21 CFR Part 11、ICH-GCP、FDA法规
- `medical_terminology.md` - SNOMED-CT、LOINC、ICD-10、CPT代码
- `data_presentation.md` - 临床表格、图表、Kaplan-Meier曲线
- `peer_review_standards.md` - 临床手稿审查标准

### 📄 模板（12个专业模板）

- `case_report_template.md` - 遵循CARE指南的结构化病例报告
- `soap_note_template.md` - SOAP进度记录格式
- `history_physical_template.md` - 完整病历检查模板
- `discharge_summary_template.md` - 医院出院文档
- `consult_note_template.md` - 专家会诊格式
- `radiology_report_template.md` - 结构化报告影像报告
- `pathology_report_template.md` - 含CAP归纳要素的外科病理报告
- `lab_report_template.md` - 临床实验室检验结果
- `clinical_trial_sae_template.md` - 严重不良事件报告表
- `clinical_trial_csr_template.md` - 临床研究报告大纲（ICH-E3）
- `quality_checklist.md` - 所有报告类型的质量保证
- `hipaa_compliance_checklist.md` - 隐私和去标识化验证

### 🔧 验证脚本（8个自动化工具）

- `validate_case_report.py` - 检查CARE指南合规性和完整性
- `check_deidentification.py` - 扫描报告中18个HIPAA标识符
- `validate_trial_report.py` - 验证ICH-E3结构和必需元素
- `format_adverse_events.py` - 从CSV数据生成不良事件汇总表
- `generate_report_template.py` - 交互式模板选择和生成
- `extract_clinical_data.py` - 解析和提取结构化临床数据
- `compliance_checker.py` - 验证监管合规要求
- `terminology_validator.py` - 验证医学术语和禁用缩写

## 快速开始

### 生成模板

```bash
cd .claude/skills/clinical-reports/scripts
python generate_report_template.py

# 或直接指定类型
python generate_report_template.py --type case_report --output my_case_report.md
```

### 验证病例报告

```bash
python validate_case_report.py my_case_report.md
```

### 检查去标识化

```bash
python check_deidentification.py my_case_report.md
```

### 验证临床试验报告

```bash
python validate_trial_report.py my_csr.md
```

## 主要功能

### CARE指南合规性
- 完整的CARE清单覆盖
- 去标识化验证
- 知情同意文档
- 时间线创建辅助
- 文献综述整合

### 监管合规性
- **HIPAA** - 隐私保护、18个标识符移除、安全港方法
- **FDA** - 21 CFR第11、50、56、312部分合规
- **ICH-GCP** - 良好临床实践标准
- **ALCOA-CCEA** - 数据完整性原则

### 专业标准
- **ACR** - 美国放射学会报告标准
- **CAP** - 美国病理学家学会归纳报告
- **CLSI** - 临床实验室标准委员会
- **CONSORT** - 临床试验报告
- **ICH-E3** - 临床研究报告结构

### 医学编码系统
- **ICD-10-CM** - 诊断编码
- **CPT** - 操作编码
- **SNOMED-CT** - 临床术语
- **LOINC** - 实验室观察代码
- **MedDRA** - 监管活动医学词典

## 常见用例

### 1. 发表临床病例报告

```
> 为一位65岁患者创建非典型急性阑尾炎表现的临床病例报告

> 检查此病例报告的HIPAA合规性
> 根据CARE指南验证
```

### 2. 编写诊断报告

```
> 为胸部CT生成放射学报告模板
> 为结肠切除标本创建腺癌病理报告
> 为血常规编写实验室报告
```

### 3. 临床试验文档

```
> 为肺炎住院撰写严重不良事件报告
> 为3期糖尿病试验创建临床研究报告大纲
> 从试验数据生成不良事件汇总表
```

### 4. 患者临床记录

```
> 为随访就诊创建SOAP笔记
> 为胸痛入院患者生成病历记录
> 为心力衰竭住院撰写出院小结
> 创建心脏病学会诊记录
```

## 工作流程示例

### 病例报告工作流程

1. **获取患者**知情同意
2. **生成模板**: `python generate_report_template.py --type case_report`
3. **按照CARE结构撰写**病例报告
4. **验证合规性**: `python validate_case_report.py case_report.md`
5. **检查去标识化**: `python check_deidentification.py case_report.md`
6. **提交期刊**并附CARE清单

### 临床试验SAE工作流程

1. **生成SAE模板**: `python generate_report_template.py --type sae`
2. **在事件发生后24小时内**填写SAE表格
3. **使用WHO-UMC或Naranjo标准**评估因果关系
4. **验证完整性**: `python validate_trial_report.py sae_report.md`
5. **按监管时间线**（7天或15天）提交给申办方
6. **根据机构政策**通知IRB

## 最佳实践

### 隐私和伦理
✓ 病例报告始终获取知情同意  
✓ 出版前移除所有18个HIPAA标识符  
✓ 使用去标识化验证脚本  
✓ 稿件中记录同意情况  
✓ 罕见疾病考虑重新识别风险  

### 临床质量
✓ 使用专业医学术语  
✓ 遵循结构化报告模板  
✓ 包含所有必需元素  
✓ 清晰记录时间顺序  
✓ 用证据支持诊断  

### 监管合规性
✓ 遵守SAE报告时间线（7天、15天）  
✓ CSRs遵循ICH-E3结构  
✓ 维护ALCOA-CCEA数据完整性  
✓ 记录方案依从性  
✓ 不良事件使用MedDRA编码  

### 文档标准
✓ 所有临床记录签字注明日期  
✓ 记录医疗必要性  
✓ 仅使用标准缩写  
✓ 避免禁用缩写（JCAHO"勿用"清单）  
✓ 保持清晰完整  

## 集成

临床报告技能可与以下工具无缝集成：

- **scientific-writing** - 清晰专业的医学写作
- **peer-review** - 病例报告质量评估
- **citation-management** - 病例报告中的文献引用
- **research-grants** - 临床试验方案开发

## 资源

### 外部标准
- CARE指南: https://www.care-statement.org/
- ICH-E3指南: https://database.ich.org/sites/default/files/E3_Guideline.pdf
- CONSORT声明: http://www.consort-statement.org/
- HIPAA: https://www.hhs.gov/hipaa/
- ACR实践参数: https://www.acr.org/Clinical-Resources/Practice-Parameters-and-Technical-Standards
- CAP癌症方案: https://www.cap.org/protocols-and-guidelines

### 专业组织
- 美国医学会（AMA）
- 美国放射学会（ACR）
- 美国病理学家学会（CAP）
- 临床实验室标准委员会（CLSI）
- 国际协调理事会（ICH）

## 支持

如有关于临床报告技能的问题或疑问：
1. 查看综合参考文件
2. 查看模板示例
3. 运行验证脚本识别问题
4. 参阅SKILL.md获取详细指导

## 许可证

Claude科学作家项目的一部分。请参阅主LICENSE文件。
