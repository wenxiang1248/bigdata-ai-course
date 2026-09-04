---
name: concept-learning-material
description: Generate a structured, visually rich single-file HTML learning material for a given concept, following a personal 7-step learning design (学习目标 / 核心问题 / 结构化解释 / 应用案例 / 概念辨析 / 自测问题 / 参考来源). Use when the user wants to deeply understand, teach, or study a single concept (e.g. "Agent", "LLM context", "Skill", "RAG", "Transformer", "Mermaid", "向量检索"). Triggers include "生成学习资料", "做一个学习页面", "教学页面", "讲解 X 这个概念", "concept learning material", "自学 X".
---

# Concept Learning Material Generator

A reusable personal-learning workflow. Hand it **one concept name** and it returns **one self-contained HTML page** that follows a deliberate 7-step learning loop, not a one-off explanation.

The page is built so the learner (or the author's future self) can:

- **know what they will learn** before reading
- **frame the right questions** to interrogate the concept
- **get a structured walk-through** anchored by a mental-model diagram
- **see it work in one real scenario**
- **tell it apart from neighbours** and avoid common mistakes
- **test themselves** with self-check questions whose answers live on the page
- **follow real sources** to go deeper later

## When to use

Trigger this skill when the user asks any of:

- "Make a learning page for X" / "做一个 X 的学习资料"
- "Teach me X" / "讲解 X" / "用一节课讲清楚 X"
- "I want to self-study X" / "我想自学 X"
- "Generate concept learning material for X"

Do NOT trigger for: project setup, code refactors, multi-concept comparisons (use a comparison skill), or anything that needs a running app.

## Inputs

| Field         | Required | Notes                                                                |
|---------------|----------|----------------------------------------------------------------------|
| `concept`     | yes      | The single concept to teach. Concrete and unambiguous.              |
| `context`     | no       | 1–3 sentences: who is the learner, what is the goal.                 |
| `style_hint`  | no       | e.g. "first-year CS student", "with AI analogies", "in 10 minutes".  |
| `output_path` | usually  | Default: `learning-materials/<slug>.html` in the project root.       |

If `context` is missing, default to: **a curious CS undergrad who has used ChatGPT but doesn't yet know how the sausage is made.** Write at that level.

## The learning design (why 7 segments, in this order)

A learning page is not a blog post. It should mirror how a thoughtful student actually studies a concept. The page follows a fixed 7-step loop so the learner always knows where they are and what to do next:

```
学习目标 (Goals)
   │  "what will I be able to do after this"
   ▼
核心问题 (Driving questions)
   │  "what are the questions that, if answered, mean I get it"
   ▼
结构化解释 (Structured explanation)
   │  the meat: mental model, anatomy, how it works, code glimpse
   ▼
应用案例 (Applied scenario)
   │  one concrete scene where the concept earns its keep
   ▼
概念辨析 (Disambiguation)
   │  "what it is vs what it isn't", plus a misconceptions list
   ▼
自测问题 (Self-check)
   │  questions the page itself answers, with collapsible answers
   ▼
参考来源 (Sources)
      real, verifiable URLs to keep going
```

This is **deliberately** not the maximalist 10-section anatomy of a marketing-grade article. It is the minimum coherent set. If a segment would be empty or padding, it is better to say so ("see Q3 — no dedicated scenario is needed because …") than to fill it with fluff.

### Reasons behind each segment

- **学习目标** forces the author to commit to verbs ("能说出 / 能辨别 / 能用 / 能避开误区"). Without it, the page drifts into storytelling.
- **核心问题** turns reading into answering. The 3–5 questions become the reader's private table of contents.
- **结构化解释** is the only segment that allows SVG diagrams and code. Everything else is prose.
- **应用案例** is required: a concept without one stays abstract.
- **概念辨析** prevents the most common failure mode — confusing this concept with its neighbours (e.g. Agent vs Workflow vs RAG).
- **自测问题** with collapsible answers turns passive reading into retrieval practice.
- **参考来源** with real URLs gives the reader an off-ramp if they want to go further.

## Output contract (hard constraints)

The output is a single HTML file that opens correctly in any modern browser with no external dependencies.

1. **Self-contained**: no `<script src>` to CDN, no `<link rel="stylesheet">` to remote. All CSS inline in `<style>`.
2. **Inline SVG only** for diagrams. No external images.
3. **Light theme by default** (IDE Theme: light), dark text on light backgrounds.
4. **Chinese-language primary** text. English technical terms in parentheses on first use.
5. **Viewport**: written for ~960px max-width centered reading column; readable on mobile.
6. **No JavaScript required** to view the content. Optional, very light JS is OK (e.g. copy buttons, tabs).
7. **Filename**: lowercase kebab-case of the concept in English. Examples: `agent.html`, `llm-context.html`, `skill.html`, `transformer.html`.

## Document anatomy — 7 segments in order

Every page must contain exactly these seven sections in this order. Some may be short; none may be missing.

### 1 · 学习目标 (Goals) — 3–5 bullets
Verbs in the head: "能 **说出** …"、"能 **辨别** …"、"能 **动手** 写出最小示例"、"能 **避开** 常见误区". Each goal is one short line.

### 2 · 核心问题 (Driving questions) — 3–5 questions
Questions that, if you can answer them, mean you understand the concept. These double as the reader's mental checklist.

### 3 · 结构化解释 (Structured explanation)
The meat of the page. May contain, in this order:
- one anchor **mental-model diagram** (inline SVG) answering "what is it, really?"
- **anatomy** breakdown (labeled SVG or styled boxes) — the moving parts
- **how it works** — 3–6 numbered steps with a small sequence SVG
- *optional* **code-level glimpse** — minimal, commented snippet (10–30 lines), only if it adds value
For meta-concepts (e.g. "Skill", "Agent", "Context"), add a small **"为什么这件事重要"** mini-section.

### 4 · 应用案例 (Applied scenario)
**One** concrete scene: "假设你是 X，你要 Y，你会怎样用这个概念一步步解决它?" Mention a real domain (e-commerce, school grading, travel planning, knowledge base, etc.). Include the specific input, decision points, and outcome.

### 5 · 概念辨析 (Disambiguation)
- A short comparison table with **one near-neighbour** (e.g. Agent vs Workflow; Skill vs Prompt; Context vs Token).
- A **常见误区** list of 3–4 misconceptions with one-line corrections.

### 6 · 自测问题 (Self-check) — 4–6 questions
Each question is a `<details><summary>` block. The summary is the question; the body is the answer. Every question must be **answered by content above it**. Never add a question whose answer isn't on the page.

### 7 · 参考来源 (Sources) — 4–6 URLs
Only well-known sources: Wikipedia, official docs (Anthropic, OpenAI, GitHub, Hugging Face), arXiv papers with verifiable titles, university course pages. **No invented URLs.** Use real anchors (`<a href="…">`).

## Content rules

- **No hallucinated facts.** Numbers, years, papers, products must be verifiable. Hedge when unsure ("约 2023 年前后", "业界普遍认为…").
- **Define jargon on first use** in one short clause: "Embedding（把文本映射到一个向量空间的表示）".
- **At least one concrete analogy** for every abstract concept. Repertoire: kitchen, orchestra, library, factory line, postal system, restaurant, exam.
- **No marketing tone.** No "颠覆性", "赋能", "革命性".
- **Length**: 1,800–3,500 Chinese characters of body text. The page is meant to be read in 8–12 minutes.
- **Pick one anchor mental model.** Don't show three competing diagrams. If the concept has multiple valid framings, choose the one you can defend in one sentence.

## Visual / design system

Use the following tokens. Inline as CSS variables in `<style>`.

```css
:root {
  --bg: #fafaf7;           /* warm off-white page background */
  --surface: #ffffff;      /* card surface */
  --ink: #1f2328;          /* primary text */
  --ink-2: #57606a;        /* secondary text */
  --muted: #8b949e;        /* tertiary, captions */
  --line: #e6e8eb;         /* dividers */
  --accent: #b14e2b;       /* rust / brick — primary accent */
  --accent-2: #2f6f5e;     /* deep green for secondary */
  --accent-3: #3b4d80;     /* navy for tertiary */
  --code-bg: #f6f4ee;      /* warm code block background */
  --shadow: 0 1px 2px rgba(20,25,30,0.04), 0 8px 24px rgba(20,25,30,0.06);
  --radius: 14px;
  --maxw: 960px;
}
* { box-sizing: border-box; }
html, body { background: var(--bg); color: var(--ink); }
body { margin: 0; font-family: -apple-system, BlinkMacSystemFont, "Segoe UI",
       "PingFang SC", "Microsoft YaHei", "Helvetica Neue", Arial, sans-serif;
       font-size: 16px; line-height: 1.75; }
.wrap { max-width: var(--maxw); margin: 0 auto; padding: 56px 28px 96px; }
```

**Component patterns:**

- **Segment section header**: H2 with a small ordinal badge, e.g. `1 · 学习目标`. Use a uniform `letter-spacing: .04em` for the number.
- **At-a-glance card row** (optional, in hero): CSS grid `repeat(auto-fit, minmax(150px, 1fr))`, each card uses `--surface`, border 1px solid `--line`, radius `--radius`, small label + value.
- **Diagram block**: `<figure>` with an inline `<svg viewBox="0 0 680 360">` and a `<figcaption>`. Always self-contained.
- **Comparison table**: 2-column or 3-column table, header row with `--accent` tint, semantic `<table>`.
- **Code block**: `<pre><code>` with `--code-bg` background, 13.5px font, no external highlighter (escape `<` and `&`).
- **Self-check**: `<details><summary>` so answers are collapsible by default, still accessible without JS.

## Workflow (do this every invocation)

1. **Disambiguate the concept.** If a name could mean several things (e.g. "context"), pick one and *say so* in the goals segment.
2. **Write the 3–5 学习目标 first.** If you cannot write them, the concept is too fuzzy — ask the user or pick a narrower concept.
3. **Write the 3–5 核心问题 next.** These drive the structure of segment 3.
4. **Sketch the mental-model SVG** before writing prose. The diagram commits you to a single framing.
5. **Write segments 3 → 4 → 5 → 6 in order.** Keep self-check answers short (1–3 sentences each).
6. **Fill 参考来源 with real URLs only.** If a URL would be invented, replace it with a publication or official doc title.
7. **Self-check pass**: open the HTML mentally, walk through each 自测问题, verify it is answered by content above.
8. **Save** to `learning-materials/<slug>.html`. Create the directory if missing.
9. **Verify** by re-reading the file: no `<?` artifacts, no half-substituted placeholders, no broken `<style>` blocks.

## Quality checklist before declaring done

Tick every item. If any item fails, fix before presenting.

- [ ] Page opens in a fresh browser tab with no console errors, no external requests.
- [ ] H1 is the concept name, with a one-sentence tagline.
- [ ] **Exactly 7 segments**, in order: 学习目标 / 核心问题 / 结构化解释 / 应用案例 / 概念辨析 / 自测问题 / 参考来源.
- [ ] At least one inline SVG diagram, fully self-contained, anchored in the 结构化解释 segment.
- [ ] 应用案例 mentions a specific domain, input, decision point, and outcome.
- [ ] All 自测问题 have answers visible on the page above them.
- [ ] 参考来源 has 4–6 real, clickable URLs — no invented links.
- [ ] Chinese primary text, English technical terms in parentheses on first use.
- [ ] Body text 1,800–3,500 Chinese characters.
- [ ] Filename is kebab-case English; matches the concept slug.
- [ ] No leftover `{{template}}` placeholders, no LLM fingerprint phrases ("当然可以！", "希望对您有帮助").

## Style block — copy-pasteable starter

Every generated page should start its `<style>` with this base. Extend as needed but don't replace:

```html
<style>
  :root {
    --bg: #fafaf7; --surface: #ffffff; --ink: #1f2328; --ink-2: #57606a;
    --muted: #8b949e; --line: #e6e8eb;
    --accent: #b14e2b; --accent-2: #2f6f5e; --accent-3: #3b4d80;
    --code-bg: #f6f4ee;
    --shadow: 0 1px 2px rgba(20,25,30,.04), 0 8px 24px rgba(20,25,30,.06);
    --radius: 14px; --maxw: 960px;
  }
  * { box-sizing: border-box; }
  html, body { background: var(--bg); color: var(--ink); margin: 0; }
  body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI",
    "PingFang SC", "Microsoft YaHei", "Helvetica Neue", Arial, sans-serif;
    font-size: 16px; line-height: 1.75; }
  .wrap { max-width: var(--maxw); margin: 0 auto; padding: 56px 28px 96px; }
  h1 { font-size: 40px; letter-spacing: -0.5px; margin: 0 0 8px; }
  h2 { font-size: 22px; margin: 48px 0 14px; padding-bottom: 8px;
       border-bottom: 1px solid var(--line); }
  h2 .num { color: var(--muted); font-weight: 500; margin-right: 10px;
            letter-spacing: .04em; }
  h3 { font-size: 18px; margin: 24px 0 8px; color: var(--accent); }
  p { margin: 12px 0; }
  .tagline { color: var(--ink-2); font-size: 17px; margin: 0 0 28px; }
  .glance { display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 12px; margin: 24px 0 36px; }
  .glance .card { background: var(--surface); border: 1px solid var(--line);
                  border-radius: var(--radius); padding: 14px 16px; box-shadow: var(--shadow); }
  .glance .card .k { color: var(--muted); font-size: 12px; margin-bottom: 4px;
                     letter-spacing: .04em; }
  .glance .card .v { color: var(--ink); font-size: 15px; line-height: 1.5; }
  figure { margin: 24px 0; background: var(--surface); border: 1px solid var(--line);
           border-radius: var(--radius); padding: 18px; box-shadow: var(--shadow); }
  figcaption { color: var(--muted); font-size: 13px; margin-top: 10px;
               text-align: center; }
  table { width: 100%; border-collapse: collapse; margin: 18px 0; background: var(--surface);
          border-radius: var(--radius); overflow: hidden; box-shadow: var(--shadow); }
  th, td { padding: 12px 14px; text-align: left; border-bottom: 1px solid var(--line); }
  th { background: #f1ede4; color: var(--ink); font-weight: 600; }
  tr:last-child td { border-bottom: 0; }
  pre { background: var(--code-bg); border: 1px solid var(--line); border-radius: 12px;
        padding: 16px; overflow-x: auto; font-size: 13.5px; line-height: 1.6; }
  code { font-family: "JetBrains Mono", Consolas, ui-monospace, monospace; }
  details { background: var(--surface); border: 1px solid var(--line);
            border-radius: var(--radius); padding: 14px 18px; margin: 12px 0;
            box-shadow: var(--shadow); }
  summary { cursor: pointer; font-weight: 600; color: var(--ink); }
  ul, ol { padding-left: 22px; }
  li { margin: 6px 0; }
  .footer { color: var(--muted); font-size: 12px; margin-top: 64px;
            border-top: 1px solid var(--line); padding-top: 18px;
            text-align: center; }
</style>
```

## Examples of good invocations

- "用 concept-learning-material 给我自学 RAG，输出到 learning-materials/rag.html"
- "用 concept-learning-material 解释一下 Transformer，给有 ML 基础但没用过大模型框架的同学看"
- "用 concept-learning-material 讲清楚 Skill 是什么，目标是 WorkBuddy 用户"
- "用 concept-learning-material 学习一下 Mermaid 语法，半小时内能上手"

## Failure modes to watch for

- **Going past 3,500 Chinese characters** — prune, don't pad. Trim SVG before prose.
- **Diagrams that aren't actually diagrams** — a styled `<div>` is not a diagram. If you draw it with SVG, encode the relationships with real shapes, lines, arrows.
- **Inventing sources** — only link to things you can name without thinking (Wikipedia, GitHub docs, official blogs, papers with known titles).
- **Drifting into a tutorial** — this is a *learning page*, not a how-to. Only segment 3 may host a small code glimpse.
- **Skipping 学习目标** to jump straight into explanation — almost always a sign the author hasn't decided what the page is for.
- **Self-check questions whose answers aren't on the page** — a cheap signal that the page is unstructured.
