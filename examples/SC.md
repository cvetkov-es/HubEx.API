# SC — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса SC, вынесенные из `endpoints/SC.md`. Сигнатуры и типы — там же и в `schemas/SC.md`.

## ServiceContract

### `GET /ServiceContract`

## Пример запроса:
`GET /ServiceContract?searchText=ТО&companyID=10&assetID=100&offset=0&fetch=50`
            
## Пример успешного ответа (200):
```json
{
  "5": {
    "contractID": 5,
    "companyID": 10,
    "companyName": "ООО Контрагент",
    "name": "Договор ТО-2026",
    "number": "SC-00005",
    "description": "Договор технического обслуживания",
    "conditions": "Условия обслуживания оборудования",
    "dateFrom": "2026-01-01T00:00:00Z",
    "dateTill": "2026-12-31T23:59:59Z"
  }
}
```
Ключ словаря — идентификатор договора (`short`), значение — сведения о договоре.
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
В заголовке ответа присутствует `Content-Range`.
            
## Негативные сценарии:
- 204 NoContent: по заданным фильтрам договоры не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractList`.

### `HEAD /ServiceContract`

## Пример запроса:
`HEAD /ServiceContract?searchText=ТО&companyID=10&assetID=100&offset=0&fetch=50`
            
## Пример успешного ответа (200):
Тело ответа отсутствует. Общее количество возвращается в заголовке `Content-Range`.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractList`.

### `GET /ServiceContract/{contractID}`

## Пример запроса:
`GET /ServiceContract/5`
            
## Пример успешного ответа (200):
```json
{
  "contractID": 5,
  "companyID": 10,
  "companyName": "ООО Контрагент",
  "name": "Договор ТО-2026",
  "number": "SC-00005",
  "description": "Договор технического обслуживания",
  "conditions": "Условия обслуживания оборудования",
  "dateFrom": "2026-01-01T00:00:00Z",
  "dateTill": "2026-12-31T23:59:59Z",
  "remindExpirationDate": true,
  "reminderDate": "2026-12-01T00:00:00Z",
  "isDeleted": false
}
```
## Негативные сценарии:
- 404 NotFound: договор с указанным `contractID` не найден.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractGet`.

### `GET /ServiceContract/{contractID}/assets`

## Пример запроса:
`GET /ServiceContract/1/assets?offset=0&fetch=50`
            
## Пример успешного ответа (200):
```json
{
  "100": { "assetID": 100, "contractID": 1, "tenantID": 1 },
  "200": { "assetID": 200, "contractID": 1, "tenantID": 1 }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
В заголовке ответа присутствует `Content-Range`.
            
## Негативные сценарии:
- 204 NoContent: у договора нет привязанных объектов.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractAssetsList`.

### `GET /ServiceContract/{contractID}/attachment/{attachmentID}`

## Пример запроса:
`GET /ServiceContract/1/attachment/1001?thumbnailSize=128`
            
## Пример успешного ответа (200):
```json
{
  "attachmentID": 1001,
  "fileName": "contract.pdf",
  "description": "Скан договора",
  "isUploaded": true,
  "publicUrl": "https://storage.example.com/public/contract.pdf",
  "thumbnailUrl": null,
  "isProtected": false,
  "size": 204800,
  "created": "2026-03-30T10:15:00Z"
}
```
            
## Негативные сценарии:
- 204 NoContent: вложение с указанным идентификатором не найдено.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractAttachmentGet`.
- 500 Internal Server Error: параметр `thumbnailSize` меньше или равен `0`.

### `GET /ServiceContract/{contractID}/attachments`

## Пример запроса:
`GET /ServiceContract/1/attachments?thumbnailSize=128&offset=0&fetch=50`
            
## Пример успешного ответа (200):
```json
{
  "1001": {
    "fileName": "contract.pdf",
    "description": "Скан договора",
    "isUploaded": true,
    "publicUrl": "https://storage.example.com/public/contract.pdf",
    "thumbnailUrl": null,
    "isProtected": false,
    "size": 204800,
    "created": "2026-03-30T10:15:00Z"
  }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
В заголовке ответа присутствует `Content-Range`.
            
## Негативные сценарии:
- 204 NoContent: у договора нет вложений.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractAttachmentsList`.
- 500 Internal Server Error: параметр `thumbnailSize` меньше или равен `0`.

### `GET /ServiceContract/{contractID}/attachments/{attachmentID}`

## Пример запроса:
`GET /ServiceContract/1/attachments/1001?thumbnailSize=128`
            
## Пример успешного ответа (307):
Тело ответа отсутствует. В заголовке `Location` передаётся временная ссылка для скачивания файла.
            
## Пример успешного ответа (200, `noRedirect=true`):
```json
{
  "fileName": "contract.pdf",
  "url": "https://storage.example.com/download/contract.pdf?sig=...",
  "created": "2026-03-30T10:15:00Z",
  "size": 204800
}
```
            
## Негативные сценарии:
- 204 NoContent: вложение с указанным идентификатором не найдено.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractAttachmentDownload`.
- 500 Internal Server Error: параметр `thumbnailSize` меньше или равен `0`.

### `GET /ServiceContract/{contractID}/attributes`

## Пример запроса:
`GET /ServiceContract/1/attributes?offset=0&fetch=50`
            
## Пример успешного ответа (200):
```json
[
  {
    "attribute": { "id": 10, "name": "Номер договора", "deleted": null },
    "values": ["Д-001"],
    "isPublic": true,
    "attributeType": { "id": 1, "name": "Строка", "code": "String" }
  },
  {
    "attribute": { "id": 20, "name": "Статус", "deleted": null },
    "values": ["Активен"],
    "isPublic": false,
    "attributeType": { "id": 5, "name": "Выбор из списка", "code": "Select" },
    "listOfValues": { "active": "Активен", "closed": "Закрыт" },
    "domain": { "id": 1, "name": "Статусы", "code": "Status" }
  }
]
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
В заголовке ответа присутствует `Content-Range`.
            
## Негативные сценарии:
- 204 NoContent: у договора нет пользовательских полей.
- 400 BadRequest: некорректные параметры запроса (например, неверный диапазон).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractAttributesList`.

### `GET /ServiceContract/{contractID}/contacts`

## Пример запроса:
`GET /ServiceContract/1/contacts?offset=0&fetch=50`
            
## Пример успешного ответа (200):
```json
{
  "10": { "contractID": 1, "contactID": 10 },
  "20": { "contractID": 1, "contactID": 20 }
}
```
            
## Пример успешного ответа (206):
Тело ответа имеет тот же формат, что и для `200`, но содержит частичный диапазон.
В заголовке ответа присутствует `Content-Range`.
            
## Негативные сценарии:
- 204 NoContent: у договора нет привязанных контактов.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractContactList`.
