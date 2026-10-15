# 6. Test summary

## Testing performed

Two exploratory sessions on staging.ablespace.io (Basic plan), on October 14 and 15, 2026, in Chrome 155 on
macOS 27. I covered the flows a teacher uses most: Caseload (add, search, view, edit, delete and restore students),
Service Time, Data and Take Data, Calendar (Day, Week, Month and List views), Goals, Notes and Accommodations. For
each flow I tried the happy path first, then empty and spaces-only fields, very long text, special characters,
impossible and future dates, boundary numbers, attendance combinations, reloads, the browser Back button and repeated
saves. I also checked layouts in a narrow 500 px Chrome window and at iPad Mini and iPad Pro widths. All data was
fictional.

## Issues found

Three bugs with full reports (BUG-01 High, BUG-02 Medium, BUG-03 Low) and 14 smaller issues (MINOR-01 to MINOR-14).
I would fix BUG-01 first. It lets service minutes and goal data be saved for a student marked absent, so the record
contradicts itself. The app already sets minutes to 0 when Absent is chosen, which shows the intended rule. BUG-02 is
next, because the same minutes field accepts values that cannot happen in one session.

## Areas not tested

- Firefox or Edge, the AbleSpace mobile app, and device emulation for 390 x 844 and iPad (see Section 5).
- Pro features marked with a crown (Groups, Archive, Transfer, Providers, Labels and the Billing sub-pages).
- Upload IEP and the AI buttons.
- Collaborators, Family Center and anything that sends invitations or emails, to follow the no-contact rule.
- Login error cases (wrong password, empty fields) and logout. Security and load testing are not allowed by the brief.

## What I would test next

1. Other places where service time can be edited (the calendar event and the Take Data screen) with the BUG-01 and
   BUG-02 inputs, to see whether the same checks are missing there.
2. Whether absent-session minutes and impossible minutes show up in the service time and attendance reports, which
   is where BUG-01 and BUG-02 would do the most harm.
3. Take Data with number-based goal types (accuracy, duration) at their edges: 0, 100%, more than 100%, and blank.
4. Repeated actions: double-clicking Save and Create, adding the same student twice, and reloading with a form open,
   including the save that never finished (MINOR-14) on a slow network.
5. Calendar recurring events and holidays together with the Calendar Visibility setting (BUG-03).
