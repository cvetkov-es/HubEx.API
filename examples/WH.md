# WH — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса WH, вынесенные из `endpoints/WH.md`. Сигнатуры и типы — там же и в `schemas/WH.md`.

## Documents

### `GET /Documents`

## Пример запроса:
`GET /Documents?fetch=100&offset=0&searchText=TR-000123`
            
Диапазон можно задать заголовком `Range` или query-параметрами `fetch` и `offset`.
            
## Пример успешного ответа (200):
```json
[
  {
    "id": 101,
    "name": "TR-000123",
    "documentTypeID": 3,
    "documentType": {
      "id": 3,
      "name": "Перемещение"
    },
    "documentStatus": {
      "id": 2,
      "code": "Posted",
      "name": "Проведен"
    },
    "created": "2026-03-30T10:15:00Z",
    "modified": null,
    "documentDate": "2026-03-30T00:00:00Z",
    "posted": "2026-03-30T10:20:00Z",
    "deleted": "2026-03-30T11:00:00Z",
    "fromWarehouseID": 10,
    "fromWarehouse": {
      "id": 10,
      "name": "Склад-источник"
    },
    "toWarehouseID": 20,
    "toWarehouse": {
      "id": 20,
      "name": "Склад-приемник"
    },
    "operationType": {
      "id": 3,
      "name": "Перемещение"
    },
    "relatedTaskID": 4567,
    "taskNumber": "TASK-4567",
    "responsiblePerson": {
      "id": 123,
      "name": "Иванов Иван"
    },
    "description": "Комментарий по документу"
  }
]
```
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200` (включая поле `documentDate`), но содержит частичный диапазон.
Общее количество записей возвращается в заголовке `Content-Range`.
## Негативные сценарии:
- 204 NoContent: по заданным фильтрам записи не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `DocumentList`.

## Issues

### `GET /Issues`

## Пример запроса:
`GET /Issues?searchText=IS-000123`
            
## Пример успешного ответа (200):
```json
{
  "101": {
    "warehouseID": 10,
    "warehouseName": "Основной склад",
    "documentStatus": null,
    "documentDate": "2026-03-30T00:00:00Z",
    "number": "IS-000123",
    "erpID": "ERP-IS-000123",
    "description": "Списание материалов",
    "deleted": null,
    "operationType": null,
    "created": "2026-03-30T10:15:00Z",
    "modified": null,
    "posted": null,
    "relatedTaskID": 4567,
    "taskNumber": "TASK-4567",
    "responsiblePerson": null
  }
}
```
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: по заданным фильтрам записи не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `IssueList`.

### `POST /Issues`

## Пример запроса:
```json
[
  {
    "warehouseID": 10,
    "operationTypeID": 3,
    "documentDate": "2026-03-30T00:00:00Z",
    "number": "IS-000123",
    "description": "Списание материалов",
    "erpID": "ERP-IS-000123",
    "relatedTaskID": 4567,
    "responsiblePersonID": 123
  }
]
```
## Пример успешного ответа (201):
```json
[101, 102]
```
## Пример ошибки (409):
```json
[
  {
    "traceIdentifier": "00-abc123",
    "code": "ValidationError",
    "message": "Validation failed",
    "arguments": {
      "field": "data"
    }
  }
]
```
## Негативные сценарии:
- 409 Conflict: пустое или отсутствующее тело запроса.
- 409 Conflict: `warehouseID` или `operationTypeID` вне диапазона `1..32767`.
- 409 Conflict: `relatedTaskID` или `responsiblePersonID` меньше `1`.
- 409 Conflict: превышены ограничения длины строк (`number` до 16, `erpID` до 64, `description` до 1024).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `IssueAdd`.

### `PUT /Issues`

## Пример запроса:
```json
[
  {
    "id": 101,
    "warehouseID": 10,
    "operationTypeID": 3,
    "documentDate": "2026-03-30T00:00:00Z",
    "number": "IS-000123",
    "description": "Обновленное описание списания",
    "erpID": "ERP-IS-000123",
    "relatedTaskID": 4567,
    "responsiblePersonID": 123
  }
]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: `id` меньше `1`.
- 409 Conflict: пустое или отсутствующее тело запроса.
- 409 Conflict: `warehouseID` или `operationTypeID` вне диапазона `1..32767`.
- 409 Conflict: `relatedTaskID` или `responsiblePersonID` меньше `1`.
- 409 Conflict: превышены ограничения длины строк (`number` до 16, `erpID` до 64, `description` до 1024).
- 401 Unauthorized / 403 Forbidden: ошибки доступа.

