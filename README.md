# NextMove: a job & internship tracker

A job tracker for MSBA students managing lots of applications at once. It starts from the Career Services *Job and Internship Search Guide* spreadsheet and turns it into a tool that tells you **what to work on today** and **how well your resume fits each job**.

**Live app:** https://carlywaldeck.github.io/job-tracker/. Anyone can use it with no sign-up. Each person's data stays private in their own browser.

## How it works (no explanation needed)

The app has one home screen:

1. **Get started in 3 steps.** New users see: upload your resume, add a job, come back to your to-do list. The guide goes away once both are done.
2. **To do.** Overdue and upcoming tasks, most urgent first. Check the circle when a task is done.
3. **My jobs.** Every job you are tracking. Change a job's status right in the list, filter by status, search, and sort.

Two more tabs: **Board** (drag jobs between stages) and **Insights** (your numbers, plus tips on why you might not be hearing back).

## Assignment checklist

| Requirement | Where |
|---|---|
| Add and edit jobs (company, title, link, location, work arrangement, deadline, notes) | **+ Add a job**, or **Open** on any row |
| Track status: Saved, Applied, Interviewing, Offer, Rejected, Withdrawn | Status dropdown on each row, or drag on the Board |
| Next action + due date | "Status and next step" in the form. Rows without a next step show "+ Add next step". |
| Search, sort, filter | My jobs: search box, status filter buttons, sort by deadline, next step, company, recent, or best fit |
| Keep your data | Saved automatically in the browser. The footer says so, with a link to back up or move your data. |

## Improvements

1. **Resume upload and match.** Upload a PDF, Word, or .txt resume under **About me & resume**. It's read in the browser (pdf.js and mammoth) and fills in your name, skills, roles, and location. When you paste a job description, the app shows a **resume match %** and the skills the job asks for that are missing from your resume. *Keyword matching, not AI*, and labeled that way.
2. **To-do list ("What should I do today?").** Your next steps plus automatic reminders: postings closing within 2 weeks, a follow-up 14 days after applying (the Career Services guide's rule), thank-you notes after interviews, and interview prep in the week before.
3. **Personalized.** Your profile (roles, places, work style, internship vs. full-time, weekly goal) drives a greeting, **Strong fit** tags, a "Best fit for me" sort, and a weekly application goal.
4. **"Why you might not be hearing back."** Rule-based tips from patterns in your own tracker: resume missing skills that jobs ask for, low interview rate, the same resume sent everywhere, no networking contact, applying near deadlines, interviews without offers, missing thank-yous or follow-ups, and applying to roles that don't fit your goals.
5. **Board.** Drag and drop between stages.
6. **Import / export.** JSON backup, CSV for Excel or Sheets, and CSV import that understands the original Career Services spreadsheet.
7. **Fill in from a job description.** Pulls out the title, company, location, work arrangement, deadline, and link (rule-based).

## Where the data is stored

Everything, including your resume text, is saved in the browser's `localStorage` on your device. No account, no server. Clearing browser data or switching computers loses it, so use **Back up or move your data** in the footer.

## Two-minute demo script

1. **Who it's for** (15s): MSBA students with 20+ applications. The spreadsheet records what happened, not what to do next.
2. **Set up** (25s): Upload a resume. Name, skills, and roles fill in automatically.
3. **Add and track** (30s): Click + Add a job, paste a job description, and click "Fill in the form from this". Show the resume match and the missing skills, then save. Change its status in the list.
4. **Deciding what to do next** (30s): Use the To do list to check off a follow-up, then show the Insights tips.
5. **What works and what's next** (20s): Everything shown works today. Next we'd add cloud sync, calendar export, and AI-written follow-up drafts.

## Running it

It's one file with no build step. Open `index.html` in a browser, or host it with GitHub Pages (Settings → Pages → Deploy from branch `main`, folder `/`).
