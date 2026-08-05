# WORK — заметки практики

> **Что здесь:** проверенные практикой правила и грабли сервиса WORK (заявки). Сигнатуры ручек — [endpoints/WORK.md](../endpoints/WORK.md).
> **Когда сюда идти:** перед работой с заявками через API.

## Грабли

⚠ Нет единого понятия «незакрытая заявка» — `isClosed` и `isDeleted` независимы. `isClosed=false` сам по себе НЕ исключает мягко удалённые заявки: чтобы получить строго активные незакрытые, нужно явно комбинировать `isClosed=false&isDeleted=false`. Расхождение в счётчиках при добавлении/убирании `isDeleted=false` — ожидаемое поведение, не баг API (проверено эмпирически 4 комбинациями `isClosed`×`isDeleted` на живом тенанте).

⚠ То же самое для «невыполненная заявка» — `isCompleted` и `isDeleted` тоже независимы (стадии «Выполнена»/«Закрыта» разные). `isCompleted=false` без `isDeleted=false` тоже включает мягко удалённые. Правило общее: любой флаг из `taskFlags` (`isClosed`, `isCompleted`, ...) нужно комбинировать с `isDeleted=false`, если нужны строго активные заявки (проверено эмпирически на тенанте 342, 2026-07-06: 8132 против 13430).

⚠ `/Tasks/count` капризна к параметрам: без `dateFrom`/`dateTill` — `500 SqlDateTime overflow`; с ними вместе с `creationFrom`/`creationTill` — `409 InvalidDatePeriod`. Для простого «сколько заявок за период» надёжнее `HEAD /Tasks ?creationFrom&creationTill` и читать `Content-Range: items=0-0/{total}` из заголовка ответа.

⚠ Сортировка — пара `orderBy` (числовой id, только из ключа map `GET /TaskOrderBy`) и `sortDirection` с доменом **1 = asc, 2 = desc** объявлена у пяти WORK-ручек (`GET /Tasks`, `HEAD /Tasks`, `GET /Tasks/count`, `GET /Tasks/groupBy/geoHash`, `GET /Tasks/short`); без `sortDirection` — desc, без `orderBy` — сортировка по дате создания заявки (`timesheet.created`; в `GET /TaskOrderBy` эта запись — id 1, `name` «Дата подачи», `code` `CreationDate`). Самая свежая заявка — `sortDirection=2` без `orderBy` (проверено 2026-08-05, тенант 185, 3951 заявка: id 3993, 3992, 3991); с явным `orderBy=1` результат тот же, поскольку это и есть дефолтное поле.

⚠ Значение вне домена ведёт себя по-разному у двух параметров — проверено это только на `GET /Tasks`, для остальных четырёх ручек с этой парой не считать доказанным. У `sortDirection` вне домена (`0`, `3`) **молча выключается сортировка целиком**, вместе с `orderBy`: выдача идёт в натуральном порядке id (`orderBy=8&sortDirection=0` → id 1,2,3; для сравнения `orderBy=8&sortDirection=1` → id 2,21,23 по возрастанию `lastModified` — сортировка работает). У `orderBy` вне домена (`99`) сортировка **не выключается — откатывается только поле**, к дате создания: `orderBy=99&sortDirection=2` → id 3993,3992,3991, ровно как без `orderBy` вовсе (будь сортировка выключена, был бы натуральный порядок id 1,2,3). Строкой не принимается ни один параметр: `sortDirection=desc`, `orderBy=CreationDate` (это `code` записи id 1 из тела `GET /TaskOrderBy`, не число) → `409 InvalidData`, тело без указания параметра.

⚠ `GET /TaskOrderBy` отдаёт map, где id есть **только в ключе** (в теле — `name` и `code`), и id разрежены: проверено 2026-08-05 — 1,2,3,4,5,7,8, шестого нет. Позицией в списке id не заменить, а `code` из тела `orderBy` не принимает (`409`). Тот же капкан, что у `GET /Tasks`: `Object.values()` теряет идентификатор молча — брать `Object.entries()`.

⚠ Даты создания заявки нет под именем `creationDate` (0 совпадений во всём `schemas/WORK.md`) — она лежит в блоке `timesheet`: `timesheet.created`, и в списке `GET /Tasks`, и в карточке `GET /Tasks/{taskID}` (проверено 2026-08-05: `О0710000` → `timesheet.created` 2019-10-07 при `lastModified` 2025-06-24). Отсюда типовой ложный вывод «дату подачи по списку не получить»; сортировка `orderBy=1` работает именно по этому полю.

⚠ На практике `GET /Tasks/{taskID}/completedWorks/technicians` отдаёт не одиночный `CWTechResult`, а `map<CWTechResult>`, ключ — `completedWorkID` (по одной записи на каждую Выполненную работу заявки). Если у заявки нет Выполненных работ с исполнителями — `204 No Content` (не пустой массив).

⚠ У элементов списка `GET /Tasks` **нет поля `id`** — идентификатор заявки есть только в ключе map-ответа (проверено 2026-07-15: ключи `7102`, `7101`). Схеме это не противоречит — у `Tasks.ListResult` в swagger `id` тоже нет, — но на практике ловушка: клиент, разворачивающий map в массив через `Object.values()`, теряет идентификатор молча. Брать `Object.entries()` и класть ключ в `id`. Человекочитаемый идентификатор заявки — `number`. Для сравнения: у `GET /ES/Assets` (`AssetExtResult`) `id` лежит в теле значения. Перечень полей — [schemas/WORK.md](../schemas/WORK.md) (`Tasks.ListResult`).

## Наиболее используемые

`GET /Tasks`, `POST /Tasks`, `GET /Tasks/{taskID}`, `PATCH /Tasks/{taskID}`, `POST /TaskStagingHistory`, `GET /Tasks/{taskID}/stages/next`, `POST /CompletedWorks` — расшифровка в [overview.md](../overview.md).
