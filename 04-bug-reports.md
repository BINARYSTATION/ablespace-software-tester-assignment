# 4. Bug reports

Full reports for the 3 most important bugs, followed by a short list of minor issues.

Severity = impact on the product. Priority = how soon it should be fixed. The scale used here:
Critical = blocks a core flow or loses data; High = a core feature saves or shows wrong data with no warning;
Medium = a feature works but hides or misstates information, and a workaround exists; Low = small or cosmetic.

---

### BUG-01

| Field | Description |
|-------|-------------|
| Bug ID | BUG-01 |
| Title | Service Time saves 99,999 minutes for a 30-minute session without any warning |
| Severity | High |
| Priority | High |
| Environment | staging.ablespace.io, October 14, 2026 |
| Browser / Device | Chrome 155.0.8059.80 on macOS 27.0.1 (desktop) |
| Reproducibility | Always (2 of 2 attempts) |
| Steps to Reproduce | 1. Open Service Time from the left menu. <br>2. Click Log Service Time. A new row appears with a 30-minute session, Present, 30 min. <br>3. Select Demo Student2 in the Student column. <br>4. In the minutes box, replace 30 with 99999. <br>5. Click the green tick (Save). <br>6. Reload the page. |
| Expected Result | The app rejects service time that is longer than the session, or at least asks the user to confirm it. 99,999 minutes (about 69 days) is not saved for a 30-minute session |
| Actual Result | "Session saved successfully" appears. The row shows the session 05:17 PM - 05:47 PM with 99999 minutes, and the cell cuts the unit off ("99999 mir"). The value is still there after reload. A second try with 5000 minutes for another student was saved the same way. The same box does block a minus sign, and the Calendar form blocks an end time before the start time, so other time inputs are validated |
| Evidence | [BUG-01-service-time-99999-min-saved.jpg](evidence/BUG-01-service-time-99999-min-saved.jpg), [BUG-01-zoom-99999-min.png](evidence/BUG-01-zoom-99999-min.png), [BUG-01-after-refresh.jpg](evidence/BUG-01-after-refresh.jpg), [BUG-01-repro-2-5000-min-saved.jpg](evidence/BUG-01-repro-2-5000-min-saved.jpg); for comparison, the Calendar time check: [PASS-calendar-end-before-start-validation.png](evidence/PASS-calendar-end-before-start-validation.png) |

Why High: service time is the provider's record of the IEP minutes delivered. A typo (for example an extra
digit) is saved silently, and the wrong number stays in the record until someone notices it.

---

### BUG-02

