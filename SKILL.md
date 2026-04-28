---
name: econ-slides-review
description: "Use when the user wants to summarize, review, or extract key points from economics lecture slides or course materials into Obsidian-compatible Markdown study notes. Triggers: 总结课件, 复习资料, 考点总结, cheat sheet, 公式速查, summarize slides, review notes, lecture summary, or any request to turn economics course materials into structured revision notes. This skill is folder-aware: it scans the course directory for lectures, problem sets, solutions, seminars, past exams, and syllabus before starting. Do NOT use for: homework solving, essay writing, non-economics slides, or .pptx files not yet exported to PDF."
---

# Econ Slides Review

Turn an economics course folder into concise, exam-oriented Obsidian Markdown study notes that integrate lecture content with problem patterns, grounded in economic intuition, with accurate page references and bilingual terminology (中文 + English).

**Core principle — intuition first:** the goal of these notes is not to compress slides into fewer words. It is to build and reinforce economic intuition. Every definition, formula, and model summary must answer: *why does this result hold? what is the economic logic?* If a summary cannot explain the intuition, it has failed, no matter how complete the coverage is.

**Second principle — integrate, don't isolate:** lecture slides alone are half the picture. Problem sets reveal what the lecturer thinks is important; solutions reveal how to structure answers; past exams reveal the actual test format. A good review note weaves all of these together.

## Non-Negotiables

* **REQUIRED COMPANION SKILL:** use `pdf` (or `pdf-reading`) for PDF intake and reading.
* **NO OTHER SKILLS:** when this skill applies, use only `econ-slides-review` plus the PDF companion.
* **SYLLABUS FIRST:** if a syllabus or outline exists, read it before any lecture content. If none is found, infer topic structure from lecture titles and headings instead.
* **FOLDER SCAN FIRST:** before summarising, scan the course directory to discover all available materials. Use whatever is found — a flat folder with only lecture PDFs is fine; but do not ignore problem sets, solutions, or past exams when they exist alongside the lectures.
* Default deliverable is a `.md` file written to disk, not a chat-only summary.
* Default writing style is Chinese-first, with all important economics terms preserving the English original in parentheses.
* Each summarised point must carry a page reference in the format `【课件页 XX-XX】`. When a matching pset or exam question exists, append it: `【课件页 XX-XX｜推荐练习：PS2 Q3】`.
* Output is a single `<stem>_review.md` file placed in the course directory. No subfolder.

## Course Folder Awareness

Course folders vary widely — some users organise materials into neat subfolders, others dump everything into one directory. This skill must handle both extremes and everything in between.

### Step 0. Folder Scan

Run a directory listing of the course folder (recursively, up to 2 levels deep). Classify every PDF found into one of these resource categories by matching against filenames, subfolder names, or content clues:

| Category | Typical names / patterns | Required? |
|---|---|---|
| **Syllabus / Outline** | `syllabus`, `outline`, `course_outline`, `module_guide` | No — infer structure from lectures if absent |
| **Lecture slides** | `lecture_notes`, `lecture`, `lectures`, `slides`, `课件`, `lec`, `Lec*.pdf`, `week*.pdf`, `topic*.pdf` | **Yes — minimum viable input** |
| **Problem sets** | `problem_set`, `pset`, `ps`, `PS`, `homework`, `hw`, `exercises` | No |
| **Seminar materials** | `seminar`, `tutorial`, `习题课`, `section` — often handwritten PDFs | No |
| **Solutions** | `solution`, `solutions`, `sol`, `answers`, `ans`, `mark_scheme` | No |
| **Past exams** | `past_exam`, `past_paper`, `exam`, `final`, `midterm`, `mock` | No |
| **Reading lists / references** | `reading`, `references`, `bibliography` | No — context only |

**Handling different folder structures:**

* **Organised subfolders** (e.g. `lecture/`, `pset/`, `solution/`): classify by subfolder name, then refine by filename.
* **Flat folder** (all PDFs at root level): classify purely by filename patterns. A file named `PS2.pdf` is a problem set; `Lec3.pdf` is a lecture; `exam_2023.pdf` is a past exam.
* **Ambiguous files**: if a file cannot be confidently classified, list it as `unclassified` in the scan report. Do not guess — the user can clarify.
* **Single PDF input**: if the user points to one specific PDF rather than a folder, treat it as the lecture source and skip folder scanning. Produce a lecture-only review.

