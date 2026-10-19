# Staying with the feature after the first merge

Source: the same git history as `achievements/2026-tallo-learner-frontend.md`. These notes describe what the commits show. They do not describe a production incident or a conversation, because Slack and Jira comments were not in the source.

## Next Step Jobs changed while it was in review

TALLO-6365 ran from about 1 May 2026 into early June, roughly 40 commits. The first version pointed at career recommendations. On 4 May the product became job recommendations, while the branch was already taking review comments and merges from `development`.

What I did next, from the commit subjects:

- Kept the work on an incremental branch instead of restarting.
- Added a feature flag around the new current-occupation prompt.
- Removed redundant API calls.
- Aligned empty states to career-transition compute results.
- Fixed the methodology redirect and the “not currently working” path.
- Sent a background-color bug out as its own reviewed pull request.

Interview line: “The hardest stretch was Next Step Jobs, because the recommendation model changed while the UI was already in review. I kept it behind a flag, cut duplicate requests, and kept fixing QA until empty states matched the compute API.”

## The checkbox was not done when the feature merged

Occupation-title search (TALLO-7081) landed, then the checkbox did not work, then the checkbox container needed another fix. A related ticket (TALLO-7644) fixed the “not currently working” checkbox background more than once. Pay, date posted, loading placeholders, and error toasts were also rebuilt after an earlier version existed.

The pattern in the log is follow-up commits on the same surface, not a handoff that treated visual bugs as someone else’s cleanup.

## Login dropped something the learner had already done

TALLO-6464: pending job favorites were removed from local storage before the authenticated session could save them. The fix deleted that local record only after the API save succeeded, and retried pending favorites once bootstrap knew the session was ready.

The same idea shows up again for course favorites (TALLO-4860) and for offsite apply after login (TALLO-5424). Anonymous “Did you apply? Yes” was persisted through the learner apply APIs (TALLO-7794).

## A test was passing against a control the screen never rendered

On TALLO-9129, resume autofill tests clicked test ids the file menu never assigned. The follow-up queried menu actions by their labels. On TALLO-9053, signature-byte tests had to copy bytes into an ArrayBuffer before constructing a `File`, so the test matched how a browser builds an upload. The product check rejects files whose contents are not really PDF, DOC, or DOCX.