### `DELETE /Issues`

## Пример запроса:
```json
[101, 102]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: ошибка валидации или бизнес-конфликт.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `IssueDelete`.

### `HEAD /Issues`

## Пример запроса:
`HEAD /Issues?searchText=IS-000123`
            
## Пример успешного ответа (200):
Тело ответа отсутствует. Общее количество возвращается в заголовке `Content-Range`.
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `IssueList`.

### `POST /Issues/items`

## Пример запроса:
```json
[
  {
    "issueID": 101,
    "items": [
      {
        "materialID": 5001,
        "measurementUnitID": 1,
        "quantity": 10.5,
        "sortOrder": 1
      }
    ]
  }
]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Пример ошибки (409):
```json
[
  {
    "traceIdentifier": "00-abc123",
    "code": "ValidationError",
    "message": "Validation failed",
    "arguments": {
      "field": "data"
    }
  }
]
```
## Негативные сценарии:
- 409 Conflict: пустое/некорректное тело запроса, ошибка валидации или бизнес-конфликт.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `IssueAdd`.

### `DELETE /Issues/items`

## Пример запроса:
```json
[
  {
    "issueID": 101,
    "items": [5001, 5002]
  }
]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: пустое/некорректное тело запроса, ошибка валидации или бизнес-конфликт.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `IssueDelete`.

### `PUT /Issues/post`

## Пример запроса:
```json
[101, 102]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: ошибка валидации или бизнес-конфликт.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `IssuePost`.

### `PUT /Issues/restore`

## Пример запроса:
```json
[101, 102]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: ошибка валидации или бизнес-конфликт.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `IssueRestore`.

### `PUT /Issues/unpost`

## Пример запроса:
```json
[101, 102]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: ошибка валидации или бизнес-конфликт.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `IssueUnpost`.

### `GET /Issues/{id}`

## Пример запроса:
`GET /Issues/101`
            
## Пример успешного ответа (200):
```json
{
  "warehouseID": 10,
  "warehouseName": "Основной склад",
  "documentStatus": null,
  "documentDate": "2026-03-30T00:00:00Z",
  "number": "IS-000123",
  "erpID": "ERP-IS-000123",
  "description": "Списание материалов",
  "deleted": null,
  "operationType": null,
  "created": "2026-03-30T10:15:00Z",
  "modified": null,
  "posted": null,
  "relatedTaskID": 4567,
  "taskNumber": "TASK-4567",
  "responsiblePerson": null
}
```
## Негативные сценарии:
- 204 NoContent: списание с указанным `id` не найдено.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `IssueGet`.

### `DELETE /Issues/{id}`

## Пример запроса:
`DELETE /Issues/101`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: бизнес-конфликт или ошибка валидации.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `IssueDelete`.

### `PUT /Issues/{id}/post`

## Пример запроса:
`PUT /Issues/101/post`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: бизнес-конфликт или ошибка валидации.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `IssuePost`.

### `PUT /Issues/{id}/restore`

## Пример запроса:
`PUT /Issues/101/restore`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: бизнес-конфликт или ошибка валидации.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `IssueRestore`.

### `PUT /Issues/{id}/unpost`

## Пример запроса:
`PUT /Issues/101/unpost`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: бизнес-конфликт или ошибка валидации.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `IssueUnpost`.

### `GET /Issues/{issueID}/items`

## Пример запроса:
`GET /Issues/101/items`
            
## Пример успешного ответа (200):
```json
[
  {
    "issueID": 101,
    "material": {
      "id": 5001,
      "name": "Материал 1",
      "vendorCode": "MAT-5001"
    },
    "measurementUnit": {
      "id": 1,
      "name": "шт"
    },
    "quantity": 10.5,
    "sortOrder": 1
  }
]
```
## Негативные сценарии:
- 204 NoContent: строки по документу не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `IssueList`.