Report what was found before proceeding. Adapt the report to what actually exists:

```
Found in EC487/:
  ✓ Syllabus: syllabus.pdf
  ✓ Lectures: lecture_notes/ (8 PDFs)
  ✓ Problem Sets: pset/ (4 PDFs)
  ✓ Solutions: solutions/ (4 PDFs)
  ✓ Past Exams: past_exam/ (3 PDFs)
  ✗ Seminar: not found
  ? Unclassified: notes_misc.pdf
```

Or for a minimal flat folder:

```
Found in ECON101/:
  ✓ Lectures: Lec1.pdf, Lec2.pdf, ... Lec10.pdf (10 PDFs)
  ✗ Syllabus: not found — will infer topic structure from lecture titles
  ✗ Problem Sets: not found
  ✗ Solutions: not found
  ✗ Past Exams: not found
```

**Only lectures are required.** Everything else enriches the output but is not mandatory. The skill degrades gracefully:

| Available materials | Output quality |
|---|---|
| Lectures only | Concept + formula summary with intuition. No problem patterns or exam analysis. |
| Lectures + syllabus | Above, plus syllabus-ordered structure and exam format info. |
| Lectures + problem sets | Above, plus "how it's tested" per topic. |
| Lectures + psets + solutions | Above, plus "how to answer" techniques. |
| Lectures + psets + solutions + past exams | Full integrated review with exam pattern analysis. |
| All of the above + seminar | Maximum quality: includes additional intuition and common mistakes from seminars. |

If lectures are missing entirely, stop and ask the user to clarify which files contain the lecture content.

### How Each Resource Type Is Used

**Syllabus / Outline** — read before anything else *if available*. Extract:
* topic sequence and lecture-to-topic mapping
* which topics the lecturer flags as important or examinable
* assessment structure (exam format, weighting, open-book or not)
* recommended readings per topic (note them, but do not summarise the readings)

If a syllabus exists, it becomes the structural backbone of the output — organise the final notes according to the syllabus topic order, not the raw PDF page order. If no syllabus exists, infer the topic structure from lecture titles, headings, and content transitions.

**Lecture slides** — the primary content source. Extract definitions, models, formulas, proofs, and examples as described in the Content Guidance section below.

**Problem sets** — scan all available problem sets. For each topic/lecture block, identify:
* which concepts the problems test
* which problem types recur (optimisation, comparative statics, prove-this-property, compute-equilibrium, etc.)
* the difficulty progression across problem sets

Do NOT solve the problems. Instead, record the *problem pattern* — what setup is given, what is asked, and what technique is needed.

**Solutions** — if available, cross-reference with problem sets to extract:
* the expected solution structure and level of rigour
* key steps that the solution emphasises (these are likely marking criteria)
* common techniques or shortcuts the model answers use

**Seminar materials** — often handwritten, may need OCR. These typically walk through problem set solutions in class. Extract:
* any additional intuition or explanation not in the lecture slides
* the seminar leader's commentary on why certain steps matter
* common student mistakes that were addressed

**Past exams** — the most valuable predictive resource. Extract:
* exam format (number of questions, choice, time, marks per part)
* topic coverage patterns across years (which topics always appear?)
* question types and difficulty level
* how questions map to lecture topics and problem set types

### Integrating Resources into the Output

When multiple resource types are available, the final output is NOT separate summaries of each resource. It is a single integrated review document where, for each topic:

1. The **concept summary** comes from lectures (with intuition) — always present
2. The **"how it's tested"** comes from problem sets and past exams — if available
3. The **"how to answer"** comes from solutions and seminars — if available
4. The **exam pattern** comes from past exam analysis — if available

When only lectures are available, the output focuses on concepts, formulas, models, and intuition. This is still a valid and useful output — just without the exam-strategy layer.

When additional resources exist, integration is the core value of this skill. Producing a lecture-only summary while ignoring available psets/exams is a failure mode.

## Economic Intuition: The Central Requirement

This is not a nice-to-have. Economic intuition is the organising principle of the entire output.

### What "Economic Intuition" Means in Practice

