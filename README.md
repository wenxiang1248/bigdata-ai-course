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

### 这个 Skill 的"个人学习设计"

我没把 Skill 写成一份"把段落塞进 HTML 的模板"——它带一个明确的<em>学习闭环</em>，是这个 Skill 真正有个人印记的地方，也是它和其他"提示词生成"工具最大的区别。

**7 段闭环**（每份学习资料都按这个顺序渲染，强约束）：

```
1 · 学习目标      →  读者下笔前先知道"读完能做啥"
2 · 核心问题      →  把阅读变成回答具体问题
3 · 结构化解释    →  心智模型 + 解剖 + 运作机制 + 代码一瞥（视觉锚点在 SVG）
4 · 应用案例      →  一个真实工作场景（domain / 输入 / 决策点 / 结果）
5 · 概念辨析      →  一张"近邻对比表" + 3-4 条"常见误区"
6 · 自测问题      →  4-6 题，可折叠，但答案必须在正文里
7 · 参考来源      →  4-6 条真实 URL（arxiv / 官方文档 / Wikipedia）
```

**为什么是 7 段，不是 10 段也不是 3 段**：经过反复使用，越"多段"越容易堆砌（"infrastructure"长尾、"CI/CD 集成"等凑出来的章节），越"少段"又容易堆成博客（一个解释+一段代码）。7 段是<em>"最小完备的学习闭环"</em>——少一段就缺一个学习要点（缺目标就不知道为啥读；缺自测就不知道自己有没有读懂），多一段就开始稀释注意力。Skill 的 Quality checklist 里写死了这 7 段必须按顺序全数存在，少一段就不交付。

**为什么这体现"个人"**：这 7 段不是从文献里搬来的——它是我（学设计的人）面对"想真的学会一个概念"时常走的步骤。Skill 把这种"我自己的学习套路"沉淀成可继承的工作流，下一次别人（或未来的我）说"学习 X"，得到的不只是文字段落，而是一份<em>知道自己目标、自带自测、能拿去考自己</em>的页面。

升级这个 Skill 时我会刻意保留这种"个人性"：每一条内容规则都有理由，每一段存在都有意义，不为了显得"完整"而加段落——这是这个 Skill 区别于通用生成器的部分。

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

## AI 协助后，我做的人工核查与修改

> 这部分是我对照评分细则逐项自查后做的修订；做了多少就写多少，不假装做了。

| 序号 | 评分点 | AI 做了什么 | 我后来又改了什么（人工） |
|---|---|---|---|
| 1 | Skill 应支持新概念 | 写了 `concept-learning-material` Skill；frontmatter 标注 `name` 与 `description`；触发短语里就写了 "RAG"、"Transformer" 等 | 重新核对一遍 Skill 文档，确认 `concept` 是唯一必填输入、文档通篇未引用本次三个概念的具体名称——证明它不是三个概念的一对一 prompt |
| 2 | 学习资料含「个人解释、核心机制、应用场景、误区、可核查链接」 | 生成了三份 HTML，覆盖前 4 项 | 三份都补了 **「4 · 一个具体的应用场景」**小节（agent / llm-context / skill 各举一个真实工作场景）；**「8 · 延伸阅读」**全部改为带 URL 的真实引用（ReAct 论文、Lost in the Middle、Anthropic engineering blog、OpenAI docs、Wikipedia 等） |
| 3 | 概念关系用 `.md` + 图 | 生成了 HTML 版 `concept-relationship.html` | 新增 **`concept-relationship.md`**，包含 3 张 Mermaid 图：① Context 影响 Agent 的回流图、② Skill 沉淀可复用知识的循环图、③ 端到端时序图；并在 7、9、10 三节用文字专门回答"上下文如何影响 Agent"、"Skill 如何沉淀知识"两个评分点 |
| 4 | README 写清 Skill 位置、调用方式、人工核查 | 写了基础 README | 重写 README：① 加入"如何在 WorkBuddy 中调用 Skill"分步说明（含五种触发句和验证方法）；② 加入**本节「AI 协助后的人工核查与修改」**如实列出每一项修订；③ 同步更新目录结构（含新增的 `concept-relationship.md`）|
| 5 | 不上传敏感文件 | git 已配置 | 把 `.gitignore` 强化，加入 `.env` / `*.pem` / `*.key` / `credentials.*` / `secrets.*` / `*.pfx` 等常见敏感文件规则——下一次添加 API key 之类就不会被误提交 |
| 6 | **Skill 应体现"个人学习设计"** | 前一版 Skill 是 10 段解剖式骨架 | 把 Skill <b>升级为 7 段学习闭环</b>（学习目标 / 核心问题 / 结构化解释 / 应用案例 / 概念辨析 / 自测问题 / 参考来源），并在 frontmatter、anatomy、quality checklist、failure modes 多处强约束它的存在性。同时按新骨架重写三份 HTML，每份都补上了 **学习目标**、**核心问题**、**自测问题** 三段——使每份资料能让读者在读前知道目标、在读时能对着问题读、在读后能自测 |

### 我没有做、也没假装做的事

- 我没有伪造论文 / URL / 数据。延伸阅读里每一条链接都用我**有把握的**来源（arXiv 公开论文、Anthropic 官方博客、Wikipedia 等），不能 100% 确认具体子路径的我就只放官网首页。
- 我没有把"AI 调用 Trace 的 JSON"、"调试日志"之类内部文件误上传。
- 我没有把任何`.env` / API key 之类的东西放进仓库。

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
