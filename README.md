# AI EasyRead Modes

As AI takes on more complex tasks, its answers can become longer, denser, and harder to follow. Readers may spend considerable time finding the main point, working through unfamiliar terms, and deciding which details matter. Clearer wording and a suitable level of detail can reduce this reading effort.

AI EasyRead Modes helps make answers easier to read while preserving key details and uncertainty. Choose a mode and a level to suit the task; all three modes default to level 2.
| Mode | Levels | Purpose |
| --- | --- | --- |
| Everyday | 1–3 | Personal choices, household tasks, and practical explanations. |
| Work | 1–5 | Professional decisions, procedures, coordination, and deliverables. Tasks can be complex; explanations go as deep as the job needs. |
| Research | 1–5 | Scientific questions, theory, study design, and evidence. Allows the greatest depth and complexity. |

Work covers professions such as e-commerce, administration, accounting, and journalism. Choose by purpose: scheduling a research team is Work; examining a scientific hypothesis is Research.

## Usage

```text
Use AI EasyRead Modes, Everyday level 2: how can I keep my desk tidy?
Use AI EasyRead Modes, Work level 3, to turn these promotion notes into a handoff.
Use AI EasyRead Modes, Research level 5, to discuss this finding's meaning and limits.
```

If you leave out the mode, the skill infers it from your task. If you leave out the level, it uses level 2 unless you have set a different conversation default.

The package is written in English. Responses follow your language; rewrites keep the source language unless you request a translation. You can ask in Chinese or another language.

## Levels

| Level | Everyday | Work | Research |
| --- | --- | --- | --- |
| 1 | Direct answer or action. | Decision, status, and immediate action. | Main judgment, scientific meaning, and key limit. |
| 2 | Brief explanation and useful steps. | Key reasons, actions, and cautions. | Main evidence and why it matters. |
| 3 | Enough explanation, options, and steps to handle the situation. | A usable plan, responsibilities, and dependencies. | Connect the question, approach, evidence, and conclusion. |
| 4 | — | Compare options, tradeoffs, exceptions, and execution risks. | Examine competing explanations, assumptions, and methodological limits. |
| 5 | — | Complete information for the requested decision, execution, or handoff. | Discuss theoretical contribution, evidence, alternative explanations, robustness, and inference limits in depth. |

Compare levels within a mode. Work level 5 can handle many steps and people; Research level 5 also examines whether an explanation holds and what the findings change about our understanding. Everyday level 3 stays focused on practical life questions.

Levels are not word counts. Short material can stay short. Every level must preserve conditions and uncertainty that affect the answer, and complete all requested deliverables.

## Switching modes

- A setting applies to the current reply unless you ask to keep it, for example: “Use Research level 4 by default in this conversation.”
- A one-reply override leaves the conversation default intact. When switching modes without a level, use that mode's established default or level 2.
- Everyday has no levels 4 or 5. A request for Everyday level 5 uses level 3 with a brief note; it does not switch modes.
- Specify any required output format, such as JSON. Format requirements take precedence over mode labels or explanatory notes.

## Installation

Download the repository and put `SKILL.md` at the path for your app. There are no runtime dependencies.

| App | File location | Invocation |
| --- | --- | --- |
| Codex, local skills | `~/.agents/skills/ai-easyread-modes/SKILL.md` | `$ai-easyread-modes` |
| Claude Code, local sessions | `~/.claude/skills/ai-easyread-modes/SKILL.md` | `/ai-easyread-modes` |

Use the folder name `ai-easyread-modes`, separate from `easyread`. For Codex, optionally copy `agents/openai.yaml` into the skill's `agents/` folder to provide its display name and default prompt.

See the [Codex](https://learn.chatgpt.com/docs/build-skills) and [Claude Code](https://code.claude.com/docs/en/skills) installation docs. For other apps that support [Agent Skills](https://agentskills.io/specification), follow the app's instructions. Reopen the session if the skill is not recognized.

## Examples and checks

[examples.md](examples.md) includes everyday, professional, and research examples, plus cases for checking mode selection and level limits.

File structure and packaging have been checked, and the examples have been manually reviewed. Automatic selection and conversation defaults have not been tested in the clients; behavior may vary by model.

## References and license

Design references: [Humanizer](https://github.com/blader/humanizer), [The Elements of Style](https://github.com/obra/the-elements-of-style), and [Technical Writing Density](https://github.com/mlwelles/technical-writing-density).

[MIT](LICENSE). For useful feedback, include the source text with sensitive details removed, the mode, the level, and the output.
