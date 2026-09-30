# AI Interaction Log

## Контекст

Проєкт: Mini Issue Tracker UX/UI.  
Вихідне джерело: `00_Source/SD_Spec.docx`.  
AI-інструменти: ChatGPT для аналізу та підготовки текстових артефактів; Figma Agent для початкової генерації low-fidelity макетів.

## Журнал

| Етап | Інструмент | Контекст і дія | Прийнятий результат | Перевірка / обмеження |
|---|---|---|---|---|
| G1 | ChatGPT | Повна специфікація SD_Spec | `01_Input_Pack_v0.1.md` | Відібрано Release MVP US-01–US-08 та UI-релевантні правила. |
| G2 | ChatGPT | Input Pack і погоджені UX-рішення | Screen Map, Decision Log | Рішення D-01–D-09 погоджено студентом. |
| G3 | ChatGPT | Screen Map та Decision Log | Screen Contracts | Перевірено ролі, статуси, Important predicate і навігацію. |
| G4 | ChatGPT | План екранів і правила | Plan Review | Виявлені дефекти усунено до побудови фінальних макетів. |
| G5 | ChatGPT | Погоджені контракти | `05_Figma_Brief_v1.0.md` | Brief використано як джерело для Figma. |
| F1 | Figma Agent | Figma Brief і контекст файлу | Початкові wireframes | Агент створив editable low-fidelity frames. |
| F2 | Figma / вручну | Після вичерпання daily credits Figma Agent | Виправлені макети та зв’язки | Подальші зміни й прототипні переходи виконано вручну. |
| P1 | Figma / вручну | Фінальні frames | Клікабельний basic prototype | Пройдено All ↔ Important, Create → Cancel, row → Details, Return. |
| G6 | ChatGPT | Figma screenshots і текстові артефакти | Review Report і Prototype Test Record | Перевірено видимі стани; backend, persistence і реальна авторизація не доведені. |

## Принцип перевірки

Результати AI не вважалися новими вимогами автоматично. Для кожного рішення використовувались вихідна специфікація, погоджений Decision Log або ручна перевірка макетів.

