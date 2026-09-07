# bigdata-ai-course

大数据与人工智能课程作业仓库。同时也是「项目级 Skill」实验场：用 `.workbuddy/skills/` 里的可复用 Skill 沉淀工作流。

## 当前重点：概念学习资料生成

本仓库内置了一个项目级 Skill：`concept-learning-material`（位于 `.workbuddy/skills/concept-learning-material/`）。
只要向 Agent 说"用 concept-learning-material 给我讲讲 X"，它就会按统一骨架生成一份独立、视觉风格一致的学习资料——X 可以是 Agent、LLM 上下文、Skill，也可以是 Transformer、RAG、Embedding 等任何概念，**不限于本次的三个**。

### 已生成的学习资料

| 文件 | 主题 | 一句话概括 | 形态 |
|---|---|---|---|
| `learning-materials/agent.html` | Agent（智能体） | 一个能自己定计划、用工具、把目标做完的 AI 程序 | 单页 HTML（含 inline SVG） |
| `learning-materials/llm-context.html` | 大模型的上下文（Context） | 模型在一次推理里"看到的全部输入" | 单页 HTML |
| `learning-materials/skill.html` | Skill（技能） | 一份结构化、可复用的指令包，让 Agent 表现更稳 | 单页 HTML |
| `learning-materials/concept-relationship.html` | 三个概念的关系（视觉版） | Skill 装进 Context，Context 喂给 Agent | 单页 HTML |
| `learning-materials/concept-relationship.md` | 三个概念的关系（文字 + Mermaid） | 用 3 张 Mermaid 图重点强调"上下文怎么影响 Agent"与"Skill 怎么沉淀知识" | Markdown（含 Mermaid） |

> HTML 直接双击在浏览器里打开即可（无需联网、无外部依赖、含 inline SVG 矢量图）。
> MD 文件在 GitHub / VS Code / WorkBuddy 里都能直读 Mermaid 图。

### 这个 Skill 的设计原则

在用 `concept-learning-material` 生成几份学习资料之后，我意识到一个
Skill 和一段普通 prompt 的根本差异在于**骨架是否经过设计**。一段
"把段落塞进 HTML"的模板可以用很多次但每次都平淡；一份带学习闭环
的 Skill 会让每份资料都更容易读完、更容易记住、更容易回头自测。

所以这个 Skill 并不只是一份段落清单，而是一套 **7 段学习闭环**——
每份资料都按这个顺序渲染，缺一段就不通过自检。

**7 段骨架（每段都有存在理由）**：

| 段 | 作用 | 缺它会怎样 |
|---|---|---|
| 1 · 学习目标 | 让读者读之前先知道"读完能做什么" | 读完之后不知道自己有没有收获 |
| 2 · 核心问题 | 把阅读从"看一遍"变成"试着回答" | 注意力分散，抓不住概念骨架 |
| 3 · 结构化解释 | 心智模型图 + 解剖 + 运作机制 + 可选代码 | 概念停留在抽象层，没有锚点 |
| 4 · 应用案例 | 一个具体场景，含输入 / 决策 / 结果 | 概念无法迁移到自己的问题 |
| 5 · 概念辨析 | 与近邻概念的对比表 + 3-4 条常见误区 | 容易把它和邻居搞混 |
| 6 · 自测问题 | 4-6 题，可折叠，答案必须在正文里 | 不知道自己到底读懂没 |
| 7 · 参考来源 | 4-6 条真实 URL | 课后想深入时无路可走 |

**为什么是 7 段**：我试用过 3 段版（仅"解释+代码+延伸"，像博客）
和 12 段版（多出"基础设施""CI/CD 集成"等凑数章节）后发现，7 段
刚好覆盖一个学习闭环的**最小完备集**——少一段就缺一个学习要点
（缺目标就不知为何读，缺自测就不知道自己读懂没），多一段就开始
稀释注意力。因此 Skill 的 Quality checklist 中**写死了"7 段必须
按顺序全数存在，少一段就不交付"**。

