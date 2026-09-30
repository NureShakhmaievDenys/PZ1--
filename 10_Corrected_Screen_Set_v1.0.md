# Mini Issue Tracker — corrected screen set v1.0

## Source alignment

This set is aligned with `00_Source/SD_Spec.docx` and the methodological guide.

| Source ID | Scope in the screen set |
|---|---|
| US-01 | Create Issue |
| US-02 | View Issues |
| US-03 | Assign Issue to the responsible team member |
| US-04 | Set Issue Priority |
| US-05 | Track Issue Progress |
| US-06 | Add Comment |
| US-07 | Update Issue Status |
| US-08 | View Important Open Issues |

## Non-negotiable rules

- Important = `(Priority is High or Critical) AND Status is not Closed`.
- Resolved High/Critical issues remain Important.
- Allowed transitions only: Open → In Progress; In Progress → Resolved; Resolved → In Progress; Resolved → Closed.
- Only the current assignee can change status, including a Lead. A Lead non-assignee has a disabled Status control.
- A Lead may assign/reassign an issue and set its priority. A Member cannot.
- A new issue has generated ID, Open, Not Set priority, no assignee, current author and generated creation time.
- The product has no real login, persistence, file attachments, search, notifications, delete action or AI features.

## Product frames

### S-01 Authentication boundary

Purpose: establish the scope boundary only.

- Header: Mini Issue Tracker.
- Centered neutral card: `Authentication entry — mechanism TBD`.
- No login form, password field, social login or submit button.
- Prototype demonstration starts at S-02-A as an already authenticated user.

### S-02-A All Issues

Purpose: canonical list of all sample issues.

- Header: Mini Issue Tracker.
- Page title: Issues List.
- Tabs: All Issues (active), Important Issues.
- Primary action: Create Issue.
- Row fields: ID, Title, Status, Priority, Assignee.
- Clicking a title or a row opens S-03 for that issue.

Sample rows:

| ID | Title | Status | Priority | Assignee |
|---|---|---|---|---|
| ISS-001 | Checkout blocks on expired session | Open | Critical | Member A |
| ISS-002 | Invite email not delivered | In Progress | High | Member B |
| ISS-003 | Export fails for large records | Resolved | High | Member A |
| ISS-004 | Archived item count is incorrect | Closed | Critical | Member B |
| ISS-005 | Profile timezone resets | Open | Normal | Unassigned |
| ISS-006 | Empty state copy wraps | Open | Not Set | Unassigned |
| ISS-007 | Audit log omits actor | Resolved | Critical | Lead |
| ISS-008 | Keyboard focus skips action | In Progress | Low | Member A |

### S-02-B Important Issues

Purpose: the same product list in its Important state.

- All Issues tab is inactive; Important Issues is active.
- Use the same columns and Create Issue action as S-02-A.
- Show only ISS-001, ISS-002, ISS-003 and ISS-007.
- Do not exclude ISS-003 or ISS-007 only because their status is Resolved.

### S-02-C Empty state

Purpose: show a zero-issue All Issues state.

- All Issues tab is active.
- Empty message: `No issues have been created`.
- Supporting text: `Create the first issue for this team.`
- Create Issue action remains available.

### M-01 Create Issue overlay

Purpose: create one issue using two editable fields only.

- Overlay above the calling list; dark scrim behind it.
- Title — required, single-line.
- Description — required, multiline.
- Actions: Cancel and Create.
- Show compact state examples: default, missing Title with `Title is required`, and missing Description with a local error.
- No inputs for ID, author, assignee, priority, status or created time.

### S-03 Issue Details

Purpose: inspect an issue, comment and expose role-dependent controls.

- Return to Issues List.
- Read-only fields: ID, Title, Description, Status, Priority, Assignee, Author, Created at.
- Comments section: ready input, empty-comment error, saved-comment example and save-error example. A save-error state must not add a saved comment.
- Keep Assignee, Priority and Status controls together. Each control uses a select plus Apply.

Canonical control example:

- Current issue: ISS-003, assignee Member A.
- Current viewer: Lead, not assignee.
- Assignee and Priority controls: enabled.
- Status control: disabled.

Compact control-state examples in REF-01:

| Viewer | Assignment / Priority | Status |
|---|---|---|
| Member, not assignee | disabled | disabled |
| Member, current assignee | disabled | enabled only for legal next transition |
| Lead, not assignee | enabled | disabled |
| Lead, current assignee | enabled | enabled only for legal next transition |

### REF-01 Review notes and states

Place this frame outside all product frames. It is not a product screen.

It must contain:

- the four-context permission matrix;
- the status transition matrix;
- the Important predicate and expected IDs;
- creation defaults and validation examples;
- comment ready, error, saved and save-error examples;
- a note that backend, persistence and real authentication are not proven by the prototype.

## Basic prototype route

1. S-02-A All Issues → Important Issues → S-02-B.
2. S-02-B → All Issues → S-02-A.
3. S-02-A or S-02-B → Create Issue → M-01 as overlay.
4. M-01 Cancel → calling list state without creation.
5. M-01 valid Create → prepared S-03 success state for a generated issue.
6. S-02 title or row → S-03 for the selected issue.
7. S-03 Return → the list state that opened it.

No interaction needs to claim a real database update or server-side authorization check.
