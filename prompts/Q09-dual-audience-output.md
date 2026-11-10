# Q9 — Dual Audience Problem

## Objective
Use one prompt and the same source input to produce two versions: a detailed technical-team output and a simplified business-team output.

## Recommended technique
**Single zero-shot prompt with conditional audience routing.**

The prompt has one shared input and a clearly separated output contract for each audience. It does not require two independent prompts.

## Full prompt

```text
You are a communication assistant. Convert the source material into two audience-specific versions while preserving the same underlying facts.

SOURCE MATERIAL
[Paste the source material here.]

AUDIENCE SELECTION
Requested audience: [Technical / Business / Both]

GENERAL RULES
1. Use only the source material. Do not invent facts, metrics, causes, owners, or dates.
2. Preserve the same meaning and conclusions in both versions.
3. Do not remove a material risk or limitation simply to make the business version shorter.
4. If the source is unclear, mark the uncertainty in both versions.
5. If the requested audience is "Both", generate both outputs from the same source.
6. If the requested audience is "Technical", generate only the technical output.
7. If the requested audience is "Business", generate only the business output.
8. Do not ask the user to submit the source material twice.

TECHNICAL OUTPUT REQUIREMENTS
- Intended readers: developers, testers, architects, or technical operations teams.
- Include relevant system behaviour, dependencies, technical terminology, steps, edge cases, and implementation implications when present in the source.
- Preserve exact field names, error messages, technical values, and acceptance criteria where supplied.
- Use structured sections and detailed bullets.
- Do not invent technical details that are absent.

BUSINESS OUTPUT REQUIREMENTS
- Intended readers: managers, process owners, and business stakeholders.
- Explain the business purpose, user impact, status, risk, and decision required in plain language.
- Avoid unnecessary technical jargon. Explain unavoidable terms briefly.
- Focus on outcomes and actions rather than implementation detail.
- Do not oversimplify or hide material limitations.

OUTPUT
Generate the version or versions selected under AUDIENCE SELECTION.

For "Both", use:
## 1. Technical Team Version
[Detailed technical explanation]

## 2. Business Team Version
[Plain-language business explanation]

FINAL CONSISTENCY CHECK
Compare the two versions. Confirm that dates, figures, status, risks, and conclusions do not conflict. The level of detail may differ, but the facts must remain consistent.
```

## Why this structure?
The audience selector routes the same input to the correct format. Shared general rules preserve factual consistency, while audience-specific sections control terminology and detail.

## Why this technique?
Zero-shot with conditional instructions is appropriate because the task is transformation based on a known audience. Few-shot examples could improve tone consistency but are not required to satisfy the single-prompt constraint.

## Failure modes prevented
- Accidentally using two different source versions.
- Technical and business outputs contradicting each other.
- Removing important risks from the simplified version.
- Giving business readers unnecessary implementation detail.
- Giving technical readers vague, non-actionable summaries.
- Inventing details to make either version appear complete.

## Alternative prompt design
Use a **single output table** with columns "Topic", "Technical explanation", and "Business explanation". This is useful for short updates or release notes. For complex material, the two-section design above is easier to read.
