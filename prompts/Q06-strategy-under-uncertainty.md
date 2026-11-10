# Q6 — Strategy Recommendation Under Uncertainty

## Objective
Assess whether a client should enter India's electric vehicle (EV) market by breaking the decision into sub-decisions, comparing scenarios, showing criteria, and presenting counterarguments.

## Recommended technique
**Structured decomposition with controlled scenario analysis.**

This is a broad strategic decision. The prompt requires evidence-based analysis and explicit assumptions rather than a one-line yes/no answer.

## Full prompt

```text
You are a strategy consultant advising a company considering entry into the electric vehicle (EV) market in India.

CLIENT CONTEXT
- Company and capabilities: [Insert]
- Target EV segment(s): [Insert, or state "Not specified"]
- Proposed business model: [Insert]
- Investment capacity and time horizon: [Insert]
- Existing customers, channels, suppliers, and capabilities: [Insert]
- Risk tolerance and strategic objectives: [Insert]
- Evidence or research supplied: [Insert]

DECISION QUESTION
Should the company enter the Indian EV market, and if so, in which segment, through what entry mode, and under what conditions?

RULES
1. Do not assume the company profile or its capabilities if not supplied.
2. Distinguish supplied facts, external evidence, assumptions, and analytical judgement.
3. If current market facts are required but not provided, list them as research needs. Do not invent current market size, growth rates, incentives, market shares, or regulations.
4. Compare more than one plausible scenario.
5. Include counterarguments and conditions that would change the recommendation.
6. Do not force a single recommendation if the evidence is insufficient. A conditional recommendation or "defer pending evidence" is acceptable.
7. Make decision criteria explicit and explain their relative importance. Do not invent numerical weights unless the client provides or approves them.

ANALYSIS
Evaluate these sub-decisions:
1. Market and segment attractiveness.
2. Customer needs and adoption barriers.
3. Competitive intensity and differentiation.
4. Technology, supply chain, and operational readiness.
5. Regulatory and policy dependencies.
6. Economics, investment requirements, and route to profitability.
7. Strategic fit with the company's capabilities.
8. Entry mode: build, buy, partner, pilot, or defer.

SCENARIOS
Assess at least:
- Upside scenario
- Base scenario
- Downside scenario

For each scenario, state the assumptions, implications, key risks, and signals that would indicate the scenario is emerging. Do not assign probabilities unless evidence supports them.

OUTPUT
A. Executive recommendation (short)
B. Decision criteria table: criterion, why it matters, evidence available, unknowns, assessment.
C. Segment and entry-mode comparison.
D. Scenario comparison table.
E. Counterarguments against the recommended option.
F. Conditions and decision gates: what must be true before investment.
G. Key information gaps and research plan.
H. Recommendation: Enter / Pilot / Partner / Defer / Do not enter, with rationale and confidence level.

FINAL CHECK
Ensure the recommendation follows from the stated criteria, includes a credible opposing view, and does not present assumptions as verified market facts.
```

## Why this structure?
The prompt decomposes a large strategic question into manageable decision areas. Scenario analysis addresses uncertainty, while decision gates turn the recommendation into a conditional and testable course of action.

## Why this technique?
Controlled decomposition is preferable to asking for an immediate answer. It encourages coverage of relevant dimensions without requiring the model to reveal unrestricted internal reasoning. Zero-shot can be used initially; few-shot examples are useful only if the organisation has an approved strategy assessment format.

## Failure modes prevented
- Giving a simplistic yes/no recommendation.
- Assuming the client's capabilities or budget.
- Using outdated or invented market statistics.
- Ignoring downside scenarios and counterarguments.
- Hiding the criteria behind an unexplained recommendation.
- Treating uncertain assumptions as facts.

## Alternative prompt design
Use a **decision matrix workshop prompt**. Ask the model to produce a list of decision criteria and evidence gaps only. Have stakeholders approve the criteria and weights, then run a second prompt to compare entry options using the approved matrix. This is stronger when the decision is high value or politically sensitive.
