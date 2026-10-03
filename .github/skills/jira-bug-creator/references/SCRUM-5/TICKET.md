# [SCRUM-5] Dynamic Web Table - Sum of processes data does not dynamically update the summary row total.

## Metadata
- Type: Bug
- Status: In Progress
- Priority: Medium
- Assignee: Unassigned
- Reporter: Pankaj qa
- Sprint: Sprint 01
- Story Points: story points
- Created: 2026-07-07T07:39:49.346+0530
- Updated: 2026-07-09T22:08:10.671+0530
- URL: https://pankajqaaitesting.atlassian.net/browse/SCRUM-5

## Description
- **Description:** On the Dynamic Web Table section, when a background process changes the CPU % or Memory (MB) of the active rows (e.g., Chrome or Firefox), the dynamic summary label text at the bottom (e.g., `"CPU load of Chrome process: X%"`) is calculating old snapshot states instead of the live data.
- **Steps to Reproduce:**
  
    1. Navigate to the page.
    2. Locate the "Dynamic Web Table".
    3. Observe the row values for Chrome CPU (%) vs the summary sentence below the table.
- **Expected Result:** The summary text matches the exact current value displayed in the table row.
- **Actual Result:** The values are out of sync or show stale data.
- **Priority:** Medium

## Custom Sections
### Description section
- **Description section**: - **Description:** On the Dynamic Web Table section, when a background process changes the CPU % or Memory (MB) of the active rows (e.g., Chrome or Firefox), the dynamic summary label text at the bottom (e.g., `"CPU load of Chrome process: X%"`) is calculating old snapshot states instead of the live data.
- **Steps to Reproduce:**Navigate to the page.Locate the "Dynamic Web Table".Observe the row values for Chrome CPU (%) vs the summary sentence below the table.
- **Expected Result:** The summary text matches the exact current value displayed in the table row.
- **Actual Result:** The values are out of sync or show stale data.
- **Priority:** Medium

### Attachments section
- **Attachments section**: Add attachmentDocument known errorsTry

### Activity section
- **Activity section**: Hey @Pankaj, please start testing.

## Comments
### Comment 1 - Pankaj qa (2026-07-09T22:08:10.671+0530)
Hey @Pankaj, please start testing.

### Comment 2 - Pankaj qa (2026-07-09T22:05:37.968+0530)
This bug is resolved.

## Attachments
_No attachments_
