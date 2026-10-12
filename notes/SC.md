# SC — заметки практики

> **Что здесь:** проверенные практикой правила и грабли сервиса SC (договоры обслуживания). Сигнатуры ручек — [endpoints/SC.md](../endpoints/SC.md).
> **Когда сюда идти:** перед работой с договорами через API.

## Грабли

⚠ `GET /ServiceContract` — мягко удалённые договоры в список **не попадают**, хотя ни query-параметра `isDeleted`, ни поля `isDeleted` в `ContractListResult` нет; `HEAD /ServiceContract` считает тотал так же, без удалённых. Карточка `GET /ServiceContract/{contractID}` удалённый договор отдаёт — `200` с `isDeleted: true`, а не `404`. Проверено живыми вызовами 2026-10-12, тенант 185: `POST /ServiceContract` → id 10, список `items=1-10/10`; `DELETE /ServiceContract/10` → `202`; список снова `items=1-9/9`, `HEAD` → `items=0-0/9`, карточка `/ServiceContract/10` → `200`, `isDeleted: true`. Правило «всегда `isDeleted=false`» из [overview.md](../overview.md) к списку договоров неприменимо — фильтровать нечем и не нужно.

⚠ `GET /ServiceContract/{contractID}/assets` — `Range` на тело ответа не действует: при `Range: items=1-5` пришли все 17 привязок, а `Content-Range` при этом заявил `items=1-5/17` (проверено 2026-10-12, тенант 185, договор 1). Границы страницы по `Content-Range` здесь не вычислять: пагинируя, считать фактически полученные записи и останавливаться, когда их не меньше тотала.
