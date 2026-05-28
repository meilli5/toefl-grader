# TOEFL Writing Grader

A Claude Code skill that grades TOEFL writing essays using official ETS rubrics. Supports both **Write an Email** and **Write for an Academic Discussion** (2026 new TOEFL format).

## Features

- Strict, objective scoring on the 0-5 ETS scale
- Band justification with direct quotes from official rubrics
- Comprehensive vocabulary upgrade table (all problematic words)
- Full-sentence rewrites for awkward or error-containing sentences
- Logic and structure diagnosis
- Score 5 model essay rewrite preserving your core ideas
- Calibrated against Magoosh scored samples (Score 5/3/2) for consistent grading

## Repository Structure

```
toefl-grader/
├── SKILL.md                        # Skill definition and grading workflow
├── toefl-grader.skill             # Skill metadata (name, description)
└── references/
    ├── writing-rubrics.md         # Official ETS scoring rubrics (0-5 bands)
    └── system_prompt.md           # Scoring methodology, audit rules, and calibration benchmarks
```

- `SKILL.md` — the core skill file loaded by Claude Code. Defines the step-by-step grading workflow: read rubrics → extract essay → score band → justify → diagnose → rewrite.
- `references/writing-rubrics.md` — the official ETS TOEFL Writing Scoring Guide rubrics for both task types, used as the scoring standard.
- `references/system_prompt.md` — methodology, Audit Focus rules (register, counter-argument quality, vague intensifiers), and Magoosh calibration benchmarks.

## Requirements

- [Claude Code](https://claude.ai/code) CLI

## Installation

```bash
npx skills add https://github.com/meilli5/toefl-grader --skill toefl-grader -g -y
```

Or manually:

```bash
git clone https://github.com/meilli5/toefl-grader.git
ln -sf "$(pwd)/toefl-grader" ~/.claude/skills/toefl-grader
```

## Usage

### 1. Create an essay file

Write your essay in a `.md` file with this structure:

```markdown
# Writing an Email

## 题目
You are an employee at a marketing firm...

**Write an email to Ms. Thompson. In your email, do the following.**
   ●  Describe the main idea of the campaign.
   ●  Explain why you believe this idea will be effective.
   ●  Ask for her feedback and any suggestions for improvement.

## 我的原文
Dear Ms. Thompson,

[your email here]
```

For Academic Discussion, use `# Write for an Academic Discussion` as the heading and include the professor's question plus both classmates' posts in `## 题目`.

### 2. Ask Claude to grade it

```
帮我批改 my-essay.md
```

The skill automatically triggers and generates `my-essay-graded.md` in the same directory.

### 3. Review the output

The graded file contains:

- **Score** (0.0 - 5.0)
- **Justification** with rubric quotes explaining why this band
- **Vocabulary upgrade table** covering all problematic words
- **Sentence upgrades** (3-5 original sentences rewritten)
- **Logic/structure diagnosis**
- **Score 5 rewrite** preserving your core ideas

## Example

**Input** (`email-1.md`):
```markdown
# Writing an Email

## 题目
You are an employee at a marketing firm...

## 我的原文
Dear Ms. Thompson,
Hope this email finds you in well spirit!
I'm writing to introduce my immutual notions for the new advertising campaign...
```

**Output** (`email-1-graded.md`):
```markdown
# 托福写作批改结果

**题型**: Email
**得分**: 3.0 / 5.0

## 定档理由
对照 Rubrics 中 Score 3 的描述...
## 诊断与修改建议
### 词汇升级
| 原文 | 问题 | 建议替换 |
...
### 整句升级
...
## Score 5 范文重写
...
```

## Credits

- **ETS TOEFL Writing Scoring Guide** — the official rubrics used as the scoring standard. Copyright 2025 by ETS. TOEFL and TOEFL iBT are registered trademarks of ETS.
- **Magoosh** — calibration samples adapted from [TOEFL Writing Academic Discussion Sample Responses](https://magoosh.com/toefl/toefl-writing-academic-discussion-sample-responses/), used to anchor grading strictness.

## License

MIT
