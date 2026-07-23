# WORK — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса WORK, вынесенные из `endpoints/WORK.md`. Сигнатуры и типы — там же и в `schemas/WORK.md`.

## CompletedWorks

### `POST /CompletedWorks`

## Пример запроса:
`POST /CompletedWorks`
            
Заголовки (опционально):
- `X-Concurrency-Stamp` (Guid) — идемпотентность; повтор с тем же значением даёт конфликт.
- `X-Suppress-Conflict: true` — при конфликте вернуть `200 OK` вместо `409 Conflict`.
            
```json
[
  {
    "taskID": 12345,
    "data": [
      {
        "workTypeID": 10,
        "maintainedAssetID": 500,
        "implementedByUserID": 1001,
        "started": "2026-05-15T08:00:00Z",
        "finished": "2026-05-15T10:30:00Z",
        "notes": "Замена фильтра",
        "quantity": 1.0,
        "measurementUnitID": 1
      }
    ]
  }
]
```
            
## Пример успешного ответа (201):
```json
[
  {
    "taskID": 12345,
    "id": 1,
    "concurrencyStamp": "a1b2c3d4-e5f6-7890-abcd-ef1234567890"
  }
]
```
            
В заголовке ответа `X-Last-Lsn` возвращается метка изменений для синхронизации клиента.
            
## Негативные сценарии:
- 400 BadRequest: заголовок `X-Concurrency-Stamp` передан, но пустой, длиннее 255 символов или не является Guid.
- 409 Conflict: повтор запроса с тем же `X-Concurrency-Stamp`.
- 200 OK: конфликт идемпотентности при заголовке `X-Suppress-Conflict: true`.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompletedWorkAdd`.

### `PUT /CompletedWorks`

## Пример запроса:
`PUT /CompletedWorks`
            
```json
[
  {
    "taskID": 12345,
    "data": [
      {
        "id": 1,
        "workTypeID": 10,
        "maintainedAssetID": 500,
        "started": "2026-05-15T08:00:00Z",
        "finished": "2026-05-15T11:00:00Z",
        "notes": "Обновлённые примечания",
        "quantity": 2.0,
        "measurementUnitID": 1
      }
    ]
  }
]
```
            
## Пример успешного ответа (202):
Тело ответа пустое. В заголовке `X-Last-Lsn` — метка изменений.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompletedWorkUpdate`.

### `DELETE /CompletedWorks`

## Пример запроса:
`DELETE /CompletedWorks`
            
```json
[
  {
    "taskID": 12345,
    "data": [1, 2]
  }
]
```
            
## Пример успешного ответа (202):
Тело ответа пустое. В заголовке `X-Last-Lsn` — метка изменений.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompletedWorkDelete`.

## Tasks

### `POST /Tasks`

## Пример запроса:
`POST /Tasks`
            
Заголовки (опционально):
- `X-Concurrency-Stamp` (Guid) — идемпотентность; повтор с тем же значением даёт конфликт.
            
```json
{
  "assetID": 500,
  "workTypeID": 10,
  "criticalityID": 1,
  "notes": "Неисправность оборудования",
  "requestedStartDateTime": "2026-05-15T08:00:00Z",
  "requestedFinishDateTime": "2026-05-15T12:00:00Z"
}
```
            
## Пример успешного ответа (201):
```json
{
  "id": 12345,
  "number": "T-12345",
  "concurrencyStamp": "a1b2c3d4-e5f6-7890-abcd-ef1234567890"
}
```
            
В заголовке ответа `X-Last-Lsn` возвращается метка изменений для синхронизации клиента.
            
## Негативные сценарии:
- 400 BadRequest: тело запроса отсутствует или заголовок `X-Concurrency-Stamp` передан, но пустой, длиннее 255 символов или не является Guid.
- 409 Conflict: повтор запроса с тем же `X-Concurrency-Stamp`.
- 422 UnprocessableEntity: замечания санитайзера текста/HTML в теле заявки.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskAdd`.

### `DELETE /Tasks/{taskId}/completedWorks/marking-codes`

Пример запроса:
```
DELETE /tasks/123/completedWorks/marking-codes
```
            
Пример успешного ответа (200 OK):
```
{
  "taskID": 123,
  "deletedCount": 42
}
```

Дополнительные ошибки (из хранилища/БД) маппятся по ключу SQL-исключения в `BaseException` с заданным `StatusCode`,
поэтому метод также может вернуть, например: `403 Forbidden` (AccessDenied*), `409 Conflict` (TaskClosed/AlreadyDone/...),
`400 BadRequest` (InvalidDataFormat*/NoDataFound/EmptyJson), `404 NotFound` (TaskNotFound/...).

            
Заголовки: поддерживает и возвращает `X-Last-Lsn` (`LastLsnHeader`) для операции записи.

