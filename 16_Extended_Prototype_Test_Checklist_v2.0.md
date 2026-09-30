# Extended prototype test checklist v2.0

## Search and filters

- [ ] Search by `ISS-003` or `Export` finds the expected issue.
- [ ] Status, priority, assignee, tag and due-date filters are available.
- [ ] Applied filters appear as visible chips.
- [ ] Filtered result state has matching issues only.
- [ ] No-result state has a clear action.

## Tags and due dates

- [ ] Tags are visible in a list row and on S-03.
- [ ] Tag filter produces the expected subset.
- [ ] Due date can be set in M-01 and changed by Lead in S-03.
- [ ] Overdue is textually labelled and is absent for Closed issues.

## Attachments

- [ ] Attachment section includes a ready state and Add attachment action.
- [ ] Uploading, upload-error and uploaded states are distinct.
- [ ] Upload error does not show a saved attachment row.

## Subtasks

- [ ] Progress count is visible.
- [ ] New subtask appears after the prepared add action.
- [ ] Checked subtask remains visible.
- [ ] Completing all subtasks does not close the parent issue.

## Regression

- [ ] Important still means High/Critical AND not Closed.
- [ ] Status is still changeable only by the current assignee.
- [ ] Assignment and priority are still Lead-only.