### `DELETE /Issues/{issueID}/items/{materialID}`

## Пример запроса:
`DELETE /Issues/101/items/5001`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: бизнес-конфликт или ошибка валидации.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `IssueDelete`.

## Receipts

### `GET /Receipts`

## Пример запроса:
`GET /Receipts?searchText=RC-000123`
            
## Пример успешного ответа (200):
```json
{
  "101": {
    "warehouseID": 10,
    "warehouseName": "Основной склад",
    "documentStatus": null,
    "documentDate": "2026-03-30T00:00:00Z",
    "number": "RC-000123",
    "erpID": "ERP-RC-000123",
    "description": "Оприходывание материалов",
    "deleted": null,
    "operationType": null,
    "created": "2026-03-30T10:15:00Z",
    "modified": null,
    "posted": null,
    "relatedTaskID": 4567,
    "taskNumber": "TASK-4567",
    "responsiblePerson": null
  }
}
```
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: по заданным фильтрам записи не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ReceiptList`.

### `POST /Receipts`

## Пример запроса:
```json
[
  {
    "warehouseID": 10,
    "operationTypeID": 3,
    "documentDate": "2026-03-30T00:00:00Z",
    "number": "RC-000123",
    "description": "Оприходывание материалов",
    "erpID": "ERP-RC-000123",
    "relatedTaskID": 4567,
    "responsiblePersonID": 123
  }
]
```
## Пример успешного ответа (201):
```json
[101, 102]
```
## Негативные сценарии:
- 409 Conflict: пустое/некорректное тело запроса, ошибка валидации или бизнес-конфликт.
- 409 Conflict: `warehouseID` или `operationTypeID` вне диапазона `1..32767`.
- 409 Conflict: `relatedTaskID` или `responsiblePersonID` меньше `1`.
- 409 Conflict: превышены ограничения длины строк (`number` до 16, `erpID` до 64, `description` до 1024).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ReceiptAdd`.

### `PUT /Receipts`

## Пример запроса:
```json
[
  {
    "id": 101,
    "warehouseID": 10,
    "operationTypeID": 3,
    "documentDate": "2026-03-30T00:00:00Z",
    "number": "RC-000123",
    "description": "Обновленное описание оприходывания",
    "erpID": "ERP-RC-000123",
    "relatedTaskID": 4567,
    "responsiblePersonID": 123
  }
]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: пустое/некорректное тело запроса, ошибка валидации или бизнес-конфликт.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ReceiptUpdate`.

### `DELETE /Receipts`

## Пример запроса:
```json
[101, 102]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: ошибка валидации или бизнес-конфликт.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ReceiptDelete`.

### `HEAD /Receipts`

## Пример запроса:
`HEAD /Receipts?searchText=RC-000123`
            
