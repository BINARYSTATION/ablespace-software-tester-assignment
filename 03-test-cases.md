# 3. Detailed test cases

**Workflow chosen:** Create Student → Save → Search → View → Edit (Caseload)

**Why this workflow:** every other feature (data, service time, calendar, reports) depends on a correct student
record, so this is the first flow a teacher uses and the one that must not break.

Eight test cases: five positive or validation checks that pass, and three edge cases that fail.

---

### TC-01

| Field | Description |
|-------|-------------|
| Test Case ID | TC-01 |
| Title | Create a student with valid details |
| Preconditions | Logged in to staging.ablespace.io; Caseload page open |
| Test Data | First Name: Test; Last Name: Student A; DOB: 05/14/2016; IEP Due Date: 03/01/2027 |
| Steps | 1. Click Add Student. <br>2. Choose Add Manually. <br>3. Enter the test data. <br>4. Click Create. <br>5. Open the new student's profile. |
| Expected Result | A success message appears; the student is listed in Caseload with IEP Due 03/01/2027; the profile shows DOB 05/14/2016 |
| Actual Result | "Student created successfully" appeared; Students changed from 2 to 3; the list and the profile show the entered values |
| Status | Pass |

---

### TC-02

| Field | Description |
|-------|-------------|
| Test Case ID | TC-02 |
| Title | Create is blocked when the required names are empty or only spaces |
| Preconditions | Add Student form open (Add Manually) |
| Test Data | First and Last Name empty; then three spaces in each |
| Steps | 1. Leave both name fields empty and check the Create button. <br>2. Type three spaces in First Name and in Last Name. <br>3. Try to click Create. |
| Expected Result | Create stays disabled and no student is created |
| Actual Result | Create stayed disabled in both cases; no student was created |
| Status | Pass |

---

### TC-03

| Field | Description |
|-------|-------------|
| Test Case ID | TC-03 |
| Title | An invalid or future date of birth is rejected with a clear message |
| Preconditions | Add Student form open; First and Last Name filled |
| Test Data | DOB 01/01/2030 (future); DOB 13/45/2016 (impossible date) |
| Steps | 1. Type 01/01/2030 in DOB. <br>2. Move focus out of the field. <br>3. Repeat with 13/45/2016. |
| Expected Result | The date is not accepted and a message explains why (for example, "Date of birth cannot be in the future") |
| Actual Result | The date picker greys out future dates, but a typed date is cleared silently when the field loses focus. No message is shown in either case |
| Status | Fail |

---

### TC-04

| Field | Description |
|-------|-------------|
| Test Case ID | TC-04 |
| Title | Search finds students regardless of letter case and by part of the name |
| Preconditions | Students "Test Student A", "Demo Student1" and "Demo Student2" exist; Caseload in table view |
| Test Data | "student a", "Stud", "zzzq" |
| Steps | 1. Type "student a" in Search students. <br>2. Replace it with "Stud". <br>3. Replace it with "zzzq". |
| Expected Result | Step 1 lists Test Student A; step 2 lists all three students; step 3 shows a clear empty state |
| Actual Result | As expected; step 3 shows "No matching results found" with a Clear All Filters link |
| Status | Pass |

---

### TC-05

| Field | Description |
|-------|-------------|
| Test Case ID | TC-05 |
| Title | Search ignores a space at the start or end of the text |
| Preconditions | Student "Test Student A" exists; Caseload in table view |
| Test Data | "Test Student A"; "Test Student A " (one trailing space); " Test" (one leading space) |
| Steps | 1. Type "Test Student A" in Search students. <br>2. Add one space at the end. <br>3. Replace the text with " Test". |
| Expected Result | All three searches list Test Student A |
| Actual Result | Step 1 lists the student; steps 2 and 3 show "No matching results found" (see BUG-03) |
| Status | Fail |

---

### TC-06

| Field | Description |
|-------|-------------|
| Test Case ID | TC-06 |
| Title | Edit a student's last name with an apostrophe and an accented letter |
| Preconditions | Student "Test Student A" exists |
| Test Data | New Last Name: O'Brien José; search text: o'brien |
| Steps | 1. Open the student's profile. <br>2. Open the menu (⋮) and choose Edit Student. <br>3. Change Last Name to O'Brien José and click Update. <br>4. Reload the page. <br>5. Search "o'brien" in the student list. |
| Expected Result | The change is saved; the name shows as "Test O'Brien José" after reload; search finds the student |
| Actual Result | "Student detail updated successfully"; the name shows correctly in Caseload after reload; search finds the student |
| Status | Pass |

---

### TC-07

| Field | Description |
|-------|-------------|
| Test Case ID | TC-07 |
| Title | Closing the form with unsaved data asks for confirmation |
| Preconditions | Add Student form open |
| Test Data | First Name: Test; Last Name: Student A; DOB: 05/14/2016 |
| Steps | 1. Enter the test data. <br>2. Press Escape. <br>3. Click Cancel in the prompt. <br>4. Check the fields. |
| Expected Result | A confirmation prompt appears; Cancel returns to the form with the data intact |
| Actual Result | "Discard Unsaved Changes?" appeared; Cancel kept all the entered data |
| Status | Pass |

---

### TC-08

| Field | Description |
|-------|-------------|
| Test Case ID | TC-08 |
| Title | A very long first name is limited or stays readable |
| Preconditions | Caseload page open |
| Test Data | First Name: "LongNameTest" repeated 25 times (300 characters); Last Name: Student B |
| Steps | 1. Click Add Student and choose Add Manually. <br>2. Enter the test data and click Create. <br>3. Check the Caseload list and the profile header, and hover over the name. <br>4. Open Delete Student for this record. |
| Expected Result | Either the field limits the length with a message, or the full name can be read (for example in a tooltip) without breaking any layout |
| Actual Result | The student was created with no length limit. The name is cut off with "..." in the list and the profile header, hovering shows no tooltip, and the last name is never visible in the header. In the Delete Student dialog the name runs outside the dialog box |
| Status | Fail |