For every result, model, or formula, the notes must answer at least one of:

* **Why does this hold?** — the economic logic, not the mathematical proof. Example: "价格歧视 (Price Discrimination) 利润更高，因为垄断者能从高支付意愿的消费者那里榨取更多剩余 (extract more surplus)，而不需要降低对所有人的价格。"
* **What would change if an assumption were relaxed?** — builds understanding of the mechanism. Example: "如果去掉 SUTVA，一个人的 treatment 会影响另一个人的 outcome，ATE 的定义就不再清晰。"
* **When does this matter in the real world?** — connects theory to application. Example: "逆向选择 (Adverse Selection) 解释了为什么二手车市场价格偏低——买家担心 lemons。"
* **What is the trade-off?** — economics is fundamentally about trade-offs. Example: "偏差-方差权衡 (Bias-Variance Trade-off): IV 消除了内生性偏差，但因为只用了部分变异 (variation)，方差更大。"

### How to Structure Intuition in the Output

After every formal result (definition, theorem, formula), include an intuition block:

```markdown
> [!intuition] 经济学直觉
> [1-3 sentences explaining WHY this result holds in plain economic reasoning]
```

This is a **mandatory** element, not optional polish. If you cannot articulate the intuition for a result, flag it as `> [!warning] 直觉待补充` rather than silently omitting it.

### Intuition Quality Checklist

Good intuition:
* Uses economic language (incentives, trade-offs, surplus, efficiency, externality)
* Explains the mechanism, not just restates the math in words
* Is short — 1-3 sentences, not a paragraph

Bad intuition:
* "由公式可得" / "from the formula we can see" — this is not intuition
* Restating the mathematical result in Chinese without explaining why
* "这很重要因为考试会考" — this is exam advice, not intuition
* Overly long storytelling that buries the point

## Output Format: Obsidian-Compatible Markdown

### YAML Frontmatter

```yaml
---
title: "<course-code> Review"
date: <YYYY-MM-DD>
course: "<course code and name>"
tags:
  - review
  - <course-tag>
---
```

Include `syllabus_topics` and `exam_format` fields only if a syllabus was found:

```yaml
syllabus_topics:
  - "<Topic 1>"
  - "<Topic 2>"
exam_format: "<e.g. 3hr, answer 3 of 5, closed-book>"
```

### Math Notation

* Inline math: `$...$` — e.g. `$\beta_1$`, `$E[Y|X]$`
* Display math: `$$...$$` on its own line
* Use standard LaTeX math commands; Obsidian's MathJax handles them
* For matrices and aligned equations: `\begin{aligned}...\end{aligned}` inside `$$...$$`
* For piecewise functions: `\begin{cases}...\end{cases}`

### Document Structure

The output should follow this hierarchy:

```
# <Course Code> 复习笔记

## Exam Information  ← from syllabus + past exams
## Topic 1: <name>   ← from syllabus ordering
### Key Concepts
### Models
### Formulas
### Problem Patterns  ← from problem sets + past exams
### 易错点与解题技巧    ← from solutions + seminars
## Topic 2: <name>
...
## Past Exam Analysis  ← cross-year patterns
## Quick Reference     ← formula/definition cheat sheet
```

### Callout Types

Use these Obsidian callouts consistently:

* `> [!definition]` — formal definitions (exact mathematical content, never paraphrased)
* `> [!formula]` — key formulas with conditions for validity
* `> [!intuition]` — economic intuition (**MANDATORY** after every formal result)
* `> [!example]` — representative problem patterns from psets/exams
* `> [!technique]` — problem-solving methods and answer structures
* `> [!warning]` — common mistakes, 易错点, tricky edge cases
* `> [!exam]` — past exam observations and predictions
* `> [!figure]` — textual description of important diagrams

### Source References and Problem Recommendations

Every knowledge point must carry two kinds of annotation at the end of the line:

**1. Page reference (mandatory):** trace the point back to its source slide.

Format: `【课件页 XX-XX】` at the end of each bullet or after each formula/definition. This is non-negotiable — every summarised point needs a page locator so the reader can flip back to the original slide instantly.