## Пример успешного ответа (200):
Тело ответа отсутствует. Общее количество возвращается в заголовке `Content-Range`.
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ReceiptList`.

### `POST /Receipts/items`

## Пример запроса:
```json
[
  {
    "receiptID": 101,
    "items": [
      {
        "materialID": 5001,
        "measurementUnitID": 1,
        "quantity": 10.5,
        "sortOrder": 1
      }
    ]
  }
]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Пример ошибки (409):
```json
[
  {
    "traceIdentifier": "00-abc123",
    "code": "InvalidData",
    "message": "Неверные данные",
    "arguments": {
      "field": "Quantity"
    }
  }
]
```
## Негативные сценарии:
- 409 Conflict: пустое или отсутствующее тело запроса.
- 409 Conflict: отсутствует или пустой массив `items`.
- 409 Conflict: в строке `items` отсутствует или некорректен обязательный параметр — `materialID`, `measurementUnitID`, `sortOrder` меньше `1`, `quantity` не больше `0` (`InvalidData`).
- 409 Conflict: документ не найден (`ReceiptNotFound`), удалён (`ReceiptDeleted`), проведён (`ReceiptPosted`).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ReceiptAdd`.

### `DELETE /Receipts/items`

## Пример запроса:
```json
[
  {
    "receiptID": 101,
    "items": [5001, 5002]
  }
]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: пустое или отсутствующее тело запроса.
- 409 Conflict: документ не найден (`ReceiptNotFound`), проведён (`ReceiptPosted`), не в статусе черновика (`ReceiptNotDraft`), строка уже удалена (`AlreadyDone`), строка не найдена (`ReceiptItemNotFound`).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ReceiptDelete`.

### `PUT /Receipts/post`

## Пример запроса:
```json
[101, 102]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: ошибка валидации или бизнес-конфликт.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ReceiptPost`.

### `PUT /Receipts/restore`

## Пример запроса:
```json
[101, 102]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: ошибка валидации или бизнес-конфликт.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ReceiptRestore`.

### `PUT /Receipts/unpost`

## Пример запроса:
```json
[101, 102]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: ошибка валидации или бизнес-конфликт.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ReceiptUnpost`.

### `GET /Receipts/{id}`

## Пример запроса:
`GET /Receipts/101`
            
## Пример успешного ответа (200):
```json
{
  "warehouseID": 10,
  "warehouseName": "Основной склад",
  "documentStatus": null,
  "documentDate": "2026-03-30T00:00:00Z",
  "number": "RC-000123",
  "erpID": "ERP-RC-000123",
  "description": "Оприходывание материалов",
  "deleted": null,
  "operationType": null,
  "created": "2026-03-30T10:15:00Z",
  "modified": null,
  "posted": null,
  "relatedTaskID": 4567,
  "taskNumber": "TASK-4567",
  "responsiblePerson": null
}
```
## Негативные сценарии:
- 204 NoContent: запись с указанным `id` не найдена.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ReceiptGet`.

### `DELETE /Receipts/{id}`

## Пример запроса:
`DELETE /Receipts/101`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: бизнес-конфликт или ошибка валидации.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ReceiptDelete`.

### `PUT /Receipts/{id}/post`

## Пример запроса:
`PUT /Receipts/101/post`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: бизнес-конфликт или ошибка валидации.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ReceiptPost`.

### `PUT /Receipts/{id}/restore`

## Пример запроса:
`PUT /Receipts/101/restore`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: бизнес-конфликт или ошибка валидации.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ReceiptRestore`.

### `PUT /Receipts/{id}/unpost`

## Пример запроса:
`PUT /Receipts/101/unpost`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: бизнес-конфликт или ошибка валидации.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ReceiptUnpost`.

### `GET /Receipts/{receiptID}/items`

## Пример запроса:
`GET /Receipts/101/items`
            
## Пример успешного ответа (200):
```json
[
  {
    "receiptID": 101,
    "material": {
      "id": 5001,
      "name": "Материал 1",
      "vendorCode": "MAT-5001"
    },
    "measurementUnit": {
      "id": 1,
      "name": "шт"
    },
    "quantity": 10.5,
    "sortOrder": 1
  }
]
```
## Негативные сценарии:
- 204 NoContent: строки по документу не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ReceiptList`.

### `DELETE /Receipts/{receiptID}/items/{materialID}`

## Пример запроса:
`DELETE /Receipts/101/items/5001`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: бизнес-конфликт или ошибка валидации.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ReceiptDelete`.

## Transfers

### `GET /Transfers`

## Пример запроса:
`GET /Transfers?searchText=TR-000123`
            
