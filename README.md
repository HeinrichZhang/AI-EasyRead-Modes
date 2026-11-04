# AI EasyRead Modes

As AI takes on more complex tasks, its answers can become longer, denser, and harder to follow. Readers may spend considerable time finding the main point, working through unfamiliar terms, and deciding which details matter. Clearer wording and a suitable level of detail can reduce this reading effort.

AI EasyRead Modes is a lightweight, instruction-only skill for AI clients that support [Agent Skills](https://agentskills.io/specification). It adjusts how much detail an answer contains while preserving the task, the main point, and essential qualifications. Higher levels explain the answer more fully and can add relevant insights after the requested work is complete. It works with your client's model and has no runtime dependencies of its own.

## Modes

| Mode | Levels | Purpose |
| --- | --- | --- |
| Everyday | 1–3 | Personal choices, household tasks, and practical explanations. |
| Work | 1–5 | Professional decisions, procedures, coordination, and deliverables. Complexity can be high; depth serves the job. |
| Research | 1–5 | Scientific questions, theory, study design, and evidence. Allows the greatest depth and complexity. |

All modes default to **level 2**. Work covers professions including e-commerce, administration, accounting, and journalism. Choose by purpose: scheduling a research team is Work; examining a scientific hypothesis is Research.

## See the difference: Research levels 1 and 5

**Same task:** Explain why a modest continuity penalty might improve flow prediction, while a strong penalty makes it worse in the reported experiments.

The example uses [Physics-Informed Deep Flow Prediction](https://github.com/ZhiboDai804/Physics-Informed-Deep-Flow-Prediction) from Stanford, which predicts airfoil pressure and velocity using simulation data resampled onto a `128 × 128` grid. Both versions explain the same reported result and the authors' proposed reason for it. These responses are authored illustrations, not an evaluation of this skill.

### Research level 1 — Essential explanation

The model's reported error was lower with a modest mass-conservation penalty and higher with a strong one. The authors suggest that resampling leaves the reference data imperfectly consistent with the constraint, so enforcing it too strongly can conflict with fitting the data. This explains the pattern plausibly, but the cause has not been established.

### Research level 5 — Complete explanation of the same result

<details>
<summary>Read the full explanation</summary>

The reported comparison suggests that a modest continuity penalty can be useful, while a strong penalty can harm agreement with the reference flow fields. The combined relative error on normalized fields falls from 2.74% for the baseline to 2.61% at penalty weight λ = 0.02. This is a reduction of 0.13 percentage points, about 4.7% relative to the baseline. At λ = 1.0, the error rises to 3.51%. Increasing the weight therefore did not consistently improve prediction in these experiments.

The model is a supervised U-Net trained on pressure and velocity fields from two-dimensional Reynolds-averaged Navier–Stokes simulations. Its data loss rewards agreement with those reference fields. The added continuity penalty discourages velocity divergence, which measures a local violation of mass conservation in incompressible flow. The weight λ sets how strongly that penalty contributes alongside the data loss.

The authors' explanation concerns the numerical representation of the reference data. The original solutions are transferred from a body-fitted mesh to a `128 × 128` Cartesian grid. After this resampling, the fields may not exactly satisfy the discrete continuity constraint used in training. Under this explanation, a modest penalty provides a useful guide while still allowing the model to fit the data. A large penalty can instead prioritize satisfying the constraint even where it conflicts with the resampled targets, increasing prediction error.

This is a plausible account of the observed pattern, not a demonstrated causal mechanism. The error comparison alone cannot establish that resampling caused the deterioration. A useful implication is that a valid physical law and its numerical enforcement are separate issues: stronger enforcement of an approximate constraint need not produce a better fit to processed data. The result supports a conditional benefit in this setup, not a general claim that more or less physical regularization is always better.

</details>

Both versions give the same finding, proposed explanation, and uncertainty. Level 5 adds the numerical evidence, method details, and reasoning behind that answer. See [source notes](examples.md#research-source-notes) for the shared material and attribution.

## Install and try

1. Download and unzip this repository using **Code → Download ZIP**.
2. Create the skill folder shown below and copy `SKILL.md` into it.
3. Open your AI client and invoke the skill. Restart the client if it does not appear.

| Client | File location | Invocation |
| --- | --- | --- |
| Codex (local skills) | `~/.agents/skills/ai-easyread-modes/SKILL.md` | `$ai-easyread-modes` |
| Claude Code (local sessions) | `~/.claude/skills/ai-easyread-modes/SKILL.md` | `/ai-easyread-modes` |

Use the exact folder name `ai-easyread-modes`, even if the downloaded folder has a branch suffix. For Codex, optionally copy `agents/openai.yaml` into the skill's `agents/` folder for its display name and default prompt.

After invoking the skill, try:

```text
Everyday level 2: how can I keep my desk tidy?
Work level 3: turn these promotion notes into a handoff.
Research level 5: discuss this finding's scientific meaning and evidence limits.
```

For the last two examples, include the notes or finding you want to discuss.

See the [Codex](https://learn.chatgpt.com/docs/build-skills) and [Claude Code](https://code.claude.com/docs/en/skills) installation docs. Other clients may use different installation methods.

## Detail levels

Changing the level keeps the task and core answer intact. It changes how much explanation and supporting detail the reader sees. Everyday uses levels 1–3; Work and Research use levels 1–5.

| Level | What changes |
| --- | --- |
| 1 · Essential | The shortest readable answer that keeps the core point, essential reasoning, and necessary qualifications. |
| 2 · Brief | The same answer with a short explanation of its main reasons or steps. |
| 3 · Standard | Enough context and supporting detail to understand the same answer. |
| 4 · Detailed | Fuller reasoning, evidence, assumptions, and limits relevant to the task. |
| 5 · Complete | A complete explanation within the requested scope, suitable for careful review or reuse. Relevant further insights may follow the core answer. |

Every level must complete the requested work. Level 5 can think further, but should first answer the original question; an explanation should not turn into a different assignment. For rewrites, expansion stays within the supplied material unless analysis is also requested. Levels are not word counts, and completeness does not require harder language or repetition.

## Defaults and language

- An explicit mode takes priority. Otherwise, the skill uses your conversation default or infers a mode from the task. Without a level, it uses that mode's established default or level 2.
- To keep a setting, say: “Use Research level 4 by default in this conversation.” A one-reply override leaves that default intact. Switching modes without a level uses the new mode's own default or level 2.
- Out-of-range requests use the nearest supported level. Everyday level 5 becomes level 3, with a brief note unless an exact format, such as JSON, forbids it.
- Responses follow your language. Rewrites keep the source language unless you request a translation. The English package does not require English output.

## Limits and validation

Research mode adapts the explanation of a scientific task; it does not by itself verify facts or citations. Results depend on the model, the supplied material, and the client's handling of skills.

The files and packaging have been checked, and the instructions and examples have been self-reviewed. The example responses are authored illustrations, not benchmark results for this skill. Cited research results belong to their source projects. Automatic activation and conversation defaults have not been tested in Codex or Claude Code. No measured improvement in reading speed or comprehension is claimed.

For useful feedback, include the input with sensitive details removed, your client and model, the mode and level, and the output.

## References and license

Design references: [Humanizer](https://github.com/blader/humanizer), [The Elements of Style](https://github.com/obra/the-elements-of-style), and [Technical Writing Density](https://github.com/mlwelles/technical-writing-density).

[MIT](LICENSE).
