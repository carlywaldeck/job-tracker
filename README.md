# NextMove: a job tracker built around your resume

A job and internship tracker for MSBA students. Upload your resume, save jobs, and NextMove scores how qualified you are for each one from 1 to 100, helps you tailor your resume to each posting, and shows everything on one dashboard.

**Live app:** https://carlywaldeck.github.io/job-tracker/. Anyone can use it with no sign-up. Each person's data, including their resume, stays private in their own browser.

## How it works

1. **Start with your resume.** Upload a PDF, Word, or .txt file, or try the sample resume. NextMove reads your skills, years of experience, and degree in the browser. You check them and save.
2. **Add a job.** Paste the posting. NextMove fills in the company, title, location, work arrangement, deadline, and link, and shows your score right away.
3. **Use the dashboard.** It shows your average match score, open jobs, applications sent, interviews, your to-do list, your pipeline by status, and your best matches to apply to.
4. **Open a job** to see why it scored what it did, tailor your resume for it, and keep notes.

## Assignment essentials

| Requirement | Where |
|---|---|
| Add and edit opportunities (company, title, link, location/work arrangement, deadline, notes) | **+ Add a job**, or **Edit** on any job |
| Track status: Saved, Applied, Interviewing, Offer, Rejected, Withdrawn | Status dropdown on the Jobs list and on each job page |
| Next action + due date | "Your next step" and "Do it by" in the job form. They show up in the dashboard's To do list. |
| Search, sort, filter | Jobs tab: search, status filter, and sort (highest score, deadline, company, recently updated). Clicking a pipeline bar filters too. |
| Keep your work | Saved automatically in the browser's `localStorage`. The footer says where the data lives. |

## Our improvements

1. **Qualification score from 1 to 100 (machine learning, in the browser).** Each job gets a score with a breakdown:
   - Skills the posting asks for (45 pts): required skills count fully, preferred skills count half.
   - Resume wording vs. the posting (30 pts): TF-IDF cosine similarity between your resume and the posting.
   - Years of experience (15 pts): years the posting asks for vs. years estimated from your resume's dates.
   - Education (10 pts): the degree the posting asks for vs. yours.

   It also lists missing skills and posting words your resume doesn't use. The app labels it as an estimate of fit, not a hiring prediction.
2. **Resume tailoring with AI (Claude).** On any job, "Tailor my resume" sends your resume and the posting to Claude, which returns a tailored summary, rewritten bullets, skills to add if true, and gaps to address. It is told never to invent experience. It needs the user's own Anthropic API key, stored only in their browser. Without a key, users still get **Quick suggestions** clearly labeled *rule-based, not AI*.
3. **Dashboard and to-dos.** Automatic reminders: apply before a posting closes, follow up 14 days after applying (the Career Services guide's rule), and tailor your resume for saved jobs.

## Demo script (2 minutes)

1. **Who it's for** (15s): MSBA students juggling many applications. The Career Services spreadsheet records what happened but doesn't tell you where you fit or what to do next.
2. **Setup** (20s): Upload a resume (or click "Try it with a sample resume and jobs"). Show the skills, years, and degree it found.
3. **Dashboard** (25s): Average score, pipeline, To do, best matches.
4. **Score** (25s): Open a job and walk through the breakdown and the missing skills.
5. **Tailor** (25s): Click Tailor my resume and show Claude's rewritten summary and bullets. Point out the rule-based fallback.
6. **Track** (10s): Add a job by pasting a posting, change a status, search and filter.

## Tech

A single `index.html` with no build step. PDF and Word resumes are read with pdf.js and mammoth, loaded from cdnjs only when you upload one. Scoring runs in plain JavaScript in the browser. AI tailoring calls the Anthropic Messages API (`claude-opus-5-5`) directly from the browser with the user's key. Data is stored in `localStorage`.
