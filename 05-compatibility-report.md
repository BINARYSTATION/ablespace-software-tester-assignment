# 5. Cross-browser and responsive report

Setups:

- Desktop: Google Chrome 155.0.8059.80 on macOS 27.0.1, viewport 1496 x 762: **tested**.
- Desktop: Firefox or Microsoft Edge: **not tested**.
- Mobile (390 x 844) and the AbleSpace mobile app: **not tested**. As a partial check I used a narrow Chrome window
  (500 x 667; Chrome does not allow a narrower desktop window). This is not device emulation.
- iPad: Chrome window resized to iPad Mini width (768 px) and iPad Pro width (1024 px), not device emulation. The
  window height was limited to 762 px by the laptop screen.

| Area / Feature | Chrome | Firefox / Edge | Mobile (390 x 844) | Notes |
|----------------|--------|----------------|--------------------|-------|
| Signup and login | Pass (happy path) | Not tested | Not tested | Account created and logged in once on Chrome. Wrong-password and empty-field login cases were not tested. |
| Main workflow | Pass, with known bugs | Not tested | Not tested | Add, search and edit student work on Chrome; defects are listed in Section 4 (BUG-01 to BUG-03, MINOR-01). |
| Forms | Pass | Not tested | Not tested | Required-field handling differs by screen (see the table at the end of Section 2). |
| Navigation | Pass, with MINOR-12 | Not tested | Not tested | Browser Back from a student profile does not return to the table (MINOR-12). |

## Extra check: narrow Chrome window (500 x 667)

| Area | Result | Notes |
|------|--------|-------|
| Navigation | Pass | The sidebar becomes a menu button; the drawer opens and closes ([RESP-narrow-500-menu-open.jpg](evidence/RESP-narrow-500-menu-open.jpg)). |
| Add Student form | Pass | Opens as a bottom sheet with a full-width Create button ([RESP-narrow-500-add-student.jpg](evidence/RESP-narrow-500-add-student.jpg)). |
| Caseload table | Pass | Full Name, Last Name and Actions stay visible ([RESP-narrow-500-caseload.jpg](evidence/RESP-narrow-500-caseload.jpg)). |
| Data and Service Time tables | Fail (minor) | Only the first columns are visible: the student name is cut to "Demo stu..." or "Demo", and the minutes column is off screen. Sideways scrolling inside the tables was not checked ([RESP-narrow-500-data.jpg](evidence/RESP-narrow-500-data.jpg), [RESP-narrow-500-service-time.jpg](evidence/RESP-narrow-500-service-time.jpg)). |

## iPad widths (resized Chrome window)

| Area | iPad Mini width (768 px) | iPad Pro width (1024 px) | Notes |
|------|--------------------------|--------------------------|-------|
| Caseload table | Pass | Pass | The 768 px screenshot was taken while the list was still loading ([RESP-ipad-mini-768-caseload.jpg](evidence/RESP-ipad-mini-768-caseload.jpg), [RESP-ipad-pro-1024-caseload.jpg](evidence/RESP-ipad-pro-1024-caseload.jpg)). |
| Calendar (List view only) | Fail (minor) | Pass | At 768 px the toolbar does not fit and the page scrolls sideways (MINOR-05; [RESP-ipad-mini-768-calendar.jpg](evidence/RESP-ipad-mini-768-calendar.jpg), [RESP-ipad-pro-1024-calendar.jpg](evidence/RESP-ipad-pro-1024-calendar.jpg)). Week and Day views were not checked at these widths. |
