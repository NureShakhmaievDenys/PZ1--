# Mini Issue Tracker Screen Map v0.1

## Status and inputs

**Status:** DRAFT for implementation review.  
**Inputs:** `01_Input_Pack_v0.1.md`; `02_Decision_Log_v1.0_APPROVED.md`.

## Product surface inventory

| ID | Name | Purpose | Actors | Entry | Key visible data and actions | Conditions and states | Exit | Source |
|---|---|---|---|---|---|---|---|---|
| S-01 | Authentication boundary | Show that access requires authentication without inventing its mechanism. | All | Opening the product. | App name; `Authentication entry — mechanism TBD`. | Placeholder only; no login fields or flow. | Demo starts at S-02. | BR-01, NFR-02, D-02 |
| S-02-A | Issues List — All | Let an authenticated user view all registered issues. | Team Member, Team Lead | Demo start; return from S-03. | Create Issue; All Issues / Important Issues tabs; rows with ID, Title, Status, Priority, Assignee if assigned. | All registered issues; no selection or bulk controls. | Open details, switch view, open create modal. | US-02, US-05, D-01 |
| S-02-B | Issues List — Important | Show the Important view of the same list. | Team Member, Team Lead | Switch from S-02-A; return from an Important-origin S-03. | Same fields and controls as S-02-A; only matching rows. | `priority ∈ {High, Critical} AND status != Closed`; Resolved stays eligible. | Return to All; open details; open create modal. | US-08, BR-09/09.1, D-01, D-07 |
| S-02-C | Issues List — Empty | Demonstrate the zero-registered-issues state. | Team Member, Team Lead | Separate demo state. | Empty-list message and Create Issue. | Represents zero issues, not a load error. | Open create modal. | AC-02.5 |
| M-01 | Create Issue modal | Create an issue from the list context. | Team Member, Team Lead | Create Issue on S-02-A or S-02-B. | Required Title; required multiline Description; Create; Cancel; validation examples. | Default, missing Title, missing Description, prepared success. Only Title and Description are inputs. | Cancel returns to invoking list state; success goes to prepared S-03. | US-01, BR-02–BR-04, D-01, D-04, D-07, D-08 |
| S-03 | Issue Details | View an issue and keep all permitted issue actions together. | Team Member, Team Lead | Select title/row from a list; prepared post-create state. | ID, Title, Description, Status, Priority, Assignee when assigned, Author, Created at; comments; Return to Issues List. | Assignee/priority only for Lead; status only for current assignee and valid next transition; comments for any team member. Show ready, validation, saved and save-error comment states. | Return to prior list state; no separate assignment/priority/status/comments pages. | US-02–US-07; BR-05–BR-08.1; D-03–D-09 |
| REF-01 | Review notes and state reference | Supply developer/reviewer evidence outside product UI. | Reviewer | Beside product frames. | Permission matrix; four status examples; test actor and issue IDs; error/empty examples. | Not clickable product UI; not a role switcher. | None. | D-05, D-08, D-09 |

## Required Figma frames

Product surfaces remain S-01, S-02, M-01 and S-03. Figma should use separate frames for the demonstrable states: S-02-A, S-02-B, S-02-C; M-01 default, missing-title and missing-description; S-03 canonical details and compact examples for comment and permission/status states. REF-01 remains outside product frames.

## Transition table

