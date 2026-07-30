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

### `HEAD /Issues`

## Пример запроса:
`HEAD /Issues?searchText=IS-000123`
            
## Пример успешного ответа (200):
Тело ответа отсутствует. Общее количество возвращается в заголовке `Content-Range`.
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `IssueList`.

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

### `HEAD /Receipts`

## Пример запроса:
`HEAD /Receipts?searchText=RC-000123`
            
## Пример успешного ответа (200):
Тело ответа отсутствует. Общее количество возвращается в заголовке `Content-Range`.
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ReceiptList`.

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

### `HEAD /Transfers`

## Пример запроса:
`HEAD /Transfers?searchText=TR-000123`
            
## Пример успешного ответа (200):
Тело ответа отсутствует. Общее количество возвращается в заголовке `Content-Range`.
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TransferList`.

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
