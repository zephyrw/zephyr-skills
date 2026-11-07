# Zephyr Skills

由我原创设计与构建的 AI Agent 核心技能库，全面适配 Claude Code、OpenAI Codex、Google Antigravity、Cursor、OpenCode 等主流 Agent 平台。

在长期使用 AI 进行软件工程规划、复杂问题排查与文学故事创作的实践中，我发现默认状态下的大模型普遍存在三大痛点：**写故事时急于把平庸套路扩写成行活大纲**、**写方案时堆砌零散技术细节而缺乏读者视角**、**日常沟通时充斥寒暄套话与过程流水账**。

为此，我从零设计并打磨了这 **3 个原创 Skill**，分别针对**小说构思与大纲打磨**、**易读方案与计划编写**、**简练准确表达**三个场景，规范 Agent 的思考与输出方式。

---

## 一、我创建的原创技能总览

| 技能名称 | 目录 | 原创设计初衷与定位 | 适用场景 | 核心方法与机制 |
| :--- | :--- | :--- | :--- | :--- |
| **[`plan-fiction`](./plan-fiction)** | `plan-fiction/` | 中短篇小说构思与大纲搭档 | 构思中短篇小说、避开常见套路构思一句话故事核心、诊断情节断裂与角色被动、生成可动笔的故事大纲 | 先排除前 3 个常见套路 + 6 种反套路构思角度 + 先定一句话核心事件再展开大纲 + 内外因果与信息差检查 + 每轮单问与多方向候选 |
| **[`human-readable-plans`](./human-readable-plans)** | `human-readable-plans/` | 易读方案与计划写作规范 | 编写或改写供人阅读、评审与跨团队分享的技术方案、产品规划、任务安排 | 按读者理解顺序展开（背景 → 现状 → 目标 → 制定原因 → 总体思路 → 依据 → 执行 → 验收）+ 全文与每项任务均采用总分结构 |
| **[`concise-complete-writing`](./concise-complete-writing)** | `concise-complete-writing/` | 简练完整表达规范 | 日常问答回复、进度同步、问题排查结论、技术报告、各类正式文档 | 结论先行 + 事实/推断/未知严格区分 + 剔除套话与过程流水账 + 输出前四步静默自检 |

---

## 二、原创技能深度解析

### 1. `plan-fiction` — 中短篇小说构思搭档

这是我为中短篇小说创作专门打造的构思搭档。许多 AI 辅助写作工具一上来就催促创作者填人物卡、套三幕式模板或直接代写正文，往往把最容易想到的老套情节强行包装成看似完整却毫无吸引力的行活。

为了解决这一问题，我设计了一套“**先避开俗套、先定一句话核心事件、每轮只问一个问题、只做大纲不代写正文**”的构思流程：

- **先排除常见套路，再用六种角度找新意**：要求 Agent 在给出点子前，先在内部默想并丢弃该题材最容易滑向的 3 个高频套路；再通过**倒置默认前提、让人物拿手本事失效、日常处境陌生化、借用其他行业的办事规矩、让两个合理愿望彼此冲突、保留一处反常细节**六种角度发散出真正出乎意料的事件，并用“换词测试”去掉换个名字就能到处套的空壳故事。
- **先立住“值得写的整件事”**：把主要精力花在探索和筛选能概括整篇故事的一句话核心事件上。尚未找到真正有吸引力的具体事件前，绝不靠扩写细节或堆砌设定推进大纲。
- **每轮只问一个关键问题，卡住时提供具体候选**：不连环追问，也不像填表一样盘问设定。当创作者没思路时，主动给出 2–4 个具体事件候选（既有贴近日常处境、马上能动笔的稳妥方向，也有打破常规预期的反套路方向）。
- **五份配套参考文档**：内置 [人物与创意](./plan-fiction/references/character-and-premise.md)、[因果与压力](./plan-fiction/references/causality-and-pressure.md)、[读者与结构](./plan-fiction/references/reader-and-structure.md)、[交付与检查](./plan-fiction/references/delivery-and-review.md) 与 [对话示例](./plan-fiction/references/dialogue-examples.md)，涵盖冲突推进与非强对抗故事、人物内外因果检查、读者与角色信息差安排，以及中短篇篇幅控制。

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
- **全文与每项任务均采用总分结构**：我设计了“任务首句定用途”的硬性规范——每项具体任务必须先用一句自然的话说明“**这项工作要解决什么、完成后有什么用**”，再展开具体实施内容；把接口字段、代码路径和详细测试清单放到后文或附录，让读者只读总体思路、任务标题和首句即可把握全局。

---

### 3. `concise-complete-writing` — 简练完整表达规范

这是我为所有面向用户的输出制定的基本表达规范，旨在做到：**在准确、完整、无歧义的前提下，用最少的文字让读者一次读懂并能据此判断或行动。**

