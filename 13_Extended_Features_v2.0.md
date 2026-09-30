# Mini Issue Tracker — extended features v2.0

## Scope

This document defines an enhanced product version. It extends the base tracker with search and filters, tags, due dates, attachments and subtasks. The extension uses IDs `EX-01`–`EX-05` so it does not overwrite the original source specification.

## EX-01 Search and filters

### User story

As a team member, I want to search and filter issues so that I can find relevant work quickly.

### Acceptance criteria

- Search matches issue ID and title.
- Filters are available for status, priority, assignee, tag and due-date state.
- Multiple selected filters use AND logic.
- Active filters are visible as chips above the list.
- Clear all restores the current list state without filters.
- The empty result state explains that no issues match the selected criteria.

## EX-02 Issue tags

### User story

As a team member, I want to add tags to an issue so that its category is obvious.

### Acceptance criteria

- An issue can have zero or more tags.
- Available tags: Bug, Feature, UI, Backend, Documentation and Urgent.
- Tags appear as compact labelled chips in the list and details.
- A team member can apply or remove existing tags from an issue.
- Tags can be used as a filter.
- A tag does not change an issue’s status, priority or Important state by itself.

## EX-03 Due dates and overdue state

### User story

As a Lead, I want to set a due date so that the team can see approaching and overdue work.

### Acceptance criteria

- Due date is optional when creating an issue.
- Lead can set or change the due date from Issue Details.
- The issue list displays a Due column or compact due-date label.
- An issue is overdue when its due date is before today and its status is not Closed.
- Overdue issues have an explicit `Overdue` label; no colour alone carries the meaning.
- Closed issues are not marked overdue.

## EX-04 Attachments

### User story

As a team member, I want to attach files to an issue so that the team has supporting evidence and context.

### Acceptance criteria

- Attachments are added in the Issue Details view.
- The visible file list shows name, file type, size, author and upload date/time.
- Supported mock file types are PNG, JPG, PDF, TXT and LOG.
- The prototype shows ready, uploading, upload-error and uploaded states.
- Upload-error does not add a file to the saved list.
- Attachment actions are simulated in the prototype; real file storage is outside this design scope.

## EX-05 Subtasks and checklist

### User story

As a team member, I want to manage subtasks so that large issues can be tracked as smaller steps.

### Acceptance criteria

- An issue can contain zero or more subtasks.
- A subtask has a title and a Done / Not done state.
- The details screen displays progress, for example `2 of 5 completed`.
- A team member can add a subtask and mark a subtask completed.
- A completed subtask stays visible in the list with a checked state.
- Completing all subtasks does not automatically close the parent issue.

## Shared rules

- Search, tags, due dates, attachments and subtasks do not bypass role restrictions for Assignee, Priority or Status.
- The original Important predicate remains unchanged: High/Critical AND not Closed.
- Base prototype states are still simulated unless a real backend is implemented.

