# Installation Guide

## For Humans

Copy and paste this to Claude Code:

```
Install the econ-slides-review skill from: ~/.claude/skills/econ-slides-review/SKILL.md
```

## Manual Installation

1. Create the skill directory:

```bash
mkdir -p ~/.claude/skills/econ-slides-review
mkdir -p ~/.claude/skills/econ-slides-review/references
```

2. Copy `SKILL.md` and the optional references into that directory:

```bash
cp SKILL.md ~/.claude/skills/econ-slides-review/
cp -R references ~/.claude/skills/econ-slides-review/
```

3. Verify:

```bash
cat ~/.claude/skills/econ-slides-review/SKILL.md | head -5
test -f ~/.claude/skills/econ-slides-review/references/heading-output-examples.md
```

You should see the YAML frontmatter starting with `name: econ-slides-review`, and the reference-file check should exit silently.

## Companion Skill: pdf

This skill requires a `pdf` or `pdf-reading` companion skill for reading PDF files. In Claude Code, the built-in PDF handling is typically sufficient. If you need the full `pdf` skill:

* Check if it exists: `ls ~/.claude/skills/pdf/SKILL.md` or check Claude Code's skill list
* If not present, you can install it from the Anthropic skills repository

## Validation

A working installation means:

* `~/.claude/skills/econ-slides-review/SKILL.md` exists
* A PDF companion skill is available (built-in or installed)
* Claude Code recognises the skill when you say "总结课件" or "summarize lecture slides"

## Usage Examples

```
总结这个课件，整理成考前复习资料
```

```
Summarize this lecture PDF into exam review notes
```

```
只总结 Lecture 3-5，重点提炼公式和模型
```

```
只生成 21 小时 problem-first 复习 roadmap，不要完整复习笔记
```

```
生成今年考纲真题映射：遍历 past exam 小题，判断是否超纲，并对应到课件页和 problem set
```

```
润色这个文件夹里的复习大纲，先对照 past exam 和 problem set 找缺口
```

```
把这份 econometrics slides 做成公式速查表
```