### `GET /Tasks/{taskId}/completedWorks/{completedWorkID}/marking-codes`

Пример запроса:
```
GET /tasks/123/completedWorks/1/marking-codes
```
            
Пример успешного ответа (200 OK):
```
{
  "taskID": 123,
  "completedWorkID": 1,
  "materialID": null,
  "items": [
    {
      "completedWorkID": 1,
      "materialID": 777,
      "warehouseID": 10,
      "inventoryID": 555001,
      "code": "0104601234567890215ABCDEF1234567890\u001d93XYZ123",
      "scannedAtUtc": null,
      "receivedAtUtc": "2026-03-05T14:12:33.456Z",
      "createdBy": 98765
    },
    {
      "completedWorkID": 1,
      "materialID": 888,
      "warehouseID": 10,
      "inventoryID": 555002,
      "code": "0104601234567890215QWERTY1234567890\u001d93AAA111",
      "scannedAtUtc": "2026-03-05T14:13:10.000Z",
      "receivedAtUtc": "2026-03-05T14:13:10.500Z",
      "createdBy": 98765
    }
  ]
}
```

Дополнительные ошибки (из хранилища/БД) маппятся по ключу SQL-исключения в `BaseException` с заданным `StatusCode`,
поэтому метод также может вернуть, например: `403 Forbidden` (AccessDenied*), `400 BadRequest` (InvalidDataFormat*/NoDataFound/EmptyJson),
`404 NotFound` (TaskNotFound/CompletedWorkMaterialNotFound/...).

            
Заголовки: `X-Last-Lsn` (`LastLsnHeader`) поддерживается для совместимости. Для операции чтения значение может не измениться.

### `POST /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/marking-codes`

Пример запроса:
```
POST /tasks/123/completedWorks/1/materials/marking-codes
{
  "materials": [
    {
      "materialId": 777,
      "warehouseID": 10,
      "inventoryID": 555001,
      "codes": [
        { "code": "010...", "scannedAtUtc": "2026-02-18T10:11:12Z" }
      ]
    },
    {
      "materialId": 888,
      "warehouseID": 10,
      "codes": [
        { "code": "010...", "scannedAtUtc": null }
      ]
    }
  ]
}
```
            
Пример успешного ответа (200 OK):
```
{
  "taskID": 123,
  "completedWorkID": 1,
  "items": [
    { "materialID": 777, "warehouseID": 10, "inventoryID": 555001, "code": "010...", "action": "INSERT" },
    { "materialID": 888, "warehouseID": 10, "inventoryID": 555002, "code": "010...", "action": "UPDATE" }
  ],
  "errors": [
    { "materialID": 999, "warehouseID": 10, "inventoryID": null, "code": "010...", "reason": "MaterialContextNotFound", "message": "Material context was not found in the selected completed work." }
  ]
}
```

Поле `items[].action` соответствует SQL Server `$action` из `MERGE` и принимает значения `INSERT`/`UPDATE`.
Важно: `UPDATE` означает восстановление ранее отвязанного кода (soft-delete), а не "обновление активной привязки".


Если код уже существует и активен (привязан в рамках тенанта) — операция завершится ошибкой.


Частичный успех: если хотя бы один код можно корректно привязать — метод вернёт `200 OK`,
а ошибки для остальных кодов будут перечислены в `errors`.


В примере ниже: `INSERT` — создана новая привязка, `UPDATE` — восстановлена ранее отвязанная (soft-delete) привязка.


Дополнительные ошибки (из хранилища/БД) маппятся по ключу SQL-исключения в `BaseException` с заданным `StatusCode`,
поэтому метод также может вернуть, например: `403 Forbidden` (AccessDenied*), `409 Conflict` (TaskClosed/AlreadyDone/...),
`400 BadRequest` (InvalidDataFormat*/NoDataFound/EmptyJson), `404 NotFound` (TaskNotFound/CompletedWorkMaterialNotFound/...).

            
Заголовки: поддерживает и возвращает `X-Last-Lsn` (`LastLsnHeader`) для операции записи.

### `PUT /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/marking-codes`

Пример запроса:
```
PUT /tasks/123/completedWorks/1/materials/marking-codes
{
  "materials": [
    {
      "materialId": 777,
      "warehouseID": 10,
      "inventoryID": 555001,
      "codes": [
        { "code": "010...", "scannedAtUtc": "2026-02-18T10:11:12Z" }
      ]
    }
  ]
}
```

