Виконавець: Свідерський Олександр

Перевіряючий (рев'ювер): Коваленко Максим

Дата: 08.11.2026

Зона відповідальності: простежуваність вимог, фінальна перевірка критичної логіки Release MVP та регресійна перевірка розширень V2.

Інструмент: ChatGPT; назва та версія моделі в інтерфейсі не фіксувалися.

Контекст: `SD_Spec.docx`, методичні рекомендації, `01_Input_Pack_v0.1.md`, `04_Screen_Contracts_v0.1.md`, `06_Review_Report_v0.2.md`, `07_Prototype_Test_Record_v0.1.md`, `13_Extended_Features_v2.0.md`, `16_Extended_Prototype_Test_Checklist_v2.0.md`.

## Запит 1

Перевір узгодженість базового UX/UI-комплекту Mini Issue Tracker з вихідною специфікацією та методичними рекомендаціями.

Не додавай нових вимог. Вважай джерелом продуктових вимог тільки специфікацію, а документи репозиторію — похідними артефактами, які потрібно перевірити.

Перевір окремо:

- Release MVP і кількість acceptance criteria;
- поля та автоматичні значення під час створення issue;
- права Member, Lead та поточного assignee;
- усі дозволені переходи status;
- правило Important Issues, зокрема Resolved і Closed;
- стани comments;
- що можна довести wireframe/prototype, а що потребує реалізації.

Поверни компактну таблицю `Перевірка | Очікування | Доказ у репозиторії | Результат | Залишкова перевірка`. Не став PASS там, де є лише текстовий опис або потрібен backend.

## Відповідь LLM 1

| Перевірка | Очікування | Доказ у репозиторії | Результат | Залишкова перевірка |
|---|---|---|---|---|
| Release scope | Release MVP містить US-01–US-08; US-09 відкладено; SR-10 і SR-11 залишаються Future | `01_Input_Pack_v0.1.md`, розділи Release scope та Source check | PASS для текстової простежуваності | Переконатися, що макет не повертає attachments або AI-функції до базового MVP |
| Повнота AC | 33 змістові AC: 5 + 5 + 4 + 2 + 3 + 5 + 5 + 4 | `01_Input_Pack_v0.1.md`, Source check | PASS для похідного документа | Під час захисту показати вибіркове звірення з повною специфікацією |
| Create Issue | Користувач вводить лише Title і Description; після успіху з'являються ID, Open, author, created_at; priority відсутній і показаний як Not Set | `04_Screen_Contracts_v0.1.md`, M-01 та T-07 | COVERED у контракті | Реальна генерація ID, збереження та серверна валідація не перевіряються статичним прототипом |
| Assignee після створення | У погодженому дизайні нова issue не має assignee; це D-рішення, а не дослівний AC | `04_Screen_Contracts_v0.1.md`, M-01 | COVERED як погоджене UX-рішення | Не видавати це за первинну вимогу S1 |
| Assignment і priority | Лише Team Lead може призначати одного члена команди та встановлювати Low, Normal, High або Critical; Not Set не є selectable value | `04_Screen_Contracts_v0.1.md`, C-15–C-18 і permission matrix | COVERED у UI-контракті | Серверна авторизація залишається implementation test |
| Status permissions | Status змінює лише current assignee. Lead non-assignee не отримує цього права автоматично | `04_Screen_Contracts_v0.1.md`, C-19/C-20 та permission matrix; `06_Review_Report_v0.2.md`, S-03 | PASS для видимого UI-стану | Потрібен implementation test, що сервер відхиляє неавторизовану зміну |
| Status transitions | Дозволено лише Open → In Progress; In Progress → Resolved; Resolved → In Progress; Resolved → Closed. Closed не має вихідного переходу | `04_Screen_Contracts_v0.1.md`, transition matrix і T-10A–T-10D | COVERED у контракті | У прототипі кожен маршрут треба пройти окремо; persistence не доведено |
| Important Issues | `priority ∈ {High, Critical} AND status != Closed`; Resolved High/Critical залишається; Closed виключається; Not Set не включається | `04_Screen_Contracts_v0.1.md`, ISS-001–ISS-008 і T-02 | PASS для тестових даних і правила | Реальну фільтрацію даних треба перевіряти в реалізації |
| Comments | Потрібні ready, empty error, saved та save-error; невдале збереження не створює comment; saved entry містить author і time | `04_Screen_Contracts_v0.1.md`, S-03; `06_Review_Report_v0.2.md`, REF-01 | COVERED у дизайні | Persistence і помилка транзакції потребують implementation test |
| Prototype navigation | Основні переходи All/Important, відкриття issue, Create/Cancel і Return мають бути пройдені вручну | `07_Prototype_Test_Record_v0.1.md` | REPORTED PASS для зафіксованих переходів | Повторити ручне проходження на фінальній версії Figma після останніх змін |
| NFR | Authentication, HTTPS, backup і фактичний response time не доводяться wireframe або клікабельним прототипом | `01_Input_Pack_v0.1.md`, NFR classification | NOT VERIFIABLE у межах макета | Перенести до implementation/deployment tests |

Критичних суперечностей між перевіреними текстовими артефактами та Release MVP не виявлено. Головне обмеження доказів: UI-контракт і підготовлений prototype state не підтверджують backend persistence, серверні права, HTTPS, backup або реальний час відповіді.

## Рішення учасника після запиту 1

Результати перевірки (виконавець: Олександр, рев'ювер: Максим):

- Підтверджено, що базовий комплект використовує остаточний Release MVP US-01–US-08, а не Candidate MVP із US-09.
- Підтверджено підрахунок 33 змістових AC; чотири ненумеровані критерії US-03 враховані окремими пунктами.
- Для захисту обрано контрольний приклад ISS-003: `Resolved + High` залишається в Important, доки status не стане Closed.
- Окремо зафіксовано негативний контроль ISS-004: `Closed + Critical` не входить до Important.
- Підтверджено, що Lead non-assignee бачить Status disabled, а право переходу залежить від current assignee і BR-08.1.
- Не прийнято твердження про повну перевірку backend. Authentication, persistence, server authorization, HTTPS, backup і response time залишено в переліку implementation tests.

## Запит 2

Підготуй регресійну перевірку розширень Mini Issue Tracker V2. Використовуй `13_Extended_Features_v2.0.md` як окремий погоджений контракт розширення, але не переписуй ним базову специфікацію.

Перевір search and filters, tags, due dates and Overdue, attachments та subtasks. Для кожного блоку вкажи позитивний сценарій, граничний або error-сценарій і правило, яке не повинно зламатися з базового MVP.

Особливо перевір:

- розширення не обходять права Assignee, Priority і Status;
- Important залишається High/Critical AND not Closed;
- Closed issue ніколи не позначається Overdue;
- upload-error не створює saved attachment row;
- виконання всіх subtasks не закриває parent issue автоматично;
- неперевірені чекбокси не можна називати PASS.

## Відповідь LLM 2

| Блок V2 | Позитивний сценарій | Граничний або error-сценарій | Регресійний інваріант MVP |
|---|---|---|---|
| Search and filters | Запит `export` разом із Tag = Backend і Status = Resolved показує лише ISS-003; активні умови видно як chips | Запит `mobile` не має результатів; показано `No issues match the selected filters`; Clear all повертає список без фільтрів | Фільтри не змінюють issue data, права або правило Important |
| Tags | Теги компактно відображаються у list row і S-03; Tag filter дає очікувану підмножину | Додавання чи видалення tag не змінює status, priority або Important state саме по собі | Priority і Status залишаються під базовими role restrictions |
| Due date / Overdue | Lead встановлює due date; прострочена non-Closed issue має текстову позначку Overdue | Member бачить due date read-only; Closed issue не має позначки Overdue навіть для минулої дати | Lead non-assignee все одно не може змінити Status; due date не змінює Important predicate |
| Attachments | Після prepared upload-success у S-03 з'являється рядок із name, type, size, author та upload time | Upload-error показує помилку і не додає saved row | Attachment не змінює assignee, priority, status або Important state |
| Subtasks | Новий subtask з'являється у списку; completed subtask залишається видимим і checked | Після завершення всіх subtasks parent issue не переходить автоматично в Closed | Status parent issue змінюється тільки current assignee через дозволений BR-08.1 transition |

`16_Extended_Prototype_Test_Checklist_v2.0.md` містить підготовлені пункти з порожніми чекбоксами. Тому цей файл є планом перевірки, а не доказом PASS. Для фінального підтвердження потрібно вручну пройти сценарії на актуальній версії Figma, поставити фактичні результати й додати посилання або скріншоти доказів.

## Рішення учасника після запиту 2

Результати перевірки (виконавець: Олександр, рев'ювер: Максим):

- Розширення EX-01–EX-05 розглядаються як окремий V2-контракт і не підміняють Release MVP вихідної специфікації.
- До фінального регресійного набору включено сценарії filtered result, no results, Clear all, Member read-only due date, Closed without Overdue, upload-error without saved row та all-subtasks-completed without auto-close.
- Незмінними правилами залишено: Status змінює лише current assignee; Assignee/Priority/Due date редагує Lead у межах відповідних контрактів; Important = High/Critical AND not Closed.
- Порожні чекбокси `16_Extended_Prototype_Test_Checklist_v2.0.md` не зараховано як виконані тести. Для фінальної версії потрібне ручне проходження та доказ по кожному фактично перевіреному пункту.
- Рев'ювер підтвердив, що підготовлений набір не додає dashboards, analytics, bulk actions, нові ролі або нові status values.
