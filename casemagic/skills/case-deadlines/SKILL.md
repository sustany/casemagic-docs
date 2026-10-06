---
name: case-deadlines
description: Lists the dates a federal docket sets, such as response deadlines and hearings, and can save them as a calendar file. Use when the user asks "what are my deadlines", "when is my hearing", "when is the response due", "what dates are set in my case", "put my court dates on my calendar", or "make an .ics of my deadlines".
---

# Case deadlines and calendar file

Report every date the docket states, with its source, and optionally write them to a calendar file the user can import.

## Steps

1. Identify the case and call `get_case_deadlines`.
2. If the case is saved to the user's account, also call `get_case_mail` and include any dates it surfaces from correspondence, labelled as the sender's words rather than an order of the court.
3. Present a table sorted by date: date, days away, what it is, the source entry number, and the quoted text. Put computed deadlines (FRCP 50/52/59, FRAP 4(a)) in a separate group showing the rule and day count the tool returns, with its caveat.
4. State plainly what the list does not cover: deadlines that depend on a district's local rules, a judge's standing orders, or service dates the docket does not record. An empty list means nothing is stated or computable, not that the user has no deadlines.
5. If the user wants a calendar, write an iCalendar file (`casemagic-<case-number>-dates.ics`) in the working folder:
   - `BEGIN:VCALENDAR`, `VERSION:2.0`, `PRODID:-//CaseMagic//Docket dates//EN`, `CALSCALE:GREGORIAN`.
   - One `VEVENT` per date: all-day `DTSTART;VALUE=DATE:YYYYMMDD`, a unique `UID` (`<case-number>-<entry>-<yyyymmdd>@casemagic.ai`), `DTSTAMP` in UTC, `SUMMARY` naming the case and the event, `DESCRIPTION` holding the quoted docket text, the entry number and "Verify against the court docket before relying on this date.", and `URL` set to the source link.
   - Add one `VALARM` per event that fires 3 days before (`TRIGGER:-P3D`, `ACTION:DISPLAY`).
   - Use CRLF line endings and fold lines longer than 75 octets.
   - Include only dates that came from the tools. Never add a date you computed yourself.
6. Tell the user where the file is and that it imports into Google Calendar, Outlook and Apple Calendar. Mention that dates set later will not appear in a file; watching the case is how they hear about new ones.

## Rules

- Never phrase a date as an instruction to file something. "The docket states responses are due 10/14/2026" is right; "you must respond by 10/14" is not.
- Do not compute deadlines from local rules or from service dates. Tell the user to confirm deadlines with the court or an attorney.