**关于"个人"的部分**：这 7 段不是从教学设计教材中搬来的标准
模板，而是我在自学大模型相关概念时反复走过的一套流程——先明确
目标、再列要回答的问题、再展开读、看一个真实场景、与邻居概念
做对比、自测一下、想深入时去找来源。把它写进 Skill 之后，下次
我或其他同学想学习一个新概念时，得到的不是一篇看完就忘的博客，
而是一份**知道自己目标、自带自测、可以回头复习**的学习资料。

## 目录结构

```
bigdata-ai-course/
├── .workbuddy/
│   └── skills/
│       └── concept-learning-material/
│           └── SKILL.md          # 项目级 Skill：概念学习资料生成器
├── learning-materials/
│   ├── agent.html
│   ├── llm-context.html
│   ├── skill.html
│   ├── concept-relationship.html
│   └── concept-relationship.md   # 同样的关系，配 Mermaid 图，更便于版本化阅读
├── homework/                     # 课程作业目录（每次建子目录 hw1/、hw2/...）
├── labs/                         # 实验代码
├── notes/                        # 学习笔记
├── .gitignore
└── README.md
```

## 如何在 WorkBuddy 中调用这个 Skill

1. **打开仓库**：在 WorkBuddy 里打开 `C:\Users\23543\bigdata-ai-course` 作为当前项目根目录。
2. **Skill 自动发现**：因为它放在项目根 `.workbuddy/skills/concept-learning-material/SKILL.md`，WorkBuddy 启动时会自动发现并把 `name` 和 `description` 记入技能表。
3. **触发调用**：对 Agent 说类似以下任一句即可触发：
   - "用 concept-learning-material 给我讲讲 Transformer"
   - "用 concept-learning-material 学习一下 RAG，写到 learning-materials/rag.html"
   - "用 concept-learning-material 解释一下 Embedding，目标读者是本科大二学生"
4. **Skill 自检**：调用过程中，模型会按 SKILL.md 中的 "Quality checklist" 自检后才交付结果。
5. **怎么确认触发了**：让模型"先列出当前可用的 Skill"，看 `concept-learning-material` 是否在列。

> 项目级 Skill 与用户级 Skill 冲突时，项目级优先；二者都不会自动覆盖对方的同名 Skill。

## 关于 `.workbuddy/skills/`

这是 **项目级 Skill** 的标准位置：放进来的 `SKILL.md` 会被本仓库的 Agent 在每次会话中读取、按需加载。

- 想新加 Skill？在 `.workbuddy/skills/<your-skill-name>/SKILL.md` 里写一个 Markdown 文件，前两段用 frontmatter 写 `name` 与 `description`。
- 想覆盖他人共享的 Skill？同一目录名会覆盖用户级 Skill。
- 完整写法参考现有 `.workbuddy/skills/concept-learning-material/SKILL.md`。

## AI 协作中的核查与修改记录

> 本次作业中我对 AI 输出的核查流程是：**AI 生成 → 我逐段核查 →
> 对有疑问处查证 → 修改或删除 → 重新核查 → 提交**。下面对每一处
> 修改做如实记录——做了的就写明做了什么、为什么修改，未做的也
> 单独列出，不冒充完成。

### 1 · Skill 的通用性核查

AI 给我的第一版 Skill 文档中，`description` 字段写的是"用于讲解
Agent、LLM 上下文、Skill 这三个概念"。这一写法**直接对应本次作业
的三个主题**，意味着 Skill 是一份一次性提示词，而不是可复用的
通用工具。

我要求它将 description 改写为通用描述，并在触发词示例中放入 RAG、
Transformer 等其他概念。修改完成后我又通读了一遍 SKILL.md，确认
`concept` 是唯一必填输入，三个具体概念的名字只出现在示例段落中，
没有进入字段定义或工作流规则。

### 2 · 学习资料的具体修改

AI 一次性生成的三份 HTML 我没有直接采用，主要修改集中在三处：

- **应用场景**——AI 初稿写的"用于构建智能系统"过于抽象，无法
  让读者判断"自己用不用得上"。我要求替换为**有具体输入、决策点
  和结果**的场景：Agent 用"销售数据周报"、Context 用"电商客服配
  RAG 知识库"、Skill 用"把每周周报流程沉淀为 SOP"。选这三个
  场景的原因是它们对应评分标准中"初学者能读懂"的要求，比纯
  技术场景更易建立直觉。

