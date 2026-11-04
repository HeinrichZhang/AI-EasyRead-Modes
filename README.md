# AI EasyRead Modes

As AI takes on more complex tasks, its answers can become longer, denser, and harder to follow. Readers may spend considerable time finding the main point, working through unfamiliar terms, and deciding which details matter. Clearer wording and a suitable level of detail can reduce this reading effort.

AI EasyRead Modes is a lightweight, instruction-only skill for AI clients that support [Agent Skills](https://agentskills.io/specification). It guides the model to write readable answers at a depth suited to the task, while preserving key details and uncertainty. It works with your client's model and has no runtime dependencies of its own.

## Modes

| Mode | Levels | Purpose |
| --- | --- | --- |
| Everyday | 1–3 | Personal choices, household tasks, and practical explanations. |
| Work | 1–5 | Professional decisions, procedures, coordination, and deliverables. Complexity can be high; depth serves the job. |
| Research | 1–5 | Scientific questions, theory, study design, and evidence. Allows the greatest depth and complexity. |

All modes default to **level 2**. Work covers professions including e-commerce, administration, accounting, and journalism. Choose by purpose: scheduling a research team is Work; examining a scientific hypothesis is Research.

## See the difference: Research levels 1 and 5

**One question:** When do physical constraints improve a learned flow model, and what can these results establish?

In [Physics-Informed Deep Flow Prediction](https://github.com/ZhiboDai804/Physics-Informed-Deep-Flow-Prediction), a U-Net learns to predict airfoil pressure and velocity from simulation data resampled onto a `128 × 128` grid. A continuity penalty encourages mass conservation. The reported combined error on normalized fields is **2.74%** without this penalty, **2.61%** at penalty weight **λ = 0.02**, and **3.51%** at **λ = 1.0**.

The results come from the cited project. The two answers below are authored illustrations, not an independent evaluation of this skill.

### Research level 1 — Main finding

The reported experiments favor a modest continuity penalty: predictions agree slightly better with the reference flow fields, while a strong penalty makes agreement worse. The benefit of adding physics appears conditional; this error comparison alone does not establish physical reliability.

<details>
<summary><strong>Research level 5 — Scientific meaning, competing explanations, and next tests</strong></summary>

The deeper question is when a conservation law remains a useful learning constraint after a simulation has been converted into training data. For an aerodynamic surrogate, agreement with reference fields and physical credibility both matter. A model could improve one without improving the other.

The reported reduction from 2.74% to 2.61% identifies a promising regime of moderate regularization, but does not establish why it works. The authors suggest that resampling leaves the reference fields inconsistent with discrete continuity, so strong enforcement can conflict with fitting those fields. Loss imbalance or optimization effects could also contribute. If target inconsistency drives the deterioration, reducing it should change the tradeoff between data fit and mass conservation.

A follow-up study should first measure the target fields' continuity residual using the same scaling, mask, and discrete operator used in training. It could then compare grid resolutions or resampling methods while controlling training budget, loss definition, model capacity, and random seeds. Changes in the error–residual relationship would help distinguish target inconsistency from a general optimization problem. A resolution change alone would not isolate the cause, because it can also change model and training requirements.

Evaluation should report pressure error, velocity error, and mass-balance residuals separately, with uncertainty across runs. Additional flow regimes beyond the published test set would test how far any benefit extends. These checks would clarify whether the constraint improves transferable flow prediction or mainly changes the fit to one numerical representation. They are proposed tests, not results already established by the project.

</details>

Both answers use the same material. Level 1 states the finding and its main limit; level 5 examines what could explain it and what evidence would change the conclusion. See [source notes](examples.md#research-source-notes) for attribution and reproduction details.

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

## Depth levels

| Level | Everyday | Work | Research |
| --- | --- | --- | --- |
| 1 | Direct answer or action. | Decision, status, and immediate action. | Main judgment, scientific meaning, and key limit. |
| 2 | Brief explanation and useful steps. | Key reasons, actions, and cautions. | Main evidence and why it matters. |
| 3 | Enough explanation, options, and steps to handle the situation. | A usable plan, responsibilities, and dependencies. | Connect the question, approach, evidence, and conclusion. |
| 4 | — | Compare options, tradeoffs, exceptions, and execution risks. | Examine competing explanations, assumptions, and methodological limits. |
| 5 | — | Complete information for the requested decision, execution, or handoff. | Discuss theoretical contribution, evidence, alternative explanations, robustness, and inference limits in depth. |

Levels control depth within each mode, not word counts or the difficulty of the language. Every level should remain readable and preserve important conditions and uncertainty. A lower level must still complete all requested deliverables.

## Defaults and language

- An explicit mode takes priority. Otherwise, the skill uses your conversation default or infers a mode from the task. Without a level, it uses that mode's established default or level 2.
- To keep a setting, say: “Use Research level 4 by default in this conversation.” A one-reply override leaves that default intact. Switching modes without a level uses the new mode's own default or level 2.
- Out-of-range requests use the nearest supported level. Everyday level 5 becomes level 3, with a brief note unless an exact format, such as JSON, forbids it.
- Responses follow your language. Rewrites keep the source language unless you request a translation. The English package does not require English output.

## Limits and validation

Research mode guides the depth of a scientific discussion; it does not by itself verify facts or citations. Results depend on the model, the supplied material, and the client's handling of skills.

The files and packaging have been checked, and the instructions and examples have been self-reviewed. The example responses are authored illustrations, not benchmark results for this skill. Cited research results belong to their source projects. Automatic activation and conversation defaults have not been tested in Codex or Claude Code. No measured improvement in reading speed or comprehension is claimed.

For useful feedback, include the input with sensitive details removed, your client and model, the mode and level, and the output.

## References and license

Design references: [Humanizer](https://github.com/blader/humanizer), [The Elements of Style](https://github.com/obra/the-elements-of-style), and [Technical Writing Density](https://github.com/mlwelles/technical-writing-density).

[MIT](LICENSE).
