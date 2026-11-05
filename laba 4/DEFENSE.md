# DEFENSE: процес надсилання розв'язку

## 1. Намір і критерії

Activity-модель деталізує UC-03 від валідації до фінального стану однієї
`Attempt`, включно з `pending`, `passed` і `failed`. Критерії у
[`spec.md`](spec.md) вимагають `if/else`, fork/join, відсутність дублювання
та узгодженість із UC і sequence-моделями.

## 2. Топ-3 розбіжності, які знайдено і виправлено

1. Повторний перегляд pending міг породити нову спробу — у `spec.md` додано
   інваріант однієї `Attempt` і гілку читання тієї самої `attemptId`.
2. У попередньому описі не було явного failed-шляху — критерії зафіксували
   `passed`/`failed` і різну поведінку Rank.
3. Паралельне dispatch/повідомлення не мало явного join — у критерії додано
   вимогу fork/join, а модель має два сходження потоків.

Повний аудит — [`audit/process-discrepancies.md`](audit/process-discrepancies.md).
Кожне виправлення внесене через зміну специфікації, а не ручний патч рендера.

## 3. Ключове рішення

Обрано activity flowchart, а не state machine: завдання потребує ролей,
дій, валідації та fork/join, тоді як стани `Attempt` уже є даними ER-моделі.
Альтернативою була state machine `pending → passed/failed`, але вона приховала
бізнес-дії API, UI та runner. ADR — [`adr/0004-submission-activity-process.md`](adr/0004-submission-activity-process.md).

## 4. Перевірка

Звірено `Attempt`, `User`, `Kata`, `Language`, `Rank` з ER-моделлю; кроки —
з UC-03, REQ-03--REQ-06 і SC-03/SC-04. Окремо перевірено досяжність усіх
гілок і відповідність SVG джерелу Mermaid на рівні вузлів та переходів.
