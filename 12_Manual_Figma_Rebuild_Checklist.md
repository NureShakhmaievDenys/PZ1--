# Manual Figma rebuild checklist

Use this checklist when rebuilding the corrected screen set manually.

## Frame structure

- [ ] Create six product frames and one REF-01 reference frame with the exact IDs from `10_Corrected_Screen_Set_v1.0.md`.
- [ ] Keep REF-01 outside the product area.
- [ ] Use desktop, grayscale, low-fidelity layout with readable labels.

## Essential checks

- [ ] S-01 has no real login controls.
- [ ] S-02-A has all eight sample rows.
- [ ] S-02-B has ISS-001, ISS-002, ISS-003 and ISS-007 only.
- [ ] S-02-C shows the empty state and Create Issue action.
- [ ] M-01 has only Title and Description; both error examples are visible.
- [ ] S-03 shows all required read-only fields and comment states.
- [ ] Lead non-assignee has Status disabled.
- [ ] Current assignee has only a legal next-status choice.
- [ ] Closed has no status transition.
- [ ] Assignment and Priority are available only to Lead.

## Prototype checks

- [ ] All Issues ↔ Important Issues works.
- [ ] Create Issue opens M-01 as an overlay.
- [ ] Cancel restores the same list state.
- [ ] Title/row opens S-03.
- [ ] Return restores the list state.
- [ ] Valid Create opens the prepared success S-03 state.

## Delivery checks

- [ ] Figma file is named `Mini Issue Tracker`.
- [ ] Anyone with the link can view, or the teacher has explicit view access.
- [ ] Export readable screenshots of list/create and details/REF-01.
- [ ] Update the report and GitHub README to reference this corrected set.
