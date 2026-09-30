# Extended screen map v2.0

## Modified screens

| Screen | New content |
|---|---|
| S-02-A All Issues | Search field, Filter button, active filter chips, tags and due-date/Overdue label in rows. |
| S-02-B Important Issues | Same search and filter controls; base Important predicate remains active. |
| S-02-D Filtered Results | A demonstrable state of S-02 with applied filters and a clear-results action. |
| S-02-E No Search Results | A demonstrable S-02 state with a clear-filter action. |
| M-01 Create Issue | Optional Tags selector and Due date field added below Description. |
| S-03 Issue Details | Tags, Due date, Attachments and Subtasks sections added below the existing details and comments. |

## New overlays and components

| ID | Purpose |
|---|---|
| M-02 Advanced Filters | Status, priority, assignee, tag and due-date state; Apply and Clear all. |
| M-03 Add Attachment | File picker mock, selected-file state, uploading, upload-error and uploaded result. |
| C-01 Tag chip | Reusable labelled tag component. |
| C-02 Due label | Reusable due-date / Overdue label. |
| C-03 Subtask row | Checkbox, title and optional completion state. |
| C-04 Attachment row | File icon, name, type, size, author and timestamp. |

## Main extension flows

1. S-02-A → M-02 → Apply filters → S-02-D.
2. S-02-D → Clear all → S-02-A.
3. S-02-A → S-02-E when search/filter produces no results.
4. S-03 → M-03 → uploaded state → attachment row appears in S-03.
5. S-03 → Add subtask inline → subtask row appears → toggle checkbox → progress updates.
6. M-01 → select tags and optional Due date → prepared S-03 success state shows them.

