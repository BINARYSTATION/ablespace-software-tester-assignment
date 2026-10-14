# 6. Test summary

## Testing performed

One exploratory session on October 14, 2026 on staging.ablespace.io (Basic plan), using Chrome 155 on macOS 27.
I covered the flows a teacher uses most: Caseload (add, search, view, edit and delete students), Service Time,
Data (Log Data), Calendar (create events, Day, Week and List views) and Accommodations. I tried the happy path
first, then empty fields, spaces only, very long text, special characters (apostrophe and accented letters),
impossible and future dates, boundary numbers, reloads and the browser Back button. I also checked the layout in
a narrow 500 px window and at iPad Mini and iPad Pro widths. All data was fictional.

## Issues found

Three bugs with full reports: BUG-01 (High), BUG-02 (Medium) and BUG-03 (Low), plus nine minor issues.
I would fix BUG-01 first. Service Time saves 99,999 minutes for a 30-minute session without any warning, and
service minutes are the record providers use to show that IEP services were delivered. The fix is small
(check the value against the session length or a sensible maximum), and the app already validates other time
inputs, such as the Calendar end time.

## Areas not tested

- Firefox or Edge, and the AbleSpace mobile app: not installed on the test machine yet.
- Pro features (Groups, Archive, Transfer, Providers, Billing pages): the account is on the Basic plan.
- Upload IEP and the other AI features: not tested in depth.
- Collaborators, Family Center and anything that sends invitations or emails: skipped to follow the rule of no
  contact with users.
- Login and logout beyond the first signup, and security or load testing: out of scope or not allowed.

## What I would test next

1. The same flows on Firefox or Edge and in the mobile app, because teachers often log data on a phone or tablet.
2. Where service time totals appear (reports, billing), to see how far a wrong value like BUG-01 spreads.
3. Calendar recurring sessions and holidays, and how they interact with the Calendar Visibility hours (BUG-02).
4. Goals: create and edit goals and log each data type (accuracy, frequency, duration) with boundary values.
