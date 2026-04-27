---
name: thesis-optimizer
description: |
  学术论文智能优化系统，专为计算机深度学习方向硕士学位论文设计。
  提供三维协同优化：降低 AI 写作风险特征、降查重率、学术润色提升。
  采用两层文档架构（总揽+章节）与显式状态追踪，实现模块化闭环优化。
  内置中文学术写作风险模式、词汇风险和句式节奏参考。严格遵循“最小干预与句内微调”原则，避免大段AI式重写，保留作者原有科研逻辑。

  Intelligent thesis optimization system for computer science deep learning master's theses.
  Provides three-dimensional optimization: AI-writing-risk reduction, plagiarism reduction,
  academic polishing. Uses two-tier document architecture (master + chapter) with explicit
  state tracking for modular closed-loop optimization. Uses writing-risk references and
  minimal intra-sentence restructuring to preserve the author's logic.

  关键词: thesis-optimization, ai-detection, plagiarism, polishing, academic-writing, perplexity, burstiness
---

# Thesis-Optimizer: 学术论文智能优化系统

## 何时使用此Skill / When to Use

当用户需要对学位论文进行以下优化时触发：
- 降低 AI 写作风险特征（可结合用户指定检测工具抽样验证）
- 降低查重率（知网、维普等）
- 学术润色和表达提升
- 系统化、可追踪的论文优化

## 核心架构 / Core Architecture

采用**两层文档架构 + 显式状态追踪**：

```
第一层: 总揽文档 (thesis_master_overview.md)
  ├── 论文整体分析与解读
  ├── 章节划分与优化策略
  ├── 全局进度追踪 [██████░░░░] 60%
  └── 章节状态矩阵
      │
      ├─→ 第二层: chapter_01_abstract.md
      ├─→ 第二层: chapter_02_intro.md
      └─→ ... 其他章节任务文档
```

## 工作流程 / Workflow

### Phase 0: 初始化 - 生成总揽文档

**触发条件**: 用户首次请求优化论文

**执行步骤**:
1. 使用 `view_file` 完整阅读论文LaTeX源文件
2. 分析结构：识别章节、段落、公式、图表
3. 内容解读：理解研究主题、核心贡献、论证逻辑
4. 问题诊断：识别AI特征、查重风险点、表达问题
5. 根据 `templates/master_overview_template.md` 生成总揽文档

**输出**: `thesis_master_overview.md` 存储在论文同目录

### Phase 0.5: AI 模式全景扫描

**触发条件**: 总揽文档生成后、逐章节优化开始前

**执行步骤**:
1. 依据 `references/ai_pattern_taxonomy.md` 对全文进行系统扫描
2. 定位 6 大类 30+ 种典型 AI 模式特征及高风险段落
3. 在总揽文档中生成模式检出热力图（标记各章节主要 AI 缺陷）

### Phase 1: 逐章节深度优化循环

**对于总揽文档中每个待处理章节**:

1. **创建章节任务文档**
   - 使用 `templates/chapter_task_template.md`
   - 命名: `chapter_XX_name.md`

2. **应用高阶优化策略** (阅读 `references/` 获取详细指导)
   - 核心原则：**术语保护**优先，保留公式、专业缩写和关键推理链。
   - **最小干预原则**：处理 AI 写作风险特征时，优先采用句内结构微调、局部语序调整和小范围词汇替换；不要推翻原段落逻辑或进行大段扩写。
   - **学术语体约束**：避免戏剧化、网文风、口语化或过度情绪化表达（如“暴力美学”、“疯狂抽取”、“撕碎”等）。重写应保持客观、严谨、中立、平实。
   - 策略A: 模式扫描与定位 → 对照 `references/ai_pattern_taxonomy.md`
   - 策略B: 词汇风险检查 → 参考 `references/ai_vocabulary_blacklist.md`
   - 策略C: 句式节奏检查 → 参考 `references/perplexity_burstiness.md`
   - 策略D: 降低 AI 写作风险特征 → 依据作者原有逻辑进行句内微调
   - 策略E: 降查重率（语义改写） → `references/strategy_plagiarism.md`
   - 策略F: 学术润色（精炼与连贯） → `references/strategy_polishing.md`

