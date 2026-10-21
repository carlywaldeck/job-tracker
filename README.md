# NextMove: a job tracker built around you and your resume

A simple job and internship tracker for MSBA students. Upload your resume, save the jobs you're interested in, and NextMove tells you what to do next and how well you match each job.

**Live app:** https://carlywaldeck.github.io/job-tracker/. Anyone can use it with no sign-up. Each person's data, including their resume, stays private in their own browser.

## How it works

1. **Start with your resume.** Upload a PDF, Word, or .txt file. NextMove reads it in the browser, greets you by name, and shows the skills it found. You confirm them or edit them.
2. **Add a job.** Paste the job posting. NextMove fills in the company, title, location, work arrangement, deadline, and link, and shows your resume match and any missing skills.
3. **Do your next steps.** The home screen lists what to do, most urgent first. Tap the circle when a step is done.

## Assignment essentials

| Requirement | Where |
|---|---|
| Add and edit opportunities (company, title, link, location/work arrangement, deadline, notes) | **+ Add a job**, or click any job |
| Track progress: Saved, Applied, Interviewing, Offer, Rejected, Withdrawn | Status dropdown on each job |
| Next action + due date | "Your next step" and "Do it by" in the job form |
| Search, sort, filter | Search box, status filter, and sort (best match, deadline, company, recently updated) above Your jobs |
| Keep your work | Saved automatically in the browser's local storage. The footer says where the data lives. |

## Our two improvements

1. **"Your next steps," a personal to-do list.** It answers "What should I work on today?" It combines your own next steps with automatic reminders: apply before a posting closes, follow up 14 days after applying (the Career Services guide's rule), and tailor your resume when a job asks for skills it doesn't list.
2. **Resume match.** Each job shows *Great match*, *Good match*, or *Stretch* with a percentage, based on how many of the skills in the posting appear on your resume. The job form lists the missing skills. You can sort jobs by best match. *This is keyword matching, not AI*, and the app labels it that way.

## Demo script (2 minutes)

1. **Who it's for** (15s): MSBA students juggling many applications. The Career Services spreadsheet records what happened but doesn't tell you what to do next.
2. **Personal setup** (25s): Upload a resume. The app greets you by name and shows your skills.
3. **Add and track** (35s): Click + Add a job, paste a posting, and click "Fill in the details". Show the match and the missing skills, then save. Change its status in the list.
4. **What to do next** (25s): Go through Your next steps and check one off.
5. **What's next** (20s): Everything shown works now. Next we'd add calendar reminders, cloud sync, and AI-written follow-up emails.

## Tech

A single `index.html` with no build step. PDF and Word resumes are read with pdf.js and mammoth, loaded from cdnjs only when you upload one. Data is stored in `localStorage`.
