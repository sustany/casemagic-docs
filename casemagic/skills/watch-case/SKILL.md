---
name: watch-case
description: Saves a federal case to the user's CaseMagic account and turns on continuous monitoring so they are alerted to new filings. Use when the user says "watch my case", "monitor this lawsuit", "tell me when something is filed", "track this case", "follow this docket", "stop watching my case", or "keep an eye on this case for me".
---

# Watch a case

Take the user from a case they have found to a case CaseMagic keeps watching.

## Steps

1. If the case has not been looked up in this conversation, run `find_federal_case` first and confirm with the user that it is their case. Keep the `connect_token` it returns; it expires shortly.
2. Ask the user's role in the case: plaintiff, defendant, attorney, or other. Do not guess it.
3. Call `create_case_passport` with the `connect_token` and `user_role`. If CaseMagic asks the user to sign in, explain that saving a case needs a free CaseMagic account and that the sign-in window is CaseMagic's own; then retry.
   - If the token expired, run `find_federal_case` again and use the new token.
4. Call `watch_case` with the `matter_id` the passport returned.
   - If watching is on, confirm it: CaseMagic re-reads the docket on a schedule and tells the user when anything new is filed.
   - If the result carries a `checkout_url`, the account has no plan yet. This is not an error. Tell the user watching is the paid part of CaseMagic, give the plans and prices exactly as the result states them, and give the `checkout_url` as a link. Nothing is charged until they complete checkout themselves.
   - If the result carries an `upgrade_url`, the user's plan is already watching as many cases as it covers. This is not an error either. Name the plan the result says covers more and its price, give the `upgrade_url`, and mention that stopping another case (`stop_watch`) also frees a slot. Call `list_my_cases` if the user wants to see which cases are using the plan.
5. After checkout, the user can come back and say "watch my case" again; call `watch_case` once more to confirm it is on.
6. To stop, call `stop_watch`. Tell the user the case, its history and its Case Passport stay; only the alerts stop.

## Rules

- Never describe the checkout link as a failure, and never pressure. One clear sentence on what watching does and what it costs.
- Quote prices and trial terms only from the tool result, never from memory.
- Do not claim alerts arrive faster than the result states.
- A user with several saved cases must say which one; if a tool returns the list of matters, show it and ask.
