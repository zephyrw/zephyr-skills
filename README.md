# Zephyr Skills

由我原创设计与构建的 AI Agent 核心技能库，全面适配 Claude Code、OpenAI Codex、Google Antigravity、Cursor、OpenCode 等主流 Agent 平台。

在长期使用 AI 进行软件工程规划、复杂问题排查与文学故事创作的实践中，我发现默认状态下的大模型普遍存在三大痛点：**写故事时急于把平庸套路扩写成行活大纲**、**写方案时堆砌零散技术细节而缺乏读者视角**、**日常沟通时充斥寒暄套话与过程流水账**。

为此，我从零设计并打磨了这 **3 个原创 Skill**，分别从**故事创意破局与结构孵化**、**易读方案与计划架构**、**高信噪比简练表达**三个维度重塑 Agent 的思考与输出方式。

---

## 一、我创建的原创技能总览

| 技能名称 | 目录 | 原创设计初衷与定位 | 适用场景 | 核心方法与机制 |
| :--- | :--- | :--- | :--- | :--- |
| **[`plan-fiction`](./plan-fiction)** | `plan-fiction/` | 中短篇小说构思与大纲搭档 | 构思中短篇小说、打破平庸套路发散一句话故事前提、诊断情节断裂与角色被动、生成可动笔的故事大纲 | 内部滤除前 3 个直觉套路 + 6 种反套路破局发散法 + “一句话核心事件优先”门禁 + 内外双层因果与信息边界核验 + 单问交互与梯度化候选 |
| **[`human-readable-plans`](./human-readable-plans)** | `human-readable-plans/` | 易读方案与计划写作规范 | 编写或改写供人阅读、评审与跨团队分享的技术方案、产品规划、任务安排 | 读者认知八步顺序（背景 → 现状 → 目标 → 制定原因 → 总体思路 → 依据 → 执行 → 验收）+ 全文及任务双层总分结构 |
| **[`concise-complete-writing`](./concise-complete-writing)** | `concise-complete-writing/` | 简练完整表达规范 | 日常问答回复、进度同步、问题排查结论、技术报告、各类正式文档 | 结论先行 + 事实/推断/未知严格区分 + 剔除套话与过程流水账 + 输出前四步静默自检 |

---

## 二、原创技能深度解析

### 1. `plan-fiction` — 中短篇小说构思搭档

这是我为中短篇小说创作专门打造的构思搭档。许多 AI 辅助写作工具一上来就催促创作者填人物卡、套三幕式模板或直接代写正文，往往把最容易想到的平均值套路强行包装成看似完整却毫无吸引力的行活。

为了解决这一问题，我设计了一套**“防平庸破局、一句话核心事件优先、单问推进、不越界代写”**的原创构思体系：

- **过滤直觉套路与六种破局发散法**：要求 Agent 在给出点子前，先在内部默想并丢弃该题材最容易滑向的 3 个高频套路；再通过**倒置默认前提、让人物拿手本事失效、日常处境陌生化、跨领域借用运作结构、双合理愿望彼此拆台、保留单一反常点**六种方法发散出真正出乎意料的事件，并用“换词测试”剔除通用套路外壳。
- **先立住“值得写的整件事”**：把主要精力花在探索和筛选能概括整篇故事的一句话核心事件上。尚未找到真正有吸引力的事件机制前，绝不靠扩写细节或堆砌设定推进大纲。
- **每轮只问一个关键问题 + 梯度化候选**：严格禁止连环追问和填表式审讯。当创作者卡住时，主动给出 2–4 个落在具体事件机制与矛盾上的梯度候选（至少含 1 个扎根处境、立即可动笔的扎实方案，以及 1–2 个打破常规预期的刁钻方案）。
- **五大模块化构思参考**：内置 [人物与创意](./plan-fiction/references/character-and-premise.md)、[因果与压力](./plan-fiction/references/causality-and-pressure.md)、[读者与结构](./plan-fiction/references/reader-and-structure.md)、[交付与检查](./plan-fiction/references/delivery-and-review.md) 与 [对话示例](./plan-fiction/references/dialogue-examples.md)，覆盖冲突型与容器型（非强对抗）叙事、内外双层因果核验、三层信息边界与中短篇容量裁剪。

---

### 2. `human-readable-plans` — 易读方案与计划规范

在工程与产品协作中，AI 写出的方案经常一上来就是满屏的文件路径、字段罗列和零散步骤，导致没有参与前期对话的评审者根本看不懂“为什么要做这件事、现在卡在哪、整体怎么解决”。

我创建 `human-readable-plans` 的核心目标，就是**让任何没有参与前期讨论的读者拿到文档都能一次看懂来龙去脉**：

