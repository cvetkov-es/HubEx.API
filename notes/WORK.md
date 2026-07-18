# WORK — заметки практики

> **Что здесь:** проверенные практикой правила и грабли сервиса WORK (заявки). Сигнатуры ручек — [endpoints/WORK.md](../endpoints/WORK.md).
> **Когда сюда идти:** перед работой с заявками через API.

## Грабли

⚠ Нет единого понятия «незакрытая заявка» — `isClosed` и `isDeleted` независимы. `isClosed=false` сам по себе НЕ исключает мягко удалённые заявки: чтобы получить строго активные незакрытые, нужно явно комбинировать `isClosed=false&isDeleted=false`. Расхождение в счётчиках при добавлении/убирании `isDeleted=false` — ожидаемое поведение, не баг API (проверено эмпирически 4 комбинациями `isClosed`×`isDeleted` на живом тенанте).

⚠ То же самое для «невыполненная заявка» — `isCompleted` и `isDeleted` тоже независимы (стадии «Выполнена»/«Закрыта» разные). `isCompleted=false` без `isDeleted=false` тоже включает мягко удалённые. Правило общее: любой флаг из `taskFlags` (`isClosed`, `isCompleted`, ...) нужно комбинировать с `isDeleted=false`, если нужны строго активные заявки (проверено эмпирически на тенанте 342, 2026-07-06: 8132 против 13430).

⚠ `/Tasks/count` капризна к параметрам: без `dateFrom`/`dateTill` — `500 SqlDateTime overflow`; с ними вместе с `creationFrom`/`creationTill` — `409 InvalidDatePeriod`. Для простого «сколько заявок за период» надёжнее `HEAD /Tasks ?creationFrom&creationTill` и читать `Content-Range: items=0-0/{total}` из заголовка ответа.

⚠ На практике `GET /Tasks/{taskID}/completedWorks/technicians` отдаёт не одиночный `CWTechResult`, а `map<CWTechResult>`, ключ — `completedWorkID` (по одной записи на каждую Выполненную работу заявки). Если у заявки нет Выполненных работ с исполнителями — `204 No Content` (не пустой массив).

⚠ У элементов списка `GET /Tasks` **нет поля `id`** — идентификатор заявки есть только в ключе map-ответа (проверено 2026-07-15: ключи `7102`, `7101`). Схеме это не противоречит — у `Tasks.ListResult` в swagger `id` тоже нет, — но на практике ловушка: клиент, разворачивающий map в массив через `Object.values()`, теряет идентификатор молча. Брать `Object.entries()` и класть ключ в `id`. Человекочитаемый идентификатор заявки — `number`. Для сравнения: у `GET /ES/Assets` (`AssetExtResult`) `id` лежит в теле значения. Перечень полей — [schemas/WORK.md](../schemas/WORK.md) (`Tasks.ListResult`).

## Наиболее используемые

`GET /Tasks`, `POST /Tasks`, `GET /Tasks/{taskID}`, `PATCH /Tasks/{taskID}`, `POST /TaskStagingHistory`, `GET /Tasks/{taskID}/stages/next`, `POST /CompletedWorks` — расшифровка в [overview.md](../overview.md).
