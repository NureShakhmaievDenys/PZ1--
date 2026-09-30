# Mini Issue Tracker Decision Log v0.1

## Статус

**Статус документа:** DRAFT / PROPOSED. Жодне рішення нижче не є вимогою `SD_Spec.docx` і не набуває статусу APPROVED без явного погодження людиною.

**Дата підготовки:** 2026-09-28  
**Основа:** `01_Input_Pack_v0.1.md`, `SD_Spec.docx`, методичний гайд.

## Proposed decisions

| ID | Статус | Рішення | Обґрунтування та джерело | Наслідок для дизайну |
|---|---|---|---|---|
| D-01 | PROPOSED | Зробити desktop, grayscale, low-fidelity макет. Показати один список issues з вкладками All Issues та Important Issues; створення issue відкривати у modal. | Методичний гайд, §6 / D-01. S1 не визначає візуальний стиль, вкладки чи форму створення. | Не створювати окремий продуктовый екран Important Issues або New Issue page. |
| D-02 | PROPOSED | `S-01` є лише нейтральною межею authentication. Демонстрація починається із уже автентифікованого `S-02`. | NFR-02 і BR-01 вимагають authentication, але спосіб не визначений; методичний гайд, D-02. | Не додавати пароль, SSO, recovery або інші login-механізми. |
| D-03 | PROPOSED | Відсутній priority відображати як `Not Set`; вибирати можна лише Low, Normal, High, Critical. Не додавати reset action. | BR-04–BR-06; методичний гайд, D-03. | `Not Set` — display state, а не selectable priority value. |
| D-04 | PROPOSED | Після створення issue assignee відсутній. Team Lead може перепризначати issue одному члену команди. | S1 прямо не визначає початковий assignee або перепризначення; методичний гайд, D-04. | Потрібне явне підтвердження перед позначенням як APPROVED. |
| D-05 | PROPOSED | Role-dependent controls, заборонені для поточного користувача, відображати disabled, а не приховувати. | Права визначені US-03, US-04, AC-07.4; спосіб їх UI-подання не визначений. Методичний гайд, D-05. | У review notes потрібно показати стан disabled для неуповноважених контекстів. |
| D-06 | PROPOSED | Для assignee, priority і status застосовувати модель `select → Apply` біля відповідного control; після успіху залишатися на `S-03`. | Методичний гайд, D-06. У S1 не визначено interaction model. | Не створювати окремі сторінки Assignment, Priority або Status. |
| D-07 | PROPOSED | Return from issue details відновлює попередній list state: All або Important. | Методичний гайд, D-07. | У prototype має бути контекстне повернення, а не фіксований перехід на All. |
| D-08 | PROPOSED | Wireframes використовують фіктивні дані; prototype демонструє підготовлені результати без справжнього login, database або persistence. | Методичний гайд, D-08; NFR-01–NFR-04. | У звітах чітко відділяти UI/prototype evidence від implementation tests. |
| D-09 | PROPOSED | Для забороненої або недопустимої status-дії показувати локальний недвозначний error/disabled state; текст повідомлення є UX-copy, а не цитатою S1. | AC-07.4–AC-07.5 визначають заборону, але не точний текст feedback. | Screen Contract повинен містити visible error state без вигадування нового бізнес-правила. |

## Questions and approval record

| Q-ID | Пов’язане рішення | Що має підтвердити людина | Поточний статус |
|---|---|---|---|
| Q-01 | D-02 | Достатньо neutral authentication boundary для навчального макета. | PENDING |
| Q-02 | D-04 | Новий issue є unassigned; Team Lead може reassignment. | PENDING |
| Q-03 | D-05, D-06 | Disabled controls і select → Apply є прийнятною моделлю взаємодії. | PENDING |
| Q-04 | — | Closed блокує лише наступні status transitions; інші дії не блокуються без окремої вимоги. | PENDING |
| Q-05 | D-09 | Допустимий локальний error/disabled feedback без заданого в S1 wording. | PENDING |

## Approval section

Після погодження скопіюйте потрібні рядки до версії `v1.0`, змініть їхній статус на **APPROVED** та вкажіть reviewer, date і version. Непогоджені рядки залишаються **UNRESOLVED** і не повинні непомітно потрапити до Figma Brief.

| D-ID | APPROVED / REJECTED / UNRESOLVED | Reviewer | Date | Note |
|---|---|---|---|---|
| D-01 |  |  |  |  |
| D-02 |  |  |  |  |
| D-03 |  |  |  |  |
| D-04 |  |  |  |  |
| D-05 |  |  |  |  |
| D-06 |  |  |  |  |
| D-07 |  |  |  |  |
| D-08 |  |  |  |  |
| D-09 |  |  |  |  |
