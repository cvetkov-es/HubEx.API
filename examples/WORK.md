# WORK — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса WORK, вынесенные из `endpoints/WORK.md`. Сигнатуры и типы — там же и в `schemas/WORK.md`.

## Tasks

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
