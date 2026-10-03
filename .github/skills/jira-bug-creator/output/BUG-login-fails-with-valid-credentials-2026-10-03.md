# Bug Report — Login Fails with Valid Credentials

> Status: **DRAFT — pending human review.** Not final until a QA owner signs off.

## Summary

| Field | Value |
|---|---|
| **Bug ID** | [SCRUM-17](https://pankajqaaitesting.atlassian.net/browse/SCRUM-17) |
| **Title** | [Login] User unable to log in with valid credentials on the login page |
| **Severity** | High |
| **Priority** | P1 |
| **Environment** | Chrome browser, Windows OS, Desktop, QA environment |
| **Reported By** | Pankaj qa |
| **Date Reported** | 2026-10-03 |
| **Component / Module** | Authentication / Login |
| **Affected Version** | [TO CONFIRM] |

---

## Severity & Priority Justification

- **Severity rationale:** **High** — Login is a core authentication feature. Users cannot access the application at all with valid credentials, which completely blocks all downstream functionality. No workaround is apparent from the screenshot.
- **Priority rationale:** **P1** — This blocks all user access to the application. Without login, no other testing or user workflows can proceed. Must be fixed immediately.

---

## Steps to Reproduce

1. Navigate to the login page of the application.
2. Enter a valid username in the Username field.
3. Enter the corresponding valid password in the Password field.
4. Click the "Log in" button.

---

## Expected Result

The user should be successfully authenticated and redirected to the application's dashboard or home page. A successful login should display the authenticated user's session without any error messages.

---

## Actual Result

The login does not succeed despite valid credentials being entered. The user remains on the login page and is not redirected to the authenticated area of the application. The login attempt fails silently or displays an error — the user is unable to proceed past the login screen.

---

## Attachments

| File | Description |
|---|---|
| `01.png` | Screenshot of the login page showing the login form with valid credentials entered, where the login attempt is not succeeding. |

---

## Additional Notes

- **Frequency:** [TO CONFIRM] — Needs verification if this occurs for all users or specific accounts.
- **Workaround:** None identified. Users cannot access the application.
- **Related Issues:** None identified.
- **Browser Console / Logs:** [TO CONFIRM] — Console logs were not captured in the screenshot. Recommend checking for JavaScript errors or failed network requests during login.
- **Network:** [TO CONFIRM] — Network tab was not captured. Recommend checking the login API endpoint response for status codes and error payloads.

---

## Environment Details

| Detail | Value |
|---|---|
| **Browser** | Chrome [TO CONFIRM version] |
| **Operating System** | Windows [TO CONFIRM version] |
| **Device** | Desktop |
| **Screen Resolution** | [TO CONFIRM] |
| **App Version** | [TO CONFIRM] |
| **Server / Environment** | QA |

---

## HUMAN REVIEW GATE

- **I observed in the screenshot:** A login form with Username and Password fields and a "Log in" button. The user has entered credentials but the login is not succeeding — the user remains stuck on the login page.
- **I assumed:** The credentials entered are valid and correct. The environment is QA. The browser is Chrome on Windows Desktop.
- **I could not determine:** The exact browser version, OS version, screen resolution, app build version, any console errors, network response from the login API, whether this affects all users or specific accounts, and the exact error message (if any) displayed.
- ▶ **Approve, or edit, before this bug is treated as final.**