* Single page: `【课件页 16】`
* Page range: `【课件页 12-18】`
* Multiple lectures: `【Lec 3 课件页 12-18】`
* Non-lecture source: `【PS2 Q3】`, `【Exam 2023 Q1b】`

**2. Problem recommendation (when available):** if a problem set question, past exam question, or seminar exercise tests this specific concept, append it after the page reference.

Format: `【课件页 XX-XX｜推荐练习：PS2 Q3, Exam 2023 Q1b】`

The `｜推荐练习：` delimiter separates the source reference from related practice problems. This tells the reader: "after reviewing this concept, go practice these."

**Example of a fully annotated knowledge point:**

```markdown
- 联合概率质量函数 (joint pmf)：$p_{X,Y}(j,k) = P(X=j, Y=k)$，
  包含离散随机向量的全部信息。【课件页 16｜推荐练习：PS3 Q1, Exam 2022 Q2a】
```

**Example of a definition callout with annotation:**

```markdown
> [!definition] 边缘 pmf (Marginal pmf)
> $p_X(j) = \sum_k p_{X,Y}(j,k)$
> 表格题通常是"沿列求 $p_X$，沿行求 $p_Y$"。
> 【课件页 20-25｜推荐练习：PS3 Q2】

> [!intuition] 经济学直觉
> 边缘分布是"忽略另一个变量"后的分布——
> 对所有可能的 $k$ 求和，就是把 $Y$ 的信息积掉。
```

**Example of a formula with technique and annotation:**

```markdown
> [!formula] 矩形区域概率公式
> $$P(x_1 < X \le x_2,\; y_1 < Y \le y_2) = F(x_2,y_2) - F(x_2,y_1) - F(x_1,y_2) + F(x_1,y_1)$$
> 【课件页 39-42｜推荐练习：PS3 Q4, Exam 2023 Q3a】

> [!technique] 解题技巧
> 连续题先画支撑区域 (support region)，再写积分上下限；
> 别一上来就列积分。【课件页 51-56】
```

**Rules:**

* Page references go on **every** bullet point, definition, formula, and technique — not just at the section level.
* Problem recommendations go only where a matching pset/exam question was actually found. Do not fabricate recommendations.
* If no matching problem exists for a concept, just use the page reference alone: `【课件页 16】`
* If a concept is tested in multiple places, list all of them: `【课件页 16｜推荐练习：PS2 Q1, PS4 Q3, Exam 2022 Q2, Exam 2023 Q1a】`
* Keep the annotation at the end of the content block, not on a separate line — it should feel like a natural suffix, not a separate element.

### Formatting Rules

* `#` for major topic divisions (from syllabus), `##` for sub-topics, `###` for concepts
* Bilingual terms inline: `边际替代率 (MRS)`, `无差异曲线 (Indifference Curve)`
* Short bullets, not large explanatory paragraphs — except for intuition blocks which can be 1-3 sentences
* Do NOT use Obsidian wikilinks (`[[...]]`) — keep the file self-contained
* No HTML tags, no embedded images
* No nested bullets deeper than 3 levels

## Economics Content Guidance

### Models and Theoretical Frameworks

When summarising an economic model:

1. **Setup**: agents, choice variables, constraints, objective functions
2. **Solution concept**: Nash, Walrasian, competitive, Bayesian, etc.
3. **Key result**: the main proposition or comparative statics conclusion
4. **Intuition** (mandatory): why does this result hold economically?
5. **How it's tested**: what do problem sets / past exams ask about this model?

Do not just copy the final equation. The setup-to-result-to-intuition chain is what exams test.

### Proofs and Derivations

* Summarise the proof strategy (contradiction, FOC+SOC, envelope theorem, etc.)
* Preserve key intermediate results that exams might ask to reproduce
* Note specific tricks ("add and subtract $E[X]$", "take logs", "apply Itô's lemma")
* For long derivations: starting point → key transformation → result
* Always add: why does this proof work? What is the economic content of each step?

### Econometrics

* State the **estimator**, its **assumptions**, and its **properties**
* Write out: population model → sample analogue → what each coefficient identifies
* Distinguish: population parameter vs. estimator vs. estimate
* Hypothesis testing: null → test statistic → distribution under $H_0$ → decision rule
* Preserve exact variance formulas and SE corrections
* **Intuition**: what source of variation identifies the parameter? Why might the assumption fail?

