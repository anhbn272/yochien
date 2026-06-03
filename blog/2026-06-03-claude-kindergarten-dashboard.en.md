# I Built a Kindergarten Dashboard Without Writing a Single Line of Code

My son Huy started kindergarten in Japan this June. Within the first week I had a folder full of PDFs, a school app I half-understood, a wife who needed the same information, and a bus schedule I kept getting wrong.

I'm not a developer. I work in a completely unrelated field. But I ended up building a synced, auto-updating web dashboard for all of it — and I want to explain how, because the process surprised me.

---

## The Problem

Japanese kindergartens run on paper. Or rather, they run on a hybrid of paper handouts, a school communication app (ours uses BusCatch), and occasional LINE messages. In our case there's an extra layer: my wife and I are Vietnamese, our Japanese is functional but not effortless, and our son enrolled mid-year in June rather than April — which meant half the systems weren't set up for him and we had to chase the teachers to verify everything.

What I needed was simple: one place to see the week's events, upcoming deadlines, uniform rules, and a shared checklist my wife and I could both check off. In Japanese. Updated when new school documents arrived.

What I didn't want to do was build it — because I didn't know how.

---

## Enter Claude Code

Claude Code is Anthropic's AI coding assistant. I'd heard of it but assumed it was for developers. Then I tried something: I just described what I wanted, in plain English, as if explaining to a very capable colleague.

I didn't write any code. I described the problem.

*"I want a dashboard that shows this week's schedule, upcoming deadlines, a daily bag-packing checklist, uniform rules, and school contacts. My wife and I should be able to check items off and see each other's changes in real time."*

Claude asked a few clarifying questions, then built it. A single HTML file, deployable to GitHub Pages for free. Japanese UI. Mobile-friendly. The whole thing.

---

## The Moments That Surprised Me

### 1. I caught a logic bug without understanding the code

We set up a weekly checklist — items with deadlines that you check off as you complete them. Claude's first implementation reset all checkboxes every Sunday when the week changed. I pointed out the flaw:

*"If I check an item with a June 15 deadline on June 3, and you refresh the dashboard on June 8, it'll show as unchecked again. But I already did it."*

Claude agreed immediately and redesigned it. Items now persist until the deadline actually passes — at which point I ask Claude to do a weekly refresh and it removes only the expired ones.

I didn't understand any of the code. But I understood the logic, and that was enough.

### 2. GitHub blocked a push because the code contained a secret

To sync the checklist between devices, Claude used GitHub as a mini-database — a small JSON file in the repo that both our phones read and write. This required an access token embedded in the page.

GitHub's push protection detected the token pattern in the code and blocked the commit. Claude had to squash the git history to remove the token from past commits, then rejoin it as a split string that GitHub's scanner wouldn't flag.

I watched this happen. I understood none of it. It got fixed.

### 3. "Persistent memory" across sessions

One thing I didn't expect: Claude Code supports a file called `CLAUDE.md` in your repository. Every time you start a new session, Claude reads it automatically. So I asked Claude to write one — documenting Huy's class, teachers, bus times, the Drive folder where I drop school PDFs, and the workflow for processing new documents.

Now every session starts with full context. I don't re-explain anything.

---

## The Workflow Now

When the school sends home a new PDF:

1. I drop it in a Google Drive folder
2. I open Claude and say *"new document in Drive"*
3. Claude reads the file, extracts deadlines, items to prepare, uniform changes, and event dates
4. It updates the dashboard and pushes the changes to GitHub
5. The live site updates automatically

For the weekly refresh, I ask Claude on Sunday. It reads the current checklist state, removes items whose deadlines have passed, adds upcoming events from the calendar, and updates the "next week preview" section.

---

## What It Can't Do (Yet)

It's not fully automatic. Claude doesn't run in the background — it acts when I ask it to. The weekly refresh happens because I remember to ask for it. If I drop a PDF in Drive and forget to mention it, nothing happens.

That's a real limitation. Fully automatic would require scheduled tasks and triggers that either cost money or involve setup complexity I haven't bothered with. For now, a Sunday prompt is easy enough.

---

## What This Actually Means

I think the interesting thing here isn't the dashboard. It's the interaction model.

I never learned what a GitHub SHA is or how base64 encoding works. I never read about API authentication. But I could describe what I wanted the system to *do*, notice when it did something wrong, and explain *why* it was wrong in plain terms.

That turned out to be enough.

The tools did change: Google Drive as a document inbox, GitHub as a deployment platform and sync backend, a persistent context file as session memory. But the skill that made it work was just describing a problem clearly.

If you have a workflow that's mostly manual, mostly repetitive, and involves documents — there's a good chance you can build something like this. You don't need to know how to code. You need to know what you want.

---

*The dashboard is live at [anhbn272.github.io/yochien](https://anhbn272.github.io/yochien). The source is public on GitHub.*
