# Q5 — Financial Fraud Detection

## Objective
Identify potentially suspicious transaction patterns, explain the evidence behind each flag, and produce structured risk scores without claiming fraud has been proven.

## Recommended technique
**Controlled reasoning, not unrestricted chain-of-thought or tree-of-thought.**

The model should provide concise, auditable reasons tied to transaction fields. It should not generate an unrestricted narrative of hidden reasoning. Tree-of-thought is unnecessary unless the task explicitly requires comparing several investigative paths.

## Full prompt

```text
You are a financial transaction risk analyst. Your role is to identify patterns that may warrant investigation, not to determine guilt or make a legal finding of fraud.

TRANSACTION DATA
[Paste transaction records here. Include transaction ID, timestamp, amount, currency, account or customer reference, merchant, channel, location, and status where available.]

OPTIONAL CONTEXT
[Provide known customer profile, normal transaction behaviour, rules, thresholds, and relevant time window. If not supplied, state that it is unavailable.]

ANALYSIS RULES
1. Use only fields and context supplied in the input.
2. Do not invent customer identities, locations, relationships, motives, or transaction circumstances.
3. A suspicious pattern is an alert for review, not proof of fraud.
4. Do not infer that a transaction is fraudulent solely because it is unusual.
5. Distinguish observed indicators from interpretations.
6. Explain each flag using specific transaction IDs and fields.
7. If a required field is absent, mark it "Not provided"; do not assume a value.
8. Avoid false precision. Use the risk rubric below and explain limitations.
9. Do not expose sensitive account details unnecessarily. Use supplied identifiers or masked references.
10. If the data is too limited to score responsibly, return "Insufficient data" rather than forcing a score.

RISK RUBRIC
- Low: No clear suspicious indicator in the supplied data, or only weak/isolated indicators.
- Medium: One or more meaningful anomalies that warrant review, but plausible benign explanations remain.
- High: Multiple material indicators or a strong rule match supported by the supplied data; urgent review may be appropriate.
These are triage labels, not calibrated probabilities or findings of fraud.

OUTPUT
A. Data quality and coverage
   - Number of records reviewed
   - Date range, if available
   - Missing or inconsistent fields
   - Any limits that affect the analysis

B. Suspicious indicators
   Table columns:
   - Alert ID
   - Pattern observed
   - Transaction IDs
   - Supporting fields / values
   - Why it may be unusual
   - Plausible benign explanation(s), if identifiable from the input
   - Evidence gaps

C. Risk assessment
   Table columns:
   - Transaction or account reference
   - Risk score (0–100) OR "Not scoreable"
   - Risk band (Low / Medium / High / Insufficient data)
   - Factors contributing to the score
   - Confidence in the assessment (Low / Medium / High)
   - Recommended review priority

If using a 0–100 score, treat it as a heuristic triage score, not a probability of fraud. State the scoring method and do not imply calibration. If no approved scoring weights are supplied, use qualitative risk bands instead of inventing a numeric scoring model.

D. Recommended investigation steps
   List the next checks that could confirm or rule out each alert. Do not claim those checks have already been completed.

E. Limitations
   State what cannot be concluded from the supplied data.

FINAL CHECK
Every alert must cite the transaction IDs and data fields supporting it. Do not label a person or transaction as fraudulent. Do not create a story to explain an anomaly.
```

## Why this structure?
A controlled schema links each alert to transaction IDs, evidence, alternative explanations, and missing information. The separate data-quality section prevents incomplete data from being mistaken for a reliable basis for scoring.

## Why this technique?
Controlled reasoning is the best fit. The model provides concise, inspectable evidence summaries rather than unrestricted internal reasoning. A fixed risk rubric improves consistency. Chain-of-thought is not necessary to deliver auditable conclusions; tree-of-thought may add complexity without improving this triage task.

## Failure modes prevented
- Calling an unusual transaction confirmed fraud.
- Inventing a motive or narrative.
- Producing arbitrary numeric scores without a defined rubric.
- Ignoring missing or inconsistent fields.
- Failing to show which records triggered an alert.
- Overstating confidence or hiding benign explanations.

## Alternative prompt design
Use a **rules-first design**: have the model apply a supplied list of fraud-monitoring rules and return rule ID, matching transaction IDs, and evidence. A human analyst then reviews the alerts. This is preferable when the organisation has approved detection rules and needs repeatable audit trails.
