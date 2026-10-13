# Вимоги та сценарії платформи Codewars

## EARS-вимоги

| ID | Вимога |
|---|---|
| REQ-01 | **WHEN** неавторизований відвідувач відкриває каталог kata, **the system SHALL** показати назву, складність і доступні мови кожної опублікованої kata. |
| REQ-02 | **WHEN** зареєстрований користувач відкриває kata, **the system SHALL** показати її опис і мови, які підтримує ця kata. |
| REQ-03 | **WHEN** користувач надсилає непорожній вихідний код із вибраною підтримуваною мовою, **the system SHALL** передати спробу зовнішньому сервісу виконання тестів. |
| REQ-04 | **WHILE** сервіс виконання тестів обробляє спробу, **the system SHALL** показувати користувачеві стан `pending` і не створювати другий запис для того самого надсилання. |
| REQ-05 | **WHEN** сервіс виконання тестів повертає результат, **the system SHALL** зберегти одну `Attempt` із користувачем, kata, мовою, часом надсилання, кодом і статусом `passed` або `failed`. |
| REQ-06 | **WHEN** спроба має статус `passed`, **the system SHALL** показати користувачеві успішний результат і оновлений ранг. |
| REQ-07 | **WHEN** користувач із роллю автора подає коректні назву, опис, складність і щонайменше одну мову, **the system SHALL** створити kata, пов'язану з цим користувачем як автором. |
| REQ-08 | **WHEN** автор подає kata без назви, опису, складності або мови, **the system SHALL** відхилити створення та показати перелік відсутніх полів. |

## User stories

- **US-01:** Як відвідувач, я хочу переглядати каталог kata з мовами й складністю, щоб вибрати задачу.
- **US-02:** Як користувач, я хочу читати опис kata та доступні мови, щоб підготувати розв'язок.
- **US-03:** Як користувач, я хочу надсилати код і бачити стан виконання, щоб перевірити розв'язок.
- **US-04:** Як користувач, я хочу бачити результат спроби й оновлений ранг, щоб розуміти свій прогрес.
- **US-05:** Як автор kata, я хочу створювати повністю описану kata з мовами, щоб інші користувачі могли її розв'язувати.

## Gherkin-сценарії

### SC-01 — Перегляд каталогу

```gherkin
Scenario: Visitor views published kata catalog
  Given published kata "Two Sum" has difficulty 3 and supports "Python"
  When a visitor opens the kata catalog
  Then the system shows "Two Sum", difficulty 3, and "Python"
```

### SC-02 — Перегляд деталей kata

```gherkin
Scenario: User opens kata details
  Given user "alice" is registered
  And kata "Two Sum" has description "Find two numbers" and supports "Python"
  When "alice" opens "Two Sum"
  Then the system shows the description and the supported language "Python"
```

### SC-03 — Успішне надсилання

```gherkin
Scenario: User submits code that passes tests
  Given "alice" selected kata "Two Sum" and supported language "Python"
  And the submitted source code is not empty
  When "alice" submits the source code
  Then the system sends one attempt to the test runner
  And the attempt is stored with status "passed"
  And the system shows the updated rank
```

### SC-04 — Очікування результату

```gherkin
Scenario: User sees a pending attempt
  Given "alice" submitted valid code
  When the test runner has not returned a result
  Then the system shows status "pending"
  And the system does not create a duplicate attempt
```

### SC-05 — Створення kata

```gherkin
Scenario: Author creates a kata with required data
  Given "alice" has the author role
  When "alice" submits title "Two Sum", a description, difficulty 3, and "Python"
  Then the system creates a kata authored by "alice"
```

### SC-06 — Неповна kata

```gherkin
Scenario: Author is warned about missing kata data
  Given "alice" has the author role
  When "alice" submits a kata without a description
  Then the system rejects creation
  And the system lists "description" as missing
```

