# SC — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса SC, вынесенные из `endpoints/SC.md`. Сигнатуры и типы — там же и в `schemas/SC.md`.

## ContractAttributes

### `POST /ContractAttributes`

## Пример запроса:
`POST /ContractAttributes`
            
```json
[
  {
    "contractID": 1,
    "data": [
      {
        "attributeID": 10,
        "value": ["значение"],
        "isPublic": true
      }
    ]
  }
]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAttributeMerge`.

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

### `POST /ServiceContract`

## Пример запроса:
```json
[
  {
    "companyID": 10,
    "number": "SC-00005",
    "name": "Договор ТО-2026",
    "description": "Договор технического обслуживания",
    "agreementConditions": "Условия обслуживания оборудования",
    "remindExpirationDate": true,
    "reminderDate": "2026-12-01T00:00:00Z",
    "dateFrom": "2026-01-01T00:00:00Z",
    "dateTill": "2026-12-31T23:59:59Z"
  }
]
```
## Пример успешного ответа (201):
```json
[5, 6]
```
В ответе возвращаются идентификаторы только что созданных договоров.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractMerge`.

### `PUT /ServiceContract`

## Пример запроса:
```json
[
  {
    "id": 5,
    "companyID": 10,
    "number": "SC-00005",
    "name": "Договор ТО-2026",
    "description": "Обновленное описание договора",
    "agreementConditions": "Обновленные условия обслуживания",
    "remindExpirationDate": true,
    "reminderDate": "2026-12-01T00:00:00Z",
    "dateFrom": "2026-01-01T00:00:00Z",
    "dateTill": "2026-12-31T23:59:59Z"
  }
]
```
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractMerge`.

### `DELETE /ServiceContract`

## Пример запроса:
```json
[5, 6]
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
      "field": "id"
    }
  }
]
```
## Негативные сценарии:
- 409 Conflict: бизнес-конфликт или ошибка валидации.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractDelete`.

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

### `POST /ServiceContract/{contractID}/assets`

## Пример запроса:
`POST /ServiceContract/1/assets`
            
```json
[
  { "assetID": 100, "includeChildren": true },
  { "assetID": 200, "includeChildren": false }
]
```
            
## Пример успешного ответа (201):
```json
[
  { "tenantID": 1, "contractID": 1, "assetID": 100, "isNew": true },
  { "tenantID": 1, "contractID": 1, "assetID": 200, "isNew": false }
]
```
            
## Негативные сценарии:
- 204 NoContent: объекты не были добавлены (пустой результат операции).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractAssetAdd`.
- 409 Conflict: один или несколько объектов не могут быть добавлены (конфликт данных).

### `DELETE /ServiceContract/{contractID}/assets`

## Пример запроса:
`DELETE /ServiceContract/1/assets`
            
```json
[100, 200, 300]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractAssetDelete`.
- 409 Conflict: один или несколько объектов не могут быть удалены (конфликт данных).

### `PUT /ServiceContract/{contractID}/assets/{assetID}`

## Пример запроса:
`PUT /ServiceContract/1/assets/100?includeChildren=true`
            
## Пример успешного ответа (201):
```json
[
  { "tenantID": 1, "contractID": 1, "assetID": 100, "isNew": true },
  { "tenantID": 1, "contractID": 1, "assetID": 101, "isNew": true }
]
```
            
## Негативные сценарии:
- 204 NoContent: объекты не были добавлены (пустой результат операции).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractAssetAdd`.
- 409 Conflict: объект уже привязан к договору или возник конфликт данных.

### `DELETE /ServiceContract/{contractID}/assets/{assetID}`

## Пример запроса:
`DELETE /ServiceContract/1/assets/100`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractAssetDelete`.
- 409 Conflict: объект не может быть удалён (конфликт данных).

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

### `POST /ServiceContract/{contractID}/attachments`

## Пример запроса:
`POST /ServiceContract/1/attachments`
            
```json
[1001, 1002, 1003]
```
            
## Пример успешного ответа (201):
```json
[
  { "tenantID": 1, "contractID": 1, "attachmentID": 1001 },
  { "tenantID": 1, "contractID": 1, "attachmentID": 1002 }
]
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractAttachmentAdd`.

### `DELETE /ServiceContract/{contractID}/attachments`

## Пример запроса:
`DELETE /ServiceContract/1/attachments`
            
```json
[1001, 1002]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractAttachmentDelete`.

