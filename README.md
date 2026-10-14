# AbleSpace - Software Tester (QA) assignment

- Candidate: Manish Mewada
- Application: Software Tester (QA), AbleSpace (via Internshala)
- Application tested: staging.ablespace.io
- Date tested: October 14, 2026

## Contents

| # | Section | File |
|---|---------|------|
| 2 | Exploratory testing: scenarios | [02-exploratory-scenarios.md](02-exploratory-scenarios.md) |
| 3 | Detailed test cases | [03-test-cases.md](03-test-cases.md) |
| 4 | Bug reports (with evidence) | [04-bug-reports.md](04-bug-reports.md) |
| 5 | Cross-browser and responsive report | [05-compatibility-report.md](05-compatibility-report.md) |
| 6 | Test summary | [06-test-summary.md](06-test-summary.md) |
| 7 | Optional: Playwright automation | Not attempted |

Screenshots referenced by the reports are in the [evidence](evidence/) folder. Each file name starts with the
item it belongs to: `BUG-01-...`, `MINOR-1-...`, `RESP-...` (responsive checks) or `PASS-...`.

## How I tested

- One account, created manually through the normal signup flow, with fictional data only (for example
  "Test Student A", plus the two demo students that come with a new account).
- No security, penetration or load testing. No injection-style input. No scripts that create accounts.
- No contact with AbleSpace users or support. No invitations or emails were sent from the app.
- Plan: Basic (free). Features marked with a crown (Pro) were not tested.
- AI assistance: an AI assistant (Claude, driving the Chrome browser) helped run the exploratory session,
  capture the screenshots and draft this write-up. I reviewed every finding and re-ran the three main bugs
  myself before submitting.

## Environment

| Setup | Details |
|-------|---------|
| Desktop browser 1 | Google Chrome 155.0.8059.80 on macOS 27.0.1, viewport 1496 x 762 |
| Desktop browser 2 | Firefox or Edge: not tested yet (see Section 5) |
| Mobile | Narrow Chrome window, 500 x 667 viewport (Chrome's minimum window width). Play Store app: not tested |
| Tablet | Chrome window at iPad Mini width (768 px) and iPad Pro width (1024 px); height limited to 762 px by the laptop screen |
