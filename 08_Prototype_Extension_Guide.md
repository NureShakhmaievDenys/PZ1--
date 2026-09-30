# Mini Issue Tracker Prototype Extension Guide

## Purpose

Create prepared prototype states for presentation. These frames simulate visible outcomes; they do not prove database persistence, authentication or server authorization.

## 1 Create success

1. Duplicate S-03 and name the copy `S-03 Create Success`.
2. Set visible data to: ID `ISS-009`; Title `New issue title`; Description `New issue description`; Status `Open`; Priority `Not Set`; Assignee `Unassigned`; Author `Member A`; Created at `28 Sep 2026, 10:00`.
3. Keep only Title and Description as the M-01 inputs. The other values are generated results.
4. Connect Create in the default M-01 state to `S-03 Create Success` with `On click → Navigate to → Instant`.

## 2 Status transitions

Create four prepared copies of S-03 with the same issue ID and assignee. Keep role notes outside product frames in REF-01.

| Frame name | Current visible status | Enabled next action | Destination |
|---|---|---|---|
| S-03 Status Open | Open | In Progress | S-03 Status In Progress |
| S-03 Status In Progress | In Progress | Resolved | S-03 Status Resolved |
| S-03 Status Resolved | Resolved | In Progress | S-03 Status In Progress |
| S-03 Status Resolved | Resolved | Closed | S-03 Status Closed |
| S-03 Status Closed | Closed | No enabled next-status action | None |

Use the prepared current-assignee context for these frames. Connect the visible Apply status control to its destination with `On click → Navigate to → Instant`. Do not add any other transition.

## 3 Comment states

Create three prepared S-03 copies:

| Frame name | Visible state | Prototype result |
|---|---|---|
| S-03 Comment Validation | Empty comment input, inline required error, no added entry. | Add Comment → this frame. |
| S-03 Comment Saved | Comment entry with text, Member A and timestamp. | Add Comment from ready state → this frame. |
| S-03 Comment Save Error | Error message, no new saved comment entry. | Add Comment from a prepared failure state → this frame. |

Use `On click → Navigate to → Instant` for every prepared route. Keep the comment text, author and time readable.

## 4 Test record

When done, manually traverse and record:

- M-01 valid prepared Create → S-03 Create Success;
- Open → In Progress → Resolved → In Progress;
- Resolved → Closed; Closed shows no next status action;
- empty comment → validation; prepared success → saved comment; prepared failure → error with no saved entry.
