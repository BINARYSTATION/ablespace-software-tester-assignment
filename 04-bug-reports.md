# 4. Bug reports

Full reports for the 3 most important bugs, followed by a short list of other issues (MINOR-01 to MINOR-14).

Severity = impact on the product. Priority = how soon it should be fixed. The scale used here:

| Severity | Meaning |
|----------|---------|
| Critical | Blocks a core flow, or loses saved data |
| High | Saves contradictory data in a core record (attendance, service minutes, goal data) with no warning |
| Medium | Accepts impossible input, or hides information, and the user can notice and fix it |
| Low | Small usability, wording or display issue |

---

### BUG-01

| Field | Description |
|-------|-------------|
| Bug ID | BUG-01 |
| Title | An absent student is credited with service minutes and goal data, with no warning |
| Severity | High |
| Priority | High |
| Environment | staging.ablespace.io/service-time and the session page it links to (/session/...); Basic plan; tested October 15, 2026; time zone IST |
| Browser / Device | Chrome 155.0.8059.80 on macOS 27.0.1 (desktop) |
| Reproducibility | Always (2 of 2: Demo Student1 with 30 min, Demo Student2 with 15 min) |
| Steps to Reproduce | Precondition: logged in; the two demo students that come with a new account exist. <br>1. Open Service Time from the left menu and click Log Service Time. <br>2. In the new row, select Demo Student1. <br>3. Change Attendance from Present to Absent. The minutes change to 0 min and a "Select Reason" dropdown appears. <br>4. Replace 0 with 30 and click the green check-mark button (Save). <br>5. Reload the page. <br>6. Open Data from the left menu and click the blue session link of that session (today's date and time) to open the Take Data screen. Select goal "1. Social Studies" and click + three times. <br>7. Open Data from the left menu again. |
| Expected Result | Minutes and goal data are not saved for an absent student, or the app asks the user to confirm first. The app itself sets minutes to 0 when Absent is chosen, and the help center says the service time "will automatically adjust based on attendance changes" ([How to track services](https://help.ablespace.io/en-us/knowledge-base/how-to-track-services-in-ablespace)). |
| Actual Result | "Session saved successfully". The row shows Demo Student1, Absent, 30 min, and stays after reload. The Take Data screen shows an ABSENT badge on the student but still records the count (3), and the Data page lists that session with Social Studies = 3. No warning at any step. A second try (Demo Student2, Absent, 15 min) gave the same result. |
| Evidence | [BUG-01-1-absent-sets-0-min-and-reason.png](evidence/BUG-01-1-absent-sets-0-min-and-reason.png), [BUG-01-2-absent-30-min-saved-after-reload.jpg](evidence/BUG-01-2-absent-30-min-saved-after-reload.jpg), [BUG-01-3-absent-30-min-zoom.png](evidence/BUG-01-3-absent-30-min-zoom.png), [BUG-01-4-second-try-absent-15-min-saved.jpg](evidence/BUG-01-4-second-try-absent-15-min-saved.jpg), [BUG-01-5-goal-data-recorded-for-absent-student.png](evidence/BUG-01-5-goal-data-recorded-for-absent-student.png), [BUG-01-6-data-page-lists-absent-session-data.jpg](evidence/BUG-01-6-data-page-lists-absent-session-data.jpg) |

Why High: the service record now contradicts itself (Absent, yet 30 minutes delivered), and goal data from a session
the student missed is stored as progress. Anyone reviewing minutes or progress later sees numbers that did not happen.

---

### BUG-02

| Field | Description |
|-------|-------------|
| Bug ID | BUG-02 |
| Title | Service Time accepts any number of minutes, such as 99,999 on a 30-minute session, with no limit or confirmation |
| Severity | Medium |
| Priority | Medium |
| Environment | staging.ablespace.io/service-time; Basic plan; tested October 14, 2026; time zone IST |
| Browser / Device | Chrome 155.0.8059.80 on macOS 27.0.1 (desktop) |
| Reproducibility | Always (2 of 2: 99,999 for Demo Student2, 5,000 for Test O'Brien José) |
| Steps to Reproduce | Precondition: logged in; Demo Student2 exists. <br>1. Open Service Time and click Log Service Time. A new row appears for a 30-minute session with Attendance = Present and 30 min. <br>2. Select Demo Student2. <br>3. Replace 30 with 99999 in the minutes box. <br>4. Click the green check-mark button (Save). <br>5. Reload the page. |
| Expected Result | The help center says the service time equals the session duration by default and "you can manually adjust it", and it gives no limit. Even so, a value that cannot happen in one session should be rejected or need confirmation: 99,999 minutes is about 69 days, and anything over 1,440 minutes is more than a full day. |
| Actual Result | "Session saved successfully". The row shows the 05:17 PM - 05:47 PM session with 99999 minutes, the cell cuts the unit off ("99999 mir"), and the value is still there after reload. 5,000 minutes on another 30-minute session was saved the same way. |
| Evidence | [BUG-02-1-99999-min-row.jpg](evidence/BUG-02-1-99999-min-row.jpg), [BUG-02-2-99999-min-zoom.png](evidence/BUG-02-2-99999-min-zoom.png), [BUG-02-3-99999-min-after-reload.jpg](evidence/BUG-02-3-99999-min-after-reload.jpg), [BUG-02-4-5000-min-saved-toast.jpg](evidence/BUG-02-4-5000-min-saved-toast.jpg) |

Note: the same box blocks a minus sign, and the Calendar form blocks an end time before the start time
([PASS-calendar-end-before-start-validation.png](evidence/PASS-calendar-end-before-start-validation.png)), so other time inputs are checked. Why Medium: the wrong
number is visible in the table, so a careful user can spot and fix it, but nothing stops the typo.

---

### BUG-03

| Field | Description |
|-------|-------------|
| Bug ID | BUG-03 |
| Title | An event created after 4 PM disappears from Day and Week view right after "Event created successfully" |
| Severity | Low |
| Priority | Medium |
| Environment | staging.ablespace.io/calendar; Basic plan; Calendar Visibility at its default, 07:00 AM - 04:00 PM (Settings > Preferences > Calendar); tested October 14 and 15, 2026; time zone IST |
| Browser / Device | Chrome 155.0.8059.80 on macOS 27.0.1 (desktop) |
| Reproducibility | Always (Create flow 2 of 2: default time 05:33 PM on Oct 14, and a time set by hand to 05:30 PM on Oct 15; the 5:17, 5:18 and 5:30 PM sessions made through Service Time and Data are hidden the same way) |
| Steps to Reproduce | Precondition: Calendar Visibility not changed (07:00 AM - 04:00 PM). <br>1. Open Calendar and click Create. <br>2. Set the time to 05:30 PM - 06:00 PM (by default the form uses the current time). <br>3. Add Demo Student1 and click Save. <br>4. Switch to Week view (or Day view) and scroll the grid to the bottom. <br>5. Switch to Month view, then to List view. |
| Expected Result | Hiding hours is by design: the help center says Calendar Preferences "Control the hours visible in your calendar view" ([Calendar and Calendar Preferences](https://help.ablespace.io/en-us/knowledge-base/calendar-and-calendar-preferences-in-ablespace)). But a just-saved event should not vanish without a cue: Day and Week view should show an indicator for events outside the visible hours (as Month view does with "+1 more"), or extend the grid to include them, or the Create dialog should warn that the chosen time is outside the visible hours. |
| Actual Result | "Event created successfully" appears. In Week and Day view the grid ends after the 4 PM row and the event is not shown, with no indicator. Month view shows it only as "+1 more", and List view shows it. Every session after 5 PM behaves the same way. |
| Evidence | [BUG-03-1-event-created-toast-list-view.jpg](evidence/BUG-03-1-event-created-toast-list-view.jpg), [BUG-03-2-week-view-bottom-event-missing.jpg](evidence/BUG-03-2-week-view-bottom-event-missing.jpg), [BUG-03-3-month-view-plus-more.jpg](evidence/BUG-03-3-month-view-plus-more.jpg), [BUG-03-4-calendar-visibility-default-7am-4pm.png](evidence/BUG-03-4-calendar-visibility-default-7am-4pm.png), [BUG-03-5-day-view-bottom-oct14-event-missing.jpg](evidence/BUG-03-5-day-view-bottom-oct14-event-missing.jpg), [BUG-03-6-list-view-oct14-events.jpg](evidence/BUG-03-6-list-view-oct14-events.jpg) |

Why it matters: a provider who schedules an after-school session sees a success message but no event, may think the
save failed, and may create a duplicate.

---

## Other issues (one line each)

- **MINOR-01:** In the Caseload table, a search with one space before or after the name returns "No matching results found", while the Caseload side list, Service Time and Data searches ignore the space ([MINOR-01-1-table-search-found.jpg](evidence/MINOR-01-1-table-search-found.jpg), [MINOR-01-2-table-search-trailing-space-no-results.jpg](evidence/MINOR-01-2-table-search-trailing-space-no-results.jpg), [MINOR-01-3-side-list-search-trailing-space-found.png](evidence/MINOR-01-3-side-list-search-trailing-space-found.png), [MINOR-01-4-table-search-jose-space-no-results.jpg](evidence/MINOR-01-4-table-search-jose-space-no-results.jpg), [MINOR-01-5-table-search-box-zoom.png](evidence/MINOR-01-5-table-search-box-zoom.png)).
- **MINOR-02:** The same student name is shown three ways: "Test O'Brien José" in Caseload, "Test O'brien José" in the Service Time student picker, and "Test o'brien josé" on the Data page ([MINOR-02-1-caseload-name.png](evidence/MINOR-02-1-caseload-name.png), [MINOR-02-2-service-time-picker-name.png](evidence/MINOR-02-2-service-time-picker-name.png), [MINOR-02-3-data-page-name.png](evidence/MINOR-02-3-data-page-name.png)).
- **MINOR-03:** In the Delete Student dialog, a 300-character name runs outside the dialog box ([MINOR-03-04-delete-dialog.jpg](evidence/MINOR-03-04-delete-dialog.jpg)).
- **MINOR-04:** The same dialog is titled "Delete Student Permanently" but also says "Recoverable for 90 days" (Restore from Deleted Records did work) ([MINOR-03-04-delete-dialog.jpg](evidence/MINOR-03-04-delete-dialog.jpg)).
- **MINOR-05:** At iPad Mini width (768 px, resized Chrome window) the Calendar toolbar does not fit: "School" is cut to "Schc", the three-dot menu is off-screen, and the page scrolls sideways ([MINOR-05-1-ipad-mini-calendar-toolbar.png](evidence/MINOR-05-1-ipad-mini-calendar-toolbar.png), [MINOR-05-2-ipad-mini-calendar-sideways-scroll.jpg](evidence/MINOR-05-2-ipad-mini-calendar-sideways-scroll.jpg)).
- **MINOR-06:** Add Goal accepts a goal number that is already used: Demo Student1 now has two goals labeled "Goal 1", with no warning ([MINOR-06-1-existing-goal-1.png](evidence/MINOR-06-1-existing-goal-1.png), [MINOR-06-2-second-goal-1-saved.jpg](evidence/MINOR-06-2-second-goal-1-saved.jpg)).
- **MINOR-07:** When the last name has two words, the avatar initials differ: the Edit Student dialog shows "TO" while the list shows "TJ" for "Test O'Brien José"; one-word last names match ([MINOR-07-edit-dialog-TO-vs-list-TJ.jpg](evidence/MINOR-07-edit-dialog-TO-vs-list-TJ.jpg)).
- **MINOR-08:** In Add Goal, after turning off "Auto-generate mastery criterion", the text "AI will generate a mastery criterion for this goal" stays on screen ([MINOR-08-mastery-help-text-toggle-off.png](evidence/MINOR-08-mastery-help-text-toggle-off.png)).
- **MINOR-09:** A typed future or impossible date of birth (01/01/2030, 13/45/2016) is cleared silently when the field loses focus, with no message (TC-03).
- **MINOR-10:** For the same mistake (no student chosen), Accommodations says "Option is required." while Service Time says "Please select at least one student".
- **MINOR-11:** The empty Accommodation dropdown shows only "No data found"; it does not tell the user that typing a name offers "(Create New)" ([MINOR-11-accommodation-create-new-option.png](evidence/MINOR-11-accommodation-create-new-option.png)).
- **MINOR-12:** Browser Back from a student profile opened from the table view reloads the same profile; a second Back leaves Caseload, so Back never returns to the table.
- **MINOR-13:** A 300-character first name is accepted with no length limit; in the list and profile header it is cut off with "..." and no tooltip (TC-08).
- **MINOR-14 (seen once, not reproduced):** Saving an Absent row on Service Time showed "Saving..." for about 15 seconds; the draft row then disappeared and nothing was saved, with no error. The same steps a minute later saved normally ([MINOR-14-1-save-spinner-stuck.jpg](evidence/MINOR-14-1-save-spinner-stuck.jpg), [MINOR-14-2-row-missing-after-wait.jpg](evidence/MINOR-14-2-row-missing-after-wait.jpg)).
