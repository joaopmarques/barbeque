# barbeque

A Claude Code skill that grills your plan for you. Claude asks the hard questions, picks its own recommended answer for each one, and serves a short plan. It builds nothing until you say **go**.

Inspired by [Matt Pocock](https://github.com/mattpocock)'s [`grilling` skill](https://github.com/mattpocock/skills/blob/main/skills/productivity/grilling/SKILL.md). Barbeque is the same interview, but Claude answers its own questions.

Claude's picks are right most of the time and sometimes totally off. Barbeque shows you every pick, so you can trust the plan in 30 seconds or fix the one bad call.

## What it does

1. **Self-grill:** Claude walks the plan's decision tree and answers each question itself. It asks 12 questions by default, and never more than 20.
2. **Full plan:** Claude writes the full plan to a temporary `.md` file, like plan mode does.
3. **Report:** Claude posts a short plan in chat, with:
   - A decision log table. Each pick gets a rating:
     - ✅ Grilled: a confident pick
     - 🔥 Burned: low confidence, check this one
     - 🥩 Underdone: Claude could not decide, so you must
   - 🥫 **Sauces:** up to 3 small tweaks to this plan.
   - 🥗 **Sides:** up to 2 different approaches you did not consider.
   - A verdict: 😋 **Delicious** (ready to build) or 🍖 **Needs a slow cook** (too many 🔥/🥩 picks).
4. **Wait:** Claude builds only after you say go.

## Usage

Say any spelling of barbeque:

```
bbq this: a site-wide light/dark mode toggle
```

Then:

- `go`: build from the full plan.
- Fix a pick, for example "use a cookie, not localStorage": Claude updates the plan and posts a new report.
- `yes` to a slow cook: Claude runs a normal grilling session on only the 🔥 and 🥩 questions.

To change how deep it goes, give it a number or a list: `bbq this, 5 questions max`.

## Example report

```
# 🍖 Barbeque: Light/dark mode toggle

## The plan (short)
1. Add a toggle button to the site header.
2. Follow the system theme until the user picks one.
3. Save the pick so it stays after a reload.

Full plan: barbeque-dark-mode-toggle.md

## Decision log
| Rating       | Area  | Question                   | Pick          | Note                            |
|--------------|-------|----------------------------|---------------|---------------------------------|
| 🔥 Burned    | Tech  | Where do we save the pick? | localStorage  | A cookie stops the flash on SSR |
| ✅ Grilled   | Scope | Which pages get it?        | All pages     |                                 |
| ✅ Grilled   | UX    | Default theme?             | System theme  |                                 |

## 🥫 Sauces: small tweaks to this plan
| Tweak                     | Why it matters                    |
|---------------------------|-----------------------------------|
| Add a keyboard shortcut   | Power users switch without a click |

## 🥗 Sides: a different plate entirely
| Idea                          | Why it matters                          |
|-------------------------------|-----------------------------------------|
| Skip the toggle, follow system | Less code, and most users never switch |

## Verdict
😋 Delicious. Say go and I start.
```

## Requirements

Matt Pocock's [`grilling` skill](https://github.com/mattpocock/skills/blob/main/skills/productivity/grilling/SKILL.md), for the slow-cook handoff. Without it, Claude asks the hard questions in chat. Install it with:

```bash
npx skills add mattpocock/skills --skill grilling
```

## Install

**As a Claude Code plugin** (Claude Code 2.1.275 or later). This plugin lives in the [joaopmarques/claude-plugins](https://github.com/joaopmarques/claude-plugins) marketplace:

```bash
claude plugin marketplace add joaopmarques/claude-plugins
claude plugin install barbeque@joaopmarques
```

**With the skills CLI** (works with Claude Code and other agents):

```bash
npx skills add joaopmarques/barbeque
```

**By hand:** copy `skills/barbeque/` into `~/.claude/skills/`.

## Credits

The idea and the interview loop come from Matt Pocock's [`grilling` skill](https://github.com/mattpocock/skills/blob/main/skills/productivity/grilling/SKILL.md), part of [mattpocock/skills](https://github.com/mattpocock/skills). Go grill with the original too. 🔥

## License

MIT. See [LICENSE](LICENSE).
