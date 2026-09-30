# Mini Issue Tracker Developer Verifiable Screen Contracts v0.1

## Status and verification boundaries

**Status:** DRAFT for plan review.  
**Inputs:** `SD_Spec.docx`; `01_Input_Pack_v0.1.md`; `02_Decision_Log_v1.0_APPROVED.md`; `03_Screen_Map_v0.1.md`.

Verification levels: **UI** = visible in a wireframe; **PROTOTYPE** = manually demonstrable prepared navigation/state; **IMPLEMENTATION** = needs actual authentication, backend, persistence, authorization or performance/security testing.

## Shared data and rules

| Data/control | Contract | Source |
|---|---|---|
| Issue ID | Generated on successful creation; visible in list and details. | AC-01.4, AC-02.2, AC-02.4 |
| Title / Description | Both are required to create. Description is multiline. No post-create editing in approved scope. | AC-01.1–AC-01.3, D-01 |
| Status | Values: Open, In Progress, Resolved, Closed. Initial: Open. | BR-03, BR-07, AC-07.1–AC-07.2 |
| Priority | Display values: Not Set, Low, Normal, High, Critical. Selectable values: Low, Normal, High, Critical. Initial: Not Set. | BR-04–BR-06, AC-01.5, AC-04.1 |
| Assignee | One team member; initial value absent by D-04. | US-03; A-04; D-04 |
| Important predicate | `priority ∈ {High, Critical} AND status != Closed`. Resolved High/Critical remains included. | AC-08.1–AC-08.4; BR-09/09.1 |
| Comments | Non-empty text; saved entry contains text, author and creation date/time. Failed save leaves no saved entry. | AC-06.1–AC-06.5 |

### Required test data

| ID | Status | Priority | Assignee | Important result |
|---|---|---|---|---|
| ISS-001 | Open | Critical | Member A | Included |
| ISS-002 | In Progress | High | Member B | Included |
| ISS-003 | Resolved | High | Member A | Included |
| ISS-004 | Closed | Critical | Member B | Excluded |
| ISS-005 | Open | Normal | Unassigned | Excluded |
| ISS-006 | Open | Not Set | Unassigned | Excluded |
| ISS-007 | Resolved | Critical | Lead | Included |
| ISS-008 | In Progress | Low | Member A | Excluded |

Expected Important IDs: ISS-001, ISS-002, ISS-003 and ISS-007. This set proves that Resolved is not excluded, Closed is excluded despite Critical priority, and Not Set is not silently treated as Normal or High.

## S-01 Authentication boundary

**Purpose:** state the authentication requirement without inventing a login mechanism.  
**Actors:** Team Member, Team Lead.  
**Entry:** product opening.  
**Visible data:** product name and `Authentication entry — mechanism TBD`.  
**Controls:** none.  
**Exit:** the wireframe/prototype demo begins at S-02 as an authenticated user.

| C-ID | Control | Visible/enabled condition | Result | Source | Verification |
|---|---|---|---|---|---|
| C-01 | Authentication boundary note | Always visible on S-01. | Makes the auth boundary explicit; does not authenticate. | BR-01, NFR-02, D-02 | UI |

**Not proven:** actual authentication, identity, access enforcement or security.

## S-02 Issues List

### S-02-A All Issues

**Purpose:** view all registered issues. **Actors:** authenticated Team Member and Team Lead. **Entry:** demo start, All tab, return from S-03.  
**Visible data per row:** ID, Title, Status, Priority, Assignee when assigned.  
**Empty state:** use S-02-C if zero issues exist.

| C-ID | Control | Visible/enabled condition | Trigger and result | Source | Verification |
|---|---|---|---|---|---|
| C-02 | All Issues tab | Visible and selected in S-02-A. | Shows all registered issues. | AC-02.1, D-01 | UI / PROTOTYPE |
| C-03 | Important Issues tab | Visible for any authenticated user. | Switches to S-02-B. | US-08, T-02 | UI / PROTOTYPE |
| C-04 | Issue title/row | One control for each visible issue. | Opens matching S-03 by issue ID. | AC-02.3, T-01 | UI / PROTOTYPE |
| C-05 | Create Issue | Visible and enabled for authenticated Team Member and Team Lead. | Opens M-01. | BR-02, T-04 | UI / PROTOTYPE |

### S-02-B Important Issues

**Purpose:** show the filtered state of S-02, not a separate product page. **Entry:** C-03 or return from an Important-origin details view.  
**Visible data:** same columns as S-02-A.  
**Predicate:** High/Critical AND not Closed. A Resolved High/Critical issue remains visible.

