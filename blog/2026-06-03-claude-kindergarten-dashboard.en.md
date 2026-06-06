# A Non-Developer Built a Self-Updating School Dashboard With AI — Here's the Exact Process

My son Huy started kindergarten in Japan this June. By the end of the first week I had 23 pages of PDFs I hadn't fully read, a school app I'd set up wrong, a bus schedule I'd already gotten wrong once, and a wife who needed all the same information I was struggling to keep straight.

I'm not a developer. I don't write code. I work in a completely unrelated field.

I still built a dashboard. It updates itself when new school documents arrive. My wife and I can both check items off from our phones and see each other's changes in real time. It cost nothing to deploy and runs on free infrastructure.

This post is for anyone who has a workflow that's mostly manual and involves documents — and who has assumed "I'd need to hire someone to build this."

---

## The Problem (Which You Probably Recognize)

Japanese kindergartens run on paper. Or rather, on a hybrid of paper handouts, a school communication app (ours uses BusCatch), and occasional LINE messages. Every document needs to be read, understood, and acted on.

In our case there's an extra layer: my wife and I are Vietnamese. Our Japanese is functional, but reading dense school documents slowly and carefully is a different skill from daily conversation. And our son enrolled mid-year in June rather than April — which meant half the systems weren't set up for him, and we had to chase the teachers to verify whether his bus registration, lunch registration, and after-care registration had actually gone through.

What I needed was simple:

- This week's events
- Upcoming deadlines
- A daily bag-packing checklist my wife and I both update
- Uniform rules
- School contact numbers

All in one place. In Japanese. Updated when new school documents arrived. Free.

What I didn't want to do was build it — because I didn't know how.

---

## What I Actually Did

I described the problem to Claude Code — Anthropic's AI coding assistant — in plain English, the same way I'd explain it to a capable colleague.

*"I want a dashboard that shows this week's schedule, upcoming deadlines, a daily bag-packing checklist, uniform rules, and school contacts. My wife and I should be able to check items off and see each other's changes in real time."*

Claude asked a few clarifying questions, then built it: a single HTML file, deployable to GitHub Pages for free. Japanese UI. Mobile-friendly.

I didn't write a single line of code. I described the problem clearly. That was the whole job.

---

## The Moments Where It Nearly Fell Apart (And Didn't)

I want to be honest about this part, because the clean version of this story — "I described it, Claude built it, everything worked" — would be misleading.

### The checklist reset bug

We have a weekly checklist with deadlines attached to each item. Claude's first implementation reset all checkboxes every Sunday when the week changed. I noticed the flaw immediately:

*"If I check an item with a June 15 deadline on June 3, and you refresh the dashboard on June 8, it'll show as unchecked again. But I already did it."*

Claude agreed, redesigned it. Items now persist until the deadline actually passes — at which point I ask Claude to do a weekly refresh and it removes only the expired ones.

I didn't read the code. I understood the logic, and that was enough to catch the bug.

### GitHub blocked the push

To sync the checklist between our two phones, Claude used GitHub as a mini-database — a small JSON file that both devices read and write. This required an access token embedded in the page.

GitHub's push protection detected the token pattern in the code and rejected the upload. Claude had to squash the git history to remove the token from past commits, then rejoin it as a split string the scanner wouldn't flag.

I watched all of this happen. I understood none of it. It got fixed in about ten minutes.

### The session memory problem

Early on I kept having to re-explain context at the start of every session: Huy's class, his teachers, his bus times, the Drive folder where I drop school PDFs.

Claude Code has a file called `CLAUDE.md` that lives in the repository. Every new session reads it automatically. Once I had Claude write that file — with all the details about Huy, the school, the workflow — I never had to explain anything again.

---

## The Workflow Now

When the school sends home a new PDF:

1. I drop it in a Google Drive folder
2. I open Claude and say *"new document in Drive"*
3. Claude reads the file, extracts deadlines, items to prepare, uniform changes, and event dates
4. It updates the dashboard and pushes the changes to GitHub
5. The live site updates automatically

For the weekly refresh, I ask Claude on Sunday. It reads the current checklist state, removes items whose deadlines have passed, adds upcoming events from the calendar, and updates the "next week preview" section.

Total time each week: about five minutes.

---

## What It Can't Do

It's not fully automatic. Claude doesn't run in the background — it acts when I ask it to. If I drop a PDF in Drive and forget to mention it, nothing happens.

That's a real limitation. Fully automatic would require scheduled tasks and triggers that either cost money or involve setup I haven't bothered with. For now, one message on Sunday is easy enough.

---

## What I Actually Learned

I never learned what a GitHub SHA is or how base64 encoding works. I never read about API authentication. But I could describe what I wanted the system to *do*, notice when something was wrong, and explain *why* it was wrong in ordinary words.

That turned out to be the whole skill.

The tools shifted — Google Drive as a document inbox, GitHub as a deployment platform and sync backend, CLAUDE.md as session memory. But what made the thing work was just describing a problem precisely.

If you have a workflow that's mostly manual, mostly repetitive, and involves documents — you can probably build something like this. You don't need to know how to code. You need to know what you want, and you need to be able to say clearly when something isn't working.

Start there.

---

*The dashboard is live at [anhbn272.github.io/yochien](https://anhbn272.github.io/yochien). The source is public on GitHub.*
