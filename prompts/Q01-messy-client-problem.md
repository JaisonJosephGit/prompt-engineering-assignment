# Q1 — Consulting Case: Messy Client Problem

## Objective
Convert an unstructured telecom-client description about declining average revenue per user (ARPU) into testable hypotheses, identify missing information, and recommend next steps without inventing facts.

## Recommended technique
**Zero-shot with structured extraction and explicit uncertainty controls.**

No labelled examples are supplied. A zero-shot prompt is appropriate because the task is analytical rather than a narrowly defined classification task. The schema and evidence rules provide the required structure.

## Full prompt

```text
You are a careful business analyst supporting a telecom consulting team.

TASK
Analyse the client material provided below. The material may be unstructured, incomplete, ambiguous, or internally contradictory. The topic is a reported decline in average revenue per user (ARPU).

CLIENT MATERIAL
[Paste the client's paragraph, stakeholder comments, and any available notes here.]

RULES
1. Use only facts explicitly present in the supplied material.
2. Do not invent figures, dates, causes, customer segments, market conditions, or stakeholder positions.
3. Separate observed facts from stakeholder claims, assumptions, interpretations, and hypotheses.
4. If two statements conflict, show both statements and describe the conflict. Do not silently choose one.
5. Do not treat correlation as proof of causation.
6. Mark unsupported conclusions as "Not established by the input".
7. Use "Unknown" or "Not provided" for missing information. Do not fill gaps with guesses.
8. Assign each hypothesis a confidence label (Low, Medium, or High) based on the evidence in the input. Explain the evidence and uncertainty behind the label. Do not use numerical probabilities unless the input supports them.
9. Ask for the smallest set of additional data that would meaningfully distinguish between the hypotheses.

OUTPUT
A. Executive summary
   - State what the client appears to be reporting.
   - State the most important uncertainty.
   - Do not claim that a cause has been proven.

B. Evidence register
   Create a table with columns:
   - Item
   - Statement or data point
   - Type (fact / stakeholder claim / assumption / interpretation)
   - Source in the supplied material
   - Reliability or limitation

C. Problem hypotheses
   Create a table with:
   - Hypothesis ID
   - Possible explanation
   - Supporting evidence
   - Contradicting or missing evidence
   - Confidence (Low / Medium / High)
   - Data needed to test it

D. Contradictions and ambiguities
   List each conflict, the statements involved, and what clarification is required.

E. Missing data
   Group missing information under:
   - Revenue and ARPU trends
   - Subscriber/customer base
   - Product, plan, and usage mix
   - Churn, acquisition, and retention
   - Geography and customer segments
   - Time period and calculation methodology
   Include only categories relevant to the input; mark unavailable details as not provided.

F. Recommended next steps
   Give prioritised actions. For each action include its purpose, required owner or data source (if known), and expected output. If the owner is not known, write "Owner to be assigned".

G. Questions for the client
   Ask concise questions that resolve the highest-impact unknowns first.

FINAL CHECK
Before responding, verify that every factual statement is traceable to the supplied material, every unsupported point is labelled, contradictions remain visible, and no missing fact has been fabricated.
```

## Why this structure?
- The evidence register prevents stakeholder opinions from being presented as verified facts.
- Separate hypotheses make competing explanations visible instead of forcing one premature answer.
- A dedicated contradiction section prevents inconsistent input from being silently reconciled.
- The missing-data and next-step sections turn analysis into an actionable consulting plan.
- The final check reinforces traceability and uncertainty disclosure.

## Why this technique?
Zero-shot is suitable because there are no trusted examples to imitate. The prompt uses explicit instructions and a fixed output schema to guide the analysis. Few-shot examples could be added later if the consulting team adopts a standard hypothesis taxonomy.

## Failure modes prevented
- Hallucinating ARPU values, dates, or causes.
- Treating stakeholder opinion as fact.
- Ignoring contradictory statements.
- Claiming causation from weak evidence.
- Producing generic recommendations that are not tied to missing data.
- Hiding uncertainty behind confident wording.

## Alternative prompt design
Use a **two-stage prompt workflow**:
1. First prompt: extract only facts, claims, contradictions, and unknowns into JSON.
2. Second prompt: generate hypotheses and next steps using only the validated extraction.

This is preferable when source material is long or when auditability is especially important. The second stage should receive the extracted evidence and must not introduce new facts.