### `POST /ServiceContract/{contractID}/attachments/upload/fromBody`

## Пример запроса:
`POST /ServiceContract/1/attachments/upload/fromBody`
            
```json
{
  "fileName": "contract.pdf",
  "contentType": "application/pdf",
  "file": "JVBERi0xLjQK...",
  "description": "Скан договора",
  "isPublic": false
}
```
            
## Пример успешного ответа (201):
```json
{
  "contractID": 1,
  "attachmentID": 1001,
  "md5Hash": "d41d8cd98f00b204e9800998ecf8427e",
  "fileName": "contract.pdf",
  "isProtected": false
}
```
            
## Негативные сценарии:
- 400 BadRequest: ошибка загрузки или валидации файла. Тело ошибки: массив объектов ErrorModel.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractAttachmentUpload`.

### `POST /ServiceContract/{contractID}/attachments/upload/fromForm`

## Пример запроса:
`POST /ServiceContract/1/attachments/upload/fromForm`
            
Content-Type: `multipart/form-data`
            
## Пример успешного ответа (201):
```json
{
  "contractID": 1,
  "attachmentID": 1001,
  "md5Hash": "d41d8cd98f00b204e9800998ecf8427e",
  "fileName": "contract.pdf",
  "isProtected": false
}
```
            
## Негативные сценарии:
- 400 BadRequest: ошибка загрузки или валидации файла. Тело ошибки: массив объектов ErrorModel.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractAttachmentUpload`.

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

### `POST /ServiceContract/{contractID}/contacts`

## Пример запроса:
`POST /ServiceContract/1/contacts`
            
```json
[10, 20, 30]
```
            
## Пример успешного ответа (201):
```json
[
  { "tenantID": 1, "contractID": 1, "contactID": 10, "isNew": true },
  { "tenantID": 1, "contractID": 1, "contactID": 20, "isNew": false }
]
```
            
## Негативные сценарии:
- 204 NoContent: контакты не были добавлены (пустой результат операции).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractContactAdd`.
- 409 Conflict: один или несколько контактов не могут быть добавлены (конфликт данных).

### `DELETE /ServiceContract/{contractID}/contacts`

## Пример запроса:
`DELETE /ServiceContract/1/contacts`
            
```json
[10, 20, 30]
```
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractContactDelete`.
- 409 Conflict: один или несколько контактов не могут быть удалены (конфликт данных).

### `PUT /ServiceContract/{contractID}/contacts/{contactID}`

## Пример запроса:
`PUT /ServiceContract/1/contacts/10`
            
## Пример успешного ответа (201):
```json
{ "tenantID": 1, "contractID": 1, "contactID": 10, "isNew": true }
```
            
## Негативные сценарии:
- 204 NoContent: контакт не был добавлен (пустой результат операции).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractContactAdd`.
- 409 Conflict: контакт уже привязан к договору или возник конфликт данных.

### `DELETE /ServiceContract/{contractID}/contacts/{contactID}`

## Пример запроса:
`DELETE /ServiceContract/1/contacts/10`
            
## Пример успешного ответа (202):
Тело ответа отсутствует.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractContactDelete`.
- 409 Conflict: контакт не может быть удалён (конфликт данных).

### `POST /ServiceContract/{contractID}/v2/attachments/upload/fromForm`

## Пример запроса:
`POST /ServiceContract/1/v2/attachments/upload/fromForm`
            
Content-Type: `multipart/form-data`
            
## Пример успешного ответа (201):
```json
[
  {
    "contractID": 1,
    "attachmentID": 1001,
    "md5Hash": "d41d8cd98f00b204e9800998ecf8427e",
    "fileName": "contract.pdf",
    "isProtected": false
  },
  {
    "contractID": 1,
    "attachmentID": 1002,
    "md5Hash": "098f6bcd4621d373cade4e832627b4f6",
    "fileName": "appendix.pdf",
    "isProtected": true
  }
]
```
            
## Негативные сценарии:
- 400 BadRequest: ошибка загрузки или валидации файлов. Тело ошибки: массив объектов ErrorModel.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractAttachmentUpload`.

### `DELETE /ServiceContract/{id}`

## Пример запроса:
`DELETE /ServiceContract/5`
            
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
      "field": "id"
    }
  }
]
```
## Негативные сценарии:
- 409 Conflict: бизнес-конфликт или ошибка валидации.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `ContractDelete`.
