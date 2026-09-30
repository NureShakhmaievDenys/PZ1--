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

Improve only the selected search, filter and due-date frames. Preserve the existing grayscale low-fidelity visual language.

Make the filter flow clearer:

Keep Search issues and Filters visible on all list states.
In S-02-D, make active chips “export”, “Backend” and “Resolved” clearly readable and keep Clear all visible.
In S-02-E, keep the message “No issues match the selected filters” and make Clear all the clear primary recovery action.
In M-02 Advanced Filters, align all labels, selects, radio options and actions consistently.
Keep filter options: Status, Priority, Assignee, Tag and Due date state.
Due date states: Any date, Due today, Due this week, Overdue, No due date.
Ensure Overdue is always shown as readable text, not colour alone.
Keep tags compact and visually consistent across list rows.
Do not add dashboards, analytics, calendar views or new roles.

## Відповідь LLM 2

Updated the selected grayscale wireframes:

: refined filter, tags, and due-date readability.
: strengthened active chips and Clear all.
: made Clear all the primary recovery action.
: aligned controls, radio states, and actions consistently.

## Рішення учасника після запиту 2

LLM виконала свою роботу в Figma правильно