Output of `openspec --version`: 1.16.0

| # | Problem | Category | What the agent must guess / risk |
|---|---|---|---|
| R1 | "use AI to understand GitHub issues..." | Ambiguity, untestable | No output is defined any behavior satisfies the requirement |
| R2 | "right category (bug, feature, docs, etc.)" | Incompleteness | The category list is open ("etc.") the agent invents categories that may break downstream validation |
| R3 | "Severity should be determined accurately" | Ambiguity, untestable | Severity scale is undefined |
| R4 | "Important issues must be escalated quickly" | Ambiguity, untestable | "Important", "escalated" and "quickly" are undefined, so critical issues may be missed |
| R5 | "output the queue, SLA and whether to escalate as JSON" | Incompleteness | No JSON schema (field names, types, SLA units) consumers break on guessed key names |
| R6 | Req 05 omits confidence, but Req 10 requires it | Inconsistency | Unclear whether confidence belongs in the JSON output |
| R7 | "If the AI isn't sure, it should do its best" | Ambiguity, untestable | No threshold for "not sure" the agent may guess instead of sending to human review |
| R8 | "Bugs go to engineering. Bugs without repro steps go to the clarify queue. Critical issues always go to the on-call queue." | Inconsistency | A critical bug without repro steps matches all three rules. precedence is undefined |
| R9 | Req 07 defines routing only for bugs | Incompleteness | No destination for feature, docs and other categories |
| R10 | "The system should be fast and secure" | Untestable, missing non-functional concern | No latency target and no threat model cannot be verified |
| R11 | "Use the issue's labels and comments to improve accuracy" | Ambiguity, missing non-functional concern | Unclear how they are used, comments are untrusted input (prompt injection risk) |
| R12 | "Confidence should be between 0 and 100" | Ambiguity | Integer or float? How is it calibrated? Confidence in what (category, severity, overall)? |
| R13 | US-A: "so that things are better" | Ambiguity, untestable | No measurable success criterion |
| R14 | US-C: GPT-4, temperature 0, regex parser | Design-in-requirements, inconsistency | Locks in vendor and model, and a regex parser contradicts the JSON output requirement |
| R15 | US-D: "handle weird issues gracefully" | Ambiguity, untestable | "Weird" and "gracefully" are undefined |

**Requirements topics that are completely missing:**

1. Failure handling: model timeouts, rate limits, malformed output, GitHub API outages, retries.
2. Security and privacy: prompt-injection defense, sending private repo content to a third-party model, token management.
3. Quality evaluation and measurable targets: labeled test set, accuracy targets, cost and latency budgets.
