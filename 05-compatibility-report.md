# 5. Cross-browser and responsive report

Setups tested:

- Desktop: Google Chrome 155.0.8059.80 on macOS 27.0.1, viewport 1496 x 762
- Desktop: Firefox or Microsoft Edge: not tested yet (neither was installed on the test machine)
- Mobile view: a narrow Chrome window, 500 x 667 viewport. Chrome does not let a desktop window go below
  500 px wide, so this is close to, but not exactly, 390 x 844. The Play Store app was not tested.
- iPad view: a Chrome window at iPad Mini width (768 px) and iPad Pro width (1024 px). The window height was
  limited to 762 px by the laptop screen.

Pass / Fail below is about layout and behavior on each setup. Functional bugs that appear on every setup are in
Section 4.

| Area / Feature | Chrome | Firefox / Edge | Mobile (500 x 667 window) | Notes |
|----------------|--------|----------------|---------------------------|-------|
| Signup and login | Pass | Not tested | Not tested | The account was created and logged in manually on Chrome. Login was not repeated on other setups (one account; I did not log out). |
| Main workflow (add, search, edit student) | Pass | Not tested | Pass | On the narrow window, Add Student opens as a bottom sheet with a full-width Create button; the Caseload table keeps Full Name, Last Name and Actions visible. |
| Forms | Pass | Not tested | Pass | Required-field rules behave the same on both widths. On the narrow window the Data and Service Time tables show the first columns and cut the rest at the right edge; I did not check sideways scrolling inside those tables. |
| Navigation | Pass | Not tested | Pass | Below desktop width the sidebar becomes a menu button; the drawer opens and closes correctly. |

iPad Mini / iPad Pro notes:

- iPad Mini width (768 px): Caseload and the student forms fit. Calendar: Fail. The toolbar does not fit:
  "School" is cut to "Schc", Collaborators shows only an icon, the more-options (⋮) button is off-screen, and
  the whole page scrolls sideways (evidence/MINOR-3-ipad-mini-calendar-toolbar-cut.png,
  evidence/MINOR-3-ipad-mini-calendar-horizontal-scroll.jpg).
- iPad Pro width (1024 px): Calendar and Caseload fit with no overflow. Pass (evidence/RESP-ipad-pro-1024-*).
- Screens from the narrow-window and iPad checks: evidence/RESP-*.
