# Лабораторні Codewars: дані та вимоги

## Домен

Codewars — це онлайн-платформа для практики програмування через розв'язання
задач, які називаються kata. Користувач може багато разів розв'язувати одну
kata, надсилати спроби різними мовами та отримувати результат автоматичних
тестів. Користувачі можуть створювати kata, а одна kata може підтримувати
кілька мов програмування.

Цей репозиторій описує концептуальні дані платформи та вимоги до її
взаємодій. Він навмисно не містить SQL DDL, ORM-відображень, індексів чи
іншого фізичного проєктування бази даних.

## Структура репозиторію

- [`spec.md`](spec.md) — межі домену та критерії прийняття.
- [`model/er-diagram.mmd`](model/er-diagram.mmd) — декларативна ER-модель Mermaid.
- [`model/er-diagram.svg`](model/er-diagram.svg) — відрендерена діаграма.
- [`audit/discrepancies.md`](audit/discrepancies.md) — аудит узгодженості.
- [`adr/0001-attempt-as-associative-entity.md`](adr/0001-attempt-as-associative-entity.md) — ключове рішення моделювання.
- [`DEFENSE.md`](DEFENSE.md) — точка входу для рев'ю.
- [`requirements.md`](requirements.md) — EARS-вимоги, user stories і Gherkin.
- [`traceability.md`](traceability.md) — матриця вимога ↔ сценарій/UC.
- [`model/use-case-diagram.puml`](model/use-case-diagram.puml) — Use Case-джерело.
- [`model/use-case-diagram.svg`](model/use-case-diagram.svg) — рендер Use Case.
- [`audit/requirements-discrepancies.md`](audit/requirements-discrepancies.md) — аудит лабораторної №2.
- [`adr/0002-requirements-and-use-case-boundaries.md`](adr/0002-requirements-and-use-case-boundaries.md) — ADR лабораторної №2.

## Межі

Модель охоплює користувачів, ранги, kata, мови програмування та спроби
надсилання розв'язків. Вона не охоплює обговорення, honor/badges, команди,
підписки та внутрішню реалізацію запуску тестів.

Перевірку лабораторної №1 зручно виконувати від ER-специфікації до діаграми.
Лабораторна №2 читається від [`spec.md`](spec.md) до вимог, сценаріїв,
трасування, Use Case-рендера та [`DEFENSE.md`](DEFENSE.md).
