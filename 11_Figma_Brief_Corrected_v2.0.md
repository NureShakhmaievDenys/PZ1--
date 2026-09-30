# Mini Issue Tracker — corrected Figma brief v2.0

Build editable native Figma layers on one page. Use desktop grayscale low-fidelity wireframes, readable text, reusable local rows and controls, and preserve the frame IDs below. Put all review notes outside product frames in REF-01.

## Scope

Create only US-01–US-08 from the source specification: create, view, assign, prioritize, track progress, comment, update status and view important non-closed issues. Use fictional users Member A, Member B and Lead. Assignee is an issue-specific relationship, not a global role.

## Required frames

- `S-01 Authentication boundary`
- `S-02-A All Issues`
- `S-02-B Important Issues`
- `S-02-C Empty`
- `M-01 Create Issue overlay`
- `S-03 Issue Details`
- `REF-01 Review notes outside product frames`

## Hard rules

- S-01 is a neutral `Authentication entry — mechanism TBD` boundary. Do not design login fields, passwords or social login.
- S-02 rows show ID, Title, Status, Priority and Assignee. Use the sample issue data in `10_Corrected_Screen_Set_v1.0.md`.
- Important = High/Critical AND not Closed. Resolved High/Critical issues stay in Important.
- M-01 has only required Title and multiline Description. Show default, missing-Title and missing-Description examples. Do not expose generated values as inputs.
- New issue result: generated ID, Open, Not Set priority, Unassigned assignee, current author and generated time.
- S-03 shows ID, Title, Description, Status, Priority, Assignee, Author, Created at and comments.
- Lead can assign/reassign and set priority. Only current assignee can change status, including Lead. Lead non-assignee must see Status disabled.
- Legal transitions only: Open → In Progress; In Progress → Resolved; Resolved → In Progress or Closed. Closed has no outgoing transition.
- Show comments ready, empty validation, saved and save-error states. Do not show a saved comment after a save error.
- Do not add delete, attachments, search, sort, filters, analytics, dashboard, notifications, user administration, history, extra metadata, multi-assignee, invented login, row selection, bulk actions, decorative images or icon placeholders.

## Prototype

Wire only basic navigation: All ↔ Important; list → Create overlay; Cancel → calling list; successful prepared Create → S-03; row/title → S-03; Return → prior list state. The prototype is a simulation, not a backend application.
