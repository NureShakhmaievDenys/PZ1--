# Mini Issue Tracker UX UI Design Input Pack v0.1

## Статус і джерело

**Статус:** DRAFT. Цей документ не є погодженим рішенням і не замінює специфікацію.

**Прочитаний файл:** `SD_Spec.docx`.

**Доступні розділи джерела:** Customer Request; Discovery; Open Questions; Stakeholder Requirements і Business Rules; Candidate MVP; User Stories та Acceptance Criteria; NFR; Feasibility; Release Scope; Updated NFRs.

Позначення: **SOURCE** — пряма вимога джерела; **DERIVED** — обережний висновок із наведених джерел; **UNRESOLVED** — питання, яке має вирішити людина. У цьому Pack немає погоджених **PROPOSED** UX-рішень.

## 1. Призначення продукту та межі релізу

Mini Issue Tracker — внутрішній web-застосунок для невеликої команди розробників. Він дає змогу реєструвати, переглядати, призначати, пріоритизувати та супроводжувати issues, а також швидко бачити важливі незакриті issues. [SOURCE: Product Vision; §1 Customer Request]

**Основні користувачі:** Team Member і Team Lead. Product Owner та System Administrator є secondary stakeholders, а не primary users MVP. [SOURCE: §1 Primary users; Stakeholders]

**Release MVP:** US-01…US-08. [SOURCE: §8 Release MVP]

## 2. Scope

### Included — Release MVP

| ID | Вимога |
|---|---|
| US-01 | Create Issue |
| US-02 | View Issues |
| US-03 | Assign Issue to the responsible team member |
| US-04 | Set Issue Priority |
| US-05 | Track Issue Progress |
| US-06 | Add Comment |
| US-07 | Update Issue Status |
| US-08 | View Important Open Issues |

SOURCE: §5 User Stories; §8 Release MVP.

### Deferred

| ID | Причина |
|---|---|
| US-09 Attach files to an issue | Відкладено за межі першого релізу через storage, size limits, malware scanning і backup. |

SOURCE: §8 Deferred; Feasibility / Recommended scope adjustment.

### Future

| ID | Вимога |
|---|---|
| SR-10 | Automatic issue categorization |
| SR-11 | Automatic priority recommendation |

SOURCE: §8 Future.

### Explicitly out of scope for MVP UI

Customer support portal, billing, source-code hosting, CI/CD, time tracking, full project management, mobile app, GitHub/GitLab/Jira integrations, user-visible change history, issue deletion, attachments and AI features. [SOURCE: §2 Out of Scope; KC-05–KC-07; BR-10–BR-12; §8 Release Scope]

## 3. Included User Stories and Acceptance Criteria

### US-01 — Create Issue

**Actor:** authenticated team member. **Goal:** record a problem so it can be tracked. [SOURCE: US-01; BR-02]

- **AC-01.1:** user can enter Title and Description. [SOURCE: AC-01.1]
- **AC-01.2:** Title is required. [SOURCE: AC-01.2]
- **AC-01.3:** Description is required. [SOURCE: AC-01.3]
- **AC-01.4:** after creation an issue receives ID, `status = Open`, `created_at` and `author`. [SOURCE: AC-01.4]
- **AC-01.5:** after creation, priority is not set. [SOURCE: AC-01.5; BR-04]

### US-02 — View Issues

**Actor:** authenticated team member. **Goal:** inspect reported issues and their current details. [SOURCE: US-02; AC-02.1]

- **AC-02.1:** an authenticated team member can view the list of registered issues. [SOURCE: AC-02.1]
- **AC-02.2:** each list item shows at least ID, Title, Status, Priority and Assignee when assigned. [SOURCE: AC-02.2]
- **AC-02.3:** user can select an issue and open its details. [SOURCE: AC-02.3]
- **AC-02.4:** details show ID, Title, Description, Status, Priority, Assignee when assigned, Author and Created at. [SOURCE: AC-02.4]
- **AC-02.5:** if no issues are registered, show an empty list or a no-issues message. [SOURCE: AC-02.5]

### US-03 — Assign Issue to the responsible team member

**Actor:** Team Lead. **Goal:** make responsibility clear. [SOURCE: US-03]

- **US-03 AC, point 1:** one assignee can be selected. [SOURCE: US-03 Acceptance Criteria 03]
- **US-03 AC, point 2:** assignee must be a team member. [SOURCE: US-03 Acceptance Criteria 03]
- **US-03 AC, point 3:** only Team Lead can assign an issue. [SOURCE: US-03 Acceptance Criteria 03; Open Question answer]
- **US-03 AC, point 4:** current assignee is displayed in the issue. [SOURCE: US-03 Acceptance Criteria 03]

### US-04 — Set Issue Priority

**Actor:** Team Lead. **Goal:** establish work order. [SOURCE: US-04]

- **AC-04.1:** allowed set priority values are Low, Normal, High and Critical. [SOURCE: AC-04.1; BR-05]
- **AC-04.2:** only Team Lead can set and change priority. [SOURCE: AC-04.2; BR-06]

### US-05 — Track Issue Progress

**Actor:** team member. **Goal:** understand current progress. [SOURCE: US-05]

- **AC-05.1:** current status is shown for every issue. [SOURCE: AC-05.1]
- **AC-05.2:** status is shown on issue details. [SOURCE: AC-05.2]
- **AC-05.3:** status is shown in the issues list. [SOURCE: AC-05.3]

### US-06 — Add Comment

**Actor:** team member. **Goal:** discuss an issue. [SOURCE: US-06]