- **结论先行**：先给出结论、答案或当前状态，再补充必要依据与后续行动。
- **只留有用信息，删掉废话**：只保留影响理解、判断、执行或验收的信息；彻底删除重复背景、寒暄套话、空泛评价、内部细节与过程流水账。
- **消除指代与条件歧义**：
  - 同一对象全程使用同一术语，不为避免词面重复而随意换叫法。
  - 用具体动词写清“谁对什么做什么”，拒绝“进行处理”式模糊表达。
  - 执行前必须满足的前提、条件与限制紧贴在对应动作之前。
  - 严格区分**已验证事实、推断、未验证假设、已完成与待完成事项**。
- **输出前四步静默自检**：要求 Agent 在发送或保存任何文字前，静默完成“**1. 完整 → 2. 无歧义 → 3. 精简 → 4. 易读可用**”四步自检。

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

### 1. 方式一：发送提示词让 Agent 自动安装（推荐）

直接复制以下任一提示词发给 Claude Code、OpenAI Codex、Google Antigravity、Cursor 或 OpenCode，让 Agent 自动完成“**克隆临时仓库 → 按需复制指定 Skill → 删除克隆的临时仓库**”：

- **通用模板**（按需只安装 1 个或多个指定 Skill）：
  ```text
  请帮我从 https://github.com/zephyrw/zephyr-skills.git 安装指定的 Skill：
  1. 先将仓库克隆到临时目录 /tmp/zephyr-skills；
  2. 只将其中我需要的 [填写技能名，例如：plan-fiction，或 human-readable-plans 和 concise-complete-writing] 复制到我当前客户端的全局技能目录（如 ~/.agents/skills、~/.claude/skills、~/.codex/skills 或 ~/.gemini/config/skills），不要安装其他未指定的 Skill；
  3. 复制完成后，删除克隆的临时目录 /tmp/zephyr-skills，并告诉我最终安装好的路径。
  ```

- **开箱即用提示词示例**（可直接复制发送）：
  - **只安装小说构思**（`plan-fiction`）：
    ```text
    请帮我把 https://github.com/zephyrw/zephyr-skills.git 克隆到临时目录 /tmp/zephyr-skills，只把里面的 plan-fiction 复制到当前客户端的全局技能目录，复制完成后删除 /tmp/zephyr-skills 临时目录。
    ```
  - **只安装写方案 + 简练表达**（`human-readable-plans` + `concise-complete-writing`）：
    ```text
    请帮我把 https://github.com/zephyrw/zephyr-skills.git 克隆到临时目录 /tmp/zephyr-skills，只把里面的 human-readable-plans 和 concise-complete-writing 复制到当前客户端的全局技能目录，复制完成后删除 /tmp/zephyr-skills 临时目录。
    ```
  - **安装全部 3 个 Skill**：
    ```text
    请帮我把 https://github.com/zephyrw/zephyr-skills.git 克隆到临时目录 /tmp/zephyr-skills，把里面的 plan-fiction、human-readable-plans、concise-complete-writing 全部复制到当前客户端的全局技能目录，复制完成后删除 /tmp/zephyr-skills 临时目录。
    ```

### 2. 方式二：命令行手动安装（克隆 → 复制 → 删除临时目录）

- **只安装单个或指定几个 Skill**（以 `plan-fiction` 为例，如需同时安装多个可在 `cp -R` 后追加目录名）：
  ```bash
  git clone --depth 1 https://github.com/zephyrw/zephyr-skills.git /tmp/zephyr-skills && \
  mkdir -p ~/.agents/skills && \
  cp -R /tmp/zephyr-skills/plan-fiction ~/.agents/skills/ && \
  rm -rf /tmp/zephyr-skills
  ```
  *(注：根据你使用的客户端，可将目标路径 `~/.agents/skills/` 替换为 `~/.claude/skills/`、`~/.codex/skills/` 或 `~/.gemini/config/skills/`。)*

- **一次性安装全部 3 个 Skill**：
  ```bash
  git clone --depth 1 https://github.com/zephyrw/zephyr-skills.git /tmp/zephyr-skills && \
  mkdir -p ~/.agents/skills && \
  cp -R /tmp/zephyr-skills/concise-complete-writing /tmp/zephyr-skills/human-readable-plans /tmp/zephyr-skills/plan-fiction ~/.agents/skills/ && \
  rm -rf /tmp/zephyr-skills
  ```

### 3. 组合使用建议

- **编写技术方案、产品规划或重构计划时**：同时启用 `human-readable-plans` 与 `concise-complete-writing`，产出的方案不仅从背景到验收脉络清晰、适合直接转发给团队评审，而且行文干净利落、毫无废话。
- **日常开发、排查问题与同步进度时**：将 `concise-complete-writing` 作为常驻规范，让每一次回复都结论先行、事实与推断界限分明。
- **构思中短篇小说时**：使用 `plan-fiction`，避开常见套路，从一句真正出乎意料且让你有写作冲动的核心事件出发，在单问互动中打磨出严密的因果链与故事大纲。
