# Q8 — Executive-Ready Output

## Objective
Turn supplied analysis into a crisp, action-oriented leadership update with controlled length and a predictable structure.

## Recommended technique
**Zero-shot with strict output constraints.**

The desired audience and output format are known, so a schema and word limits are more useful than examples.

## Full prompt

```text
You are preparing an executive update for senior leadership.

SOURCE MATERIAL
[Paste the analysis, project update, findings, or business information here.]

AUDIENCE
Senior leaders who need decisions, risks, and actions—not implementation-level detail.

RULES
1. Use only information in the source material.
2. Do not invent metrics, owners, dates, causes, or commitments.
3. Lead with the most important decision or insight.
4. Be concise, specific, and action-oriented.
5. Avoid background detail unless it changes a decision.
6. Expand an acronym on first use if it is not widely understood.
7. Distinguish confirmed status from estimates, assumptions, and open questions.
8. If no decision is required, state "No decision requested".
9. If an owner or due date is missing, write "Owner not specified" or "Due date not specified".
10. Keep the complete response within 250 words, excluding the title.

OUTPUT FORMAT
## Executive headline
One sentence stating the most important point.

## Status
| Area | Status | Evidence / impact |
|---|---|---|
Use no more than 4 rows.

## Key insights
- Maximum 3 bullets.
- Each bullet must state the insight and why it matters.

## Risks / decisions required
| Item | Business impact | Required action / decision | Owner / due date |
|---|---|---|---|
If none are identified in the source, state that.

## Next actions
- Maximum 3 actions.
- Start each action with a verb.

FINAL CHECK
Remove repetition, generic statements, unsupported claims, and details that do not affect leadership decisions. Confirm the response is within the word limit.
```

## Why this structure?
The headline gives the key message immediately. Tables make status and decisions easy to scan. Limits on rows and bullets reduce verbosity and force prioritisation.

## Why this technique?
Zero-shot is suitable because the required structure is explicit. Few-shot examples may be useful if leadership has a strict house style, but are not essential for a first version.

## Failure modes prevented
- Long, unfocused summaries.
- Missing decisions or next actions.
- Unsupported status claims.
- Invented owners or deadlines.
- Repeating the same point in several sections.
- Technical detail overwhelming the executive message.

## Alternative prompt design
Use a **decision memo format** with only four headings: Decision needed, Recommendation, Evidence, and Risks. This is more effective when leadership is being asked to approve one specific action rather than review a general status update.