## Пример успешного ответа (200):
```json
{
  "101": {
    "fromWarehouseID": 10,
    "fromWarehouseName": "Склад-источник",
    "toWarehouseID": 20,
    "toWarehouseName": "Склад-приемник",
    "documentStatus": null,
    "documentDate": "2026-03-30T00:00:00Z",
    "number": "TR-000123",
    "erpID": "ERP-TR-000123",
    "description": "Перемещение материалов между складами",
    "deleted": null,
    "operationType": null,
    "created": "2026-03-30T10:15:00Z",
    "modified": null,
    "posted": null,
    "relatedTaskID": 4567,
    "taskNumber": "TASK-4567",
    "responsiblePerson": null
  }
}
```
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
## Негативные сценарии:
- 204 NoContent: по заданным фильтрам записи не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TransferList`.

### `POST /Transfers`

## Пример запроса:
```json
[
  {
    "fromWarehouseID": 10,
    "toWarehouseID": 20,
    "operationTypeID": 3,
    "documentDate": "2026-03-30T00:00:00Z",
    "number": "TR-000123",
    "description": "Перемещение материалов между складами",
    "erpID": "ERP-TR-000123",
    "relatedTaskID": 4567,
    "responsiblePersonID": 123
  }
]
```
## Пример успешного ответа (201):
```json
[101, 102]
```
## Негативные сценарии:
- 409 Conflict: пустое или отсутствующее тело запроса.
- 409 Conflict: `fromWarehouseID`, `toWarehouseID` или `operationTypeID` вне диапазона `1..32767`.
- 409 Conflict: `fromWarehouseID` совпадает с `toWarehouseID` (`WarehousesMustBeDifferent`).
- 409 Conflict: `relatedTaskID` или `responsiblePersonID` меньше `1`.
- 409 Conflict: превышены ограничения длины строк (`number` до 16, `erpID` до 64, `description` до 1024).
- 409 Conflict: `fromWarehouseID` или `toWarehouseID` не найден (`WarehouseNotFound`).
- 409 Conflict: `responsiblePersonID` ссылается на удалённого пользователя (`UserDeleted`).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TransferAdd`.

### `PUT /Transfers`

## Пример запроса:
```json
[
  {
    "id": 101,
    "fromWarehouseID": 10,
    "toWarehouseID": 20,
    "operationTypeID": 3,
    "documentDate": "2026-03-30T00:00:00Z",
    "number": "TR-000123",
    "description": "Обновленное описание перемещения",
    "erpID": "ERP-TR-000123",
    "relatedTaskID": 4567,
    "responsiblePersonID": 123
  }
]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: `id` меньше `1`.
- 409 Conflict: пустое или отсутствующее тело запроса.
- 409 Conflict: `fromWarehouseID`, `toWarehouseID` или `operationTypeID` вне диапазона `1..32767`.
- 409 Conflict: `fromWarehouseID` совпадает с `toWarehouseID` (`WarehousesMustBeDifferent`).
- 409 Conflict: `relatedTaskID` или `responsiblePersonID` меньше `1`.
- 409 Conflict: превышены ограничения длины строк (`number` до 16, `erpID` до 64, `description` до 1024).
- 401 Unauthorized / 403 Forbidden: ошибки доступа.

### `DELETE /Transfers`

## Пример запроса:
```json
[101, 102]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Пример ошибки (409):
```json
[
  {
    "traceIdentifier": "00-abc123",
    "code": "ValidationError",
    "message": "Validation failed",
    "arguments": {
      "field": "data"
    }
  }
]
```
## Негативные сценарии:
- 409 Conflict: пустое или отсутствующее тело запроса, ошибки валидации.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TransferDelete`.

### `HEAD /Transfers`

## Пример запроса:
`HEAD /Transfers?searchText=TR-000123`
            
## Пример успешного ответа (200):
Тело ответа отсутствует. Общее количество возвращается в заголовке `Content-Range`.
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TransferList`.

### `POST /Transfers/items`

## Пример запроса:
```json
[
  {
    "transferID": 101,
    "items": [
      {
        "materialID": 5001,
        "measurementUnitID": 166,
        "quantity": 10.5,
        "sortOrder": 1
      }
    ]
  }
]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Пример ошибки (409):
```json
[
  {
    "traceIdentifier": "00-abc123",
    "code": "InvalidData",
    "message": "Количество материала должно быть больше нуля."
  }
]
```
## Негативные сценарии:
- 409 Conflict: пустое или отсутствующее тело запроса.
- 409 Conflict: отсутствует или пустой массив `items`.
- 409 Conflict: в строке `items` отсутствует или некорректен обязательный параметр — `materialID`, `measurementUnitID`, `sortOrder` меньше `1`, `quantity` не больше `0` (`InvalidData`).
- 409 Conflict: дубликат `sortOrder` в рамках одного `transferID` (`SortOrderDuplicated`).
- 409 Conflict: документ не найден (`TransferNotFound`), удалён (`TransferDeleted`), проведён (`TransferPosted`).
- 409 Conflict: материал или единица измерения не найдены (`MaterialNotFound`, `MeasurementUnitNotFound`) — при переданных ID, прошедших валидацию модели.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TransferAdd`.

