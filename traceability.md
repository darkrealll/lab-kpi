# Матриця трасування

Позначення `REQ-*` — EARS-вимоги, `SC-*` — Gherkin-сценарії, `US-*` —
user stories, `UC-*` — прецеденти з діаграми. Один рядок навмисно може мати
кілька сценаріїв, а один сценарій — покривати кілька вимог.

| Вимога | User story | Use case | Сценарії | Покриття |
|---|---|---|---|---|
| REQ-01 | US-01 | UC-01 Browse kata catalog | SC-01 | покрито |
| REQ-02 | US-02 | UC-02 View kata details | SC-02 | покрито |
| REQ-03 | US-03 | UC-03 Submit solution | SC-03, SC-04 | покрито |
| REQ-04 | US-03 | UC-03 Submit solution, UC-05 Track attempt status | SC-03, SC-04 | покрито |
| REQ-05 | US-03, US-04 | UC-03 Submit solution, UC-04 Evaluate solution | SC-03 | покрито |
| REQ-06 | US-04 | UC-04 Evaluate solution, UC-06 View rank | SC-03 | покрито |
| REQ-07 | US-05 | UC-07 Create kata | SC-05 | покрито |
| REQ-08 | US-05 | UC-07 Create kata | SC-06 | покрито |
| — | — | UC-08 Retry failed attempt | — | **непокритий UC**: запланований для наступної ітерації |

Кожна вимога має принаймні один сценарій. Трасування не є 1:1: `SC-03`
покриває `REQ-03`, `REQ-04`, `REQ-05` і `REQ-06`, а `REQ-03` та `REQ-04`
мають по два сценарії. `UC-08` залишено непокритим навмисно, щоб явно
показати межу поточної ітерації.

