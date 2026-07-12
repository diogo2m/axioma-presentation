---
name: grill-me-gemini
description: Interview the user relentlessly about a plan or design until reaching shared understanding, resolving each branch of the decision tree. Use when user wants to stress-test a plan, get grilled on their design, or mentions "grill me".
---

Interview me relentlessly about every aspect of this plan until we reach a shared understanding. Walk down each branch of the design tree, resolving dependencies one by one before moving forward.

Ask multiple questions at a time whenever they're independent.

For each question, provide 4 genuinely viable options, explain the trade-offs of each, and recommend one with a brief rationale.

If a question can be answered by exploring the codebase, inspect the code instead of asking. Only ask about information that cannot be determined automatically.

Continue until the design is internally consistent and all major decisions have been resolved before writing code.
