# AbleSpace - Software Tester (QA) assignment

- Candidate: Manish Mewada
- Application: Software Tester (QA), AbleSpace (via Internshala)
- Application tested: staging.ablespace.io (Basic plan)
- Dates tested: October 14 and 15, 2026

## Summary

Top three bugs (full reports in Section 4):

1. **BUG-01 (High):** an absent student is credited with service minutes and goal data, with no warning.
2. **BUG-02 (Medium):** Service Time accepts any number of minutes, such as 99,999 on a 30-minute session.
3. **BUG-03 (Low):** an event created after 4 PM disappears from Day and Week view right after "Event created successfully".

Also: 14 smaller issues (end of Section 4), 10 scenarios (Section 2) and 8 test cases (Section 3).
Not tested: Firefox / Edge and the AbleSpace mobile app (Section 5).

## Contents

| # | Section | File |
|---|---------|------|
| 2 | Exploratory testing: scenarios | [02-exploratory-scenarios.md](02-exploratory-scenarios.md) |
| 3 | Detailed test cases | [03-test-cases.md](03-test-cases.md) |
| 4 | Bug reports (with evidence) | [04-bug-reports.md](04-bug-reports.md) |
| 5 | Cross-browser and responsive report | [05-compatibility-report.md](05-compatibility-report.md) |
| 6 | Test summary | [06-test-summary.md](06-test-summary.md) |
| 7 | Optional: Playwright automation | Not attempted |

Screenshots are in the [evidence](evidence/) folder. Each file name starts with the item it belongs to:
`BUG-01-...`, `MINOR-01-...`, `RESP-...` (layout checks) or `PASS-...`.

## How I tested

- One account, created manually through the normal signup flow, with fictional data only (for example
  "Test Student A", plus the two demo students that come with a new account).
- Special characters (apostrophe, accented letters, an emoji) were used as ordinary name and note text, not as
  injection attempts. No security or load testing. No scripts that create accounts.
- No contact with AbleSpace users or support. No invitations were sent.
- Features marked with a crown (Pro) were not tested.
- Who did what: an AI assistant (Claude) drove the Chrome browser during exploration, took the screenshots and
  drafted this write-up. I reviewed every finding and re-ran the three main bugs myself on October 15, 2026.

## Environment

| Setup | Details |
|-------|---------|
| Desktop browser 1 | Google Chrome 155.0.8059.80 on macOS 27.0.1, viewport 1496 x 762, time zone IST (UTC+5:30) |
| Desktop browser 2 | Firefox or Edge: not tested |
| Mobile | Not tested on a phone or in device emulation. A narrow Chrome window (500 x 667, the smallest Chrome allows) was checked instead |
| Tablet | Chrome window resized to iPad Mini width (768 px) and iPad Pro width (1024 px), not device emulation; height limited to 762 px by the screen |
