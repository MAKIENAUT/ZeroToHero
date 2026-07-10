# Bug Journal Template

```md
🐛 Bug #001 - [Short descriptive title]

Date found: YYYY-MM-DD
Found by: Me / teammate / tester / user
Status: Open / Investigating / Blocked / Resolved
Severity: Low / Medium / High / Critical
Environment: OS, browser/app version, device, branch, commit, API env, database state, or anything else relevant

Description
Write the bug in 1 to 3 sentences.
- What is broken?
- Where does it happen?
- Why does it matter?

Steps to reproduce
1. Start from a clean state if needed.
2. List the exact actions in order.
3. Include important inputs, clicked buttons, routes, accounts, roles, or seed data.
4. Make the steps reproducible enough that future me can trigger the same bug again.

Expected behavior
Describe the correct outcome.
- What should the system do?
- What should the user see?
- What response, state, or data should exist?

Actual behavior
Describe the wrong outcome.
- Wrong UI?
- Wrong data?
- Crash?
- Silent failure?
- Slow response?

Screenshots / logs / error messages
Paste only the useful evidence.
- Console errors
- Network response
- Backend logs
- SQL error
- Stack trace
- Screenshot or screen recording

Root cause
Fill this in only after confirming it.
- Was it bad logic?
- Wrong config?
- Missing validation?
- Race condition?
- Bad query?
- Bad assumptions about framework behavior?

Fix / notes
Document what changed.
- Code fix
- Config fix
- Data cleanup
- Workaround
- Related commit or PR
- Follow-up tasks if the fix is incomplete

Date resolved: YYYY-MM-DD
```
## Why This Template Works

- `Date found`, `status`, and `severity` help you prioritize instead of treating every bug like the apocalypse.
- `Environment` matters because some bugs only happen on one browser, one branch, one role, or one dirty database state.
- `Steps to reproduce` force precision. If you cannot reproduce it cleanly, you probably do not understand it yet.
- `Expected behavior` and `Actual behavior` turn vague frustration into a clear mismatch.
- `Screenshots / logs / error messages` keep you anchored to evidence instead of guessing.
- `Root cause` should be factual, not emotional. “Laravel is stupid” is not a root cause.
- `Fix / notes` create a breadcrumb trail for future regressions.
- `Date resolved` helps you see which bugs keep coming back and how long they stay alive.

## Example Entry

```md
🐛 Bug #001 - Task list does not load after login

Date found: 2026-07-10
Found by: Me
Status: Resolved
Severity: High
Environment: Ubuntu, Chrome 138, local Docker Compose, frontend branch `main`, Laravel API local env

Description
After logging in successfully, the dashboard loads but the task list stays empty. The user looks authenticated on the UI, but task data never returns.

Steps to reproduce
1. Start frontend, backend, and database locally.
2. Login with a valid test account.
3. Open the dashboard page.
4. Inspect the network request for `GET /api/tasks`.

Expected behavior
The dashboard should fetch tasks and render the task list for the authenticated user.

Actual behavior
The task request returns `401 Unauthorized`, so the UI stays empty.

Screenshots / logs / error messages
- Browser network tab: `GET /api/tasks` returned `401`
- No auth cookie present on the request

Root cause
The frontend fetch wrapper did not include credentials, so the session cookie was never sent to the backend.

Fix / notes
- Added `credentials: "include"` to the shared API client
- Retested login and dashboard flow
- Future check: add one integration test for authenticated fetches

Date resolved: 2026-07-10
```

## Final Rule

Do not use this journal to write “it broke, fixed somehow, moving on.”

If the point is to grow, then every bug entry should leave behind one useful lesson, one concrete fix, and one clue that saves future you from repeating the same stupidity.
