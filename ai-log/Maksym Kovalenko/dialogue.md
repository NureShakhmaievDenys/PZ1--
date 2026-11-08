Виконавець: Коваленко Максим
Перевіряючий (Рев'ювер): Нікулін Андрій
Зона відповідальності: UX/UI QA-перевірка макетів, деталізація матриці прав доступу (REF-01, S-03), станів коментування та верифікація навігаційних зв'язків прототипу.
Інструмент та артефакти: Figma Agent (Starter plan) + ручне тестування Figma Prototype (фрейми S-02-A–S-02-F, S-03, M-01, M-02, REF-01; результати зафіксовано в `06_Review_Report_v0.2.md`, `07_Prototype_Test_Record_v0.1.md`, `16_Extended_Prototype_Test_Checklist_v2.0.md`).

Запит 1 (Етап F2 / P1: UX/UI QA-перевірка прав доступу, станів коментарів та навігації прототипу)
Промпт виконавця (Максим):
Perform a focused UX/UI QA improvement pass on the selected Mini Issue Tracker frames. Preserve all existing functionality and grayscale low-fidelity style.

Fix clarity of permissions and interaction states: Add a compact REF-01 permission reference for Member non-assignee, Member assignee, Lead non-assignee and Lead assignee. Make it explicit that only the current assignee can change Status. Lead can change Assignee and Priority, but Lead non-assignee must see Status disabled. Clarify the current viewer state in S-03 so enabled and disabled controls are not ambiguous. Keep Due date editable only for Lead; Member view is read-only. Add an Add Comment action next to the comment input. Add separate comment states: ready, empty-comment error, saved comment and save-error without a saved entry.

Check prototype navigation: All Issues ↔ Important Issues; Create Issue → M-01; Cancel → calling list; successful prepared Create → S-03; issue row → S-03; Return → previous list; Filters → M-02 → S-02-D; Clear all → S-02-A.

## Відповідь LLM 1
All 26 prototype connections pass. Here's a summary of everything I've done in this QA pass:

Permission clarity (REF-01 + S-03):

Created a compact table showing field-level access for Member non-assignee, Member assignee, Lead non-assignee, and Lead assignee

Added "Only the current assignee can change" hint under the Status dropdown in S-03

Added "Lead only" hints under Priority and the new Assignee dropdown

Added "Lead only — Members see read-only view below" hint under Due Date

Added a context indicator showing the viewer's role and summarizing what they can/can't edit

Made the Member read-only Due Date row visually dimmed so disabled vs. enabled is unambiguous

Comment improvements:

Added an "Add Comment" button next to the comment input in S-03

Created S-03 comment states showing 4 states: ready (text entered), empty-comment error, saved comment with success banner, and save-error with text preserved

Navigation consistency:

Added navigation links to S-02-F (Issue List Selected)

Prototype wiring (26/26 connections verified):

All Issues ↔ Important Issues tabs across S-02-A, S-02-B, S-02-F

Create Issue → M-01 on every list screen

M-01 Cancel/X → S-02-A, M-01 Create → S-03

Issue row clicks → S-03 on all list screens

S-03 Back → S-02-A

Filters → M-02 on all list screens; M-02 Apply → S-02-D

Clear all → S-02-A on S-02-D and S-02-E

How does that look? Let me know if you'd like any adjustments.

## Рішення учасника після запиту 1

Результати перевірки (Виконавець: Максим, Рев'ювер: Андрій):
На основі отриманої відповіді ми перевірили оновлені макети та прийняли такі рішення:

У REF-01 підтверджено наявність компактної матриці прав для Member non-assignee, Member assignee, Lead non-assignee та Lead assignee.

Рев'ювер перевірив візуальні підказки прав доступу на екрані S-03: підтверджено, що статус редагується лише поточним Assignee, а поля Priority, Assignee та Due Date мають маркування доступу лише для Lead.

Перевірено візуальне відокремлення заблокованих полів (Member read-only Due Date зроблено тьмяним) для уникнення двозначності між активними та неактивними елементами.

Затверджено додавання кнопки «Add Comment» та 4 окремих станів для секції коментарів (ready, empty-comment error, saved comment, save-error).

У прототипі спільно протестовано працездатність усіх 26 налаштованих переходів між екранами (перемикання вкладок All / Important, відкриття/закриття модального вікна Create Issue, навігація до фільтрів M-02 та повернення до списку S-02-A).

Підтверджено, що LLM виконала роботу у Figma коректно, зберігши необхідний grayscale low-fidelity стиль.
