# Q12 — When the Model Is Wrong

## Objective
Re-evaluate a confident but potentially incorrect answer, identify weak assumptions, and produce a corrected answer based on evidence.

## Recommended technique
**Evidence-led verification and controlled re-evaluation.**

The model is asked to challenge the answer rather than defend it. Where external verification is unavailable, it must disclose that limitation.

## Full prompt

```text
You are reviewing a previous answer that may be incorrect. Your goal is to verify it, not defend it.

ORIGINAL QUESTION
[Paste the original question.]

PREVIOUS ANSWER
[Paste the answer that may be wrong.]

AVAILABLE EVIDENCE / SOURCE MATERIAL
[Paste the relevant documents, data, references, or source excerpts.]

RE-EVALUATION RULES
1. Treat the previous answer as an unverified claim, even if it sounds confident.
2. Break it into individual factual claims.
3. Check each claim against the supplied evidence. If web or other tools are available and authorised, use reliable sources and cite them; otherwise state that external verification was not performed.
4. Identify assumptions, missing evidence, outdated information, contradictions, and reasoning gaps.
5. Do not replace one unsupported claim with another.
6. If a claim cannot be verified, label it "Unverified" or "Insufficient evidence".
7. If the evidence supports the previous answer, say so; do not change it merely to appear critical.
8. If the evidence contradicts the previous answer, explain the contradiction and correct it.
9. If the correct answer cannot be determined, state what additional evidence is required.
10. Do not claim that the answer is verified unless the relevant evidence has actually been checked.

OUTPUT
A. Claim-by-claim review
   Table columns:
   - Claim from previous answer
   - Evidence available
   - Assessment (Supported / Contradicted / Unverified)
   - Weak assumption or issue

B. Main error sources
   Identify any unsupported assumptions, misread data, outdated facts, calculation errors, or omitted context.

C. Corrected answer
   Provide the best-supported answer to the original question. Preserve uncertainty where necessary.

D. What remains unknown
   List any unresolved points and the evidence needed to resolve them.

FINAL CHECK
Ensure the corrected answer is supported by evidence and does not repeat claims identified as contradicted or unverified.
```

## Why this structure?
The claim-by-claim review makes it harder to overlook a specific error. The prompt separates diagnosis of the error from the corrected answer and preserves unresolved unknowns.

## Why this technique?
Controlled re-evaluation is more suitable than asking the model to "think harder". It requires evidence checks and explicit claim status. If tools are available, verification can use external sources; otherwise, the model must be transparent about its limits.

## Failure modes prevented
- Defending an earlier answer because it was stated confidently.
- Replacing one hallucination with another.
- Failing to identify which claim is wrong.
- Treating unavailable evidence as confirmation.
- Claiming external verification when no source was checked.

## Alternative prompt design
Use an **independent reviewer prompt** in a separate model call. Provide the original question and evidence, but withhold the previous answer until the reviewer has produced an independent answer. Then compare the two answers claim by claim. This can reduce anchoring on the original response.