### `DELETE /Transfers/items`

## Пример запроса:
```json
[
  {
    "transferID": 101,
    "items": [5001, 5002]
  }
]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: пустое или отсутствующее тело запроса.
- 409 Conflict: документ не найден (`TransferNotFound`), проведён (`TransferPosted`), не в статусе черновика (`TransferNotDraft`), строка уже удалена (`AlreadyDone`), строка не найдена (`TransferItemNotFound`).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TransferDelete`.

### `PUT /Transfers/post`

## Пример запроса:
```json
[101, 102]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: пустое или отсутствующее тело запроса, ошибки валидации.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TransferPost`.

### `PUT /Transfers/restore`

## Пример запроса:
```json
[101, 102]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: пустое или отсутствующее тело запроса, ошибки валидации.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TransferRestore`.

### `PUT /Transfers/unpost`

## Пример запроса:
```json
[101, 102]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: пустое или отсутствующее тело запроса, ошибки валидации.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TransferUnpost`.

### `GET /Transfers/{id}`

## Пример запроса:
`GET /Transfers/101`
            
## Пример успешного ответа (200):
```json
{
  "fromWarehouseID": 10,
  "fromWarehouseName": "Склад-источник",
  "toWarehouseID": 20,
  "toWarehouseName": "Склад-приемник",
  "documentStatus": null,
  "documentDate": "2026-03-30T00:00:00Z",
  "number": "TR-000123",
  "erpID": "ERP-TR-000123",
  "description": "Перемещение материалов между складами",
  "deleted": null,
  "operationType": null,
  "created": "2026-03-30T10:15:00Z",
  "modified": null,
  "posted": null,
  "relatedTaskID": 4567,
  "taskNumber": "TASK-4567",
  "responsiblePerson": null
}
```
## Негативные сценарии:
- 204 NoContent: запись с указанным `id` не найдена.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TransferGet`.

### `DELETE /Transfers/{id}`

## Пример запроса:
`DELETE /Transfers/101`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: бизнес-конфликт или ошибка валидации.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TransferDelete`.

### `PUT /Transfers/{id}/post`

## Пример запроса:
`PUT /Transfers/101/post`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: бизнес-конфликт или ошибка валидации.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TransferPost`.

### `PUT /Transfers/{id}/restore`

## Пример запроса:
`PUT /Transfers/101/restore`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: бизнес-конфликт или ошибка валидации.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TransferRestore`.

### `PUT /Transfers/{id}/unpost`

## Пример запроса:
`PUT /Transfers/101/unpost`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: бизнес-конфликт или ошибка валидации.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TransferUnpost`.

### `GET /Transfers/{transferID}/items`

## Пример запроса:
`GET /Transfers/101/items`
            
## Пример успешного ответа (200):
```json
[
  {
    "transferID": 101,
    "material": {
      "id": 5001,
      "name": "Материал 1",
      "vendorCode": "MAT-5001"
    },
    "measurementUnit": {
      "id": 1,
      "name": "шт"
    },
    "quantity": 10.5,
    "sortOrder": 1
  }
]
```
## Негативные сценарии:
- 204 NoContent: строки по документу не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TransferList`.

### `DELETE /Transfers/{transferID}/items/{materialID}`

## Пример запроса:
`DELETE /Transfers/101/items/5001`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
## Негативные сценарии:
- 409 Conflict: документ не найден (`TransferNotFound`), проведён (`TransferPosted`), не в статусе черновика (`TransferNotDraft`), строка уже удалена (`AlreadyDone`), строка не найдена (`TransferItemNotFound`).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TransferDelete`.
