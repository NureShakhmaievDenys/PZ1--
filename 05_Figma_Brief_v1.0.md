# Mini Issue Tracker approved low fidelity design brief v1.0

## Purpose and scope

Create an internal desktop web issue tracker for one small team. Include only Release MVP stories US-01 through US-08: create, view, assign, prioritize, track status, comment and view Important Issues. Use fictional sample users Member A, Member B and Lead. Assignee is an issue-specific relationship, not an additional system role.

## Design constraints

Create editable native Figma layers on one working page. Use grayscale, desktop, low-fidelity wireframes, readable hierarchy, local reusable components and Auto Layout where practical. Preserve the exact Screen IDs in frame names. Put source references, role/state annotations and review notes outside product frames in REF-01.

Do not build a real application. The file demonstrates prepared UI states and prototype intent only; it does not prove authentication, server authorization, database persistence, response time, HTTPS or backup.

## Canonical product surfaces

### S-01 Authentication boundary

Show the application name and a neutral boundary labeled `Authentication entry — mechanism TBD`. Do not design password, SSO, social login, account recovery or any login mechanism. The demonstration begins at S-02 as an already authenticated user.

### S-02 Issues List

Create one product screen with these demonstrable states as separate Figma frames:

- `S-02-A All Issues`: header `Issues List`, Create Issue action, tabs `All Issues` and `Important Issues`. Each row shows ID, Title, Status, Priority and Assignee when assigned. The title opens the matching issue details. Show all eight sample issues.
- `S-02-B Important Issues`: same product screen and fields, with the Important Issues tab selected. It contains only ISS-001, ISS-002, ISS-003 and ISS-007.
- `S-02-C Empty`: the All Issues state when zero issues are registered. Show a clear no-issues message and Create Issue. This is not a loading or network error.

Important means: `priority is High or Critical AND status is not Closed`. High/Critical Resolved issues remain Important. Closed issues are excluded regardless of priority. Low, Normal and Not Set priorities are excluded.

### M-01 Create Issue overlay

Create a modal overlay, not a separate product page. It contains only:

- required Title input;
- required multiline Description input;
- Create action;
- Cancel action.

Show default, missing-Title and missing-Description examples. Invalid submission has no success result and creates no issue. Preserve the source copy `Title is required`; other validation copy may be concise and clear.

Prepared successful creation displays a new issue in S-03 with a generated ID, status Open, priority Not Set, no assignee, current author and created date/time. Do not expose those generated values as M-01 inputs.

### S-03 Issue Details

Show ID, Title, Description, Status, Priority, Assignee when assigned, Author, Created at and Return to Issues List. Keep assignment, priority, status and comments together here. Do not create separate product pages for any of these functions.

Use a canonical example of Lead viewing ISS-003 assigned to Member A: assignment and priority controls are enabled; status control is disabled because Lead is not the current assignee.

#### Assignment and priority

Only Lead can assign or reassign one team member and set or change priority. For other users these controls remain visible but disabled. Apply an assignee or priority with a nearby Apply action and remain on S-03 after success.

Priority display values are Not Set, Low, Normal, High and Critical. Only Low, Normal, High and Critical are selectable. Not Set means no priority is set; it is not a selectable priority or reset action.

#### Status

Only the current assignee can change status, including when the user is Lead. Show only legal next destinations, never the current status as a new transition:

| Current status | Allowed next status |
|---|---|
| Open | In Progress |
| In Progress | Resolved |
| Resolved | In Progress or Closed |
| Closed | None |

Closed has no enabled next-status action. Resolved is not Closed. Do not infer that a Closed issue disables comments, assignment or priority changes.

#### Comments

Show Comment input and Add Comment action. A saved entry shows text, author and creation date/time. Include ready, empty-comment validation, saved-comment and save-error examples. A save-error example displays an error and no saved comment entry.

## REF-01 Review notes outside product frames

Create compact annotations or component/state examples outside product UI. They must not look like product controls or a role switcher.

Show all four actor contexts:

| Action | Member non-assignee | Member assignee | Lead non-assignee | Lead assignee |
|---|---|---|---|---|
| View, create, comment | Enabled | Enabled | Enabled | Enabled |
| Assign assignee | Disabled | Disabled | Enabled | Enabled |
| Change priority | Disabled | Disabled | Enabled | Enabled |
| Change status | Disabled | Enabled if legal transition exists | Disabled | Enabled if legal transition exists |

Also show all four status transition examples, including In Progress, and an example where a non-assignee cannot change status. An unassigned issue has no user with status-change access until Lead assigns someone.

## Sample data

| ID | Status | Priority | Assignee | Important |
|---|---|---|---|---|
| ISS-001 | Open | Critical | Member A | Yes |
| ISS-002 | In Progress | High | Member B | Yes |
| ISS-003 | Resolved | High | Member A | Yes |
| ISS-004 | Closed | Critical | Member B | No |
| ISS-005 | Open | Normal | Unassigned | No |
| ISS-006 | Open | Not Set | Unassigned | No |
| ISS-007 | Resolved | Critical | Lead | Yes |
| ISS-008 | In Progress | Low | Member A | No |

The same issue ID must retain the same visible data in All Issues and Important Issues.

## Navigation intent

- S-02 tabs switch between All and Important states.
- Selecting an issue title/row opens its matching S-03.
- Create Issue opens M-01 as an overlay.
- Cancel closes M-01 and restores the calling list state without creation.
- Prepared successful Create opens prepared S-03.
- Return to Issues List restores the prior All or Important state.
- Assignment, priority, status and comment success remain on S-03.
- Invalid/forbidden operations show no success state.

Annotate this navigation intent only. Do not wire prototype interactions or implement backend logic.

## Exclusions

Do not add title/description editing after creation, deletion, attachments, AI features, dashboards, analytics, notifications, search, sorting, pagination, user administration, user-visible history, extra issue metadata, multiple assignees, extra status/priority values or transitions, an invented login method, row-selection checkboxes, bulk actions, branding, decorative imagery, page icons or empty square placeholders.

## Acceptance checklist

- Native editable Figma layers, not a raster screenshot.
- One working page; exact Screen IDs in frame names.
- Local reusable controls/rows and Auto Layout where practical.
- Grayscale low-fidelity desktop hierarchy; readable labels.
- Product frames contain no reviewer annotations.
- S-02-A, S-02-B, S-02-C, M-01 and S-03 are represented.
- All required data, permissions, status transitions, comment states and Important predicate are visible.
- No excluded feature, standalone assignment/priority/status/comments page, decorative square or bulk control is present.

## Completion report required from the Agent

Report created frames/state references, actual reusable components, requirements not represented, assumptions and limitations. Report only actual edits. Do not claim that persistence, authentication or server permissions were tested.
