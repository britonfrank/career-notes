# Resume evidence for Briton Frank

Learner frontend, Tallo. Source: git history on `tallo-frontend-mono` for `bfrank@k12.com`, 8 Jan 2026 through 9 Oct 2026. Slack, Jira, and Confluence were not connected when this was drafted, so comments, ticket descriptions, and writing samples are not included.

These bullets describe shipped UI and the engineering choices in the commits. They do not include product metrics, because this history does not record conversion, apply rate, or learner outcomes. Line counts include generated and merge-adjacent edits, so they show volume.

## Counts

| Measure | Value |
| --- | --- |
| Non-merge commits | 194 |
| Commits including merges | 232 |
| Jira tickets mentioned in commit messages | 57 |
| Lines added | +44,081 |
| Lines deleted | −14,887 |
| Test files touched | 47 |

## Commits per month

Source: `git log --author=bfrank@k12.com` on `tallo-frontend-mono`. Counts include merge commits. Peak months are May (Next Step Jobs) and July (occupation search and job filters).

| Month (2026) | Commits, including merges |
| --- | ---: |
| Jan | 20 |
| Feb | 18 |
| Mar | 34 |
| Apr | 7 |
| May | 48 |
| Jun | 22 |
| Jul | 39 |
| Aug | 28 |
| Sep | 8 |
| Oct | 8 |

## Tickets mentioned most often

Mention count is how many commit subjects name the ticket, not how many pull requests shipped. One feature often spans a pair of tickets (5396 with 7383, 7081 with 7669).

| Ticket | Work | Mentions |
| --- | --- | ---: |
| TALLO-6365 | Next Step Jobs | 40 |
| TALLO-5396 | Bucketed autocomplete | 12 |
| TALLO-7081 | Occupation titles | 11 |
| TALLO-7383 | Autocomplete follow-up | 10 |
| TALLO-9129 | Resume autofill | 8 |
| TALLO-8492 | Resume upload | 8 |
| TALLO-4408 | Apply block | 7 |
| TALLO-7669 | Freeform occupations | 6 |
| TALLO-5424 | Apply without login | 6 |

## Resume bullets

Written so a resume can use them as-is. Each one is grounded in commit messages from that repo.

### Job search

Replaced flat job-title autocomplete with a shared bucketed dropdown for job title, company, and career, including recent and popular suggestions on focus. Wired it through SSR job search, the keyword and location bar, and career entry points, then filtered recent searches and hid popular suggestions while the learner was typing.

Rebuilt job-search filters so the controls match the query that actually runs: hourly and annual pay plus a has-pay option, a restored date-posted radio list, benefit subtitles, distance hidden when no location is set, location defaults that stay cleared after the learner removes them or opens a direct URL, and badge counts based on applied filters rather than draft state.

### Occupations and Next Step Jobs

Replaced the crosswalk role picker with occupation-title search. Accepted freeform titles, resolved them to the occupation catalog, title-cased them on commit, and showed an account-required hint when a logged-out learner tried to save an occupation.

Owned Next Step Jobs from first API hookup through QA. Shifted the section from career cards to job recommendations, added an inline current-occupation prompt including “not currently working,” aligned empty states to career-transition compute results, removed redundant API calls, and shipped the prompt behind a feature flag while matching the Figma design.

### Signed-out learners

Let unauthenticated learners apply to offsite jobs and finish the application after login. Kept pending job saves and course favorites across the auth handoff, deleting the local pending record only after the API save succeeded and retrying it once the session was ready. Persisted an anonymous “Did you apply? Yes” through the learner apply APIs.

### Resume builder

Extended the resume dashboard from editing into import: upload a resume onto the profile, reject files whose bytes are not actually PDF, DOC, or DOCX, and start autofill from that file behind the `RESUME_AUTOFILL` gate. Treated a failed profile-file link as a failed import instead of a silent success.

Fixed what learners see in preview and PDF export: page breaks that no longer overlap content, “I currently work here” end dates, independent month and year inputs, and preview visibility for summary, phone, and location. Replaced toast-only failures with in-page errors and a sign-up path.

### Job detail and courses

Shipped a job-detail split view with similar jobs, an ApplyBlock sidebar on the job opportunity page with apply calls moved toward SSR, expired and archived job treatment, and a Closed state on past applications.

Broadened course search so subject filters query every subject field, language options come from cached data, and the default English filter stays applied.

## How this history answers “adversity”

The commits do not show a single outage or interpersonal conflict. They show the same response repeated: stay on the feature after the first merge, when QA, design, and login edge cases prove the happy path was incomplete.

| Pressure | What the commits show | Response |
| --- | --- | --- |
| Product changed mid-build | Next Step Jobs started as career cards (1 May) and became job recommendations (4 May), then ran through QA into early June. About 40 commits on TALLO-6365. | Kept an incremental branch, added a feature flag, removed redundant API calls, and tied empty states to career-transition compute results instead of a local guess. |
| QA and design after the first version | Occupation search shipped, then the checkbox failed, then its container, then the “not currently working” background on a follow-up ticket. Pay, date posted, loaders, and error toasts were also redone after an earlier version existed. | Follow-up commits on the same surface, including a separate reviewed pull request for a Next Step Jobs background bug. |
| Learner intent lost at login | Pending job favorites were cleared before the authenticated session could save them (TALLO-6464). | Delete local pending state only after a successful API save, and retry from app bootstrap. The same pattern shows up again for course favorites and offsite apply. |
| Tests certified the wrong behavior | Resume autofill tests clicked test ids the file menu never rendered. File-type tests also had to copy signature bytes into an ArrayBuffer before building a File. | Query the menu by the labels a learner sees, and make the upload test construct a file the way the browser does. |

Interview phrasing: “The hardest stretch was Next Step Jobs, because the recommendation model changed while the UI was already in review. I kept it behind a flag, cut duplicate requests, and kept fixing QA until empty states matched the compute API.”

## Still missing

Jira descriptions, Slack threads, and Confluence pages are not in this draft.
