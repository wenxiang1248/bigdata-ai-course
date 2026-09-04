# bigdata-ai-course

大数据与人工智能课程作业仓库。同时也是「项目级 Skill」实验场：用 `.workbuddy/skills/` 里的可复用 Skill 沉淀工作流。

## 当前重点：概念学习资料生成

本仓库内置了一个项目级 Skill：`concept-learning-material`（位于 `.workbuddy/skills/concept-learning-material/`）。只要向 Agent 说"用 concept-learning-material 给我讲讲 X"，就会按统一骨架生成一份独立、视觉风格统一的 HTML 学习资料。

### 已生成的三份学习资料

| 文件 | 主题 | 一句话概括 |
|------|------|-----------|
| `learning-materials/agent.html` | Agent（智能体） | 一个能自己定计划、用工具、把目标做完的 AI 程序 |
| `learning-materials/llm-context.html` | 大模型的上下文（Context） | 模型在一次推理里"看到的全部输入" |
| `learning-materials/skill.html` | Skill（技能） | 一份结构化、可复用的指令包，让 Agent 表现更稳 |
| `learning-materials/concept-relationship.html` | 三个概念的关系 | Skill 装进 Context，Context 喂给 Agent |

> 直接双击 `.html` 文件在浏览器里打开即可（无需联网、无外部依赖）。

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
│   └── concept-relationship.html
├── homework/                     # 课程作业目录（每次建子目录 hw1/、hw2/...）
├── labs/                         # 实验代码
├── notes/                        # 学习笔记
├── .gitignore
└── README.md
```

## 关于 `.workbuddy/skills/`

这是 **项目级 Skill** 的标准位置：放进来的 `SKILL.md` 会被本仓库的 Agent 在每次会话中读取、按需加载。

- 想新加 Skill？在 `.workbuddy/skills/<your-skill-name>/SKILL.md` 里写一个 Markdown 文件，前两段用 frontmatter 写 `name` 与 `description`。
- 想覆盖他人共享的 Skill？同一目录名会覆盖用户级 Skill。

完整写法参考现有 `.workbuddy/skills/concept-learning-material/SKILL.md`。

## 提交作业 / 修改仓库的步骤

在工作目录（`C:\Users\23543\bigdata-ai-course`）执行：

```bash
git add .                          # 暂存所有改动
git commit -m "完成第 1 次作业"      # 提交并写说明
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
