# Q7 — Classification with Edge Cases

## Objective
Classify customer complaints into Billing, Network, Device, or Other, and compare zero-shot and few-shot approaches for overlapping edge cases.

## Recommended technique
**Both zero-shot and few-shot classification.**

Zero-shot establishes a baseline. Few-shot adds examples that demonstrate how to handle ambiguous or multi-topic complaints.

## Zero-shot prompt

```text
You are a customer-support complaint classifier for a telecom company.

CLASS LABELS
- Billing: Charges, invoices, payment failures, refunds, plan fees, unexpected deductions, or billing disputes.
- Network: Signal, coverage, call drops, mobile data connectivity, broadband speed, outages, or network availability.
- Device: Handset, router, SIM hardware compatibility, device faults, setup, or device-specific performance.
- Other: Complaints that do not fit the above categories or are too unclear to classify.

COMPLAINT
[Paste one complaint here.]

RULES
1. Choose exactly one primary category.
2. Classify by the main issue the customer wants resolved, not by every keyword mentioned.
3. If multiple issues appear, select the issue that is most central to the complaint. Mention secondary issues separately.
4. If the complaint is too vague to determine a category, choose Other and explain what clarification is needed.
5. Do not invent facts or infer an issue that is not stated.

OUTPUT
Return valid JSON only:
{
  "primary_category": "Billing | Network | Device | Other",
  "secondary_categories": [],
  "reason": "One concise sentence based on the complaint",
  "needs_clarification": true,
  "clarification_question": "Question, or empty string if not needed"
}
```

## Few-shot prompt

```text
You are a customer-support complaint classifier for a telecom company.

CLASS LABELS
- Billing: Charges, invoices, payment failures, refunds, plan fees, unexpected deductions, or billing disputes.
- Network: Signal, coverage, call drops, mobile data connectivity, broadband speed, outages, or network availability.
- Device: Handset, router, SIM hardware compatibility, device faults, setup, or device-specific performance.
- Other: Complaints that do not fit the above categories or are too unclear to classify.

EXAMPLES
Complaint: "My bill includes a roaming charge, but I did not travel."
Output: Billing. Reason: The customer disputes a charge on the bill.

Complaint: "I paid for the data pack, but mobile data keeps disconnecting in my area."
Output: Network. Reason: The main unresolved issue is connectivity; the payment mention is context.

Complaint: "My phone restarts whenever I connect it to the charger."
Output: Device. Reason: The issue concerns handset behaviour.

Complaint: "The invoice is correct, but I cannot get a signal at home."
Output: Network. Reason: The customer explicitly identifies signal availability as the problem.

Complaint: "I need help changing the name on my account."
Output: Other. Reason: The request is an account-maintenance issue, not one of the defined complaint categories.

Complaint: "The internet is slow on every device, but it works normally when I use another provider."
Output: Network. Reason: The described issue concerns the service connection rather than one device.

Complaint: "My router will not power on, although the broadband line is active."
Output: Device. Reason: The router hardware is the reported fault.

Complaint: "You charged me twice and now my service is disconnected."
Output: Billing. Reason: The duplicate charge is the stated issue and may be related to the disconnection; flag the service impact as secondary.

NOW CLASSIFY
Complaint:
[Paste one complaint here.]

RULES
1. Choose exactly one primary category.
2. Use the examples to guide boundary decisions, but do not force a match when the complaint is materially different.
3. Mention secondary issues separately.
4. If unclear, choose Other and ask a concise clarification question.
5. Do not invent facts.

OUTPUT
Return valid JSON only:
{
  "primary_category": "Billing | Network | Device | Other",
  "secondary_categories": [],
  "reason": "One concise sentence based on the complaint",
  "needs_clarification": true,
  "clarification_question": "Question, or empty string if not needed"
}
```

## Why zero-shot?
- It is simple and quick to deploy.
- It works when category definitions are clear and examples are unavailable.
- It may be sufficient for straightforward complaints.
- It can be inconsistent on overlapping cases because the model has no demonstrations of the team's preferred boundary decisions.

## Why few-shot helps
Examples demonstrate how the categories should be applied when a complaint mentions multiple topics. They make the intended precedence and treatment of secondary issues more consistent.

## When few-shot breaks
- Examples are unrepresentative or biased.
- Examples contradict the written definitions.
- Too many examples consume context and distract from the current complaint.
- The model overfits to surface wording rather than the underlying issue.
- New complaint types are not represented.
- Examples contain incorrect labels.

## Failure modes prevented
- Returning several competing primary labels.
- Classifying by a keyword while missing the main complaint.
- Losing secondary issues.
- Guessing when a complaint is unclear.
- Returning inconsistent output formats.

## Alternative prompt design
Use **hierarchical classification**: first decide whether the complaint concerns account/charges, connectivity, equipment, or something else; then map the result to the four required labels. This can be easier to audit when category overlap is frequent. A human review queue can handle low-confidence or unclear complaints.
