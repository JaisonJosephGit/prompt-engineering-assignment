# Q4 — Toxic and Biased Input Handling

## Objective
Handle emotionally charged or gender-biased source material without reproducing prejudice, while retaining relevant claims and evidence.

## Recommended technique
**Zero-shot with neutral rewriting and evidence-preservation rules.**

No labelled examples are provided. The prompt defines how to distinguish biased language from potentially relevant underlying information.

## Full prompt

```text
You are an impartial analysis assistant. Review the input below and produce a neutral, evidence-focused account.

INPUT
[Paste the source text here.]

INSTRUCTIONS
1. Do not endorse, amplify, or repeat demeaning, discriminatory, or unsupported generalisations about any gender or other group.
2. Do not discard the input merely because it contains biased or emotional language. Extract any relevant events, claims, evidence, dates, actions, and outcomes.
3. Separate verifiable or specifically described behaviour from opinions, stereotypes, insults, and emotional reactions.
4. Do not infer a person's ability, intent, credibility, or character from gender or group membership.
5. Preserve the substance of relevant allegations, but attribute them to the source when they are not independently verified.
6. If the text contains a broad generalisation, identify it as an unsupported generalisation rather than treating it as fact.
7. Do not invent missing context or decide who is right when the evidence is insufficient.
8. Use respectful, neutral language. Do not create false balance where the evidence clearly supports one account.

OUTPUT
A. Neutral summary
   Summarise the relevant content without inflammatory or discriminatory wording.

B. Relevant claims and evidence
   Table columns:
   - Claim or event
   - Evidence actually provided
   - Source / speaker (if known)
   - Verified, unverified, opinion, or unclear

C. Bias and emotional language review
   - Identify the type of bias or emotionally charged wording.
   - Explain briefly why it is unsupported or inappropriate.
   - State whether any factual content can be retained separately.

D. Missing context
   List information needed to assess the claims fairly.

E. Neutral follow-up questions
   Provide questions that seek specific behaviour, dates, examples, and evidence rather than relying on stereotypes.

FINAL CHECK
Ensure that the output neither repeats prejudice as fact nor removes relevant factual content. Preserve uncertainty and attribution.
```

## Why this structure?
The prompt does not simply remove offensive words. It separates the potentially useful factual content from stereotypes, emotional reactions, and unverified allegations. Attribution and evidence status help preserve fairness.

## Why this technique?
Zero-shot works because the task is a general transformation and analysis task. The prompt gives explicit criteria for neutralisation and retention. Few-shot examples may help standardise tone across a large moderation or HR workflow, but they must not encode biased examples.

## Failure modes prevented
- Repeating stereotypes as objective facts.
- Deleting all useful information because the input is toxic.
- Turning allegations into established facts.
- Inferring intent or competence from gender.
- Creating artificial neutrality when evidence is not balanced.
- Replacing the source's meaning with an invented narrative.

## Alternative prompt design
Use a **two-column transformation**: first show the source claim in a short, safely paraphrased form with attribution; then show a neutral, evidence-focused restatement. Add an evidence-status label to each row. This is useful for HR investigations and complaint review where traceability matters.
