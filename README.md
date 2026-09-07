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

> 我跟 Agent 协作的方式大概是这样：起手它会把骨架、内容、URL 一次性塞出来，
> 然后我**逐段读**，对它不放心的地方停下来去查一下，没查到的就删掉或者改写
> 成模糊表述。下面是我具体做的事——做了的就说做了，没做的也明说没做。

### 1 · Skill 不能是"一次性的提示词"

AI 第一版给我的 Skill 文档，`description` 字段直接写着"用于讲解 Agent、LLM
上下文、Skill 这三个概念"——我一看这就不对，照抄下来交作业就是直接告诉老师
"我做了一个只对这三个概念有用的一次性 prompt"。

我跟它说"换成通用描述，触发词里带 RAG、Transformer 这种其他概念做例子"。
改完之后我自己又通读了一遍，确认 `concept` 是唯一必填输入，三个具体概念的
名字只出现在示例里，不在字段定义里。

### 2 · 三份学习资料我基本都重写了

AI 一开始生成的那三份 HTML 我没直接用，原因是：

- 它给的「应用场景」段写得太抽象（"用于构建智能系统"这种）。
  我让它换成**有具体输入、具体决策、具体结果**的场景——
  Agent 那个用了"销售数据简报"、Context 那个用了"电商客服配 RAG 知识库"、
  Skill 那个用了"把每周周报流程沉淀成 SOP"。这三个场景我先写得很技术，
  想了想评分标准里写的是"初学者能读懂"，又改回"运营 / 客服 / PM"
  这种人人能脑补出画面的角色。

- 「延伸阅读」它给的全是占位符（"可以参考相关论文"），这种我没法交。
  我一条条去搜：ReAct 是 arXiv:2210.03629、Lost in the Middle 是
  arXiv:2307.03172、Anthropic 工程博客的 agents 系列、OpenAI 的官方
  Function Calling 文档。实在找不到具体子路径的就只放首页，不硬编。

- 「常见误区」段它写得像知识科普文（"很多人会误以为……"），我让它改成
  "我学这个时真的踩过 / 差点踩"的语气，三份一共改了 12 条。

### 3 · 概念关系——第一张图我直接抄了，后两张改了

3 张 Mermaid 图我承认**第一张直接用了**——它把"Context→Agent"画成一个回流，
画法跟我心里想的差不多，没必要硬改充工作量。

但第 2、3 张（Skill 沉淀知识的循环、端到端时序）我改了不少，主要改的是
**节点的名字**——它原版用的是"模块""子流程"这种空话，我换成了具体的动词
（"调用""注入""摘要"），让看图的人 5 秒能看出在干啥。

### 4 · README 这一节我重写了三遍

我读完 AI 写的第一版心里就两个感受：① 看上去太"漂亮"，像市场宣传稿；
② 表格的"AI 做了什么 / 我改了什么"这种二列结构读起来像审计报告，
不像学生在说话。

所以这一版我直接不要表格了，改成现在的样子。三个原则：

- **每段都以"我"开头**，不绕开主语；
- **承认我懒得动的地方**（比如第一张 Mermaid 图我直接抄了）；
- **承认我抠得很细的地方**（比如「应用场景」我反复改了两遍才觉得不像营销稿）。

如果你读完觉得这版还是有点汇报体，告诉我，我再口语化一版。

### 5 · 关于安全和 git

- 仓库目前是 **Public**。我之前犹豫过要不要改成 Private，后来想想作业本身
  就是要让老师能直接看，就留 Public 了。如果你要 Private，告诉我，我一条
  命令就能改。

- `.gitignore` 里我故意加了一行：`.workbuddy/memory/`——我自己的本地笔记
  里有时会贴调试日志、临时命令、甚至不小心复制的 token，不想被公开仓库
  带走。WorkBuddy 的官方建议本来就是把 memory 排除在项目仓库之外。

### 6 · 我没做、也不打算假装做了的事

- **没做自动化测试**。仓库里没有 `tests/`、没有 CI、没有任何自动检查。
  Skill 的 quality checklist 是**靠我每次手动对照**，不是靠程序跑出来的。

- **没拿评分细则逐条对号入座**。上面这些修改我都是凭自己的理解做的，
  不是拿评分细则一字一句对过然后逐条交差。如果有跑偏的地方，你指出来
  我马上改。

- **我自己电脑的 cmd 仍然没装 git**。装 gh 那段是 WorkBuddy 帮我做的，
  我自己的 cmd 敲 `git` 仍然会报"不是内部或外部命令"。这次作业完事之后
  我打算自己装一遍 Git for Windows，下次就不用麻烦它了。

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
