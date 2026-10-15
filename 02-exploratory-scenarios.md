# 2. Exploratory testing - scenarios

Ten important scenarios, starting with the flows a teacher uses most. IDs point to Section 4
([04-bug-reports.md](04-bug-reports.md)).

| # | Area / flow | What I checked | Result (Pass / Fail / Observation) |
|---|-------------|----------------|------------------------------------|
| 1 | Caseload > Add Student (Add Manually) | Created "Test Student A" with DOB 05/14/2016 and IEP Due Date 03/01/2027, then checked the list and the profile | Pass: "Student created successfully"; the count went from 2 to 3; the list and profile show the entered values |
| 2 | Add Student: required fields and unsaved changes | Left First and Last Name empty, then typed only spaces; pressed Escape with data entered | Pass: Create stays disabled; Escape shows "Discard Unsaved Changes?" and Cancel keeps the data |
| 3 | Add Student: date of birth | Typed a future date (01/01/2030) and an impossible date (13/45/2016) | Fail (minor, MINOR-09): the picker grays out future dates, but a typed invalid date is cleared silently with no message |
| 4 | Caseload search | Lowercase ("student a"), partial ("Stud"), no match ("zzzq"), and one space before or after the name | Fail (minor, MINOR-01): the first three work; with one extra space the Caseload table shows "No matching results found", while the other three search boxes in the app ignore the space |
| 5 | Edit Student | Changed the last name to "O'Brien José", reloaded, searched "o'brien" | Pass in Caseload; other screens change the letter case of the name (MINOR-02) |
| 6 | Very long text | First name of 300 characters | Fail (minor, MINOR-13 and MINOR-03): accepted with no length limit; cut off with "..." and no tooltip; runs outside the Delete Student dialog |
| 7 | Attendance vs. service minutes and goal data | Marked a student Absent, typed minutes, then took goal data in that session | Fail (BUG-01): the app sets 0 min for Absent, yet 30 (and 15) minutes and a goal count are saved with no warning |
| 8 | Service Time minutes | No student; "-5"; 99999 and 5000 on 30-minute sessions | Pass for no-student and the minus sign; Fail (BUG-02): the large values are saved |
| 9 | Data > Log Data and Take Data | Saved a goal with no data; logged a checklist goal; on a frequency goal pressed minus at 0, then plus three times | Pass: "Add data or a note before saving."; rows are saved; the count never goes below 0 |
| 10 | Calendar > Create Event | End time before start time; an event at 05:30 PM | Pass for the time check; Fail (BUG-03): the saved event is hidden in Day and Week view |

**Also checked:** Delete Student with the CONFIRM step, and Restore from Settings > Deleted Records (Pass); student
Notes with an apostrophe, an accented letter and an emoji (auto-saved, correct after reload, Pass); Add Goal
validation (Pass) and a duplicate goal number (MINOR-06); Accommodations (MINOR-10, MINOR-11); browser Back
(MINOR-12); layouts in Section 5.

**One pattern across screens:** the same mistake (a required input left empty) is handled five different ways.

| Screen | What happens |
|--------|--------------|
| Add Student | Create stays disabled; no message |
| Service Time | Message: "Please select at least one student" |
| Accommodations | Message: "Option is required." even when the student is missing |
| Log Data | Save is enabled, then a message: "Add data or a note before saving." |
| Add Goal / Calendar | Message plus inline text under the field |