| C-ID | Control | Visible/enabled condition | Trigger and result | Source | Verification |
|---|---|---|---|---|---|
| C-06 | All Issues tab | Visible for any authenticated user. | Returns to S-02-A. | D-01, T-03 | UI / PROTOTYPE |
| C-07 | Important Issues tab | Visible and selected in S-02-B. | Retains filtered state. | AC-08.1–AC-08.4 | UI |
| C-08 | Issue title/row | One control for each Important issue. | Opens matching S-03. | AC-02.3, T-01 | UI / PROTOTYPE |

### S-02-C Empty All Issues

**Purpose:** show the state when zero issues are registered. **Visible data:** an unambiguous no-issues message and C-05.  
**Excluded interpretation:** it is not a loading/network error and does not represent the separate optional “no Important issues” condition.

| C-ID | Control | Visible/enabled condition | Trigger and result | Source | Verification |
|---|---|---|---|---|---|
| C-09 | Empty-list message | Visible when registered issue count is zero. | Explains no issues exist. | AC-02.5 | UI |

## M-01 Create Issue modal

**Purpose:** create one issue while retaining the calling list context.  
**Actors:** authenticated Team Member and Team Lead.  
**Entry:** C-05 from S-02-A or S-02-B.  
**User-entered fields:** Title and Description only.  
**Automatic data after prepared success:** ID, Open, Not Set, author, created_at, no assignee.

| C-ID | Control | Visible/enabled condition | Trigger and result | Source | Verification |
|---|---|---|---|---|---|
| C-10 | Title input | Always visible; required. | Accepts title. Missing value on submit shows inline error `Title is required`. | AC-01.1–AC-01.2 | UI / PROTOTYPE |
| C-11 | Description input | Always visible; required; multiline. | Accepts description. Missing value on submit shows inline required-state feedback. | AC-01.1, AC-01.3 | UI / PROTOTYPE |
| C-12 | Create | Visible and enabled before prepared submission. | Valid input → prepared S-03; invalid input → M-01 validation state; no issue on invalid submission. | AC-01.2–AC-01.5, T-06/T-07 | UI / PROTOTYPE |
| C-13 | Cancel | Always visible. | Closes M-01 and restores calling S-02 state without issue creation. | D-07, T-05 | UI / PROTOTYPE |

**Required states:** default; Title missing; Description missing; prepared success.  
**Not proven:** ID uniqueness, persistence, real created_at, authenticated current author.

## S-03 Issue Details

**Purpose:** view details and provide every approved issue action without separate assignment, priority, status or comment screens.  
**Actors:** authenticated Team Member and Team Lead.  
**Entry:** C-04/C-08 or prepared success from M-01.  
**Visible data:** ID, Title, Description, Status, Priority, Assignee if assigned, Author, Created at.

| C-ID | Control | Visible/enabled condition | Trigger and visible result | Source | Verification |
|---|---|---|---|---|---|
| C-14 | Return to Issues List | Always visible. | Restores source list state S-02-A or S-02-B. | D-07, T-14 | UI / PROTOTYPE |
| C-15 | Assignee selector | Visible for all; enabled only for Team Lead. Values are team members; one value only. | Lead selects assignee then C-16 applies it; selected assignee is displayed. | US-03, D-04–D-06, T-08 | UI / PROTOTYPE / IMPLEMENTATION authorization |
| C-16 | Apply assignee | Enabled only after a valid Lead selection. | Updates visible assignee and remains on S-03. | US-03, D-06, T-08 | UI / PROTOTYPE |
| C-17 | Priority selector | Visible for all; enabled only for Team Lead. Values only Low, Normal, High, Critical; Not Set is display only. | Lead selects priority then C-18 applies it. | AC-04.1–AC-04.2, BR-05–BR-06, D-03, T-09 | UI / PROTOTYPE / IMPLEMENTATION authorization |
| C-18 | Apply priority | Enabled only after valid Lead selection. | Updates visible priority and remains on S-03. | US-04, D-06, T-09 | UI / PROTOTYPE |
| C-19 | Status selector | Visible for all; enabled only if current user equals current assignee and current status has a BR-08.1 destination. Options only allowed next status(es), never current status. | Assignee selects next status then C-20 applies it. | AC-07.2–AC-07.5, BR-08.1, D-05–D-06, T-10/T-11 | UI / PROTOTYPE / IMPLEMENTATION authorization |
| C-20 | Apply status | Enabled only after a valid C-19 selection. | Updates status and remains on S-03. Closed has no enabled next-status action. | BR-08.1, T-10/T-11 | UI / PROTOTYPE |
| C-21 | Comment input | Visible and enabled for authenticated team members; required. | Empty submit produces validation and no entry. | AC-06.1, T-13 | UI / PROTOTYPE |
| C-22 | Add Comment | Enabled with non-empty prepared input. | Success shows saved entry; prepared failure shows error and adds no entry. | AC-06.2–AC-06.5, T-12/T-13 | UI / PROTOTYPE |
| C-23 | Comment entry | Visible after prepared successful comment. | Shows comment text, author, creation date/time. | AC-06.2–AC-06.4 | UI |
| C-24 | Status access feedback | Visible when an invalid/forbidden status attempt must be demonstrated. | Local disabled or error state; no success feedback. | AC-07.4–AC-07.5, D-09 | UI / PROTOTYPE |

