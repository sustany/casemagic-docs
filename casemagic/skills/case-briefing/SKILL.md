---
name: case-briefing
description: Catches the user up on their saved CaseMagic cases, reporting what changed since a given time across one or all of them. Use when the user asks "what changed in my case this week", "anything new since Friday", "catch me up on my case", "what happened across all my cases today", "load my case", or "give me a weekly case briefing".
---

# Case briefing

Summarize what moved in the user's saved cases since a point in time.

## Steps

1. Work out the start time from the user's words ("this week" means the most recent Monday 00:00 in the user's timezone; "since Friday" means that Friday 00:00) and convert it to an ISO-8601 timestamp. If no period is given, omit `since` to get the latest activity.
2. Call `get_case_updates` with `since`. With no `matter_id`, an account holding several cases gets a digest naming which moved.
   - If the account has no saved case, offer to find and save one (`check-case`, then `watch-case`).
3. For "load my case" or "catch me up", call `get_case_passport` for the full record: identity, parties, recent docket, correspondence and documents.
4. Write the briefing:
   - One line per case that moved: caption, court, how many new entries.
   - Under each, the new entries newest first with the court's wording, and any correspondence received (sender, subject, one-line gist).
   - A "Dates set" line for any date a new entry states.
   - Cases that did not move, listed in one line at the end.
5. If the user asks for a file, write the briefing as Markdown (`casemagic-briefing-<yyyy-mm-dd>.md`) in the working folder.
6. Offer to explain any new filing (`explain-filing`).

## Rules

- Report only what the tools return. Do not characterize a filing as good or bad for the user.
- If a case is saved but not being watched, say so once and offer `watch-case`; updates for an unwatched case may be stale.
