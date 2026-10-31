---
name: skill-tuner
description: Use when the user corrects or rejects output produced by one of their skills (log the lesson), or says "tune my skills" / "tune <skill>" (turn logged lessons into reviewed edits of those skills).
---

# Skill Tuner

Correct a skill once; it stops repeating the mistake. Lessons come from real use, fixes are batched, and nothing changes without the user's yes.

Lessons file: `~/.claude/skill-lessons.md` (create it if missing).

## Mode 1: Log a lesson

Trigger: the user corrects or rejects output from a skill ("wrong", "no, do X", "too long", "don't do that again", "log this").

1. Fix the output first, as asked.
2. Append one line to the lessons file:
   `- YYYY-MM-DD | <skill-name> | <what went wrong> | <rule that would have prevented it>`
3. The rule must be concrete and checkable ("never use more than 3 bullet points in the summary"), not vague ("be more careful").
4. One lesson per correction. If the same lesson is already there, append ` (x2)`, ` (x3)`… instead of a new line. Repeats are the strongest signal.
5. Confirm in one line: `Logged for <skill>.`

If you can't tell which skill produced the output, ask in one short question.

## Mode 2: Tune

Trigger: "tune my skills", "tune <skill>", or a scheduled run.

1. Read the lessons file. Group open lessons (no `[applied]` or `[rejected]` tag) by skill. Skip skills with none.
2. For each skill, find and read its current SKILL.md in full (`~/.claude/skills/<name>/`, then `.claude/skills/<name>/` in the project).
3. Draft the edit:
   - Fold each lesson into the section it belongs to, as a rule. Never append a "lessons" dump at the end.
   - Prefer rewriting or deleting an existing line over adding a new one. Aim for the same length or shorter.
   - Never remove a safety rule, approval step, or stop condition.
   - If two lessons conflict, keep the newer one and flag the conflict.
   - Change only what a logged lesson justifies. No speculative "improvements".
4. Show the user a diff per skill plus the lessons it applies. Wait for an explicit yes per skill.
5. On yes: write the new SKILL.md, tag those lessons `[applied YYYY-MM-DD]`.
   On no: tag them `[rejected]`. Never propose a rejected lesson again.
6. Report a terse tally: skills updated, lessons applied, lessons skipped and why.

## Rules

- Never write a skill file without the user's explicit yes in this conversation.
- Skills installed from a plugin are overwritten on update. Don't edit them in place: offer to create a local copy under a new name in `~/.claude/skills/` and apply the lessons there.
- Keep the lessons file under ~200 lines: when tuning, delete `[applied]` lines older than 30 days.