### Game Theory and Mechanism Design

* State the game form: players, strategy spaces, payoffs, timing, information
* Equilibrium: state the concept and the equilibrium strategy profile explicitly
* Mechanism design: social choice function, mechanism, properties (IC, IR, efficiency)
* Payoff matrices: use Markdown tables with clear labels
* **Intuition**: what are the strategic incentives? Why does this equilibrium survive?

### Diagrams

For concepts needing figures, describe textually:
* Axes labels and what they represent
* Key curves/lines and what shifts them
* Equilibrium point(s) and their properties
* Comparative statics: direction and magnitude of shifts

Use `> [!figure]` callout blocks for these descriptions.

## Workflow

### Step 0. Folder Scan (MANDATORY)

Scan the course directory. Report findings. Identify all available resource categories.

### Step 1. Read Syllabus (if available)

If a syllabus/outline was found in Step 0, read it first. Extract:
* Topic sequence
* Lecture-to-topic mapping
* Assessment structure and exam format
* Important topics flagged by the lecturer

This determines the structure of the final output. If no syllabus exists, skip to Step 2 and infer structure from the lectures themselves.

### Step 2. Read Lectures Globally

Do not jump into chunk summaries. Read enough to understand macro-structure:
* Identify lecture boundaries, topic transitions, summary slides
* Build a segmentation map aligned to the syllabus topic structure
* For long decks (100+ pages): segmentation is mandatory

### Step 3. Scan Problem Sets and Past Exams (if available)

If problem sets or past exams were found in Step 0, skim them before deep-reading lectures to build a **concept → question map**. For each question, record:
* which concept/topic it tests
* the question identifier (e.g. `PS2 Q3`, `Exam 2023 Q1b`)
* the question type (compute, prove, explain, compare, etc.)

This map is used in Step 4 to attach `｜推荐练习：` tags to each knowledge point. If no psets or exams were found, skip to Step 4.

### Step 4. Per-Segment Deep Reading

For each topic segment, read the corresponding:
* Lecture pages
* Problem set questions on that topic
* Solutions for those questions (if available)
* Seminar materials for that topic (if available)

Extract per segment:
* Definitions (formal + intuitive) — **record the exact slide page(s)**
* Models (setup → solution → result → intuition) — **record page range**
* Formulas with conditions — **record page(s)**
* Key propositions with proof strategies
* Problem patterns from psets and exams
* Solution techniques from solutions and seminars
* Common mistakes and 易错点

**Critical:** while extracting each point, immediately attach the `【课件页 XX-XX】` reference and look up the concept→question map from Step 3 to attach `｜推荐练习：` where matches exist. Do not defer this to later — page mappings are lost if not recorded during reading.

### Step 5. Merge into Integrated Review

Merge all segment notes into one document following the syllabus topic order.

For each topic block, include:
* 核心概念 (Key Concepts) — definitions and models with intuition
* 公式 (Formulas) — with conditions and intuitive explanations
* 题型分析 (Problem Patterns) — from psets and past exams
* 解题技巧 (Techniques) — from solutions and seminars
* 易错点 (Common Mistakes) — from seminars and personal analysis

### Step 6. Past Exam Analysis Section (if past exams available)

If past exams were found, add a dedicated section at the end analyzing cross-year patterns:
* Which topics always appear?
* What question formats recur?
* How does difficulty distribute?
* Any observable trends across years?

If no past exams were found, skip this section.

### Step 7. Quick Reference Section

Add a final cheat-sheet section: all key formulas and definitions in compact form, organised by topic, for last-minute review.

### Step 8. Verifier Pass

Check the merged draft:
* All syllabus topics are covered (or all lecture topics, if no syllabus)
* No lecture block was silently dropped
* Formulas present for formula-heavy sections
* **Every formal result has an intuition block** (the central requirement)
* **Every knowledge point has a `【课件页 XX-XX】` reference** — no orphan points without page locators
* **Problem recommendations `｜推荐练习：` are attached** wherever matching pset/exam questions exist — cross-check against the topic→question map built in Step 3
* Problem patterns from psets/exams are integrated where those resources exist
* English terms in parentheses throughout
* Math notation is correct and Obsidian-renderable