3. **生成优化后的LaTeX**
   - 保持原有格式规范
   - 记录改写前后对照

4. **更新总揽文档**
   - 更新章节状态: ⏳待处理 → 🟡进行中 → 🟢已完成
   - 更新全局进度条
   - 记录关键问题和解决方案

5. **评估质量**
   - 参考 `references/evaluation_criteria.md`
   - 记录评估结果到章节任务文档

### Phase 2: 全局评估与迭代

**触发条件**: 所有章节初次优化完成

1. 汇总各章节评估结果
2. 识别未达标章节 (标记为 🔴需返工)
3. 在总揽文档添加"迭代计划"
4. 返回Phase 1处理问题章节

## 状态追踪机制 / State Tracking

**状态标记**:
- ⏳ 待处理 (Pending)
- 🟡 进行中 (In Progress)
- 🟢 已完成 (Completed)
- 🔴 需返工 (Re-work Needed)
- ⭐ 已验证 (Verified)

**防偏移设计**:
- 每个章节在总揽文档有明确状态行
- "当前工作"和"下一步"字段指示任务
- 章节文档开头链接回总揽文档
- 每次更新记录时间戳

## 三大优化策略概览 / Optimization Strategies

### 策略A: 降低 AI 写作风险特征（坚守最小干预原则）
- **句内重组机制**：相关修改优先限于句内级别的结构重组与同义词更替，避免大范围扩写或整段洗稿。
- **顺应人类逻辑**：完全尊重并保留作者原始的人类书写逻辑与思维跳跃，不强行填补“AI式完美过渡”，保留真实的撰写颗粒度。
- **打破规整化句式**：刻意营造长短句交织，祛除AI偏爱的“高度对称、四平八稳、排比列举”等僵化行文特征。

### 策略B: 降查重率
- 深度语义改写 (同义替换、结构重组)
- 引用规范化 (直接→间接转换)
- 专业术语处理 (核心保留+描述变换)

### 策略C: 学术润色
- 表达精准化 (量化抽象概念)
- 学术规范性 (术语一致、时态规范)
- 可读性优化 (复杂句拆分、过渡流畅)

## 评估目标 / Evaluation Targets

| 指标 | 目标值 | 评估方法 / 工具 |
|------|--------|---------------|
| 5D质量评分 | 作为人工复核参考 | 依照 `references/evaluation_criteria.md` 对直接性/节奏感/自然度/学术性/精炼度进行评分 |
| AI风险抽样检测 | 以用户指定工具为准 | 检测器结果仅作参考，不承诺固定阈值 |
| 查重率 | < 10% | 知网, 维普 |
| 句式节奏 | 避免过度均匀 | 统计检查长短句分布，结合人工判断 |
| 词汇分布 | 避免高风险词密集出现 | 依照 `references/ai_vocabulary_blacklist.md` 进行校验 |

## 快速开始 / Quick Start

告诉我你的论文路径，我将：
1. 完整阅读并分析你的论文
2. 生成高质量的总揽文档
3. 按优先级逐章节进行优化
4. 持续追踪进度直至完成

---

**参考资源** (按任务需要阅读):
- *基础工作流*:
  - `templates/master_overview_template.md` - 总揽文档模板
  - `templates/chapter_task_template.md` - 章节任务模板
  - `references/evaluation_criteria.md` - 包含 5 维评分标准的评估体系
- *前置风险参考*:
  - `references/ai_pattern_taxonomy.md` - 30+ 种中文学术论文 AI 模式判别
  - `references/ai_vocabulary_blacklist.md` - 中文学术 AI 高频词汇风险参考
  - `references/perplexity_burstiness.md` - 句式节奏与统计风险提示
- *核心优化策略*:
  - `references/strategy_ai_reduction.md` - AI 写作风险特征降低策略
  - `references/strategy_plagiarism.md` - 降查重防自引策略
  - `references/strategy_polishing.md` - 严谨化学术语言指南