Важно:
<list type="bullet"><item><description>операция не создаёт новые коды: каждый код из запроса должен уже существовать и быть активным</description></item><item><description>частичный успех: если хотя бы один код можно корректно перенести — метод вернёт `200 OK`, а ошибки для остальных кодов будут перечислены в `errors`</description></item></list>
            
Пример успешного ответа (200 OK):
```
{
  "taskID": 123,
  "completedWorkID": 1,
  "items": [
    {
      "materialID": 777,
      "warehouseID": 10,
      "inventoryID": 555001,
      "code": "0104601234567890215ABCDEF1234567890\u001d93XYZ123"
    }
  ],
  "errors": [
    { "materialID": 888, "warehouseID": 10, "inventoryID": null, "code": "010...", "reason": "MarkingCodeNotFound", "message": "The marking code was not found or is not active." }
  ]
}
```

Дополнительные ошибки (из хранилища/БД) маппятся по ключу SQL-исключения в `BaseException` с заданным `StatusCode`,
поэтому метод также может вернуть, например: `403 Forbidden` (AccessDenied*), `409 Conflict` (TaskClosed/AlreadyDone/...),
`400 BadRequest` (InvalidDataFormat*/NoDataFound/EmptyJson), `404 NotFound` (TaskNotFound/CompletedWorkMaterialNotFound/...).

            
Заголовки: поддерживает и возвращает `X-Last-Lsn` (`LastLsnHeader`) для операции записи.

### `DELETE /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/marking-codes`

Пример запроса:
```
DELETE /tasks/123/completedWorks/1/materials/marking-codes
{
  "materials": [
    { "materialId": 777, "warehouseID": 10, "inventoryID": 555001, "codes": [ "010...", "010..." ] }
  ]
}
```
            
Если часть кодов не найдена — это не ошибка: такие элементы попадут в `notFound`.
Это намеренное поведение API для идемпотентности: сервер не передаёт в хранилище коды, которых нет в текущих привязках.
            
Пример успешного ответа (200 OK):
```
{
  "taskID": 123,
  "completedWorkID": 1,
  "items": [
    {
      "materialID": 777,
      "warehouseID": 10,
      "inventoryID": 555001,
      "deleted": [ "010...", "010..." ],
      "notFound": [ "010..." ]
    }
  ]
}
```

Дополнительные ошибки (из хранилища/БД) маппятся по ключу SQL-исключения в `BaseException` с заданным `StatusCode`,
поэтому метод также может вернуть, например: `403 Forbidden` (AccessDenied*), `409 Conflict` (TaskClosed/AlreadyDone/...),
`400 BadRequest` (InvalidDataFormat*/NoDataFound/EmptyJson), `404 NotFound` (TaskNotFound/CompletedWorkMaterialNotFound/...).

            
Заголовки: поддерживает и возвращает `X-Last-Lsn` (`LastLsnHeader`) для операции записи.

### `GET /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/{materialID}/marking-codes`

Пример запроса:
```
GET /tasks/123/completedWorks/1/materials/777/marking-codes
```
            
Пример успешного ответа (200 OK):
```
{
  "taskID": 123,
  "completedWorkID": 1,
  "materialID": 777,
  "items": [
    {
      "completedWorkID": 1,
      "materialID": 777,
      "warehouseID": 10,
      "inventoryID": 555001,
      "code": "0104601234567890215ABCDEF1234567890\u001d93XYZ123",
      "scannedAtUtc": "2026-03-05T14:12:31.123Z",
      "receivedAtUtc": "2026-03-05T14:12:33.456Z",
      "createdBy": 98765
    }
  ]
}
```

Дополнительные ошибки (из хранилища/БД) маппятся по ключу SQL-исключения в `BaseException` с заданным `StatusCode`,
поэтому метод также может вернуть, например: `403 Forbidden` (AccessDenied*), `400 BadRequest` (InvalidDataFormat*/NoDataFound/EmptyJson),
`404 NotFound` (TaskNotFound/CompletedWorkMaterialNotFound/...).

            
Заголовки: `X-Last-Lsn` (`LastLsnHeader`) поддерживается для совместимости. Для операции чтения значение может не измениться.

### `POST /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/{materialID}/marking-codes`