**Required state examples:**

- Lead viewing assigned issue: C-15–C-18 enabled; C-19 disabled when Lead is not current assignee.
- Member who is current assignee: C-19/C-20 enabled only for legal status destination; C-15–C-18 disabled.
- Member who is not assignee: C-15–C-20 disabled except read-only current values.
- Closed issue: no enabled next-status action even for the assignee.
- Comments: ready, empty-text validation, saved entry and failed-save error without an added entry.

## Permission matrix

| Action | Member non-assignee | Member assignee | Lead non-assignee | Lead assignee |
|---|---|---|---|---|
| View issue/list | Yes | Yes | Yes | Yes |
| Create issue | Yes | Yes | Yes | Yes |
| Add comment | Yes | Yes | Yes | Yes |
| Assign/reassign assignee | No | No | Yes | Yes |
| Set/change priority | No | No | Yes | Yes |
| Change status | No | Yes, if a legal next transition exists | No | Yes, if a legal next transition exists |

Assignee is an issue-specific relationship, not a global third role. No assigned user means nobody has status-change access until a Lead assigns one. UI availability is not proof of server-side authorization.

## Status transition matrix

| Current status | Open | In Progress | Resolved | Closed |
|---|---|---|---|---|
| Open | Current; not selectable | Allowed | Forbidden | Forbidden |
| In Progress | Forbidden | Current; not selectable | Allowed | Forbidden |
| Resolved | Forbidden | Allowed | Current; not selectable | Allowed |
| Closed | Forbidden | Forbidden | Forbidden | Current; not selectable |

Only the current assignee may execute an allowed transition. `Resolved` remains different from `Closed`; the lack of a status transition from Closed does not itself prohibit comments, assignment or priority changes.

## Test cases

| Test ID | Actor/context | Preconditions and action | Expected visible result | Not proven |
|---|---|---|---|---|
| T-01 | Any authenticated member | Select an issue row. | Matching S-03 opens. | Data retrieval/persistence. |
| T-02 | Any authenticated member | Switch All → Important with ISS-001…ISS-008 visible in All. | Important shows exactly ISS-001, ISS-002, ISS-003 and ISS-007; their field values are unchanged. | Real filtering. |
| T-03 | Any authenticated member | Switch Important → All. | All-list state appears. | Real filtering. |
| T-04 | Any authenticated member | Select Create Issue. | M-01 opens. | Authentication enforcement. |
| T-05 | Any authenticated member | Cancel M-01. | Calling list state returns; no prepared issue shown. | No database write. |
| T-06 | Any authenticated member | Submit empty Title/Description. | Inline validation; no success state. | Server validation. |
| T-07 | Any authenticated member | Submit valid prepared Title/Description. | S-03 shows generated fields, Open, Not Set, author/time and no assignee. | Persistence/ID generation. |
| T-08 | Team Lead | Select team member and Apply assignee. | One assignee shown on S-03. | Server role validation. |
| T-09 | Team Lead | Select allowed priority and Apply. | Selected priority shown. | Persistence/server role validation. |
| T-10A | Current assignee | Open → In Progress. | In Progress shown. | Persistence/server transition validation. |
| T-10B | Current assignee | In Progress → Resolved. | Resolved shown. | Persistence/server transition validation. |
| T-10C | Current assignee | Resolved → In Progress. | In Progress shown. | Persistence/server transition validation. |
| T-10D | Current assignee | Resolved → Closed. | Closed shown; no next status action. | Persistence/server transition validation. |
| T-11 | Non-assignee or Closed assignee | Attempt status action. | Control disabled/local error; no success. | Server-side enforcement. |
| T-12 | Any authenticated member | Add valid prepared comment. | Entry shows text, author and time. | Persistence/transaction. |
| T-13 | Any authenticated member | Submit empty comment or prepared save failure. | Error; failed/invalid entry absent. | Server transaction handling. |
| T-14 | Any authenticated member | Return from S-03. | Prior All/Important state restored. | Navigation state persistence. |
| T-15 | Any authenticated member | Open S-02-C when zero issues exist. | No-issues message and Create Issue are visible. | Data retrieval. |
| T-16 | Team Member | Attempt assignment or priority action. | Related controls are disabled; no success route. | Server-side role enforcement. |

