# [SCRUM-7] [Functional] Dynamic ID Changes Cause Test Automation Locators to Break

## Metadata
- Type: Bug
- Status: In Progress
- Priority: Medium
- Assignee: Unassigned
- Reporter: Pankaj qa
- Sprint: Sprint 01
- Story Points: story points
- Created: 2026-07-07T07:42:01.424+0530
- Updated: 2026-07-26T17:43:26.683+0530
- URL: https://pankajqaaitesting.atlassian.net/browse/SCRUM-7

## Description
- **Summary:** Interactive elements on the page use completely random, dynamic IDs upon every DOM refresh.
- **Description:** Elements in the AJAX/Dynamic section lack unique static testing attributes (`data-testid`), forcing automation scripts to rely on auto-generated IDs that shift on every page load.
- **Steps to Reproduce:**
  
    1. Inspect the "New Browser Window" button or specific AJAX elements using DevTools. Note the `id` attribute.
    2. Refresh the browser page.
    3. Re-inspect the exact same button element.
- **Expected Result:** The element should keep a stable ID or feature a clean `data-test` attribute for script safety.
- **Actual Result:** The ID changes (e.g., from `btn-9823` to `btn-4102`), making direct locator strategies flaky.
- **Priority:** Medium (High block for Automation)

## Custom Sections
### Description section
- **Description section**: - **Summary:** Interactive elements on the page use completely random, dynamic IDs upon every DOM refresh.
- **Description:** Elements in the AJAX/Dynamic section lack unique static testing attributes (`data-testid`), forcing automation scripts to rely on auto-generated IDs that shift on every page load.
- **Steps to Reproduce:**Inspect the "New Browser Window" button or specific AJAX elements using DevTools. Note the `id` attribute.Refresh the browser page.Re-inspect the exact same button element.
- **Expected Result:** The element should keep a stable ID or feature a clean `data-test` attribute for script safety.
- **Actual Result:** The ID changes (e.g., from `btn-9823` to `btn-4102`), making direct locator strategies flaky.
- **Priority:** Medium (High block for Automation)

### Attachments section
- **Attachments section**: Add attachmentDocument known errorsTry

### Activity section
- **Activity section**: HI

## Comments
### Comment 1 - Pankaj qa (2026-07-26T17:43:26.683+0530)
HI

## Attachments
_No attachments_
