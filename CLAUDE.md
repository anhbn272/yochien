# Huy's Kindergarten Dashboard

## Project overview
A single-page HTML dashboard (`index.html`) that tracks kindergarten info for Huy (グエン・ミン・フィー) at 鵜ノ木幼稚園. It is refreshed weekly and deployed via GitHub Pages.

## Language rules
- Dashboard content and UI: **Japanese**
- Chat with user: **English**

## Child details
- Name: グエン・ミン・フィー (Huy)
- Class: こいぬ組 (年少)
- Teachers: 小林先生 / 成岡紗那先生
- Enrollment number: No. 45
- Bus: きりんコース #7b — pickup 8:44 / Wed return 12:24 / Mon·Tue·Thu·Fri return 14:54
- Entry: June 2026 (not April — verify all system registrations with teachers)

## Google Drive
- Folder: **huy kun yochien** (ID: `1dJ5Jx60qUMr3A7O_L51h_iQP49QIzzxz`)
- Always re-read relevant Drive files when context is needed; never rely on memory alone
- When the user says "new document in Drive", search the folder for recently added files and process them

## Processing new documents
When reading any new school document, always extract in this order:
1. **Absolute deadlines** — date, time, action required
2. **Items to bring / prepare** — with dates they apply from
3. **Uniform / dress code changes**
4. **Event dates** — include whether attendance is required

Flag anything unusual immediately (e.g. schedule changes, items specific to Huy as a June enrollee).

## Dashboard update workflow
1. User drops a new PDF into the Drive folder and says "new document in Drive" (or names the file)
2. Read the file from Drive
3. Extract the four categories above
4. Update `index.html` accordingly — calendar, checklist, alerts, uniform tab, or reference tab as needed
5. Also update the 今週 (this week) section if the document affects the current or next week
6. Commit and push to branch `claude/coding-getting-started-MBhBg`

## Weekly refresh
The 今週 tab should reflect the current week. When asked to refresh for a new week:
- Update the week date range
- Pull in any deadlines or events from the calendar that fall within 7–14 days
- Update 来週の予告 (next week preview) accordingly

## Communication style
- Be direct — no unnecessary preamble
- Don't ask questions the user can't answer confidently
- Don't revisit already-decided things

## Key contacts
- School phone: 03-3750-3530 (call teachers 15:00–16:00 only)
- School doctor: Horikoshi Clinic 03-3735-3731
