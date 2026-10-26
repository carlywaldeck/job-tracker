# NextMove: a job tracker built around your resume

A job and internship tracker for MSBA students. Upload your resume, save jobs, and NextMove scores how qualified you are for each one from 1 to 100, helps you tailor your resume to each posting, and shows everything on one dashboard.

**Live app:** https://carlywaldeck.github.io/job-tracker/. Create an account to keep your jobs and resume on any device, or continue without an account to keep everything in this browser only.

## How it works

1. **Start with your resume.** Upload a PDF, Word, or .txt file, or try the sample resume. NextMove reads your skills, years of experience, and degree in the browser. You check them, add the places you'd like to live (cities, regions like Bay Area, states, or Remote), and save. Jobs in your places get a 📍 tag and their own "My places" tab.
2. **Add a job.** Click **+ Add a job**, paste the posting's link, and click **Fill from link**. NextMove retrieves the public page through Jina AI Reader and fills in the details; if that's blocked and you've added an API key, Claude's web fetch tool tries instead (labeled AI). Fields it couldn't find are highlighted for review. LinkedIn and Handshake need a login, so paste the posting text for those. NextMove fills in the company, title, location, work arrangement, deadline, and link as soon as you paste, then takes you to your score.
3. **Use the dashboard.** It's deliberately short: a banner with your single next move and one button, three numbers (due this week, applications sent, interview rate), and the three to-dos after that.
4. **Go deeper on Progress.** A **What's working** section compares the applications that led to an interview with the ones that didn't (had a contact, tailored resume, match score 75+, applied a week early), shows the interview rate for each group, and lists what to try next, with a "why" for each tip and the skills that keep showing up in postings where you didn't hear back. It's rule-based (labeled), and it warns that small samples are noisy. Below that: Every to-do grouped by Overdue / Today / Next 7 days / Later, the pipeline with conversion rates, all saved jobs ranked by match, and Career Services links. Long lists fold behind "Show more", so it stays readable with 100+ jobs.
5. **Track your applications.** The Jobs page is a table (Match, Company & role, Status, Location, Deadline, Next step): click any column name to sort, use the status tabs (Active, Saved, Applied, Interviewing, Offer, Closed, All) to filter, and change a status right in the row. Switch to Board to drag jobs between columns.
6. **Open a job** to see why it scored what it did, tailor your resume for it, and keep notes.

## Assignment essentials

| Requirement | Where |
|---|---|
| Add and edit opportunities (company, title, link, location/work arrangement, deadline, notes) | **+ Add a job**, or **Edit** on any job |
| Track status: Saved, Applied, Interviewing, Offer, Rejected, Withdrawn | Drag cards on the Jobs board, or use the status dropdown in the list view and on each job page |
| Next action + due date | "Your next step" and "Do it by" in the job form. They show up in the dashboard's To do list. |
| Search, sort, filter | Jobs page: search box, status tabs with counts, and click any column header to sort (match, company, status, location, deadline, next step). Clicking a pipeline bar on Progress filters too. |
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
   - **Why:** every to-do says why it's there (for example "You applied Oct 10. Career Services suggests following up two weeks after the posting closes"). Progress has a "How are these made?" explainer.
   - **Email drafts:** follow-up and thank-you to-dos have a "Draft the email" button. It fills in the job, date, contact, and your matching skills. With an API key, Claude personalizes it (labeled as AI). "Open in email app" and "I sent it" log it.
   - **Help from Career Services:** the same Resume Guide, Career Connections, Interview Guide, and counseling links the spreadsheet has.

## Demo script (2 minutes)

1. **Who it's for** (15s): MSBA students juggling many applications. The Career Services spreadsheet records what happened but doesn't tell you where you fit or what to do next.
2. **Setup** (20s): Upload a resume (or click "Try it with a sample resume and jobs"). Show the skills, years, and degree it found.
3. **Add a job** (20s): Click + Add a job and paste a posting. The form fills itself in; save and it opens on the score.
4. **Score** (25s): Walk through the breakdown, then "How to raise your score". Click "I have this" and watch the score go up.
5. **Tailor** (20s): Click Tailor my resume and show Claude's rewritten summary and bullets. Point out the rule-based fallback.
6. **Track** (20s): On the Jobs board, drag the job to Applied. Back on the dashboard, open a thank-you to-do and click "Draft the email".

## Tech

A single `index.html` with no build step. Visual design (navy and yellow chevron motif, company logos) by Cameron. PDF and Word resumes are read with pdf.js and mammoth, loaded from cdnjs only when you upload one. Public job links are sent to Jina AI Reader for page-text retrieval; company names may be used to find a public logo (Clearbit lookup, Hunter logos), falling back to initials. Field parsing and scoring run in plain JavaScript in the browser. AI tailoring calls the Anthropic Messages API (`claude-opus-5-5`) directly from the browser with the user's key. Accounts use Supabase (email and password); each person's jobs and resume live in one row of a `user_data` table protected by row-level security. Without an account, data is stored in `localStorage`. The Claude API key always stays in the browser.
