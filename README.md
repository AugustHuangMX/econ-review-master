# Econ Slides Review

一个为经济学学生打造的 Claude Code Skill —— 把课程文件夹里的课件、习题、答案、真题整合成一份以**经济学直觉**为核心的 Obsidian Markdown 复习笔记。

A Claude Code Skill for economics students — turns a course folder (lectures, problem sets, solutions, past exams) into integrated Obsidian Markdown review notes centered on **economic intuition**.

[中文](#中文) | [English](#english)

---

## 中文

### 它能做什么

把你一门经济学课的所有材料——课件、习题集、答案、习题课讲义、往年考题——整合成一份结构清晰的复习笔记。

**不是**把课件缩写成更短的文字。而是：

- 每个定义、公式、模型后面都附带**经济学直觉**（为什么这个结论成立？经济逻辑是什么？）
- 把习题和真题中的**题型模式**整合到对应知识点下（这个概念怎么考？怎么答？）
- 输出是 **Obsidian 兼容的 Markdown**，支持 `$...$` 数学公式和 callout 语法
- 中文为主，重要术语保留英文括注：`边际替代率 (MRS)`

### 文件夹自动识别

Skill 启动时会扫描你的课程文件夹，自动识别以下材料（都是可选的，只有课件是必须的）：

| 材料 | 常见命名 |
|---|---|
| 大纲 | `syllabus`, `outline` |
| 课件 | `lecture`, `lecture_notes`, `slides`, `课件` |
| 习题集 | `pset`, `ps`, `problem_set`, `homework` |
| 习题课 | `seminar`, `tutorial`, `习题课` |
| 答案 | `solution`, `sol`, `answers` |
| 往年考题 | `past_exam`, `past_paper`, `exam` |

不要求特定的文件夹结构——子文件夹、flat folder、甚至只有一个 PDF 都可以处理。

### 安装

```bash
# 全局安装（所有项目可用）
mkdir -p ~/.claude/skills/econ-slides-review
curl -o ~/.claude/skills/econ-slides-review/SKILL.md \
  https://raw.githubusercontent.com/AugustHuangMX/econ-review-master/main/SKILL.md
```

或者克隆仓库：

```bash
git clone https://github.com/AugustHuangMX/econ-review-master.git
mkdir -p ~/.claude/skills/econ-slides-review
cp econ-slides-review/SKILL.md ~/.claude/skills/econ-slides-review/
```

项目级安装（只在某个课程目录下生效）：

```bash
cd ~/your-course-folder
mkdir -p .claude/skills/econ-slides-review
curl -o .claude/skills/econ-slides-review/SKILL.md \
  https://raw.githubusercontent.com/AugustHuangMX/econ-review-master/main/SKILL.md
```

### 使用

在课程文件夹里启动 Claude Code，然后自然语言触发：

```
总结一下这个课件
```

```
把这门课整理成考前复习资料
```

```
只总结 Lecture 3-5，重点提炼公式和模型
```

或者直接用斜杠命令：

```
/econ-slides-review
```

### 输出示例

生成的 `EC487_review.md` 大致结构：

```markdown
---
title: "EC487 Review"
date: 2026-04-27
course: "EC487 Advanced Microeconomics"
tags: [review, EC487]
---

# EC487 复习笔记

## Topic 1: 机制设计 (Mechanism Design)

### Key Concepts

> [!definition] 激励相容 (Incentive Compatibility)
> 一个机制是激励相容的，当且仅当对所有 agent $i$，
> 真实报告是弱占优策略...
> 【课件页 34-38｜推荐练习：PS2 Q3, Exam 2023 Q1b】

> [!intuition] 经济学直觉
> 如果说谎能让你得到更好的分配结果，理性人一定会说谎。
> IC 条件确保了诚实报告本身就是最优策略——不需要外部强制。

> [!formula] Revenue Equivalence
> 满足 IC 的机制下，期望支付由最低 type 的支付和分配规则唯一决定。
> 【课件页 45-49｜推荐练习：PS3 Q1, Exam 2022 Q2】

### Problem Patterns

> [!example] 典型题型 (PS2 Q3, Exam 2023 Q1b)
> 给定一个拍卖机制，验证其是否满足 IC 和 IR...

> [!technique] 解题方法
> 1. 写出 agent 的期望效用函数
> 2. 对 type 求导，令 FOC = 0...
> 【课件页 40-42】
```

### 与原 skill 的区别

本项目基于 [summarize-slides-skill](https://github.com/Li-Baichuan-James/summarize-slides-skill) 改造。主要区别：

| | summarize-slides | econ-slides-review |
|---|---|---|
| 输出格式 | LaTeX → PDF | Obsidian Markdown |
| 学科 | 通用 | 经济学特化 |
| 输入来源 | 仅课件 PDF | 课程文件夹（课件+习题+答案+真题+大纲） |
| 核心理念 | 覆盖率 | 经济学直觉优先 |
| 构建依赖 | 需要 xelatex | 无额外依赖 |
| 文件夹要求 | 无 | 自动扫描，灵活适配 |

---

## English

### What It Does

Turns all materials from an economics course — lecture slides, problem sets, solutions, seminar notes, past exams — into a single, well-structured set of review notes.

This is **not** about compressing slides into fewer words. It's about:

- Attaching **economic intuition** after every definition, formula, and model (why does this result hold?)
- Integrating **problem patterns** from psets and past exams under each topic (how is this concept tested? how should you answer?)
- Outputting **Obsidian-compatible Markdown** with `$...$` math and callout syntax
- Chinese-first with English terms in parentheses: `边际替代率 (MRS)`

### Folder Auto-Detection

The skill scans your course folder on startup and identifies available materials (all optional except lectures):

| Resource | Common Names |
|---|---|
| Syllabus | `syllabus`, `outline` |
| Lectures | `lecture`, `lecture_notes`, `slides` |
| Problem Sets | `pset`, `ps`, `problem_set`, `homework` |
| Seminars | `seminar`, `tutorial` |
| Solutions | `solution`, `sol`, `answers` |
| Past Exams | `past_exam`, `past_paper`, `exam` |

No specific folder structure required — subfolders, flat directories, even a single PDF all work.

### Installation

```bash
# Global install (available in all projects)
mkdir -p ~/.claude/skills/econ-slides-review
curl -o ~/.claude/skills/econ-slides-review/SKILL.md \
  https://raw.githubusercontent.com/AugustHuangMX/econ-review-master/main/SKILL.md
```

Or clone and copy:

```bash
git clone https://github.com/AugustHuangMX/econ-review-master.git
mkdir -p ~/.claude/skills/econ-slides-review
cp econ-slides-review/SKILL.md ~/.claude/skills/econ-slides-review/
```

### Usage

Start Claude Code in your course folder and use natural language:

```
Summarize this lecture into exam review notes
```

```
Make a review sheet focusing on formulas and models from Lectures 3-5
```

Or invoke directly:

```
/econ-slides-review
```

### Graceful Degradation

The skill adapts to whatever materials are available:

| Available Materials | Output Quality |
|---|---|
| Lectures only | Concept + formula + intuition summary |
| + Syllabus | Adds structured topic ordering and exam format |
| + Problem sets | Adds "how it's tested" per topic |
| + Solutions | Adds "how to answer" techniques |
| + Past exams | Full integrated review with exam pattern analysis |

### Credits

Built on top of [summarize-slides-skill](https://github.com/Li-Baichuan-James/summarize-slides-skill) by [Li-Baichuan-James](https://github.com/Li-Baichuan-James), MIT License.

## License

MIT