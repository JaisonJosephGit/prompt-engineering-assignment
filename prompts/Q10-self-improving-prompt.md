# Q10 — Self-Improving Prompt

## Objective
Generate an answer, critique it against defined criteria, and produce one improved version, while keeping the critique brief and preventing repeated revision loops.

## Recommended technique
**Single-pass generate–critique–revise workflow.**

This is a controlled self-review process. It allows one revision only; it does not ask the model to repeat indefinitely until it declares perfection.

## Full prompt

```text
You are an assistant that produces and quality-checks a response.

USER TASK
[Describe the task here.]

SOURCE MATERIAL / CONTEXT
[Paste relevant information here.]

REQUIREMENTS
[Specify audience, tone, format, length, and constraints.]

PROCESS
Stage 1 — Draft
Create an initial answer that addresses the user task using only the supplied context and reliable information permitted by the task.

Stage 2 — Brief critique
Review the draft against these criteria:
- Accuracy and evidence support
- Completeness against the requirements
- Clarity and organisation
- Compliance with format and length
- Unsupported assumptions or invented details

The critique must contain no more than 5 bullets and no more than 100 words total. Identify only material issues. Do not provide hidden internal reasoning; provide concise, observable quality findings.

Stage 3 — One revision
Revise the draft once, correcting the material issues identified in Stage 2. Do not add unsupported information. If no material issue is found, retain the draft and state that no revision was necessary.

STOP RULES
1. Perform exactly one critique and at most one revision.
2. Do not start another critique–revision cycle.
3. Do not claim that the answer is perfect or guaranteed correct.
4. If essential information is missing, state the limitation rather than filling the gap.

OUTPUT
## Final answer
[Provide the revised or retained answer.]

## Quality check
- Issues found: [Brief list, or "No material issue identified"]
- Changes made: [Brief list, or "No revision required"]
- Remaining limitations: [State any material uncertainty]
```

## Why this structure?
The three stages separate creation, review, and revision. Explicit word limits control critique verbosity, and the stop rules cap the process at one revision.

## Why this technique?
A generate–critique–revise pattern is appropriate because the goal is to improve a draft against known requirements. It is more controlled than an open-ended self-improvement loop. The model's self-review is not independent verification, so high-stakes outputs still require human or external validation.

## Failure modes prevented
- Infinite critique and revision loops.
- Critique becoming longer than the answer.
- Unnecessary rewriting when no material issue exists.
- Introducing new unsupported content during revision.
- Claiming certainty based only on self-review.

## Alternative prompt design
Use a **rubric-based evaluator followed by a separate revision call**. The first call returns the draft and a compact pass/fail checklist. A second call revises only failed criteria. This is easier to audit in an automated workflow because the evaluation and revision are separate steps.