If verification finds gaps: fix and re-verify.

### Step 9. Write the Markdown File

* Write the final `.md` file to `<stem>_review.md` in the course directory (see Output Naming)
* Confirm the file exists on disk
* Do not claim completion before the file is written

## Required Outcome

Default successful outcome:
* A folder scan report (what materials were found and classified)
* A saved `<stem>_review.md` file integrating all available resources
* A final response reporting the artifact path

NOT successful completions:
* Chat-only summary
* Lecture-only summary when psets/exams/solutions exist in the same folder and were not integrated
* Summary without economic intuition blocks
* Draft never written to disk
* Stopping at segmentation without merging

## Output Naming

Output is a single `.md` file placed directly in the course directory — no subfolder.

**Naming convention:** `<stem>_review.md`

The stem is determined by this priority:

1. **Course code** if identifiable from the folder name or syllabus → `EC487_review.md`
2. **Folder name** if the course code is not clear → `microeconomics_review.md`
3. **Source PDF name** if working from a single file → `Lecture_Notes_review.md`
4. **Fallback** → `econ_review.md`

Examples:
* Folder is `EC487/` → `EC487_review.md`
* Folder is `Advanced Micro/` → `Advanced_Micro_review.md`
* Single file `labor_econ_slides.pdf` → `labor_econ_slides_review.md`

If the user specifies a custom filename, use that instead.

## Common Failure Modes

* **Not scanning the folder** — jumping straight into one PDF without checking what else is available
* **Skipping the syllabus** — producing notes in PDF page order when a syllabus exists that defines topic order
* **Missing intuition** — every formal result without a `> [!intuition]` block is a failure
* **Isolating resources** — producing separate lecture summary + separate pset summary instead of integrating them per topic
* One-pass summary of a long deck without segmentation
* Losing page/source mapping during chunking
* **Missing page references** — knowledge points without `【课件页 XX-XX】` are untraceable and useless for revision
* **Missing problem recommendations** — if a pset or past exam question tests a concept, the `｜推荐练习：` link must be there; the reader should never have to hunt for related exercises themselves
* Generic prose instead of structured exam points
* Chat-only reply when file output was not waived
* Omitting math notation — writing "the OLS estimator" instead of $\hat{\beta} = (X'X)^{-1}X'y$
* Paraphrasing formal definitions instead of preserving exact mathematical content
* Dropping proof strategies in favor of just stating results
* Writing "由公式可得" as a substitute for actual economic intuition
* Forgetting bilingual terminology labels
* Stopping after draft without writing the `.md` file
* Ignoring past exam patterns when they clearly predict exam focus areas

## Rationalisation Table

| Excuse | Reality |
|---|---|
| "I only need the lecture slides to summarise" | If psets, solutions, or past exams exist in the same folder, they reveal what actually gets tested. Ignoring them is a failure. If only lectures exist, that is fine — degrade gracefully. |
| "The syllabus is just administrative" | If a syllabus exists, it defines topic structure, flags important content, and reveals the exam format. Read it first. If it doesn't exist, infer structure from lectures. |
| "I can summarise the whole PDF in one go" | Long decks need segmentation or later sections get dropped. |
| "Section-level page ranges are good enough" | This is for exam revision lookup — point-level `【课件页】` citations matter. The reader needs to flip to the exact slide, not search through 20 pages. |
| "I'll add the problem recommendations later" | The topic→question map is built in Step 3. If a matching problem exists and the `｜推荐练习：` tag is missing, it means the map was ignored. |
| "The formula alone is enough" | Without intuition for why it holds and a problem pattern for how it's tested, the formula is useless for exam prep. |
| "Economic intuition is obvious" | If it were obvious, students wouldn't struggle with it. Write it out explicitly every time. |
| "I can skip the model setup and just give the result" | Exams test whether you can set up the model, not just recall the punchline. |
| "Past exam analysis is extra work" | Past exams are the highest-signal predictor of what will be tested. Skipping them is malpractice. |
| "A chat summary is fine for 总结课件" | When this skill triggers, the default is a file artifact integrating all available resources. |
| "由公式可得 counts as intuition" | No. Intuition uses economic language: incentives, trade-offs, surplus, efficiency, identification. Math restated in words is not intuition. |