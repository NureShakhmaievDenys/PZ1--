# Mini Issue Tracker Plan Review v0.1

## Scope of review

Reviewed against `SD_Spec.docx`: `01_Input_Pack_v0.1.md`, approved Decision Log v1.0, Screen Map v0.1 and Screen Contracts v0.1. The review checks the design plan, not a Figma file or implementation.

## Result

**PLAN NOT READY.** The required screens, core permissions, allowed transitions, scope boundaries and traceability structure are present. Four test/verification gaps must be corrected before Figma Brief generation so that acceptance evidence is not overstated.

## AC coverage matrix

| Source | Result | Evidence or issue |
|---|---|---|
| AC-01.1 | COVERED | M-01 C-10/C-11; T-07. |
| AC-01.2 | COVERED | Required Title state; T-06. |
| AC-01.3 | COVERED | Required Description state; T-06. |
| AC-01.4 | COVERED | Prepared success S-03; T-07; persistence retained as implementation test. |
| AC-01.5 | COVERED | Not Set after create; T-07. |
| AC-02.1 | COVERED | S-02-A; T-01. |
| AC-02.2 | COVERED | Required row fields on S-02-A. |
| AC-02.3 | COVERED | C-04/C-08 to S-03; T-01. |
| AC-02.4 | COVERED | S-03 detail field set. |
| AC-02.5 | AMBIGUOUS | S-02-C exists, but traceability points to T-04, which only opens Create Issue. See DEF-01. |
| US-03 AC point 1 | COVERED | Single assignee selector C-15. |
| US-03 AC point 2 | COVERED | C-15 restricts selection to team-member values; backend validation not claimed. |
| US-03 AC point 3 | AMBIGUOUS | UI says Members are disabled, but T-08 tests only Lead success. See DEF-02. |
| US-03 AC point 4 | COVERED | Assignee appears in list/details. |
| AC-04.1 | COVERED | C-17 exposes only four settable values. |
| AC-04.2 | AMBIGUOUS | UI says Member control is disabled, but T-09 tests only Lead success. See DEF-02. |
| AC-05.1 | COVERED | Current status appears on list/details. |
| AC-05.2 | COVERED | S-03 Status. |
| AC-05.3 | COVERED | S-02 Status column. |
| AC-06.1 | COVERED | Empty-comment validation; T-13. |
| AC-06.2 | COVERED | Prepared saved comment; persistence correctly kept as implementation test. |
| AC-06.3 | COVERED | Comment author visible. |
| AC-06.4 | COVERED | Comment date/time visible. |
| AC-06.5 | COVERED | Save-error state adds no entry; T-13. |
| AC-07.1 | COVERED | Prepared create result has Open. |
| AC-07.2 | COVERED | Four values and transition matrix. |
| AC-07.3 | COVERED | Prepared changed status; persistence not claimed. |
| AC-07.4 | COVERED | Non-assignee status state; T-11. |
| AC-07.5 | AMBIGUOUS | Matrix is correct, but T-10 does not enumerate all four legal transitions. See DEF-03. |
| AC-08.1 | AMBIGUOUS | Predicate is correct, but no fixed High/non-Closed sample is defined for testing. See DEF-04. |
| AC-08.2 | AMBIGUOUS | Predicate is correct, but no fixed Critical/non-Closed sample is defined for testing. See DEF-04. |
| AC-08.3 | AMBIGUOUS | Predicate is correct, but no fixed excluded Low/Normal sample is defined. See DEF-04. |
| AC-08.4 | AMBIGUOUS | Predicate is correct, but no fixed excluded Closed sample is defined. See DEF-04. |

## Targeted rule checks

| Check | Result | Evidence |
|---|---|---|
| Lead non-assignee cannot change status | PASS | Permission matrix and C-19 allow status only for current assignee. |
| Create has only Title and Description as inputs | PASS | M-01 contract explicitly limits inputs. |
| New issue defaults | PASS | Prepared success specifies Open, Not Set, ID, author, created_at and approved unassigned value. |
| All four legal status transitions | PARTIAL | Matrix is correct; explicit demonstration cases are missing. |
| Closed has no outgoing status transition | PASS | Matrix and C-20 state this. |
| Resolved differs from Closed | PASS | Matrix and Important predicate retain Resolved. |
| Important predicate | PASS in logic / PARTIAL in test data | Correct formula exists; examples are not yet fixed. |
| Comment validation and failed save | PASS | Separate no-entry validation/error states exist. |
| Out-of-scope features absent | PASS | Exclusions list prevents delete, attachments, AI, dashboard, search, bulk controls and invented login. |

## Defect log

| DEF-ID | Severity | Source | Plan location | Problem | Minimal correction |
|---|---|---|---|---|---|
| DEF-01 | Major | AC-02.5 | Screen Contracts traceability UIR-10 | AC-02.5 points to T-04, but T-04 verifies opening M-01, not the empty list. | Add a dedicated test for S-02-C: zero registered issues → visible no-issues state. Point UIR-10 to it. |
| DEF-02 | Major | US-03 AC point 3; AC-04.2 | UIR-13, UIR-16; T-08/T-09 | The contract defines Member-disabled assignment/priority controls, but both linked tests exercise only successful Team Lead actions. | Add a Member non-assignee test confirming disabled C-15/C-16 and C-17/C-18 with no success route; link both traceability rows to it. |
| DEF-03 | Major | BR-08.1; AC-07.5 | T-10; UIR-29 | The transition matrix is correct, but generic T-10 does not prove that all four permitted transitions are shown and all other destinations rejected. | Replace/expand T-10 into four explicit current-assignee scenarios: Open→In Progress; In Progress→Resolved; Resolved→In Progress; Resolved→Closed. Retain T-11 for forbidden context/Closed. |
| DEF-04 | Major | AC-08.1–AC-08.4; BR-09.1 | S-02-B, T-02, UIR-30…UIR-33 | The Important rule is correct but there are no fixed sample IDs that visibly prove High+Resolved inclusion, Critical+Closed exclusion, Low/Normal exclusion and Not Set exclusion. | Add the prescribed eight sample issues and expected Important set `ISS-001`, `ISS-002`, `ISS-003`, `ISS-007`; expand T-02 accordingly. |

## Blockers and decisions

No unresolved business decision blocks generation: D-01 through D-09 are approved. The four defects are plan-correction blockers because they would otherwise leave required states without testable evidence.

## Review conclusion

Correct DEF-01 through DEF-04, then re-run this review. Do not interpret a future wireframe, disabled control or prototype connection as proof of backend authorization, persistence, HTTPS, backup or response time.