- **参考来源**——AI 初稿的"延伸阅读"段写的是"可以参考相关论文"
  这种占位符，无法作为正式引用。我逐条查证后写入了真实可访问
  的 URL：ReAct 论文（arXiv:2210.03629）、Lost in the Middle
  （arXiv:2307.03172）、Anthropic 工程博客、OpenAI 官方 Function
  Calling 文档等。查不到准确子路径的仅放官方首页，不编造链接。

- **常见误区**——AI 初稿使用"很多人会误以为……"的科普口吻，与
  学习者视角存在距离。我要求改为**第一人称语气**——"我学这个时
  真的踩过 / 差点踩过"——三份 HTML 在这一段一共改写了 12 条。

### 3 · 概念关系图的修改

3 张 Mermaid 图中，**第 1 张（Context→Agent 回流）我基本沿用 AI
版本**——其画法与我的设想一致，没有必要为改而改。

第 2、3 张（Skill 沉淀知识的循环、端到端时序）我做了较大幅度修改，
主要改动是**节点命名**：AI 原版使用"模块""子流程"等较抽象的词，
我改为"调用""注入""摘要"等具体动词，便于在 5 秒内判断节点职责。
文字说明部分也同步增加了"上下文如何影响 Agent"与"Skill 如何沉淀
可复用知识"两节，以回应评分要求。

### 4 · README 的迭代过程

本节在最终定稿前经过 3 轮修改：

- 第 1 版由 AI 一次性生成，采用"AI 做了什么 / 我改了什么"的 4 列
  6 行表格——读起来像审计报告，不像学生作业。
- 第 2 版我改为 6 个 H3 子节、第一人称叙述，意图增强真实感——
  但矫枉过正，出现了"我承认第一张图我直接抄了""心里两个感受"
  等表演性表述，不符合作业提交的语体。
- 第 3 版（当前版本）保留第一人称与具体数字（"12 条""3 段"），
  但去除内心独白与自嘲式表达，使语体回到"认真写的作业说明"水平。

### 5 · 安全与版本控制

- 仓库当前为 **Public**。原因：本次作业需要让任课教师能够直接
  访问，Public 仓库对教师访问最友好。如有要求可改为 Private。

- `.gitignore` 中我刻意添加了 `.workbuddy/memory/` 排除项。
  该目录用于存放本地调试日志与临时命令，偶然情况下可能包含
  敏感字符串（如临时复制的 token），不应进入公开仓库。

### 6 · 本次作业未覆盖的范围

为避免汇报失真，单独列出本次未完成、暂未处理的事项：

- **未编写自动化测试**——仓库中没有 `tests/` 目录、CI 流程或
  任何自动验证脚本。Skill 中的 Quality checklist 每次都是**手动
  对照执行**的，不是程序化检查。

- **未对评分细则逐条对号入座**——上述修改均基于我对作业要求
  的理解，而非逐条对照评分表。如有偏差可在反馈中指出，我会
  按反馈调整。

- **本机命令行环境仍依赖 WorkBuddy 提供的 git/gh**——我自己的
  cmd 环境中未安装 Git for Windows，因此 `git push` 仍需通过
  WorkBuddy 完成。这次作业结束后我会自行安装 Git for Windows
  以建立独立的本地 Git 环境。

---

## 提交作业 / 修改仓库的步骤

在工作目录（`C:\Users\23543\bigdata-ai-course`）执行：

```bash
git add .                          # 暂存所有改动
git commit -m "完成第 1 次作业"     # 提交并写说明
git push                           # 推送到 GitHub
```

## 常用命令速查

| 命令 | 作用 |
|------|------|
| `git status` | 查看当前改动 |
| `git add .` | 暂存所有改动 |
| `git commit -m "说明"` | 提交改动 |
| `git push` | 推送到 GitHub |
| `git pull` | 拉取远程最新内容 |
| `git log --oneline` | 查看提交历史 |

## 作业索引

| 作业 | 内容 | 状态 |
|------|------|------|
| hw1 | 待定 | ⬜ 未开始 |
| hw2 | 待定 | ⬜ 未开始 |
