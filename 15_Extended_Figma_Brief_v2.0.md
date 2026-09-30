# Mini Issue Tracker — enhanced Figma brief v2.0

Extend the current Mini Issue Tracker Figma page. Preserve the original low-fidelity grayscale style and existing base screens. Add editable native Figma layers only; interactions demonstrate prepared states and do not claim a real backend.

## List enhancements

Add a Search issues input and a Filter button to S-02-A and S-02-B. Add compact tag chips and a Due date / Overdue label to list rows. Create these additional list states:

- `S-02-D Filtered Results`: search `export`, tag `Backend`, Status `Resolved`; show matching ISS-003 and active filter chips.
- `S-02-E No Search Results`: query `mobile`; show `No issues match the selected filters` and Clear all.

Create `M-02 Advanced Filters` as an overlay with Status, Priority, Assignee, Tag and Due date state. Due-date state options: Any date, Due today, Due this week, Overdue, No due date. Actions: Apply filters and Clear all.

## Create Issue enhancement

Keep Title and Description required. Add optional Tags multi-select and optional Due date. Do not add Assignee, Priority, Status, ID, Author or Created at inputs.

## Issue Details enhancement

Below the existing Comments section add:

### Tags

Show applied tag chips and `Add tag`. Use Bug, Feature, UI, Backend, Documentation and Urgent. Tags are categorical labels only; they do not change the Important predicate.

### Due date

Show a Due date control with Apply. For a date in the past on a non-Closed issue, display text `Overdue`. Lead can change the date; Members see the control disabled. Closed issues do not show Overdue.

### Attachments

Show an Attachments section with `Add attachment`. Create `M-03 Add Attachment` overlay. It contains a file-picker mock and demonstrates selected file, uploading, upload-error and uploaded states. Uploaded rows show name, type, size, author and time. In an upload-error state, do not show a new saved row.

### Subtasks

Show `Subtasks (2 of 5 completed)`, an `Add subtask` input and reusable checkbox rows. Completed rows remain visible and checked. Do not automatically change the parent issue status when all subtasks are complete.

## Basic extension prototype links

- Filter button → M-02.
- M-02 Apply filters → S-02-D.
- M-02 Clear all or S-02-D Clear all → S-02-A.
- S-02-D / S-02-E keep the same title-to-details navigation.
- Add attachment → M-03; prepared success returns to S-03 with an attachment row.
- Add subtask and checkbox can show prepared updated states in S-03.

## Do not add

Do not add dashboards, analytics, bulk selection, task deletion, user administration, chat, AI recommendations, calendar views, recurring tasks, or separate pages for tags, due dates, attachments or subtasks.