Пример запроса:
```
POST /tasks/123/completedWorks/1/materials/777/marking-codes
{
  "warehouseID": 10,
  "inventoryID": 555001,
  "codes": [
    { "code": "010...", "scannedAtUtc": "2026-02-18T10:11:12Z" },
    { "code": "010...", "scannedAtUtc": "2026-02-18T10:11:15Z" }
  ]
}
```
`warehouseID` обязателен.
`inventoryID` опционален на уровне API: если не передан — сервер попытается определить его по контексту материала
(taskId + completedWorkId + materialId + warehouseID). Если определить однозначно нельзя — вернётся `409 Conflict` (нужно указать `inventoryID`).


Поле `items[].action` соответствует SQL Server `$action` из `MERGE` и принимает значения `INSERT`/`UPDATE`.
Важно: `UPDATE` означает восстановление ранее отвязанного кода (soft-delete), а не "обновление активной привязки".


Частичный успех: если хотя бы один код можно корректно привязать — метод вернёт `200 OK`,
а ошибки для остальных кодов будут перечислены в `errors`.


В примере ниже: `INSERT` — создана новая привязка, `UPDATE` — восстановлена ранее отвязанная (soft-delete) привязка.


Важно про коды ответа:
<list type="bullet"><item><description>если есть хотя бы один успешно обработанный код — ответ `200 OK` и подробности ошибок в `errors`</description></item><item><description>если ни один код не может быть обработан (например, `MaterialContextNotFound`/`DuplicateInRequest`/...) — ответ `409 Conflict` и подробности в `errors`</description></item></list>

Дополнительные ошибки (из хранилища/БД) маппятся по ключу SQL-исключения в `BaseException` с заданным `StatusCode`,
поэтому метод также может вернуть, например: `403 Forbidden` (AccessDenied*), `409 Conflict` (TaskClosed/AlreadyDone/...),
`400 BadRequest` (InvalidDataFormat*/NoDataFound/EmptyJson), `404 NotFound` (TaskNotFound/...).

            
Пример успешного ответа (200 OK):
```
{
  "taskID": 123,
  "completedWorkID": 1,
  "materialID": 777,
  "warehouseID": 10,
  "inventoryID": 555001,
  "items": [
    { "code": "010...", "action": "INSERT" },
    { "code": "010...", "action": "UPDATE" }
  ],
  "errors": [
    { "code": "010...", "reason": "MarkingCodeAlreadyExists", "message": "The marking code is already in use." }
  ]
}
```
            
Заголовки: поддерживает и возвращает `X-Last-Lsn` (`LastLsnHeader`) для операции записи.

### `PUT /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/{materialID}/marking-codes`

Пример запроса:
```
PUT /tasks/123/completedWorks/1/materials/777/marking-codes
{
  "warehouseID": 10,
  "inventoryID": 555001,
  "codes": [
    { "code": "010...", "scannedAtUtc": "2026-02-18T10:11:12Z" },
    { "code": "010...", "scannedAtUtc": "2026-02-18T10:11:15Z" }
  ]
}
```
            
Важно:
<list type="bullet"><item><description>операция не создаёт новые коды: каждый код из запроса должен уже существовать и быть активным</description></item><item><description>операция не удаляет коды, которые уже привязаны к материалу, но не перечислены в запросе (для удаления используйте DELETE)</description></item><item><description>частичный успех: если хотя бы один код можно корректно перенести — метод вернёт `200 OK`, а ошибки для остальных кодов будут перечислены в `errors`</description></item></list>
            
После выполнения метод возвращает актуальный список кодов для (materialId + warehouseID + inventoryID).
            

`warehouseID` обязателен.
`inventoryID` опционален на уровне API: если не передан — сервер попытается определить его по контексту материала
(taskId + completedWorkId + materialId + warehouseID). Если определить однозначно нельзя — вернётся `409 Conflict` (нужно указать `inventoryID`).


Важно про коды ответа:
<list type="bullet"><item><description>если есть хотя бы один успешно обработанный код — ответ `200 OK` и подробности ошибок в `errors`</description></item><item><description>если ни один код не может быть обработан (например, `MaterialContextNotFound`/`MarkingCodeNotFound`/...) — ответ `409 Conflict` и подробности в `errors`</description></item></list>

