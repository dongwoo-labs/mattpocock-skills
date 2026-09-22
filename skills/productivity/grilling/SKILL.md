---
name: grilling
description: Grill the user relentlessly about a plan, decision, or idea. Use when the user wants to stress-test their thinking, or uses any 'grill' trigger phrases.
---

Interview the user until you reach a shared understanding, but do not turn routine defaults into an interview. Map this as a **design tree**: every decision branches into the decisions that hang off it.

Summarize only changed decisions or assumptions relevant to this round. Use settled facts, ADRs, investigation results, and accepted recommendations without repeating them. Decide routine, reversible defaults; ask only about materially consequential, hard-to-reverse decisions or the user's explicit preference or authority.

Work the tree in **rounds**. The **frontier** is every unresolved owner decision whose prerequisites are already settled: the questions you can ask _now_ without guessing at answers you haven't heard yet. Ask the whole frontier in one round: number each question and give your recommended answer. Ask one question per decision, merge duplicates, and omit questions the agent can decide. Then wait for the user's answers before the next round. If the frontier contains no owner decision, state the assumptions and proceed without asking.

Format a round like so:

```
❓ **Q1** - **<question title>**: <question body, might be multiple paragraphs, including multiple choices>

➡️ <your recommended answer>

---

❓ **Q2** - **<question title>**: <question body, might be multiple paragraphs, including multiple choices>

➡️ <your recommended answer>
```

Each round the user answers reshapes the tree: settled decisions push the frontier outward and unblock questions that depended on them. Recompute the frontier and ask the next round. A question whose answer depends on another question still open in this round belongs to _later_ round, not this one. Never use Q1–Qn as a checklist: ask the minimum number of nonredundant questions needed to resolve genuine owner decisions, not low-stakes defaults.

Retrieve missing facts directly; delegate independent research when useful. Pending research is an unsettled prerequisite: only downstream questions wait; ask the rest of the frontier now. Put decisions to the user only when the settled record cannot responsibly determine them.

The interview is done when no consequential owner decision remains and material assumptions are visible. Confirm shared understanding with the user before acting on a newly proposed plan. A prior explicit acceptance of that same plan satisfies this gate; do not request it again. An empty frontier permits continuing the interview and authorized documentation, not silently starting implementation. An assessment-only request ends with the assessment.
