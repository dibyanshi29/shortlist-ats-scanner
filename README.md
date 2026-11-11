# Shortlist ATS Scanner

A free resume scanner that runs entirely in your browser. Paste your resume and a job
description to get an ATS match score, the skills you're missing, stronger bullet points, an
ATS-friendly resume and a cover letter written for that job.

**Live demo:** `https://<your-username>.github.io/<repo-name>/` (after enabling GitHub Pages, see below)

No server, no sign-up, no build step. It's a single `index.html` file.

## Features

- **ATS match score (0–100):** strict scoring close to tools like Jobscan. About 70% of the
  score is keywords.
- **Missing skills:** hard skills, soft skills and partial matches, each with mention counts
  (your resume / the job description).
- **ATS checks:** exact job title, degree requirement, years of experience, exact keyword
  wording, section headings, contact details, numbers in bullets, weak phrasing.
- **Keyword map:** your resume with the job's keywords highlighted.
- **Bullet rewrites and builder:** turns weak bullets into action + result statements.
- **ATS resume template:** one-column layout, downloadable as .docx, .pdf or .txt.
- **Cover letter:** tailored to the job, company and tone you choose.
- **Upload:** PDF, DOCX or TXT resumes (drag and drop supported).

## How the AI features work

The page doesn't call any AI service directly and has no API keys. Each AI button builds a
prompt containing your resume and the job description. You copy it into any AI chat
(Claude, ChatGPT, Gemini), paste the answer back, and the page displays it.

Every prompt tells the AI never to invent jobs, skills or results. Where a number would help,
it uses a placeholder like `[X%]` for you to fill in.

## Run it

- **Online:** open the GitHub Pages link.
- **Offline:** download `index.html` and double-click it.

The score, skill matching and checks work offline. Reading PDF/DOCX files, building
.docx/.pdf downloads and the AI chat sites need internet.

## Privacy

The instant scan runs only in your browser. Your resume is never uploaded anywhere by the
page. Your last inputs are remembered in your own browser (localStorage) until you press
**Clear**. The AI features only send your resume where you paste the prompt yourself.

## How the score works

| Part | Points | Rule |
|---|---|---|
| Hard skills & keywords | 55 | Weighted share of the job's hard keywords found in your resume |
| Soft skills | 10 | Same, for soft skills (full marks if the job lists none) |
| Job title | 8 | Exact title phrase = 8; otherwise up to 4 for matching words |
| Quantified impact | 7 | Full marks when ~60% of bullets contain a number |
| Education | 5 | Your degree meets the job's stated degree |
| Years of experience | 5 | Your work dates meet the job's stated years |
| Sections & contact | 7 | Standard headings, email, phone, LinkedIn |
| Action verbs & length | 3 | Strong verbs and a sensible length |

Keyword rules:
- A keyword the job mentions 3+ times needs at least 2 mentions in your resume for full credit.
- A different spelling than the job uses gets at most 70% credit.
- Keywords listed only under "nice to have" count half.

Matching uses a built-in list of about 950 skills (870 hard, 75 soft) across tech, data/AI,
cloud, security, product, design, marketing, sales, finance, HR, operations, healthcare,
legal and education. It also counts repeated phrases and acronyms from the job description.

75+ is a strong match. Every ATS tool scores differently; none of them is an official score.

## Customise

Everything lives in `index.html`:

- **Add skills:** find `SKILL_SRC3` (hard) or `SOFT_SRC` (soft) and add `skill name|other spelling;` in lowercase.
- **Change colours:** edit the CSS variables at the top of `<style>` (`--accent`, `--bg`, …).
- **Scoring:** see the `analyze()` function.

## Built with

Plain HTML, CSS and JavaScript. These libraries load from cdnjs only when needed:
[pdf.js](https://mozilla.github.io/pdf.js/) (PDF reading),
[mammoth.js](https://github.com/mwilliamson/mammoth.js) (DOCX reading),
[JSZip](https://stuk.github.io/jszip/) (.docx export),
[jsPDF](https://github.com/parallax/jsPDF) (.pdf export).
