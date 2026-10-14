# 2. Exploratory testing - scenarios

Ten important scenarios, starting with the flows a teacher uses first. Bug IDs point to full reports in
[04-bug-reports.md](04-bug-reports.md).

| # | Area / flow | What I checked | Result (Pass / Fail / Observation) |
|---|-------------|----------------|------------------------------------|
| 1 | Caseload > Add Student (Add Manually) | Created "Test Student A" with DOB 05/14/2016 and IEP Due Date 03/01/2027, then checked the list and the profile | Pass: "Student created successfully"; the count went from 2 to 3 and the list and profile show the entered values |
| 2 | Add Student: required fields and unsaved changes | Left First and Last Name empty, then typed only spaces; pressed Escape with data entered | Pass: Create stays disabled; Escape shows "Discard Unsaved Changes?" and Cancel keeps the data |
| 3 | Add Student: date fields | Typed a future DOB (01/01/2030) and an impossible date (13/45/2016) | Observation: the picker greys out future dates, but a typed invalid date is cleared silently with no message |
| 4 | Caseload search | Lowercase ("student a"), partial ("Stud"), no match ("zzzq"), and one leading or trailing space | Fail (BUG-03): the first three work, but a single leading or trailing space gives "No matching results found" in the table view |
| 5 | Edit Student | Changed the last name to "O'Brien José", reloaded the page and searched "o'brien" | Pass: "Student detail updated successfully"; the name persists after reload and search finds it |
| 6 | Very long text | First name of 300 characters | Observation: accepted with no length limit; the name is cut off with "..." and no tooltip, and it runs outside the Delete Student dialog |
| 7 | Service Time > Log Service Time | No student; "-5" minutes; 99999 minutes on a 30-minute session | Fail (BUG-01): no-student and the minus sign are blocked, but 99999 minutes is saved |
| 8 | Data > Log Data | Saved with a goal but no data; then logged a checklist goal (D, E) for Demo Student1 | Pass: "Add data or a note before saving."; the data row is saved and listed |
| 9 | Calendar > Create Event | End time before start time; a new event at the current time (5:33 PM) | Fail (BUG-02): time validation works, but the saved event is not shown in Day or Week view |
| 10 | Accommodations > Log Accommodation | Saved an empty row; picked a student with no accommodations | Observation: the message says "Option is required." even with no student selected; the list shows "No data found" with no hint on where to add one |

Also checked: Delete Student with the CONFIRM step (Pass), browser Back from a student profile (Observation),
and the responsive layouts in Section 5. Smaller issues are listed at the end of Section 4.
