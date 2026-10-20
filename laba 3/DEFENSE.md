# DEFENSE: Sequence-діаграма надсилання розв'язку

## 1. Намір і критерії

Діаграма деталізує UC-03 «Submit solution» та асинхронне оцінювання з UC-04:
від завантаження kata до фінального `passed`/`failed`. Критерії у
[`spec.md`](spec.md) вимагають узгоджених учасників, напрямлених викликів,
return-повідомлень, `alt`, `loop`, `opt` і коректного переходу `Attempt`.

## 2. Топ-3 розбіжності, які знайдено і виправлено

1. Нова сутність `Submission`/`TestRun` суперечила ER-моделі — залишено
   `Attempt`, а runner визначено зовнішнім сервісом (пункт 4 `spec.md`).
2. Відсутність `pending` приховувала REQ-04 — додано одну `Attempt` у
   `pending` і `loop` опитування до фінального статусу (пункти 2–3).
3. Випадали перевірка `Language` і ранг — додано `validateSupported()` та
   умовний `getUpdatedRank()` після `passed` (пункт 3).

Деталі наведено в [`audit/sequence-discrepancies.md`](audit/sequence-discrepancies.md);
критерії є джерелом виправлень, а не ручний патч SVG.

## 3. Ключове рішення

Обрано асинхронну модель з однією `Attempt` та статусом `pending`. Розглянуті
синхронний виклик і нова `TestRun` сутність відхилено, бо вони приховують
вимогу про проміжний стан або порушують ER-модель. Рішення зафіксовано в
[`adr/0003-asynchronous-attempt-sequence.md`](adr/0003-asynchronous-attempt-sequence.md).

## 4. Перевірка узгодженості

Звірено `User`, `Kata`, `Language`, `Attempt`, `Rank` і їхні ролі з
[`model/er-diagram.mmd`](../model/er-diagram.mmd). Кроки надсилання звірено з
REQ-03--REQ-06, SC-03--SC-04 і UC-03/UC-04 у
[`laba 2/requirements.md`](../laba%202/requirements.md). SVG згенеровано
безпосередньо з [`model/submit-solution-sequence.mmd`](model/submit-solution-sequence.mmd).
