## Запит 1

Я відповідаю за базові UX/UI-вимоги Mini Issue Tracker.

Проаналізуй додану специфікацію та підготуй компактну таблицю для Figma з такими колонками:

- правило або функція;
- хто має доступ;
- очікувана поведінка в UI;
- джерело вимоги: US, AC або BR.

Обов’язково включи: створення issue, перегляд списку, призначення assignee, зміну priority, зміну status, коментарі та Important Issues.

Не додавай нових функцій, ролей або статусів, яких немає у специфікації.

## Відповідь LLM 1

| Правило або функція | Хто має доступ | Очікувана поведінка в UI | Джерело |
|---|---|---|---|
| Створення issue | Member, Lead | Відкривається форма Create Issue з обов’язковими полями Title і Description. | US-01 |
| Перегляд задач | Member, Lead | У списку показано ID, Title, Status, Priority та Assignee. Натискання на Title відкриває деталі. | US-02 |
| Призначення виконавця | Lead | Lead може вибрати одного виконавця та підтвердити дію кнопкою Apply. Для Member control disabled. | US-03 |
| Зміна пріоритету | Lead | Lead обирає Low, Normal, High або Critical та натискає Apply. | US-04 |
| Перегляд прогресу | Member, Lead | У деталях відображається поточний Status задачі та допустимі наступні стани. | US-05 |
| Додавання коментаря | Member, Lead | Поле Comment і кнопка Add Comment доступні обом ролям. Порожній коментар не зберігається. | US-06 |
| Зміна статусу | Лише поточний Assignee | Status control активний лише тоді, коли поточний користувач є виконавцем задачі та існує дозволений перехід. | US-07, BR-08, BR-08.1 |
| Important Issues | Member, Lead | До Important потрапляють задачі з High або Critical, якщо Status не Closed. | US-08, BR-09.1 |

Дозволені переходи статусів:

- Open → In Progress;
- In Progress → Resolved;
- Resolved → In Progress;
- Resolved → Closed.

Lead, який не є поточним Assignee, не має права змінювати Status. Closed issue не має доступного наступного статусу.

## Рішення учасника після запиту 1

На основі відповіді перевірено та прийнято такі рішення:

- У `REF-01` додано матрицю прав для Member non-assignee, Member assignee, Lead non-assignee та Lead assignee.
- Для Lead non-assignee Status control має бути disabled.
- Для current assignee показуються лише допустимі наступні статуси.
- Important Issues використовує правило: High або Critical AND Status не Closed.
- У Figma перевірено, що Resolved issue з High або Critical priority залишається у списку Important Issues.

## Запит 2

Extend existing Mini Issue Tracker Figma file. Keep desktop grayscale low-fi style, base screens, typography, spacing and reusable components. Do not redesign the product or add bulk actions, delete, dashboards, analytics or AI.

Add V2 features with native editable Figma layers:

Search & Filters:
Add "Search issues" input and "Filters" button to S-02-A and S-02-B, plus active filter chips and "Clear all".
Create S-02-D Filtered Results: query "export", tag "Backend", status "Resolved"; show only ISS-003.
Create S-02-E No Search Results: query "mobile"; show "No issues match the selected filters" and "Clear all".
Create M-02 Advanced Filters modal: Status, Priority, Assignee, Tag, Due date state (Any date, Due today, Due this week, Overdue, No due date), actions "Apply filters" and "Clear all".

Tags:
Compact tag chips: Bug, Feature, UI, Backend, Documentation, Urgent. Show in issue rows and S-03.
Add "Add tag" control in S-03.

Due Dates & Overdue:
M-01 Create modal: add optional Tags and Due date inputs (never expose ID, Assignee, Priority, Status, Author, Created at).
S-03: add Due date control with Apply (Lead can edit; Member sees disabled).
Show explicit "Overdue" label if non-Closed issue date is in the past. Closed issues never show Overdue.