Дополнительные ошибки (из хранилища/БД) маппятся по ключу SQL-исключения в `BaseException` с заданным `StatusCode`,
поэтому метод также может вернуть, например: `403 Forbidden` (AccessDenied*), `409 Conflict` (TaskClosed/AlreadyDone/...),
`400 BadRequest` (InvalidDataFormat*/NoDataFound/EmptyJson), `404 NotFound` (TaskNotFound/...).

            
Пример успешного ответа (200 OK):
```
{
  "taskID": 123,
  "completedWorkID": 1,
  "materialID": 777,
  "items": [
    {
      "completedWorkID": 1,
      "materialID": 777,
      "warehouseID": 10,
      "inventoryID": 555001,
      "code": "0104601234567890215ABCDEF1234567890\u001d93XYZ123",
      "scannedAtUtc": "2026-03-05T14:12:31.123Z",
      "receivedAtUtc": "2026-03-05T14:12:33.456Z",
      "createdBy": 98765
    }
  ],
  "errors": [
    { "code": "010...", "reason": "MarkingCodeNotFound", "message": "The marking code was not found or is not active." }
  ]
}
```

Дополнительные ошибки (из хранилища/БД) маппятся по ключу SQL-исключения в `BaseException` с заданным `StatusCode`,
поэтому метод также может вернуть, например: `403 Forbidden` (AccessDenied*), `409 Conflict` (TaskClosed/AlreadyDone/...),
`400 BadRequest` (InvalidDataFormat*/NoDataFound/EmptyJson), `404 NotFound` (TaskNotFound/CompletedWorkMaterialNotFound/...).

            
Заголовки: поддерживает и возвращает `X-Last-Lsn` (`LastLsnHeader`) для операции записи.

### `DELETE /Tasks/{taskId}/completedWorks/{completedWorkID}/materials/{materialID}/marking-codes`

Пример запроса:
```
DELETE /tasks/123/completedWorks/1/materials/777/marking-codes
{
  "warehouseID": 10,
  "inventoryID": 555001,
  "codes": [ "010...", "010..." ]
}
```
            
Если часть кодов не найдена — это не ошибка: такие элементы попадут в `notFound`.
Это намеренное поведение API для идемпотентности: сервер не передаёт в хранилище коды, которых нет в текущих привязках.
            

`warehouseID` обязателен.
`inventoryID` опционален на уровне API: если не передан — сервер попытается определить его по контексту материала
(taskId + completedWorkId + materialId + warehouseID). Если определить однозначно нельзя — вернётся `409 Conflict` (нужно указать `inventoryID`).


Дополнительные ошибки (из хранилища/БД) маппятся по ключу SQL-исключения в `BaseException` с заданным `StatusCode`,
поэтому метод также может вернуть, например: `403 Forbidden` (AccessDenied*), `409 Conflict` (TaskClosed/AlreadyDone/...),
`400 BadRequest` (InvalidDataFormat*/NoDataFound/EmptyJson), `404 NotFound` (TaskNotFound/CompletedWorkMaterialNotFound/...).

            
Пример успешного ответа (200 OK):
```
{
  "taskID": 123,
  "completedWorkID": 1,
  "materialID": 777,
  "warehouseID": 10,
  "inventoryID": 555001,
  "deleted": [ "010...", "010..." ],
  "notFound": [ "010..." ]
}
```
            
Заголовки: поддерживает и возвращает `X-Last-Lsn` (`LastLsnHeader`) для операции записи.

### `GET /Tasks/{taskId}/marking-codes`

Пример запроса:
```
GET /tasks/123/marking-codes
```
            
Пример успешного ответа (200 OK):
```
{
  "taskID": 123,
  "completedWorkID": null,
  "materialID": null,
  "items": [
    {
      "completedWorkID": 1,
      "materialID": 777,
      "warehouseID": 10,
      "inventoryID": 555001,
      "code": "0104601234567890215ABCDEF1234567890\u001d93XYZ123",
      "scannedAtUtc": "2026-03-05T14:12:31.123Z",
      "receivedAtUtc": "2026-03-05T14:12:33.456Z",
      "createdBy": 98765
    },
    {
      "completedWorkID": 2,
      "materialID": 888,
      "warehouseID": 10,
      "inventoryID": 555002,
      "code": "0104601234567890215QWERTY1234567890\u001d93AAA111",
      "scannedAtUtc": null,
      "receivedAtUtc": "2026-03-05T14:13:10.500Z",
      "createdBy": 98765
    }
  ]
}
```

Дополнительные ошибки (из хранилища/БД) маппятся по ключу SQL-исключения в `BaseException` с заданным `StatusCode`,
поэтому метод также может вернуть, например: `403 Forbidden` (AccessDenied*), `400 BadRequest` (InvalidDataFormat*/NoDataFound/EmptyJson),
`404 NotFound` (TaskNotFound/CompletedWorkMaterialNotFound/...).

            
Заголовки: `X-Last-Lsn` (`LastLsnHeader`) поддерживается для совместимости. Для операции чтения значение может не измениться.
