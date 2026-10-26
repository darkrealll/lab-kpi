# DEFENSE: Sequence-діаграми сценаріїв надсилання розв'язку

## 1. Намір і критерії

Дві діаграми деталізують окремі сценарії UC-03 «Submit solution»: SC-03
показує успішне надсилання до `passed` і рангу, а SC-04 — очікування
`pending` без дублювання `Attempt`. Критерії у [`spec.md`](spec.md) вимагають
окрему діаграму на сценарій, activation bars, напрямлені виклики,
return-повідомлення та комбіновані фрагменти.

## 2. Топ-3 розбіжності, які знайдено і виправлено

1. Нова сутність `Submission`/`TestRun` суперечила ER-моделі — залишено
   `Attempt`, а runner визначено зовнішнім сервісом (пункт 4 `spec.md`).
2. Одна загальна діаграма змішувала SC-03 і SC-04 — створено окремі джерела й
   рендери для кожного сценарію (пункти 1–2).
3. Не було видно життєвого циклу активації навколо гілок — додано `activate`
   до комбінованих фрагментів і `deactivate` після них для UI/API та
   локальних виконавців (пункт 2).

Деталі наведено в [`audit/sequence-discrepancies.md`](audit/sequence-discrepancies.md);
критерії є джерелом виправлень, а не ручний патч SVG.

## 3. Ключове рішення

Обрано асинхронну модель з однією `Attempt` та статусом `pending`, але
представлено її двома діаграмами — окремо для SC-03 і SC-04. Розглянуті
синхронний виклик і нова `TestRun` сутність відхилено, бо вони приховують
вимогу про проміжний стан або порушують ER-модель. Рішення зафіксовано в
[`adr/0003-asynchronous-attempt-sequence.md`](adr/0003-asynchronous-attempt-sequence.md).

## 4. Перевірка узгодженості

Звірено `User`, `Kata`, `Language`, `Attempt`, `Rank` і їхні ролі з
[`model/er-diagram.mmd`](../model/er-diagram.mmd). Кроки надсилання звірено з
REQ-03--REQ-06, SC-03--SC-04 і UC-03/UC-04 у
[`laba 2/requirements.md`](../laba%202/requirements.md). SVG згенеровано
окремо з [`model/sc-03-successful-submission.mmd`](model/sc-03-successful-submission.mmd)
і [`model/sc-04-pending-attempt.mmd`](model/sc-04-pending-attempt.mmd).