- **AC-06.1:** comment text cannot be empty. [SOURCE: AC-06.1]
- **AC-06.2:** an added comment is stored and shown for the issue. [SOURCE: AC-06.2]
- **AC-06.3:** comment author is stored and displayed. [SOURCE: AC-06.3]
- **AC-06.4:** creation date/time is stored and displayed. [SOURCE: AC-06.4]
- **AC-06.5:** failed save creates no comment and produces an error. [SOURCE: AC-06.5]

### US-07 — Update Issue Status

**Actor:** team member responsible for the issue. **Goal:** show work progress to the team. [SOURCE: US-07; BR-08]

- **AC-07.1:** a new issue is created with status Open. [SOURCE: AC-07.1; BR-03]
- **AC-07.2:** allowed statuses are Open, In Progress, Resolved and Closed. [SOURCE: AC-07.2; BR-07]
- **AC-07.3:** after a status change, the system stores and shows the new value on next viewing. [SOURCE: AC-07.3]
- **AC-07.4:** a user who is not the issue assignee cannot change its status. [SOURCE: AC-07.4]
- **AC-07.5:** the system rejects a status outside the allowed set. [SOURCE: AC-07.5]

### US-08 — View Important Open Issues

**Actor:** team member. **Goal:** focus on problems needing priority attention. [SOURCE: US-08]

- **AC-08.1:** an issue with High priority and status other than Closed appears in Important Issues. [SOURCE: AC-08.1]
- **AC-08.2:** an issue with Critical priority and status other than Closed appears in Important Issues. [SOURCE: AC-08.2]
- **AC-08.3:** issues with Low or Normal priority do not appear in Important Issues. [SOURCE: AC-08.3]
- **AC-08.4:** Closed issues do not appear in Important Issues regardless of priority. [SOURCE: AC-08.4]

## 4. UI relevant business rules

| ID | Rule | Type |
|---|---|---|
| BR-01 | Only authenticated team members use the system; version one has two Team Members and one Team Lead. | SOURCE |
| BR-02 | Any authenticated team member can create an issue. | SOURCE |
| BR-03 / BR-04 | New issue has Open status and priority Not Set. | SOURCE |
| BR-05 / BR-06 | Low, Normal, High and Critical are the selectable priority values; only Team Lead sets or changes priority. Not Set is an absent value before a priority is set. | SOURCE |
| BR-07 / BR-08 | Statuses are Open, In Progress, Resolved, Closed; the responsible team member can change status. | SOURCE |
| BR-08.1 | Only Open → In Progress; In Progress → Resolved; Resolved → Closed; Resolved → In Progress are allowed. | SOURCE |
| BR-09 / BR-09.1 | Important means High or Critical; Resolved is not Closed and can remain among Important Issues until Closed. | SOURCE / DERIVED: together with AC-08.1–AC-08.4, Important = priority in {High, Critical} AND status != Closed. |
| BR-10 / BR-11 | No issue deletion and no separate user-visible history in version one. | SOURCE |
| A-04 / A-05 | One assignee and one current priority per issue are stated assumptions. | SOURCE; validate if implementation treats assumptions as constraints. |

## 5. Relevant non functional requirements

| ID | Requirement | Wireframe verification |
|---|---|---|
| NFR-01 | Response time under 1 second. | NOT VERIFIABLE in a wireframe or static prototype. |
| NFR-02 | Authentication required. | Authentication boundary can be represented, but real authentication is NOT VERIFIABLE. |
| NFR-03 | HTTPS only. | NOT VERIFIABLE in a wireframe or prototype. |
| NFR-04 | Backup of all data. | NOT VERIFIABLE in a wireframe or prototype. |

SOURCE: §8 Updated NFRs.

## 6. Unresolved questions requiring a human decision

| Q-ID | Question | Why it matters | Source |
|---|---|---|---|
| Q-01 | What authentication mechanism and entry UI will be used? | Authentication is required, but the method is unspecified. Do not invent login, password or SSO controls. | NFR-02; R-01; Open Questions |
| Q-02 | Is an issue explicitly unassigned immediately after creation? | S1 defines initial status and priority but not initial assignee. A blank assignee is plausible, but is not stated as a requirement. | AC-01.4–AC-01.5; BR-03–BR-04 |
| Q-03 | What exact UI interaction confirms assignment, priority and status changes? | Rights and allowed values are specified; dropdown, modal, Apply button and optimistic/error behavior are not. | US-03, US-04, BR-08.1 |
| Q-04 | What actions remain available for a Closed issue besides status transitions? | Closed has no outgoing status transition, but S1 does not say it blocks comments, assignment or priority changes. | BR-08.1; BR-10–BR-11 |
| Q-05 | What user-facing feedback is required for a forbidden status change or invalid status value? | Prohibition is specified, but exact message and UI state are not. | AC-07.4–AC-07.5 |

## 7. Source check

| Included US | AC coverage in this Pack | Result |
|---|---|---|
| US-01 | AC-01.1–AC-01.5 | Covered: 5 |
| US-02 | AC-02.1–AC-02.5 | Covered: 5 |
| US-03 | four unnamed Acceptance Criteria points | Covered: 4 |
| US-04 | AC-04.1–AC-04.2 | Covered: 2 |
| US-05 | AC-05.1–AC-05.3 | Covered: 3 |
| US-06 | AC-06.1–AC-06.5 | Covered: 5 |
| US-07 | AC-07.1–AC-07.5 | Covered: 5 |
| US-08 | AC-08.1–AC-08.4 | Covered: 4 |

**Total:** 33 substantive Acceptance Criteria. Gherkin examples under US-01 are evidence/examples for existing criteria, not additional AC.

**Excluded requirements:** US-09 is Deferred; SR-10 and SR-11 are Future. All other exclusions are listed in section 2 with their source basis.

**Open items:** Q-01…Q-05. No item in this draft is approved automatically.