## Traceability

| Source | UIR-ID | Screen/state and evidence | Test | Level |
|---|---|---|---|---|
| AC-01.1 | UIR-01 | M-01 C-10/C-11 | T-07 | UI / PROTOTYPE |
| AC-01.2 | UIR-02 | M-01 Title required state | T-06 | UI / PROTOTYPE |
| AC-01.3 | UIR-03 | M-01 Description required state | T-06 | UI / PROTOTYPE |
| AC-01.4 | UIR-04 | M-01 prepared success → S-03 visible ID/Open/author/created_at | T-07 | UI / PROTOTYPE; generation/persistence IMPLEMENTATION |
| AC-01.5 | UIR-05 | S-03 prepared success shows Not Set | T-07 | UI / PROTOTYPE |
| AC-02.1 | UIR-06 | S-02-A C-02 | T-01 | UI / PROTOTYPE |
| AC-02.2 | UIR-07 | S-02-A row data | T-01 | UI |
| AC-02.3 | UIR-08 | S-02 C-04/C-08 → S-03 | T-01 | UI / PROTOTYPE |
| AC-02.4 | UIR-09 | S-03 visible detail fields | T-01 | UI |
| AC-02.5 | UIR-10 | S-02-C C-09 | T-15 | UI |
| US-03 AC point 1 | UIR-11 | S-03 C-15 single selector | T-08 | UI |
| US-03 AC point 2 | UIR-12 | S-03 C-15 team-member options | T-08 | UI; data validation IMPLEMENTATION |
| US-03 AC point 3 | UIR-13 | REF-01 / C-15 disabled for Members | T-16 | UI / PROTOTYPE; authorization IMPLEMENTATION |
| US-03 AC point 4 | UIR-14 | S-02 row and S-03 Assignee display | T-08 | UI |
| AC-04.1 | UIR-15 | S-03 C-17 allowed values | T-09 | UI |
| AC-04.2 | UIR-16 | C-17/C-18 disabled for Members | T-16 | UI / PROTOTYPE; authorization IMPLEMENTATION |
| AC-05.1 | UIR-17 | S-02 and S-03 current status | T-01 | UI |
| AC-05.2 | UIR-18 | S-03 Status display | T-01 | UI |
| AC-05.3 | UIR-19 | S-02 row Status column | T-01 | UI |
| AC-06.1 | UIR-20 | S-03 C-21 validation | T-13 | UI / PROTOTYPE |
| AC-06.2 | UIR-21 | S-03 C-22/C-23 saved comment | T-12 | UI / PROTOTYPE; persistence IMPLEMENTATION |
| AC-06.3 | UIR-22 | S-03 C-23 author | T-12 | UI |
| AC-06.4 | UIR-23 | S-03 C-23 date/time | T-12 | UI |
| AC-06.5 | UIR-24 | S-03 save-error with no C-23 entry | T-13 | UI / PROTOTYPE; transaction IMPLEMENTATION |
| AC-07.1 | UIR-25 | M-01 success / S-03 Open | T-07 | UI / PROTOTYPE |
| AC-07.2 | UIR-26 | S-03 C-19 and transition matrix | T-10A–T-10D | UI |
| AC-07.3 | UIR-27 | S-03 updated prepared status | T-10A–T-10D | UI / PROTOTYPE; persistence IMPLEMENTATION |
| AC-07.4 | UIR-28 | C-19/C-20 disabled for non-assignee | T-11 | UI / PROTOTYPE; authorization IMPLEMENTATION |
| AC-07.5 | UIR-29 | C-19 only exposes valid allowed destinations | T-10A–T-10D, T-11 | UI / PROTOTYPE; enforcement IMPLEMENTATION |
| AC-08.1 | UIR-30 | S-02-B High non-Closed row | T-02 | UI |
| AC-08.2 | UIR-31 | S-02-B Critical non-Closed row | T-02 | UI |
| AC-08.3 | UIR-32 | S-02-B excludes Low/Normal rows | T-02 | UI |
| AC-08.4 | UIR-33 | S-02-B excludes every Closed row | T-02 | UI |

## Outstanding implementation tests

Authentication, server-side authorization, database persistence, ID uniqueness, true timestamps, actual response time under one second, HTTPS and backup require implementation-level tests. A static wireframe or prepared prototype state must not be marked PASS for these items.