| T-ID | From | Actor | Trigger | Preconditions | To | Visible result | Source |
|---|---|---|---|---|---|---|---|
| T-01 | S-02-A | Any authenticated member | Select a title/row | Issue exists. | S-03 | Details match selected issue ID. | AC-02.3, D-07 |
| T-02 | S-02-A | Any authenticated member | Select Important Issues | Test data ISS-001…ISS-008 is present. | S-02-B | Only ISS-001, ISS-002, ISS-003 and ISS-007 are visible. | AC-08.1–AC-08.4, BR-09.1, D-01 |
| T-03 | S-02-B | Any authenticated member | Select All Issues | — | S-02-A | Same list surface, all registered issues. | US-02, D-01 |
| T-04 | S-02-A or S-02-B | Any authenticated member | Create Issue | — | M-01 | Modal opens over calling list state. | US-01, D-01 |
| T-05 | M-01 | Any authenticated member | Cancel | No submission. | Calling S-02 state | Modal closes; no issue is created. | US-01, D-07 |
| T-06 | M-01 | Any authenticated member | Create with missing Title or Description | Required value absent. | M-01 validation state | Error shown; no issue created. | AC-01.2, AC-01.3, D-08 |
| T-07 | M-01 | Any authenticated member | Create valid issue | Title and Description present. | Prepared S-03 | New ID, Open, Not Set, author and created_at shown; assignee absent. | AC-01.4–AC-01.5, D-04, D-08 |
| T-08 | S-03 | Team Lead | Apply assignee | Selected user is team member. | S-03 | Selected assignee shown. | US-03, D-04, D-06 |
| T-09 | S-03 | Team Lead | Apply priority | Selected value is Low/Normal/High/Critical. | S-03 | Selected priority shown. | US-04, BR-05–BR-06, D-06 |
| T-10A | S-03 | Current assignee | Apply In Progress | Current status is Open. | S-03 | Status becomes In Progress. | BR-08.1 |
| T-10B | S-03 | Current assignee | Apply Resolved | Current status is In Progress. | S-03 | Status becomes Resolved. | BR-08.1 |
| T-10C | S-03 | Current assignee | Apply In Progress | Current status is Resolved. | S-03 | Status becomes In Progress. | BR-08.1 |
| T-10D | S-03 | Current assignee | Apply Closed | Current status is Resolved. | S-03 | Status becomes Closed. | BR-08.1 |
| T-11 | S-03 | Non-assignee or assignee in Closed | Attempt status action | Not current assignee or no valid outgoing transition. | No product transition | Status control disabled or local error state; no success shown. | AC-07.4–AC-07.5, BR-08.1, D-05, D-09 |
| T-12 | S-03 | Any authenticated member | Add valid comment | Non-empty text; prepared success. | S-03 | Saved entry with text, author and date/time. | AC-06.1–AC-06.4, D-08 |
| T-13 | S-03 | Any authenticated member | Add empty comment or simulate save failure | Empty text or prepared failure state. | S-03 | Validation/error; no saved entry in failure case. | AC-06.1, AC-06.5, D-08 |
| T-14 | S-03 | Any authenticated member | Return to Issues List | Origin list state known. | Origin S-02-A or S-02-B | Previous list context restored. | D-07 |
| T-15 | S-02-C | Any authenticated member | Open the zero-issues state | No issues are registered. | S-02-C | No-issues message and Create Issue are visible. | AC-02.5 |
| T-16 | S-03 | Team Member, any assignee context | Attempt assignment or priority action | Current actor is not Team Lead. | No product transition | Assignment and priority controls are disabled; no success result exists. | US-03 AC point 3, AC-04.2, D-05 |

## Scenario flows

1. **Create and inspect:** S-02-A → M-01 → validation or prepared success → S-03 → S-02-A.
2. **Assign and prioritize:** S-02-A → S-03 as Team Lead → select assignee / Apply → select priority / Apply → remain S-03.
3. **Change status:** current assignee completes each prepared route: Open → In Progress; In Progress → Resolved; Resolved → In Progress; Resolved → Closed. Closed has no outgoing status action.
4. **Comment:** S-03 → Add Comment → saved state, validation state, or save-error state on S-03.
5. **View Important:** S-02-A → S-02-B; show High/Critical issues except Closed, including High/Critical Resolved issues.
6. **Forbidden status action:** S-03 as non-assignee or as Lead who is not assignee → no success route; disabled/error evidence only.
7. **Empty list:** S-02-C → M-01 or remain in clear no-issues state.

## Test data for Important Issues

| ID | Status | Priority | Assignee | Expected in Important |
|---|---|---|---|---|
| ISS-001 | Open | Critical | Member A | Yes |
| ISS-002 | In Progress | High | Member B | Yes |
| ISS-003 | Resolved | High | Member A | Yes |
| ISS-004 | Closed | Critical | Member B | No |
| ISS-005 | Open | Normal | Unassigned | No |
| ISS-006 | Open | Not Set | Unassigned | No |
| ISS-007 | Resolved | Critical | Lead | Yes |
| ISS-008 | In Progress | Low | Member A | No |

Expected S-02-B set: **ISS-001, ISS-002, ISS-003, ISS-007**. The same ID must retain the same field values between S-02-A and S-02-B.

## Exclusions to preserve

Do not add deletion, attachments, AI features, dashboards, analytics, search, sort, pagination, notifications, user administration, history, bulk actions, row selection, extra metadata, multiple assignees, extra statuses/priorities/transitions, or a real login method.

## Coverage gaps before Screen Contracts

The plan covers all source scenarios at screen/state level. Screen Contracts must still define every C-ID, exact visible error state, sample data and AC-to-test traceability. Persistence, server authorization, response time, HTTPS and backup remain implementation tests, not wireframe PASS conditions.