Attachments:
S-03: add Attachments section with "Add attachment" action.
Create M-03 Add Attachment modal. Show file-selected, uploading, upload-error, uploaded states.
Attachment rows: name, type (PNG/JPG/PDF/TXT/LOG), size, author, upload time. Error state must not add saved row.

Subtasks:
S-03: add "Subtasks (2 of 5 completed)" with inline "Add subtask" input.
Reusable subtask rows: checkbox, title, completed state (stays visible and checked). Never auto-close parent issue.

Prototype Intent: Filters -> M-02; M-02 Apply -> S-02-D; Clear all -> S-02-A; Add attachment -> M-03; Upload success -> S-03 with row; preserve existing navigation.

## Відповідь LLM 2

Generated and updated the following Figma wireframe components and states according to the V2 contract:

1. **Search & Filters:**
   - Updated `S-02-A` and `S-02-B`: added search input bar, "Filters" button, active filter tags row, and "Clear all" link.
   - Created `S-02-D` (Filtered Results): displays query "export", chip "Backend", status "Resolved", and filters list down to single match `ISS-003`.
   - Created `S-02-E` (No Search Results): displays query "mobile", empty-state notification "No issues match the selected filters", and primary recovery button "Clear all".
   - Created `M-02` (Advanced Filters modal): added dropdowns/controls for Status, Priority, Assignee, Tag, and radio list for Due date state (Any date, Due today, Due this week, Overdue, No due date). Added "Apply filters" and "Clear all" action buttons.

2. **Tags:**
   - Created reusable tag badge components: `Bug`, `Feature`, `UI`, `Backend`, `Documentation`, `Urgent`.
   - Embedded tag chips into table issue rows on `S-02` and into the metadata sidebar of `S-03`.
   - Added an "+ Add tag" interactive placeholder button inside `S-03`.

3. **Due Dates & Overdue State:**
   - Extended `M-01` (Create Issue modal): added optional dropdown for Tags and date picker input for Due Date without exposing non-editable fields.
   - Extended `S-03` (Issue Details): added Due Date selector with adjacent `Apply` button (configured as enabled for Lead and disabled for Member).
   - Added visual text badge `"Overdue"` to past-due items; confirmed suppressed on Closed issues.

4. **Attachments:**
   - Extended `S-03`: added dedicated "Attachments" section with an "Add attachment" action.
   - Created `M-03` (Add Attachment modal) displaying: file selection picker, progress indicator ("Uploading..."), error state ("Upload failed. Try again"), and complete list with columns: file name, type (PNG/JPG/PDF/TXT/LOG), size, author, upload timestamp.

5. **Subtasks:**
   - Extended `S-03`: added checklist block titled "Subtasks (2 of 5 completed)" with inline input field "+ Add subtask".
   - Created subtask row component with checkbox and title label. Completed items remain struck-through/checked and visible without modifying the parent issue status.

6. **Prototype Annotations:**
   - Annotated hotspot routes: `Filters` button → `M-02`; `Apply filters` → `S-02-D`; `Clear all` → `S-02-A`; `Add attachment` → `M-03`; upload completion → updated `S-03`.

## Рішення учасника після запиту 2

На основі отриманого результату від Figma Agent перевірено та зафіксовано:

- **Повнота артефактів:** створено фрейми `S-02-D`, `S-02-E`, `M-02`, `M-03` та оновлено `M-01`, `S-03`.
- **Контроль ролей:** перевірено, що поле `Due date` на екрані `S-03` для ролі Member відображається як `disabled`, а доступне для редагування лише Team Lead.
- **Граничні випадки:** перевірено, що бейдж `Overdue` не з'являється у задач зі статусом `Closed`, навіть якщо дата минула.
- **Стан помилки (Attachments):** підтверджено, що у стані `upload-error` новий рядок файлу не додається до списку на `S-03`.
- **Чистота макета:** перевірено відсутність нерелевантних графічних елементів (іконки-заглушки видалено, збережено строго чорно-білий wireframe стиль).