- **按人类读者的理解顺序展开**：
  1. **背景**：交代涉及的人、业务或系统，以及促成本次安排的场景。
  2. **现状**：说明当前进展、实际问题与影响，区分已知事实与待确认情况。
  3. **目标**：用读者能观察或判断的结果描述完成后应当发生的变化，拒绝“提升体验”等空泛口号。
  4. **制定原因**：讲清现状与目标的差距，以及为何现在选择这一方向。
  5. **总体思路**：用简明段落串起主要工作、先后关系与各部分作用，先立主线再进细节。
  6. **依据与关键判断**：呈现支撑方案可行的事实、调研结果与关键取舍。
  7. **执行安排**：按阶段或任务写清前提、依赖、步骤与交付结果。
  8. **完成标准及风险处理**：给出可核对的验收标准及关键风险应对。
- **全文与每项任务均采用总分结构**：我设计了“任务首句定用途”的硬性规范——每项具体任务必须先用一句自然的话说明**“这项工作要解决什么、完成后有什么用”**，再展开具体实施内容；把密集接口契约、代码路径与测试矩阵后置，让读者只读总体思路、任务标题和首句即可把握全局。

---

### 3. `concise-complete-writing` — 简练完整表达规范

这是我为所有面向用户的输出设计的底层表达契约，旨在做到：**在准确、完整、无歧义的前提下，用最少的文字让读者一次读懂并能据此判断或行动。**

- **结论先行**：先给出结论、答案或当前状态，再补充必要依据与后续行动。
- **极高信噪比**：只保留影响理解、判断、执行或验收的信息；彻底删除重复背景、寒暄套话、空泛评价、内部细节与过程流水账。
- **消除指代与条件歧义**：
  - 同一对象全程使用同一术语，不为避免词面重复而随意换叫法。
  - 用具体动词写清“谁对什么做什么”，拒绝“进行处理”式模糊表达。
  - 执行前必须满足的前提、条件与限制紧贴在对应动作之前。
  - 严格区分**已验证事实、推断、未验证假设、已完成与待完成事项**。
- **输出前四步静默自检**：要求 Agent 在发送或保存任何文字前，静默完成**“1. 完整 → 2. 无歧义 → 3. 精简 → 4. 易读可用”**四道质量检验。

---

## 三、目录结构

```text
zephyr-skills/
├── README.md
├── concise-complete-writing/          # [原创] 简练完整表达规范
│   └── SKILL.md
├── human-readable-plans/              # [原创] 易读方案与计划规范
│   └── SKILL.md
└── plan-fiction/                      # [原创] 中短篇小说构思搭档
    ├── SKILL.md
    ├── agents/
    │   └── openai.yaml
    └── references/
        ├── causality-and-pressure.md
        ├── character-and-premise.md
        ├── delivery-and-review.md
        ├── dialogue-examples.md
        └── reader-and-structure.md
```

---

## 四、安装与使用

### 1. 克隆仓库

```bash
git clone git@github.com:zephyrw/zephyr-skills.git ~/zephyr-skills
```

### 2. 按客户端软链接安装（推荐，便于 `git pull` 同步更新）

根据你使用的 AI 客户端，将技能软链接到对应的全局技能目录：

```bash
# 通用 Agent Skills 目录（Claude Code / Antigravity 等共享推荐）
mkdir -p ~/.agents/skills
for skill in concise-complete-writing human-readable-plans plan-fiction; do
  ln -sfn ~/zephyr-skills/$skill ~/.agents/skills/$skill
done

# Claude Code
mkdir -p ~/.claude/skills
for skill in concise-complete-writing human-readable-plans plan-fiction; do
  ln -sfn ~/zephyr-skills/$skill ~/.claude/skills/$skill
done

# OpenAI Codex
mkdir -p ~/.codex/skills
for skill in concise-complete-writing human-readable-plans plan-fiction; do
  ln -sfn ~/zephyr-skills/$skill ~/.codex/skills/$skill
done

# Google Antigravity / Gemini CLI
mkdir -p ~/.gemini/config/skills
for skill in concise-complete-writing human-readable-plans plan-fiction; do
  ln -sfn ~/zephyr-skills/$skill ~/.gemini/config/skills/$skill
done
```

### 3. 组合使用建议

- **编写技术方案、产品规划或重构计划时**：同时启用 `human-readable-plans` 与 `concise-complete-writing`，产出的方案不仅从背景到验收脉络清晰、适合直接转发给团队评审，而且行文干净利落、毫无废话。
- **日常开发、排查问题与同步进度时**：将 `concise-complete-writing` 作为常驻底层规范，让每一次回复都结论先行、事实与推断界限分明。
- **构思中短篇小说时**：调用 `plan-fiction`，滤除常见套路，从一句真正出乎意料且让你有写作冲动的核心事件出发，在单问互动中打磨出严密的因果链与故事大纲。