| Field | Description |
|-------|-------------|
| Bug ID | BUG-02 |
| Title | Calendar Day and Week views hide sessions after 5 PM, including an event the user has just created |
| Severity | Medium |
| Priority | Medium |
| Environment | staging.ablespace.io, October 14, 2026 |
| Browser / Device | Chrome 155.0.8059.80 on macOS 27.0.1 (desktop) |
| Reproducibility | Always (4 of 4 sessions after 5 PM were hidden) |
| Steps to Reproduce | Precondition: Calendar Visibility is at its default, 07:00 AM - 04:00 PM (Settings > Preferences > Calendar). Tested at 5:33 PM. <br>1. Open Calendar and switch from Week view (the default) to Day view. <br>2. Click Create. The form fills in the current time (05:33 PM - 06:03 PM). <br>3. Add a student (Test O'Brien José) and click Save. <br>4. Scroll the Day view to the bottom. <br>5. Switch the view to List. |
| Expected Result | The new event appears on the calendar after saving. If an event falls outside the visible hours, the grid extends to show it, or an indicator tells the user that more events exist outside the visible hours |
| Actual Result | "Event created successfully" appears, but the event is not shown in Day or Week view; the grid stops at 5 PM with no indicator. List view shows the event (05:33 PM - 06:03 PM). Three other sessions from the same day (5:17, 5:18 and 5:30 PM) are also missing from Day and Week view |
| Evidence | [BUG-02-1-event-created-successfully.jpg](evidence/BUG-02-1-event-created-successfully.jpg), [BUG-02-2-day-view-bottom-event-missing.jpg](evidence/BUG-02-2-day-view-bottom-event-missing.jpg), [BUG-02-3-list-view-event-exists.jpg](evidence/BUG-02-3-list-view-event-exists.jpg), [BUG-02-4-calendar-visibility-default-7am-4pm.png](evidence/BUG-02-4-calendar-visibility-default-7am-4pm.png) |

Why it matters: a provider with an after-school session may think it was never saved and create a duplicate.

---

### BUG-03

| Field | Description |
|-------|-------------|
| Bug ID | BUG-03 |
| Title | Caseload table search returns no results when the text has a space at the start or end |
| Severity | Low |
| Priority | Medium |
| Environment | staging.ablespace.io, October 14, 2026 |
| Browser / Device | Chrome 155.0.8059.80 on macOS 27.0.1 (desktop) |
| Reproducibility | Always |
| Steps to Reproduce | Precondition: a student named "Test Student A" exists; Caseload is in table view. <br>1. Type Test Student A in Search students. The student is listed. <br>2. Add one space at the end of the text. <br>3. Replace the text with one space followed by Test. |
| Expected Result | Spaces at the start or end are ignored and the student is still listed, as the side-list search on the same page already does |
| Actual Result | Steps 2 and 3 show "No matching results found". By comparison, the side-list search in the split view still finds "Test O'Brien José" with "José " (trailing space), while the table search with the same text shows no results |
| Evidence | [BUG-03-search-no-space-found.jpg](evidence/BUG-03-search-no-space-found.jpg), [BUG-03-search-trailing-space-no-results.jpg](evidence/BUG-03-search-trailing-space-no-results.jpg), [BUG-03-side-panel-search-trailing-space-found.png](evidence/BUG-03-side-panel-search-trailing-space-found.png), [BUG-03-table-search-trailing-space-no-results.jpg](evidence/BUG-03-table-search-trailing-space-no-results.jpg), [BUG-03-table-search-box-zoom.png](evidence/BUG-03-table-search-box-zoom.png) |

Why it matters: names are often pasted from a spreadsheet or email with a trailing space. "No matching results"
suggests the student does not exist, which can lead to a duplicate record. Trimming the text is a small fix.

---

## Other minor issues (one line each)

- Student names change letter case across screens: "Test O'Brien José" in Caseload, "Test O'brien José" in the Service Time student picker, and "Test o'brien josé" on the Data page ([MINOR-1-caseload-name-correct.png](evidence/MINOR-1-caseload-name-correct.png), [MINOR-1-data-page-name-lowercased.png](evidence/MINOR-1-data-page-name-lowercased.png), [MINOR-1-service-time-picker-name-case.png](evidence/MINOR-1-service-time-picker-name-case.png)).
- Delete Student dialog: a long name runs outside the dialog box, and the text says "permanently delete" but also "Recoverable for 90 days" ([MINOR-2-delete-dialog-long-name-overflow.jpg](evidence/MINOR-2-delete-dialog-long-name-overflow.jpg)).
- At iPad Mini width (768 px) the Calendar toolbar does not fit: "School" is cut to "Schc", the more-options button is off-screen, and the page scrolls sideways ([MINOR-3-ipad-mini-calendar-horizontal-scroll.jpg](evidence/MINOR-3-ipad-mini-calendar-horizontal-scroll.jpg), [MINOR-3-ipad-mini-calendar-toolbar-cut.png](evidence/MINOR-3-ipad-mini-calendar-toolbar-cut.png)).
- Avatar initials differ for the same student: "TS" in the Edit Student dialog but "TA" in the list and profile for "Test Student A" ([MINOR-4-edit-dialog-initials-TS.png](evidence/MINOR-4-edit-dialog-initials-TS.png)).
- A typed future or impossible date of birth is cleared silently, with no message (see TC-03).
- Accommodations: saving an empty row says "Option is required." even when no student is selected, and the accommodation list shows only "No data found" with no hint on where to add one.
- Browser Back from a student profile (opened from the table view) reloads the same profile; a second Back leaves Caseload, so Back never returns to the table.
- A 300-character first name is accepted with no limit, and the full name cannot be read anywhere (see TC-08).
- The relative time label ("0 Seconds Ago") on a new Service Time row does not update until the page is reloaded.
