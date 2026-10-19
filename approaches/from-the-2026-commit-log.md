# What the 2026 commit log suggests about how I work

Source: commit messages only, Jan–Oct 2026, `tallo-frontend-mono`. This is a reading of that log, not a personal essay. Replace or extend it when I write the approach in my own words.

## Patterns that show up more than once

- Ship the interaction, then stay for the cases QA and design find. Next Step Jobs, occupation checkboxes, pay filters, and resume errors all have a second and third pass.
- Preserve what a signed-out learner already did. Pending saves, favorites, and offsite applies wait for a successful authenticated write instead of being cleared at the redirect.
- Put a new path behind a feature flag when the surrounding page is already live (`RESUME_AUTOFILL`, the Next Step Jobs prompt).
- Prefer the label a person sees over an internal test id when a test and the UI disagree.
- Check file contents, not just the extension, before treating an upload as a resume.
- Share a control once two screens need it. Bucketed search landed in the UI kit and was reused by job search and the keyword/location bar. The login prompt became a shared modal.

## Still to write in my own words

When I add a note here, include a date and a concrete example. Useful prompts:

- A bug I would now catch before review.
- A time I pushed back on a design, and what I said.
- How I decide a feature flag is ready to come out.
- How I write a pull request description.
