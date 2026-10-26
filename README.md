# NextMove: a job tracker built around your resume

A job and internship tracker for MSBA students. Upload your resume, save jobs, and NextMove scores how qualified you are for each one from 1 to 100, helps you tailor your resume to each posting, and shows everything on one dashboard.

**Live app:** https://carlywaldeck.github.io/job-tracker/. Create an account to keep your jobs and resume on any device, or continue without an account to keep everything in this browser only.

## How it works

1. **Start with your resume.** Upload a PDF, Word, or .txt file, or try the sample resume. NextMove reads your skills, years of experience, and degree in the browser. You check them and save.
2. **Add a job.** Paste the posting into the dashboard's "Add a job" box. NextMove fills in the company, title, location, work arrangement, deadline, and link, and takes you straight to your score.
3. **Use the dashboard.** A "Get started" checklist guides new users. Then the dashboard shows this week's to-dos, your pipeline, and the saved jobs you're most qualified for.
4. **Track jobs on the board.** Drag a job between Saved, Applied, Interviewing, Offer, and Closed. A list view has filters and sorting.
5. **Open a job** to see why it scored what it did, tailor your resume for it, and keep notes.

## Assignment essentials

| Requirement | Where |
|---|---|
| Add and edit opportunities (company, title, link, location/work arrangement, deadline, notes) | **+ Add a job**, or **Edit** on any job |
| Track status: Saved, Applied, Interviewing, Offer, Rejected, Withdrawn | Drag cards on the Jobs board, or use the status dropdown in the list view and on each job page |
| Next action + due date | "Your next step" and "Do it by" in the job form. They show up in the dashboard's To do list. |
| Search, sort, filter | Jobs tab: search and sort on the board; the list view adds a status filter. Sort options: (highest score, deadline, company, recently updated). Clicking a pipeline bar filters too. |
| Keep your work | Saved to your account (Supabase) when signed in, or to the browser's `localStorage` without an account. The footer says where the data lives. |

## Our improvements

1. **Qualification score from 1 to 100 (machine learning, in the browser).** Each job gets a score with a breakdown:
   - Skills the posting asks for (45 pts): required skills count fully, preferred skills count half.
   - Wording match (30 pts): TF-IDF cosine similarity between your resume and the posting.
   - Years of experience (15 pts): years the posting asks for vs. years estimated from your resume's dates.
   - Education (10 pts): the degree the posting asks for vs. yours.

   **How to raise your score** lists the three changes worth the most points (for example "+9: add A/B testing to your resume, if you have it"). Clicking "I have this" adds the skill and re-scores instantly. The app labels the score as an estimate of fit, not a hiring prediction.
2. **Resume tailoring with AI (Claude).** On any job, "Tailor my resume" sends your resume and the posting to Claude, which returns a tailored summary, rewritten bullets, skills to add if true, and gaps to address. It is told never to invent experience. It needs the user's own Anthropic API key, stored only in their browser. Without a key, users still get **Quick suggestions** clearly labeled *rule-based, not AI*.
3. **A dashboard that does the spreadsheet's bookkeeping for you.** The Career Services sheet has columns for closing date, network connection, "heard back? reach out two weeks after closing", interview dates, and thank-you notes, but you have to check them yourself. NextMove turns them into reminders:
   - **This week:** to-dos grouped into Overdue, Today, Next 7 days, and Later. Each one is tagged Apply, Follow up (two weeks after the posting closes), Interview, Thank-you note (the day after an interview), or Your step.
   - **Pipeline:** how many jobs reached Applied, Interviewing, and Offer, and what share moved on from each stage.
   - **Ready to apply:** saved jobs ranked by match score, with the closing date, network contact, and one button (Tailor or Mark applied).
   - **Email drafts:** follow-up and thank-you to-dos have a "Draft the email" button. It fills in the job, date, contact, and your matching skills. With an API key, Claude personalizes it (labeled as AI). "Open in email app" and "I sent it" log it.
   - **Help from Career Services:** the same Resume Guide, Career Connections, Interview Guide, and counseling links the spreadsheet has.

## Demo script (2 minutes)

1. **Who it's for** (15s): MSBA students juggling many applications. The Career Services spreadsheet records what happened but doesn't tell you where you fit or what to do next.
2. **Setup** (20s): Upload a resume (or click "Try it with a sample resume and jobs"). Show the skills, years, and degree it found.
3. **Add a job** (20s): Paste a posting into the dashboard's Add a job box. It opens on the score.
4. **Score** (25s): Walk through the breakdown, then "How to raise your score". Click "I have this" and watch the score go up.
5. **Tailor** (20s): Click Tailor my resume and show Claude's rewritten summary and bullets. Point out the rule-based fallback.
6. **Track** (20s): On the Jobs board, drag the job to Applied. Back on the dashboard, open a thank-you to-do and click "Draft the email".

## Tech

A single `index.html` with no build step. PDF and Word resumes are read with pdf.js and mammoth, loaded from cdnjs only when you upload one. Scoring runs in plain JavaScript in the browser. AI tailoring calls the Anthropic Messages API (`claude-opus-5-5`) directly from the browser with the user's key. Accounts use Supabase (email and password); each person's jobs and resume live in one row of a `user_data` table protected by row-level security. Without an account, data is stored in `localStorage`. The Claude API key always stays in the browser.
