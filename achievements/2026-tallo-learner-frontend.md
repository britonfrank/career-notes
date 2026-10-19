# Tallo learner frontend, 2026

Source: git history on `tallo-frontend-mono`, author `bfrank@k12.com`, 8 Jan 2026 through 9 Oct 2026.

Evidence in that window: 194 non-merge commits, about 57 Jira tickets mentioned in commit messages, 47 test files touched, +44,081 / −14,887 lines. Line counts include generated and merge-adjacent edits, so they show volume. This repo does not contain conversion or apply-rate numbers, so those are not claimed here.

Stack in that codebase: React 18, React Router 7 with SSR, TypeScript, Redux Toolkit, SCSS modules, and the internal Tallo UI kit.

## Job search

Replaced flat job-title autocomplete with a shared bucketed dropdown for job title, company, and career, including recent and popular suggestions on focus. Wired it through SSR job search, the keyword and location bar, and career entry points, then filtered recent searches and hid popular suggestions while the learner was typing.

Tickets: TALLO-5396, TALLO-7383.

Rebuilt job-search filters so the controls match the query that actually runs: hourly and annual pay plus a has-pay option, a restored date-posted radio list, benefit subtitles, distance hidden when no location is set, location defaults that stay cleared after the learner removes them or opens a direct URL, and badge counts based on applied filters.

Tickets: TALLO-8477, TALLO-8007, TALLO-7779, TALLO-6698, TALLO-7431, TALLO-7564, TALLO-8266, TALLO-7820, TALLO-7767, TALLO-7939, TALLO-7507.

## Occupations and Next Step Jobs

Replaced the crosswalk role picker with occupation-title search. Accepted freeform titles, resolved them to the occupation catalog, title-cased them on commit, and showed an account-required hint when a logged-out learner tried to save an occupation.

Tickets: TALLO-7081, TALLO-7669, TALLO-8364.

Owned Next Step Jobs from first API hookup through QA. Shifted the section from career cards to job recommendations, added an inline current-occupation prompt including “not currently working,” aligned empty states to career-transition compute results, removed redundant API calls, and shipped the prompt behind a feature flag while matching the Figma design.

Ticket: TALLO-6365 (about 40 commits, May through early June 2026). Heaviest paths: `next-step-jobs-section` and `occupation-picker`.

## Signed-out learners

Let unauthenticated learners apply to offsite jobs and finish the application after login. Kept pending job saves and course favorites across the auth handoff, deleting the local pending record only after the API save succeeded and retrying it once the session was ready. Persisted an anonymous “Did you apply? Yes” through the learner apply APIs.

Tickets: TALLO-5424, TALLO-6464, TALLO-4860, TALLO-7794.

## Resume builder

Extended the resume dashboard from editing into import: upload a resume onto the profile, reject files whose bytes are not actually PDF, DOC, or DOCX, and start autofill from that file behind the `RESUME_AUTOFILL` gate. Treated a failed profile-file link as a failed import.

Tickets: TALLO-8492, TALLO-9053, TALLO-9129.

Fixed what learners see in preview and PDF export: page breaks that no longer overlap content, “I currently work here” end dates, independent month and year inputs, and preview visibility for summary, phone, and location. Replaced toast-only failures with in-page errors and a sign-up path.

Tickets: TALLO-4941, TALLO-4942, TALLO-4752, TALLO-4463, TALLO-5252, TALLO-4841, TALLO-5224.

## Job detail and courses

Shipped a job-detail split view with similar jobs, an ApplyBlock sidebar on the job opportunity page with apply calls moved toward SSR, expired and archived job treatment, and a Closed state on past applications.

Tickets: TALLO-6968, TALLO-4408, TALLO-5544, TALLO-5508, TALLO-6227, TALLO-5255.

Broadened course search so subject filters query every subject field, language options come from cached data, and the default English filter stays applied.

Tickets: TALLO-4384, TALLO-4630, TALLO-4916, TALLO-4451, TALLO-3971.

## Resume-ready lines

Use these when a resume needs a short form. Do not add metrics that are not in the source.

- Replaced flat job-title autocomplete with a bucketed job, company, and career search on the learner job-search experience, including SSR and career entry points.
- Replaced a crosswalk role picker with occupation-title search that accepts freeform titles and maps them back to the catalog.
- Shipped Next Step Jobs as job recommendations with an inline current-occupation prompt, feature-flagged, and aligned to career-transition results through QA.
- Kept job saves, course favorites, and offsite applications intact when a learner signs in, and let signed-out learners finish an offsite apply after login.
- Added resume upload, real file-type checks for PDF, DOC, and DOCX, and gated resume autofill from an uploaded file.
- Fixed resume preview and PDF export fidelity, including dates, page breaks, and in-page errors instead of toasts.
