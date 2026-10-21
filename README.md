# NextMove: a job & internship tracker

A tracker built for MSBA students juggling a lot of applications at once. It starts from the Career Services *Job and Internship Search Guide* spreadsheet and turns it into a tool that tells you **what to work on today**.

**Live app:** https://carlywaldeck.github.io/job-tracker/ (after GitHub Pages is turned on, see below)

## Who it's for

A graduate student tracking 10 to 50 opportunities across saved postings, applications, interviews, and offers, who keeps losing track of deadlines, follow-ups, and thank-you notes.

## What it does

### Essentials
| Requirement | Where |
|---|---|
| Add and edit opportunities (company, title, link, location, work arrangement, deadline, notes) | **+ Add opportunity**, or click any card/row |
| Track stage: Saved, Applied, Interviewing, Offer, Rejected, Withdrawn | Stage field, Board columns |
| Next action + due date | "Stage and next step" section of the form |
| Search, sort, filter | **All opportunities** tab (search, stage, work arrangement, interest; sort by deadline, next step, company, interest, stage, recently updated) |
| Keep your data | Saved automatically in your browser's local storage. The footer and **Import / Export** say exactly where it lives. |

### Improvements
1. **"What should I do today?" view.** Pulls together your next steps plus automatic reminders: postings closing in the next 2 weeks, a follow-up 14 days after you apply with no reply (the rule from the Career Services guide), thank-you notes after an interview, and interview prep in the week before. Grouped into Overdue, Due today, Next 7 days. Check a box to complete it; the tool then asks for the next step.
2. **Kanban board.** Drag cards between stages (or use the dropdown on mobile). Moving to Applied stamps the date and starts the follow-up clock; moving to Interviewing asks for the interview date.
3. **Dashboard.** Open opportunities, applications sent, interview rate, offers, pipeline by stage, applications per week, upcoming dates, and work-arrangement mix.
4. **Import / export.** JSON backup, CSV export for Excel/Sheets, and CSV import that understands the original Career Services spreadsheet's columns (save it as CSV, then import).
5. **Paste a job description.** Fills in title, company, location, work arrangement, deadline, and link. *This is rule-based text matching that runs in the browser, not AI*, and it's labeled that way in the app.
6. Also: interest level (high/medium/low) used to rank tasks, resume/cover-letter version sent, network contact, stage history, undo on moves and deletes.

## Where the data is stored

Everything is saved in the browser's `localStorage` on the device you use. No account, no server. Clearing browser data or switching computers loses it, so use **Import / Export → Download backup** to keep a copy or move it.

The app opens with example opportunities (dates are relative to today, so the demo always looks current). Click **Clear examples** to start fresh.

## Running it

It's one file, no build step. Open `index.html` in a browser, or use GitHub Pages:

1. Repo **Settings → Pages**
2. Source: **Deploy from a branch**, branch **main**, folder **/ (root)**, Save
3. After a minute it's live at `https://carlywaldeck.github.io/job-tracker/`

## Two-minute demo script

1. **Who it's for** (15s): MSBA students with 20+ applications; the spreadsheet tells you what happened, not what to do next.
2. **Add and track** (30s): + Add opportunity → paste a job description → Extract details → set a next action → Add. Show it on the Board, drag it to Applied.
3. **Strongest improvements** (45s): the Today view (overdue follow-up, thank-you reminder, deadline closing soon; check one off and set the next step) and the Board/Dashboard.
4. **Deciding what's next** (15s): Today's focus count, "Missing a next step" list, postings closing soon.
5. **What works / what's next** (15s): all of the above works now; next we'd add cloud sync, calendar export, and AI-written follow-up drafts.

## Ideas for next steps
- Calendar (.ics) export for deadlines and interviews
- Networking section with multiple contacts and conversation logs per opportunity
- Interview question bank organized by role
- Optional AI follow-up email drafts (would need an API key)
