---
name: explain-filing
description: Explains a federal court filing or docket entry in plain English using the court's own text. Use when the user asks "what does this order mean", "explain the latest filing", "what did the judge rule", "what is docket entry 45", "read me the complaint", or "summarize the motion to dismiss".
---

# Explain a filing

Turn the court's wording into plain English without adding anything the record does not say.

## Steps

1. Identify the case (`case_number` and `court`, or `matter_id` for a case saved to the user's CaseMagic account) and the entry. "The latest" means omit `docket_number`.
2. Call `explain_docket_entry`. It returns the entry's exact text, whether a document is attached, the entries around it and the case posture.
3. If the case is saved to the account and the user wants what the document itself says, call `get_case_docket` to find the `document_id`, then `read_case_document`. Pass `next_offset` to keep reading long documents. If a document has no text, say so and give the PDF link if there is one; never describe the contents of a document you have not read.
4. Explain, in this shape:
   - **What it is**: the type of filing and who filed it, in one sentence.
   - **What it says**: the operative part, quoting the court's words for anything that sets a date, grants or denies something, or orders someone to act.
   - **Where it fits**: how it relates to the entries before it (for example, "this order rules on the motion filed at entry 32").
   - **What the record shows comes next**: only dates or events the docket itself states. If none are stated, say none are stated.
5. Offer one follow-up: the dates the docket sets (`case-deadlines`) or watching the case for the response (`watch-case`).

## Rules

- Explain what the filing says and does. Do not advise the user on what to do about it, predict outcomes, or draft a response; say that is a question for a licensed attorney.
- Define legal terms the first time they appear ("dismissed without prejudice means the case can be refiled").
- Keep quotes exact. Mark any paraphrase as a paraphrase.
