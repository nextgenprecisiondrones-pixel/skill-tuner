# Skill Tuner

**Correct a skill once. It stops repeating the mistake.**

One file. No code, no hooks, no database, no Python. Works anywhere skills work: Claude Code, Claude apps, Codex, Cursor.

<!-- DEMO GIF: correction → "Logged for x" → "tune my skills" → diff → approved -->

## The problem

You correct your skills the same way over and over. "Too long." "Wrong format." "I said no emojis." The fix lives in one chat and dies there. Next week, same mistake.

## How it works

1. **You correct a skill like you normally would.** Skill Tuner fixes the output and logs one line: what went wrong and the rule that would have prevented it.
2. **You say "tune my skills."** It reads the lessons, rewrites only the affected skills, and shows you a diff.
3. **You say yes or no.** Yes: the skill is updated. No: that lesson is never proposed again.

```
- 2026-10-31 | sfx-cue-picker | whoosh landed on a spoken word | TALKING mode: no SFX within 0.3 s of a word (x3)
```

## Why it's different

| | Skill Tuner | Most "self-learning" setups |
| --- | --- | --- |
| What it changes | The skill that made the mistake | One ever-growing CLAUDE.md or a database |
| File growth | Lessons are folded into existing rules, so skills stay the same length or shorter | Rules get appended forever |
| Rejected ideas | Remembered and never re-proposed | Often suggested again |
| Install | One SKILL.md | Hooks, scripts, runtimes |
| Approval | Every edit, shown as a diff | Varies |

## Install

**Claude Code plugin**
```
/plugin marketplace add nextgenprecisiondrones-pixel/skill-tuner
/plugin install skill-tuner@skill-tuner
```

**Any agent (skills CLI)**
```
npx skills add nextgenprecisiondrones-pixel/skill-tuner
```

**Manual:** copy `skills/skill-tuner/SKILL.md` into `~/.claude/skills/skill-tuner/`.

## Use

- Correct any skill's output. You'll see `Logged for <skill>.`
- Say `tune my skills` (or `tune <skill>`) whenever you like. Weekly works well.

Lessons live in `~/.claude/skill-lessons.md`. It's plain text: read it, edit it, delete lines.

## Rules it follows

- Never edits a skill without your explicit yes.
- Never removes safety rules, approval steps, or stop conditions.
- Only changes what a logged lesson justifies.
- Won't edit plugin-installed skills in place (updates would wipe the change); it offers a local copy instead.

## License

MIT. Built by [NextGen Lab Studio](https://github.com/nextgenprecisiondrones-pixel). Star the repo if it saves you a correction.
