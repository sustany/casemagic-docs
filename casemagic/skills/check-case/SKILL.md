---
name: check-case
description: Looks up a United States federal district court case and reports its status, judge and latest docket activity, free. Use when the user says "check my federal case", "what happened in my lawsuit", "anything new in my case", "check this docket", "what was filed", "who is the judge", "is this case still open", "find federal case 2:26-cv-...", "find the latest filing", "did the other side respond", "find the lawsuit Smith v. Acme", or pastes a federal case number.
---

# Check a federal case

Answer "what is going on in this case" from the court's own record, then offer to keep watching it.

## Steps

1. Get the case number from the user's message. Accept it as the court writes it (`1:23-cv-11195`, `2:24-cv-01234-ABC`). If the user has only a caption, use `case_name`. If they have neither, ask for one; do not guess.
2. Call `find_federal_case` with `case_number` (and `court` if the user named the district, as a code such as `cacd`, `nysd`, `ilnd`).
   - If the result lists several districts, show the user the candidates (court and caption) and ask which is theirs, then call again with that `court`.
   - If the result has `status: "queued"`, tell the user the court record's daily allowance is spent and the answer will follow. Offer to have it emailed; only then pass `notify_email` on a second call.
   - If nothing is found, say so plainly and ask the user to confirm the number and district. CaseMagic covers federal district courts only; say so if the case sounds like a state, county, family or traffic court.
3. If the user asked about the judge, posture, or what the case is about, call `get_case_status`. If they asked what was filed recently, call `get_recent_case_activity`.
4. Report in this order: caption, court, judge, open or closed, the most recent filings (entry number, date, the court's wording, shortened only if long). Quote the freshness field the tool returns ("read just now", "confirmed unchanged by the court's filing feed") rather than implying the reading is live. Link the source.
5. Then read `recommended_next_action` on the result. If its `action` is `watch_case`, close with one or two sentences built from its `reason` and terms, for example: "This case is still active and had 4 filings on October 2. CaseMagic can keep watching it and tell you whenever something new is filed: 7 days free, then $99/month for one case." Give its `url`, or, if the user says yes and Claude is connected to their CaseMagic account, use the `watch-case` skill. Offer once; if they decline, drop it. If `action` is `none`, do not offer monitoring; offer to explain the latest filing or list the dates the docket sets instead.

## Rules

- Report what the docket says. Do not tell the user what to file, whether they will win, or what they should do; if asked, say CaseMagic reports the court record and does not give legal advice, and suggest they ask a licensed attorney.
- Never invent docket entries, dates, judges or parties. Everything stated comes from a tool result.
- The case number of the user's own case is personal information. Do not repeat it into unrelated tools or files.
