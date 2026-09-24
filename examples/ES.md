# ES — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса ES, вынесенные из `endpoints/ES.md`. Сигнатуры и типы — там же и в `schemas/ES.md`.

## AssetAttachments

### `POST /AssetAttachments`

## Пример запроса:
`POST /AssetAttachments`
            
```json
[
  {
    "assetID": 101,
    "data": [501, 502]
  }
]
```
            
## Пример успешного ответа (201):
```json
[
  {
    "assetID": 101,
    "attachmentID": 501
  },
  {
    "assetID": 101,
    "attachmentID": 502
  }
]
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAttachmentAdd`.

### `DELETE /AssetAttachments`

## Пример запроса:
`DELETE /AssetAttachments`
            
```json
[
  {
    "assetID": 101,
    "data": [501, 502]
  }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAttachmentDelete`.

### `POST /AssetAttachments/upload`

## Пример запроса:
`POST /AssetAttachments/upload`
            
Multipart/form-data с полями `assetID`, `fileName`, `content` и др.
            
## Пример успешного ответа (201):
```json
{
  "assetID": 101,
  "attachmentID": 501,
  "fileName": "document.pdf",
  "checkSum": "d41d8cd98f00b204e9800998ecf8427e",
  "isProtected": false
}
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAttachmentUpload`.

### `POST /AssetAttachments/upload/fromBody`

## Пример запроса:
`POST /AssetAttachments/upload/fromBody`
            
```json
{
  "assetID": 101,
  "fileName": "document.pdf",
  "contentType": "application/pdf",
  "content": "JVBERi0xLjQK..."
}
```
            
## Пример успешного ответа (201):
```json
{
  "assetID": 101,
  "attachmentID": 501,
  "fileName": "document.pdf",
  "checkSum": "d41d8cd98f00b204e9800998ecf8427e",
  "isProtected": false
}
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAttachmentUpload`.

### `POST /AssetAttachments/upload/fromForm`

## Пример запроса:
`POST /AssetAttachments/upload/fromForm`
            
Multipart/form-data с полями `assetID`, `fileName`, `content` и др.
            
## Пример успешного ответа (201):
```json
{
  "assetID": 101,
  "attachmentID": 501,
  "fileName": "document.pdf",
  "checkSum": "d41d8cd98f00b204e9800998ecf8427e",
  "isProtected": false
}
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAttachmentUpload`.

## AssetAttributes

### `POST /AssetAttributes`

## Пример запроса:
`POST /AssetAttributes`
            
```json
[
  {
    "assetID": 101,
    "data": [
      {
        "attributeID": 2,
        "value": "Значение атрибута",
        "isPublic": true,
        "sortOrder": 1
      }
    ]
  }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат запроса или отсутствуют обязательные поля.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAttributeMerge`.

### `DELETE /AssetAttributes`

## Пример запроса:
`DELETE /AssetAttributes`
            
```json
[
  {
    "assetID": 101,
    "data": [
      {
        "attributeID": 2
      }
    ]
  }
]
```
            
## Пример успешного ответа (202):
```json
[
  {
    "tenantID": 105,
    "assetID": 101,
    "attributeID": 2,
    "error": "InvalidDataFormat@AlreadyActive"
  }
]
```
Пустой массив — если все строки запроса обработаны успешно.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат запроса или отсутствуют обязательные поля.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAttributeDelete`.
            
Удаляются только явно переданные пары AssetID+AttributeID.
Непереданные атрибуты объекта не затрагиваются.

### `POST /AssetAttributes/v2`

## Пример запроса:
`POST /AssetAttributes/v2`
            
```json
[
  {
    "assetID": 101,
    "data": [
      {
        "attributeID": 2,
        "value": "Новый атрибут",
        "isPublic": true,
        "sortOrder": 1
      }
    ]
  }
]
```
            
## Пример успешного ответа (202):
```json
[
  {
    "tenantID": 105,
    "assetID": 101,
    "attributeID": 2,
    "error": "InvalidDataFormat@AlreadyActive"
  }
]
```
Пустой массив — если все строки запроса обработаны успешно.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат запроса или отсутствуют обязательные поля.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAttributeAdd`.
            
Добавляются только явно переданные атрибуты.
Пустое значение не создает запись значения атрибута.
При отсутствии `SortOrder` значение по умолчанию обрабатывается на стороне backend.

### `PUT /AssetAttributes/v2`

## Пример запроса:
`PUT /AssetAttributes/v2`
            
```json
[
  {
    "assetID": 101,
    "data": [
      {
        "attributeID": 2,
        "value": "Обновленное значение",
        "isPublic": false
      }
    ]
  }
]
```
            
## Пример успешного ответа (202):
```json
[
  {
    "tenantID": 105,
    "assetID": 101,
    "attributeID": 2,
    "error": "InvalidDataFormat@AlreadyActive"
  }
]
```
Пустой массив — если все строки запроса обработаны успешно.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат запроса или отсутствуют обязательные поля.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAttributeUpdate`.
            
Обновляются только явно переданные атрибуты.
Если для атрибута передать пустое значение, его значение будет удалено.
При отсутствии `SortOrder` значение по умолчанию обрабатывается на стороне backend.

## AssetClasses

### `GET /AssetClasses`

## Пример запроса:
`GET /AssetClasses`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "id": 1,
    "name": "Оборудование",
    "isDefault": true,
    "erpID": "EQ-001"
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: классы не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetClassesList`.
- 206 PartialContent: при использовании заголовка Range.

### `POST /AssetClasses`

## Пример запроса:
`POST /AssetClasses`
            
```json
[
  {
    "name": "Оборудование",
    "isDefault": false,
    "erpID": "EQ-001"
  }
]
```
            
## Пример успешного ответа (201):
```json
[
  {
    "id": 5
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: классы не были созданы.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetClassAdd`.

### `PUT /AssetClasses`

## Пример запроса:
`PUT /AssetClasses`
            
```json
[
  {
    "id": 1,
    "name": "Оборудование (обновлено)",
    "isDefault": true,
    "erpID": "EQ-001"
  }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetClassUpdate`.

### `DELETE /AssetClasses`

## Пример запроса:
`DELETE /AssetClasses`
            
```json
[1, 2]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetClassDelete`.

### `GET /AssetClasses/{id}`

## Пример запроса:
`GET /AssetClasses/1`
            
## Пример успешного ответа (200):
```json
{
  "id": 1,
  "name": "Оборудование",
  "isDefault": true,
  "deleted": null,
  "erpID": "EQ-001"
}
```
            
## Негативные сценарии:
- 204 NoContent: класс не найден.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetClassGet`.

### `DELETE /AssetClasses/{id}`

## Пример запроса:
`DELETE /AssetClasses/1`
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetClassDelete`.
- 409 Conflict: класс используется и не может быть удалён.

## AssetDistricts

### `POST /AssetDistricts`

## Пример запроса:
`POST /AssetDistricts`
            
```json
{
  "assetID": 101,
  "data": [
    { "id": 5 },
    { "id": 7 }
  ]
}
```
            
## Пример успешного ответа (201):
Пустое тело ответа.
            
## Негативные сценарии:
- 400 BadRequest: тело запроса отсутствует или некорректно.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetDistrictsAdd`.
- 409 Conflict: участок уже привязан или объект недоступен.

### `DELETE /AssetDistricts`

## Пример запроса:
`DELETE /AssetDistricts`
            
```json
{
  "assetID": 101,
  "data": [5, 7]
}
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 400 BadRequest: тело запроса отсутствует или некорректно.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetDistrictsDelete`.
- 409 Conflict: связь не найдена или объект недоступен.

## AssetFilter

### `GET /AssetFilter`

## Пример запроса:
`GET /AssetFilter?selectedOnly=true`
            
## Пример успешного ответа (200):
```json
[
  {
    "filterID": 1,
    "name": "Мои объекты",
    "sortOrder": 1,
    "isSelected": true
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: фильтры не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetsList`.

### `PUT /AssetFilter`

## Пример запроса:
`PUT /AssetFilter`
            
```json
[
  { "filterID": 1, "sortOrder": 1 },
  { "filterID": 3, "sortOrder": 2 }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetsList`.

## AssetListQueries

### `GET /AssetListQueries`

## Пример запроса:
`GET /AssetListQueries`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "name": "Мои объекты",
    "searchText": "насос",
    "queryString": "?searchText=насос"
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: сохранённые запросы не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetListQueryList`.
- 206 PartialContent: при использовании заголовка Range.

### `POST /AssetListQueries`

## Пример запроса:
`POST /AssetListQueries`
            
```json
[
  {
    "name": "Мои объекты",
    "queryString": "?companyID=10&searchText=насос"
  }
]
```
            
## Пример успешного ответа (201):
```json
[15]
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetListQueryAdd`.

### `PUT /AssetListQueries`

## Пример запроса:
`PUT /AssetListQueries`
            
```json
[
  {
    "id": 15,
    "name": "Мои объекты (обновлено)",
    "queryString": "?companyID=10"
  }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetListQueryUpdate`.

### `DELETE /AssetListQueries`

## Пример запроса:
`DELETE /AssetListQueries`
            
```json
[15, 16]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetListQueryDelete`.

### `DELETE /AssetListQueries/remove`

## Пример запроса:
`DELETE /AssetListQueries/remove`
            
```json
[15, 16]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetListQueryRemove`.

### `GET /AssetListQueries/{id}`

## Пример запроса:
`GET /AssetListQueries/1`
            
## Пример успешного ответа (200):
```json
{
  "name": "Мои объекты",
  "searchText": "насос",
  "filterList": {
    "companies": [{ "id": "10", "name": "ООО Пример" }]
  },
  "queryString": "?companyID=10&searchText=насос"
}
```
            
## Негативные сценарии:
- 204 NoContent: запрос не найден.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetListQueryGet`.

### `DELETE /AssetListQueries/{id}`

## Пример запроса:
`DELETE /AssetListQueries/15`
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetListQueryDelete`.

### `DELETE /AssetListQueries/{id}/remove`

## Пример запроса:
`DELETE /AssetListQueries/15/remove`
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetListQueryRemove`.

## AssetLocations

### `GET /AssetLocations`

## Пример запроса:
`GET /AssetLocations?assetID=101`
            
## Пример успешного ответа (200):
```json
{
  "42": {
    "assetID": 101,
    "location": {
      "id": 42,
      "address": "г. Москва, ул. Примерная, д. 1",
      "coordinate": "55.7558:37.6173",
      "description": "Офис",
      "dateFrom": "2024-01-01T00:00:00Z",
      "dateTill": "9999-12-31T23:59:59Z",
      "timezoneID": 1,
      "timezoneUtcOffsetMinutes": 180,
      "countryID": 1,
      "countryTwoSymbolCode": "RU"
    }
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: локации не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetLocationsList`.
- 409 Conflict: объект недоступен.
- 206 PartialContent: при использовании заголовка Range.

### `POST /AssetLocations`

## Пример запроса:
`POST /AssetLocations`
            
```json
{
  "assetID": 101,
  "locationID": 42,
  "dateFrom": "2024-01-01T00:00:00Z",
  "dateTill": "9999-12-31T23:59:59Z"
}
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetLocationAdd`.

### `PUT /AssetLocations`

## Пример запроса:
`PUT /AssetLocations`
            
```json
{
  "assetID": 101,
  "locationID": 42,
  "dateFrom": "2024-06-01T00:00:00Z",
  "dateTill": "9999-12-31T23:59:59Z"
}
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetLocationUpdate`.

### `DELETE /AssetLocations`

## Пример запроса:
`DELETE /AssetLocations`
            
```json
{
  "assetID": 101
}
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetLocationRemove`.

## AssetSchemas

### `GET /AssetSchemas/ascList/{assetID}`

## Пример запроса:
`GET /AssetSchemas/ascList/101`
            
## Пример успешного ответа (200):
```json
{
  "0": { "schemaID": 3, "assetID": 50, "name": "Схема здания" },
  "1": { "schemaID": 5, "assetID": 101, "name": "Схема 1 этажа" }
}
```
Ключ словаря — порядковый индекс от корня дерева (0 — верхний уровень).
            
## Негативные сценарии:
- 204 NoContent: план-схемы не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetSchemaGet`.

### `GET /AssetSchemas/asset/{assetID}`

## Пример запроса:
`GET /AssetSchemas/asset/101`
            
## Пример успешного ответа (200):
```json
{
  "schemaID": 5,
  "assetID": 101,
  "imageID": 12,
  "name": "Схема 1 этажа",
  "assets": [
    { "id": 1, "assetID": 101, "x": 120, "y": 340 }
  ]
}
```
            
## Негативные сценарии:
- 204 NoContent: план-схема для объекта не найдена.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetSchemaGet`.

### `POST /AssetSchemas/asset/{assetId}`

## Пример запроса:
`POST /AssetSchemas/asset/101`
            
```json
{
  "name": "Схема 1 этажа",
  "assets": [
    { "assetID": 101, "x": 120, "y": 340 }
  ]
}
```
            
## Пример успешного ответа (201):
```json
{ "id": 5, "name": "Схема 1 этажа" }
```
            
## Негативные сценарии:
- 400 BadRequest: тело запроса отсутствует или некорректно.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetSchemaAdd`.
- 409 Conflict: план-схема не может быть создана.

### `PUT /AssetSchemas/asset/{assetId}`

## Пример запроса:
`PUT /AssetSchemas/asset/101`
            
```json
{
  "schemaID": 5,
  "name": "Обновлённая схема",
  "assets": [
    { "assetID": 101, "x": 150, "y": 400 }
  ]
}
```
            
## Пример успешного ответа (202):
```json
{ "id": 5, "name": "Обновлённая схема" }
```
            
## Негативные сценарии:
- 400 BadRequest: тело запроса отсутствует или не указан schemaID.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetSchemaUpdate`.
- 409 Conflict: план-схема не может быть обновлена.

### `GET /AssetSchemas/list`

## Пример запроса:
`GET /AssetSchemas/list`
            
## Пример успешного ответа (200):
```json
{
  "0": { "schemaID": 3, "assetID": 50, "name": "Схема здания" },
  "1": { "schemaID": 5, "assetID": 101, "name": "Схема 1 этажа" }
}
```
            
## Негативные сценарии:
- 204 NoContent: план-схемы не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetSchemaGet`.

### `GET /AssetSchemas/{schemaId}`

## Пример запроса:
`GET /AssetSchemas/5`
            
## Пример успешного ответа (200):
```json
{
  "schemaID": 5,
  "assetID": 101,
  "imageID": 12,
  "name": "Схема 1 этажа",
  "assets": [
    { "id": 1, "assetID": 101, "x": 120, "y": 340 }
  ]
}
```
            
## Негативные сценарии:
- 404 NotFound: план-схема не найдена.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetSchemaGet`.

### `DELETE /AssetSchemas/{schemaId}`

## Пример запроса:
`DELETE /AssetSchemas/5`
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetSchemaDelete`.
- 409 Conflict: план-схема не может быть удалена.

### `POST /AssetSchemas/{schemaId}/bind`

## Пример запроса:
`POST /AssetSchemas/5/bind`
            
```json
[101, 102, 103]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 400 BadRequest: передан пустой массив объектов.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetUpdate`.
- 409 Conflict: привязка не может быть выполнена.

### `GET /AssetSchemas/{schemaId}/image`

## Пример запроса:
`GET /AssetSchemas/5/image?thumbnailSize=128`
            
## Пример успешного ответа (200):
```json
{
  "attachmentID": 42,
  "fileName": "floor-plan.png",
  "description": "Схема 1 этажа",
  "isUploaded": true,
  "publicUrl": "https://example.com/files/floor-plan.png",
  "thumbnailUrl": "https://example.com/files/floor-plan_128.png",
  "isProtected": false,
  "size": 245760,
  "created": "2026-01-15T10:30:00Z",
  "originalSize": { "width": 1920, "height": 1080 }
}
```
            
## Негативные сценарии:
- 404 NotFound: у план-схемы нет привязанного изображения.
- 400 BadRequest: некорректное значение thumbnailSize.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetSchemaImageGet`.

### `DELETE /AssetSchemas/{schemaId}/image`

## Пример запроса:
`DELETE /AssetSchemas/5/image`
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 404 NotFound: у план-схемы нет привязанного изображения.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetSchemaImageDelete`.
- 409 Conflict: изображение не может быть удалено.

### `POST /AssetSchemas/{schemaId}/image/attach/{attachmentId}`

## Пример запроса:
`POST /AssetSchemas/5/image/attach/42`
            
```json
{ "width": 1920, "height": 1080 }
```
            
## Пример успешного ответа (201):
```json
{ "schemaID": 5, "assetID": 101, "imageID": 12, "name": "Схема 1 этажа" }
```
            
## Негативные сценарии:
- 404 NotFound: план-схема не найдена.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetSchemaImageBind`.
- 409 Conflict: вложение уже привязано к схеме.

### `GET /AssetSchemas/{schemaId}/image/download`

## Пример запроса:
`GET /AssetSchemas/5/image/download?thumbnailSize=256`
            
## Пример успешного ответа (303):
Redirect на временную ссылку для скачивания файла.
            
## Негативные сценарии:
- 404 NotFound: у план-схемы нет привязанного изображения.
- 400 BadRequest: некорректное значение thumbnailSize.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetSchemaImageDownload`.

### `POST /AssetSchemas/{schemaId}/image/upload`

## Пример запроса:
`POST /AssetSchemas/5/image/upload`
            
Content-Type: multipart/form-data с полем файла.
            
## Пример успешного ответа (201):
```json
{
  "attachmentID": 42,
  "md5Hash": "d41d8cd98f00b204e9800998ecf8427e",
  "fileName": "floor-plan.png",
  "isProtected": false
}
```
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат файла или content-type.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetSchemaImageUpload`.
- 409 Conflict: изображение уже привязано к схеме.

### `GET /AssetSchemas/{schemaId}/points`

## Пример запроса:
`GET /AssetSchemas/5/points?taskID=100&assetID=101`
            
## Пример успешного ответа (200):
```json
[
  {
    "pointID": 1,
    "taskID": 100,
    "x": 120,
    "y": 340
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: точки-задания не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetSchemaPointsGet`.

### `POST /AssetSchemas/{schemaId}/points`

## Пример запроса:
`POST /AssetSchemas/5/points`
            
```json
[
  {
    "pointID": null,
    "taskID": 100,
    "x": 120,
    "y": 340
  },
  {
    "pointID": 2,
    "taskID": 101,
    "x": 200,
    "y": 450
  }
]
```
            
## Пример успешного ответа (200):
```json
[
  {
    "pointID": 1,
    "taskID": 100,
    "x": 120,
    "y": 340
  }
]
```
            
## Негативные сценарии:
- 400 BadRequest: передан пустой массив точек.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetSchemaPointsUpdate`.
- 409 Conflict: точки не могут быть сохранены.

### `DELETE /AssetSchemas/{schemaId}/points`

## Пример запроса:
`DELETE /AssetSchemas/5/points`
            
```json
[1, 2, 3]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetSchemaPointsDelete`.
- 409 Conflict: точки не могут быть удалены.

### `PUT /AssetSchemas/{schemaId}/unbind`

## Пример запроса:
`PUT /AssetSchemas/5/unbind`
            
```json
[101, 102]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 400 BadRequest: передан пустой массив объектов.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetUpdate`.
- 409 Conflict: отвязка не может быть выполнена.

## AssetSearchSettings

### `GET /AssetSearchSettings`

## Пример запроса:
`GET /AssetSearchSettings`
            
## Пример успешного ответа (200), пользователь ещё не сохранял выбор:
```json
[
  {
    "searchFieldID": 1,
    "entityCode": "Asset",
    "fieldCode": "Name",
    "descriptionRu": "Название",
    "isSelected": true,
    "isSelectedByUser": false
  },
  {
    "searchFieldID": 2,
    "entityCode": "Asset",
    "fieldCode": "SerialNumber",
    "descriptionRu": "Серийный номер",
    "isSelected": true,
    "isSelectedByUser": false
  }
]
```
## Пример ответа после сохранения выбора (только SerialNumber):
```json
[
  {
    "searchFieldID": 1,
    "entityCode": "Asset",
    "fieldCode": "Name",
    "descriptionRu": "Название",
    "isSelected": false,
    "isSelectedByUser": false
  },
  {
    "searchFieldID": 2,
    "entityCode": "Asset",
    "fieldCode": "SerialNumber",
    "descriptionRu": "Серийный номер",
    "isSelected": true,
    "isSelectedByUser": true
  }
]
```
`fieldCode` — технический код поля; `descriptionRu` — подпись для UI.
`isSelected` — итоговое состояние чекбокса (при отсутствии сохранённых настроек все доступные поля `true`).
`isSelectedByUser` — поле сохранено в `TenantMemberSearchField`; при первом сохранении у всех строк `false` — отправлять `POST /tenantMember` с отмеченными id.
## Негативные сценарии:
- 204 NoContent: для пользователя нет доступных полей поиска.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetSearchFieldListForTenantMember`.

### `POST /AssetSearchSettings/tenant`

## Пример запроса:
`POST /AssetSearchSettings/tenant`
            
```json
[1,2,3]
```
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTenantSearchSettingsAdd`.

### `DELETE /AssetSearchSettings/tenant`

## Пример запроса:
`DELETE /AssetSearchSettings/tenant`
            
```json
[2,3]
```
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTenantSearchSettingsDelete`.

### `POST /AssetSearchSettings/tenantMember`

## Пример запроса:
`POST /AssetSearchSettings/tenantMember`
            
```json
[1,2]
```
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTenantMemberSearchSettingsAdd`.
- 409 Conflict: поле поиска скрыто для компании (`SearchFieldNotAllowedForTenant`).

### `DELETE /AssetSearchSettings/tenantMember`

## Пример запроса:
`DELETE /AssetSearchSettings/tenantMember`
            
```json
[2]
```
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTenantMemberSearchSettingsDelete`.
- 409 Conflict: поле поиска скрыто для компании (`SearchFieldNotAllowedForTenant`).

## AssetSkills

### `POST /AssetSkills`

## Пример запроса:
`POST /AssetSkills`
            
```json
[
  {
    "assetID": 101,
    "data": [1, 2]
  }
]
```
            
## Пример успешного ответа (201):
```json
[
  {
    "assetID": 101,
    "skillID": 1
  },
  {
    "assetID": 101,
    "skillID": 2
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: навыки не добавлены (пустой результат).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetSkillAdd`.
- 409 Conflict: навык уже привязан или объект недоступен.

### `DELETE /AssetSkills`

## Пример запроса:
`DELETE /AssetSkills`
            
```json
[
  {
    "assetID": 101,
    "data": [1, 2]
  }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetSkillDelete`.
- 409 Conflict: связь не найдена или объект недоступен.

## AssetTags

### `POST /AssetTags`

## Пример запроса:
`POST /AssetTags`
            
```json
[
  {
    "assetID": 101,
    "tag": "Сервисное обслуживание"
  }
]
```
            
## Пример успешного ответа (201):
```json
[
  {
    "assetID": 101,
    "tag": "Сервисное обслуживание"
  }
]
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTagAdd`.
- 409 Conflict: тег уже существует или объект недоступен.

### `DELETE /AssetTags`

## Пример запроса:
`DELETE /AssetTags`
            
```json
[
  {
    "assetID": 101,
    "tag": "Сервисное обслуживание"
  }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTagRemove`.

## AssetTemplateAttachments

### `POST /AssetTemplateAttachments`

## Пример запроса:
`POST /AssetTemplateAttachments`
            
```json
[
  {
    "assetTemplateID": 1,
    "data": [501, 502]
  }
]
```
            
## Пример успешного ответа (201):
```json
[
  {
    "assetTemplateID": 1,
    "attachmentID": 501
  },
  {
    "assetTemplateID": 1,
    "attachmentID": 502
  }
]
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateAttachmentAdd`.

### `DELETE /AssetTemplateAttachments`

## Пример запроса:
`DELETE /AssetTemplateAttachments`
            
```json
[
  {
    "assetTemplateID": 1,
    "data": [501, 502]
  }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateAttachmentDelete`.

### `POST /AssetTemplateAttachments/upload`

## Пример запроса:
`POST /AssetTemplateAttachments/upload`
            
Multipart/form-data с полями `assetTemplateID`, `fileName`, `content` и др.
            
## Пример успешного ответа (201):
```json
{
  "assetTemplateID": 1,
  "attachmentID": 501,
  "fileName": "document.pdf",
  "checkSum": "d41d8cd98f00b204e9800998ecf8427e",
  "isProtected": false
}
```
            
## Негативные сценарии:
- 400 BadRequest: некорректные данные файла.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateAttachmentUpload`.

### `POST /AssetTemplateAttachments/upload/fromBody`

## Пример запроса:
`POST /AssetTemplateAttachments/upload/fromBody`
            
```json
{
  "assetTemplateID": 1,
  "fileName": "document.pdf",
  "contentType": "application/pdf",
  "contentBase64": "..."
}
```
            
## Пример успешного ответа (201):
```json
{
  "assetTemplateID": 1,
  "attachmentID": 501,
  "fileName": "document.pdf",
  "checkSum": "d41d8cd98f00b204e9800998ecf8427e",
  "isProtected": false
}
```
            
## Негативные сценарии:
- 400 BadRequest: некорректные данные файла.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateAttachmentUpload`.

### `POST /AssetTemplateAttachments/upload/fromForm`

## Пример запроса:
`POST /AssetTemplateAttachments/upload/fromForm`
            
Multipart/form-data с полями `assetTemplateID`, `fileName`, `content` и др.
            
## Пример успешного ответа (201):
```json
{
  "assetTemplateID": 1,
  "attachmentID": 501,
  "fileName": "document.pdf",
  "checkSum": "d41d8cd98f00b204e9800998ecf8427e",
  "isProtected": false
}
```
            
## Негативные сценарии:
- 400 BadRequest: некорректные данные файла.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateAttachmentUpload`.

## AssetTemplateAttributes

### `POST /AssetTemplateAttributes`

## Пример запроса:
`POST /AssetTemplateAttributes`
            
```json
[
  {
    "assetTemplateID": 1,
    "data": [
      {
        "attributeID": 2,
        "value": "Значение атрибута",
        "isPublic": true,
        "sortOrder": 1
      }
    ]
  }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateAttributeMerge`.

## AssetTemplateDistricts

### `POST /AssetTemplateDistricts`

## Пример запроса:
`POST /AssetTemplateDistricts`
            
```json
[
  {
    "assetTemplateID": 1,
    "data": [5, 6]
  }
]
```
            
## Пример успешного ответа (201):
```json
[
  {
    "assetTemplateID": 1,
    "districtID": 5
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: участки не добавлены (пустой результат).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateDistrictAdd`.
- 409 Conflict: участок уже привязан или шаблон недоступен.

### `DELETE /AssetTemplateDistricts`

## Пример запроса:
`DELETE /AssetTemplateDistricts`
            
```json
[
  {
    "assetTemplateID": 1,
    "data": [5, 6]
  }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateDistrictDelete`.
- 409 Conflict: связь не найдена или шаблон недоступен.

### `DELETE /AssetTemplateDistricts/{id}`

## Пример запроса:
`DELETE /AssetTemplateDistricts/1`
            
```json
[5, 6]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateDistrictDelete`.
- 409 Conflict: связь не найдена или шаблон недоступен.

## AssetTemplateSkills

### `POST /AssetTemplateSkills`

## Пример запроса:
`POST /AssetTemplateSkills`
            
```json
[
  {
    "assetTemplateID": 1,
    "data": [
      { "skillID": 1, "isOptional": false },
      { "skillID": 2, "isOptional": true }
    ]
  }
]
```
            
## Пример успешного ответа (201):
```json
[
  {
    "assetTemplateID": 1,
    "skillID": 1
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: навыки не добавлены (пустой результат).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateSkillAdd`.
- 409 Conflict: навык уже привязан или шаблон недоступен.

### `DELETE /AssetTemplateSkills`

## Пример запроса:
`DELETE /AssetTemplateSkills`
            
```json
[
  {
    "assetTemplateID": 1,
    "data": [1, 2]
  }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateSkillDelete`.
- 409 Conflict: связь не найдена или шаблон недоступен.

### `DELETE /AssetTemplateSkills/{id}`

## Пример запроса:
`DELETE /AssetTemplateSkills/1`
            
```json
[1, 2]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateSkillDelete`.
- 409 Conflict: связь не найдена или шаблон недоступен.

## AssetTemplateWorkTypes

### `POST /AssetTemplateWorkTypes`

## Пример запроса:
`POST /AssetTemplateWorkTypes`
            
```json
[
  {
    "assetTemplateID": 1,
    "data": [1, 2]
  }
]
```
            
## Пример успешного ответа (201):
```json
[
  {
    "assetTemplateID": 1,
    "workTypeID": 1
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: виды работ не добавлены (пустой результат).
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateWorkTypeAdd`.
- 409 Conflict: вид работ уже привязан или шаблон недоступен.

### `DELETE /AssetTemplateWorkTypes`

## Пример запроса:
`DELETE /AssetTemplateWorkTypes`
            
```json
[
  {
    "assetTemplateID": 1,
    "data": [1, 2]
  }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateWorkTypeDelete`.
- 409 Conflict: связь не найдена или шаблон недоступен.

### `DELETE /AssetTemplateWorkTypes/{id}`

## Пример запроса:
`DELETE /AssetTemplateWorkTypes/1`
            
```json
[1, 2]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateWorkTypeDelete`.
- 409 Conflict: связь не найдена или шаблон недоступен.

## AssetTemplates

### `GET /AssetTemplates`

## Пример запроса:
`GET /AssetTemplates?searchText=насос&assetClassID=1&assetTypeID=2`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "name": "Шаблон насосного оборудования",
    "description": "Стандартный шаблон",
    "assetName": "Насос",
    "hostAsset": { "id": 50, "name": "Здание А" },
    "company": { "id": 10, "name": "ООО Ремонт" },
    "assetType": { "id": 2, "name": "Оборудование" },
    "assetClass": { "id": 1, "name": "Насосы" }
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: шаблоны не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateList`.
- 206 PartialContent: при использовании заголовка Range.

### `POST /AssetTemplates`

## Пример запроса:
`POST /AssetTemplates`
            
```json
[
  {
    "name": "Шаблон насосного оборудования",
    "description": "Стандартный шаблон",
    "assetName": "Насос",
    "companyID": 10,
    "assetTypeID": 2,
    "assetClassID": 1,
    "hostAssetID": 50,
    "locationID": 20,
    "responsiblePerson": 5,
    "erpID": "ERP-001",
    "isMobileAsset": false,
    "isInheritParentDistricts": true
  }
]
```
            
## Пример успешного ответа (201):
```json
[1]
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateAdd`.
- 409 Conflict: конфликт данных при создании шаблона.

### `PUT /AssetTemplates`

## Пример запроса:
`PUT /AssetTemplates`
            
```json
[
  {
    "id": 1,
    "name": "Обновлённый шаблон",
    "description": "Новое описание",
    "assetName": "Насос",
    "companyID": 10,
    "assetTypeID": 2,
    "notes": "Обновлённые заметки"
  }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateUpdate`.
- 409 Conflict: конфликт данных при обновлении шаблона.

### `DELETE /AssetTemplates`

## Пример запроса:
`DELETE /AssetTemplates`
            
```json
[1, 2, 3]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateDelete`.
- 409 Conflict: шаблон используется или недоступен для удаления.

### `DELETE /AssetTemplates/avatar`

## Пример запроса:
`DELETE /AssetTemplates/avatar`
            
```json
[1, 2, 3]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateAvatarDelete`.

### `GET /AssetTemplates/{assetTemplateID}/attachments`

## Пример запроса:
`GET /AssetTemplates/1/attachments?thumbnailSize=128`
            
## Пример успешного ответа (200):
```json
{
  "501": {
    "fileName": "document.pdf",
    "description": "Паспорт оборудования",
    "isUploaded": true,
    "isProtected": false,
    "size": 102400,
    "created": "2024-01-15T10:00:00Z",
    "publicUrl": "https://storage.example.com/file.pdf",
    "thumbnailUrl": null
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: вложения не найдены.
- 400 BadRequest: некорректный thumbnailSize.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateAttachmentList`.
- 206 PartialContent: при использовании заголовка Range.

### `GET /AssetTemplates/{assetTemplateID}/attachments/{attachmentID}`

## Пример запроса:
`GET /AssetTemplates/1/attachments/501?noRedirect=false`
            
## Пример успешного ответа (307):
Редирект на временную ссылку для скачивания файла.
            
## Негативные сценарии:
- 400 BadRequest: некорректный thumbnailSize.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `TaskAttachmentDownload`.
- 404 NotFound: вложение не найдено.

### `GET /AssetTemplates/{assetTemplateID}/attributes`

## Пример запроса:
`GET /AssetTemplates/1/attributes`
            
## Пример успешного ответа (200):
```json
[
  {
    "attribute": { "id": 2, "name": "Мощность", "deleted": null },
    "value": "100",
    "isPublic": true,
    "sortOrder": 1,
    "attributeType": { "id": 1, "name": "Число", "code": "Number" },
    "measurementUnit": {
      "id": 3,
      "name": "Киловатт",
      "abbreviation": "кВт",
      "designation": "kW"
    },
    "listOfValues": null,
    "domain": null
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: атрибуты не найдены.
- 400 BadRequest: некорректный идентификатор шаблона.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateAttributeList`.
- 206 PartialContent: при использовании заголовка Range.

### `GET /AssetTemplates/{assetTemplateID}/districts`

## Пример запроса:
`GET /AssetTemplates/1/districts`
            
## Пример успешного ответа (200):
```json
{
  "5": {
    "parentID": null,
    "name": "Центральный район"
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: участки не найдены.
- 400 BadRequest: некорректный идентификатор шаблона.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateDistrictList`.
- 206 PartialContent: при использовании заголовка Range.

### `GET /AssetTemplates/{assetTemplateID}/skills`

## Пример запроса:
`GET /AssetTemplates/1/skills`
            
## Пример успешного ответа (200):
```json
[
  {
    "skill": { "id": 1, "name": "Электромонтаж", "description": "Работы по электрике" },
    "skillClass": { "id": 2, "name": "Электрика" },
    "isOptional": false
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: навыки не найдены.
- 400 BadRequest: некорректный идентификатор шаблона.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateSkillList`.
- 206 PartialContent: при использовании заголовка Range.

### `GET /AssetTemplates/{assetTemplateID}/workTypes`

## Пример запроса:
`GET /AssetTemplates/1/workTypes`
            
## Пример успешного ответа (200):
```json
[
  {
    "workType": { "id": 1, "name": "Техническое обслуживание", "description": "Плановое ТО" },
    "workClass": { "id": 2, "name": "Сервис" },
    "isDefault": true
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: виды работ не найдены.
- 400 BadRequest: некорректный идентификатор шаблона.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateWorkTypeList`.
- 206 PartialContent: при использовании заголовка Range.

### `GET /AssetTemplates/{id}`

## Пример запроса:
`GET /AssetTemplates/1`
            
## Пример успешного ответа (200):
```json
{
  "name": "Шаблон насосного оборудования",
  "description": "Стандартный шаблон",
  "hostAsset": { "id": 50, "name": "Здание А" },
  "assetName": "Насос",
  "company": { "id": 10, "name": "ООО Ремонт" },
  "assetType": { "id": 2, "name": "Оборудование", "isHostable": true },
  "assetClass": { "id": 1, "name": "Насосы" },
  "responsiblePerson": { "id": 5, "firstName": "Иван", "lastName": "Иванов", "middleName": null },
  "erpID": "ERP-001",
  "scheduleRuleID": 3,
  "checkListID": 7,
  "warrantyTill": "2026-12-31T00:00:00Z",
  "notes": "Заметки",
  "isMobileAsset": false,
  "isInheritParentDistricts": true,
  "isSkipForEscalation": false,
  "isStopEscalation": false,
  "location": {
    "id": 20,
    "address": "г. Москва, ул. Примерная, 1",
    "coordinate": "55.7558:37.6173",
    "description": "Офис",
    "deleted": null
  },
  "parentAsset": null,
  "avatarUrl": "https://storage.example.com/avatar.jpg"
}
```
            
## Негативные сценарии:
- 204 NoContent: шаблон не найден.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateGet`.

### `DELETE /AssetTemplates/{id}`

## Пример запроса:
`DELETE /AssetTemplates/1`
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateDelete`.
- 409 Conflict: шаблон используется или недоступен для удаления.

### `DELETE /AssetTemplates/{id}/avatar`

## Пример запроса:
`DELETE /AssetTemplates/1/avatar`
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateAvatarDelete`.

### `PUT /AssetTemplates/{id}/avatar/upload/fromBody`

## Пример запроса:
`PUT /AssetTemplates/1/avatar/upload/fromBody`
            
```json
{
  "fileName": "avatar.jpg",
  "contentType": "image/jpeg",
  "contentBase64": "..."
}
```
            
## Пример успешного ответа (200):
```json
{
  "fileName": "avatar.jpg",
  "publicUrl": "https://storage.example.com/avatar.jpg"
}
```
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат изображения или размер менее 128×128.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateAvatarUpload`.

### `PUT /AssetTemplates/{id}/avatar/upload/fromForm`

## Пример запроса:
`PUT /AssetTemplates/1/avatar/upload/fromForm`
            
Multipart/form-data с полем изображения.
            
## Пример успешного ответа (200):
```json
{
  "fileName": "avatar.jpg",
  "publicUrl": "https://storage.example.com/avatar.jpg"
}
```
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат изображения или размер менее 128×128.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTemplateAvatarUpload`.

## AssetTypes

### `GET /AssetTypes`

## Пример запроса:
`GET /AssetTypes`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "name": "Здание",
    "isHostable": true,
    "isDefault": false
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: типы объектов не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTypesList`.
- 206 PartialContent: при использовании заголовка Range.

### `POST /AssetTypes`

## Пример запроса:
`POST /AssetTypes?relatedToAnyWorkType=false`
            
```json
[
  {
    "name": "Здание",
    "isHostable": true,
    "isDefault": false
  }
]
```
            
## Пример успешного ответа (201):
```json
[
  {
    "id": 5
  }
]
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTypeAdd`.
- 409 Conflict: тип с таким именем уже существует.

### `PUT /AssetTypes`

## Пример запроса:
`PUT /AssetTypes?relatedToAnyWorkType=false`
            
```json
[
  {
    "id": 1,
    "name": "Здание (обновлено)",
    "isHostable": true,
    "isDefault": false
  }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTypeUpdate`.
- 409 Conflict: конфликт при обновлении типа.

### `DELETE /AssetTypes`

## Пример запроса:
`DELETE /AssetTypes`
            
```json
[1, 2]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTypeDelete`.
- 409 Conflict: тип используется и не может быть удалён.

### `GET /AssetTypes/{id}`

## Пример запроса:
`GET /AssetTypes/1`
            
## Пример успешного ответа (200):
```json
{
  "name": "Здание",
  "isHostable": true,
  "isDefault": false
}
```
            
## Негативные сценарии:
- 204 NoContent: тип объекта не найден.
- 400 BadRequest: некорректный идентификатор.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTypeGet`.
- 404 NotFound: тип объекта не существует.
- 409 Conflict: конфликт при получении типа.

### `DELETE /AssetTypes/{id}`

## Пример запроса:
`DELETE /AssetTypes/1`
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTypeDelete`.
- 409 Conflict: тип используется и не может быть удалён.

### `GET /AssetTypes/{id}/workTypes`

## Пример запроса:
`GET /AssetTypes/1/workTypes?isPublished=true`
            
## Пример успешного ответа (200):
```json
{
  "1": "Ремонт",
  "2": "Обслуживание"
}
```
            
## Негативные сценарии:
- 204 NoContent: виды работ не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `WorkTypeList`.
- 206 PartialContent: при использовании заголовка Range.

### `POST /AssetTypes/{id}/workTypes`

## Пример запроса:
`POST /AssetTypes/1/workTypes`
            
```json
[1, 2, 3]
```
            
## Пример успешного ответа (200):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTypeUpdate`.

### `DELETE /AssetTypes/{id}/workTypes`

## Пример запроса:
`DELETE /AssetTypes/1/workTypes`
            
```json
[1, 2]
```
            
## Пример успешного ответа (200):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTypeUpdate`.

## AssetWorkTypes

### `POST /AssetWorkTypes`

## Пример запроса:
`POST /AssetWorkTypes`
            
```json
{
  "assetID": 101,
  "data": [1, 2]
}
```
            
## Пример успешного ответа (201):
```json
[
  {
    "tenantID": 105,
    "assetID": 101,
    "workTypeID": 1
  }
]
```
            
## Негативные сценарии:
- 400 BadRequest: тело запроса отсутствует или некорректно.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetWorkTypeAdd`.
- 409 Conflict: вид работ уже привязан или объект недоступен.

### `DELETE /AssetWorkTypes`

## Пример запроса:
`DELETE /AssetWorkTypes`
            
```json
{
  "assetID": 101,
  "data": [1, 2]
}
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 400 BadRequest: тело запроса отсутствует или некорректно.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetWorkTypeDelete`.

## Assets

### `GET /Assets`

## Пример запроса:
`GET /Assets?includePath=true&includeTaskActuality=true&searchText=насос`
            
## Пример успешного ответа (200):
```json
{
  "101": {
    "id": 101,
    "name": "Насосная станция №1",
    "parentID": 50,
    "deleted": null,
    "hasChildren": true,
    "sortOrder": 100,
    "serialNumber": "SN-001",
    "erpID": "ERP-101",
    "warrantyTill": "2027-12-31T00:00:00Z",
    "published": "2026-01-15T10:00:00Z",
    "useAllWorkTypes": true,
    "company": { "id": 5, "name": "ООО Сервис" },
    "path": [{ "id": 1, "name": "Завод" }, { "id": 50, "name": "Цех №1" }],
    "tasksActualities": {
      "1": { "self": 2, "nested": 5 }
    }
  }
}
```
            
При заголовке `Range` ответ может быть 206 Partial Content с заголовком `Content-Range`.
            
## Негативные сценарии:
- 204 NoContent: объекты не найдены.
- 400 BadRequest: multi-search (`;;`) при выборе более одного поля поиска пользователем.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetsList`.

### `POST /Assets`

## Пример запроса:
`POST /Assets`
            
Заголовок `X-Concurrency-Stamp` (опционально) — идентификатор запроса для идемпотентности.
            
```json
{
  "name": "Насосная станция №1",
  "parentID": 50,
  "companyID": 5,
  "assetTypeID": 1,
  "assetClassID": 2,
  "locationID": 300,
  "serialNumber": "SN-001",
  "erpID": "ERP-101",
  "notes": "Новый объект",
  "isMobileAsset": false,
  "isAutoPublish": false,
  "assetTemplateID": null
}
```
            
## Пример успешного ответа (201):
```json
{
  "id": 101,
  "name": "Насосная станция №1"
}
```
            
## Пример ответа при конфликте идемпотентности (409):
```json
{
  "id": 101,
  "name": "Насосная станция №1",
  "сoncurrencyStamp": "a1b2c3d4-e5f6-7890-abcd-ef1234567890"
}
```
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат запроса или отсутствуют обязательные поля.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAdd`.
- 409 Conflict: повторный запрос с тем же `X-Concurrency-Stamp`.

### `PUT /Assets`

## Пример запроса:
`PUT /Assets`
            
```json
{
  "assets": [101, 102, 103],
  "parentID": 50,
  "companyID": 5,
  "assetTypeID": 1,
  "isPublished": true,
  "addedWorkTypes": [1, 2],
  "deletedWorkTypes": [3]
}
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetsUpdate`.
- 409 Conflict: конфликт при массовом обновлении.

### `DELETE /Assets`

## Пример запроса:
`DELETE /Assets`
            
```json
[101, 102, 103]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetDelete`.
- 409 Conflict: конфликт при удалении.

### `HEAD /Assets`

## Пример запроса:
`HEAD /Assets?parentID=-1`
            
## Пример успешного ответа (200):
Пустое тело ответа. Заголовок `Content-Range: items 0-0/42` содержит общее количество записей, удовлетворяющих фильтру.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetsList`.

### `GET /Assets/attributes`

## Пример запроса:
`GET /Assets/attributes?assetID=101&attributeID=2`
            
## Пример успешного ответа (200):
```json
[
  {
    "assetID": 101,
    "attributeID": 2,
    "attributeName": "Мощность",
    "value": "100"
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: атрибуты не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAttributeList`.
- 206 PartialContent: при использовании заголовка Range.

### `DELETE /Assets/avatar`

## Пример запроса:
`DELETE /Assets/avatar`
            
```json
[101, 102]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAvatarDelete`.

### `POST /Assets/contacts`

## Пример запроса:
`POST /Assets/contacts`
            
```json
[
  {
    "assetID": 101,
    "data": [10, 11]
  }
]
```
            
## Пример успешного ответа (201):
```json
[
  {
    "assetID": 101,
    "contactID": 10,
    "id": 10
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: контакты не добавлены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetContactAdd`.
- 409 Conflict: контакт уже привязан или объект недоступен.

### `DELETE /Assets/contacts`

## Пример запроса:
`DELETE /Assets/contacts`
            
```json
[
  {
    "assetID": 101,
    "data": [10, 11]
  }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetContactDelete`.
- 409 Conflict: связь не найдена или объект недоступен.

### `DELETE /Assets/full`

## Пример запроса:
`DELETE /Assets/full`
            
```json
[101, 102]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetDeleteFull`.
- 409 Conflict: конфликт при удалении.

### `PUT /Assets/restore`

## Пример запроса:
`PUT /Assets/restore?withNested=true`
            
```json
[101, 102]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetRestore`.
- 409 Conflict: конфликт при восстановлении.

### `GET /Assets/{assetID}`

## Пример запроса:
`GET /Assets/101`
            
## Пример успешного ответа (200):
```json
{
  "id": 101,
  "name": "Насосная станция №1",
  "parentID": 50,
  "deleted": null,
  "isMobileAsset": false,
  "serialNumber": "SN-001",
  "erpID": "ERP-101",
  "warrantyTill": "2027-12-31T00:00:00Z",
  "published": "2026-01-15T10:00:00Z",
  "publishedBy": 12,
  "notes": "Основной объект",
  "avatarUrl": "https://cdn.example.com/avatar/101.jpg",
  "useAllWorkTypes": true,
  "isInheritParentDistricts": false,
  "isHostLocation": false,
  "sortOrder": 100,
  "assetType": { "id": 1, "name": "Оборудование", "isHostable": true },
  "assetClass": { "id": 2, "name": "Насосное" },
  "company": { "id": 5, "name": "ООО Сервис" },
  "scheduleRule": { "id": 3, "name": "5/2" },
  "parent": { "id": 50, "name": "Цех №1", "deleted": null },
  "responsiblePerson": {
    "userID": 20,
    "firstName": "Иван",
    "lastName": "Иванов",
    "email": "ivan@example.com"
  },
  "location": { "id": 300, "address": "г. Москва, ул. Примерная, 1" },
  "path": [{ "id": 1, "name": "Завод" }, { "id": 50, "name": "Цех №1" }]
}
```
            
## Негативные сценарии:
- 204 NoContent: объект не найден или недоступен пользователю.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetGet`.

### `PUT /Assets/{assetID}`

## Пример запроса:
`PUT /Assets/101`
            
```json
{
  "name": "Насосная станция №1 (обновлено)",
  "parentID": 50,
  "companyID": 5,
  "assetTypeID": 1,
  "assetClassID": 2,
  "locationID": 300,
  "serialNumber": "SN-001",
  "notes": "Обновлённое описание"
}
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetUpdate`.
- 409 Conflict: конфликт версий или бизнес-ограничений.

### `DELETE /Assets/{assetID}`

## Пример запроса:
`DELETE /Assets/101`
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetDelete`.
- 409 Conflict: конфликт при удалении.

### `GET /Assets/{assetID}/assignments`

## Пример запроса:
`GET /Assets/101/assignments?userID=5&validOn=2024-06-01`
            
## Пример успешного ответа (200):
```json
[
  {
    "user": {
      "id": 5,
      "firstName": "Иван",
      "lastName": "Иванов",
      "deleted": null
    },
    "validityPeriod": {
      "from": "2024-01-01T00:00:00Z",
      "till": "9999-12-31T23:59:59Z"
    },
    "notes": "Ответственный инженер"
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: назначения не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAssignmentList`.
- 404 NotFound: объект не найден.
- 206 PartialContent: при использовании заголовка Range.

### `GET /Assets/{assetID}/attachments`

## Пример запроса:
`GET /Assets/101/attachments?thumbnailSize=128`
            
## Пример успешного ответа (200):
```json
{
  "501": {
    "fileName": "document.pdf",
    "description": "Паспорт оборудования",
    "isUploaded": true,
    "isProtected": false,
    "size": 102400,
    "created": "2024-01-15T10:00:00Z",
    "publicUrl": "https://storage.example.com/file.pdf",
    "thumbnailUrl": null
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: вложения не найдены.
- 400 BadRequest: некорректный thumbnailSize.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAttachmentsList`.
- 206 PartialContent: при использовании заголовка Range.

### `GET /Assets/{assetID}/attachments/{attachmentID}`

## Пример запроса:
`GET /Assets/101/attachments/501?noRedirect=false`
            
## Пример успешного ответа (307):
Редирект на временную ссылку для скачивания файла.
            
## Негативные сценарии:
- 400 BadRequest: некорректный thumbnailSize.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAttachmentDownload`.
- 404 NotFound: вложение не найдено.

### `GET /Assets/{assetID}/attributes`

## Пример запроса:
`GET /Assets/101/attributes`
            
## Пример успешного ответа (200):
```json
[
  {
    "attribute": { "id": 2, "name": "Мощность", "deleted": null },
    "value": "100",
    "isPublic": true,
    "sortOrder": 1,
    "attributeType": { "id": 1, "name": "Число", "code": "Number" }
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: атрибуты не найдены.
- 400 BadRequest: некорректный идентификатор объекта.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAttributeList`.
- 206 PartialContent: при использовании заголовка Range.

### `GET /Assets/{assetID}/checkLists`

## Пример запроса:
`GET /Assets/101/checkLists`
            
## Пример успешного ответа (200):
```json
{
  "101": [
    {
      "id": 3,
      "name": "Ежемесячное ТО",
      "description": "Чек-лист технического обслуживания"
    }
  ]
}
```
            
## Негативные сценарии:
- 204 NoContent: чек-листы не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetCheckListList`.

### `POST /Assets/{assetID}/checkLists`

## Пример запроса:
`POST /Assets/101/checkLists`
            
```json
[3, 5]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetCheckListAdd`.

### `DELETE /Assets/{assetID}/checkLists`

## Пример запроса:
`DELETE /Assets/101/checkLists`
            
```json
[3, 5]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetCheckListDelete`.

### `POST /Assets/{assetID}/checkLists/{checkListID}`

## Пример запроса:
`POST /Assets/101/checkLists/3`
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetCheckListAdd`.

### `DELETE /Assets/{assetID}/checkLists/{checkListID}`

## Пример запроса:
`DELETE /Assets/101/checkLists/3`
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetCheckListDelete`.

### `GET /Assets/{assetID}/contacts`

## Пример запроса:
`GET /Assets/101/contacts?searchText=Иванов`
            
## Пример успешного ответа (200):
```json
{
  "10": {
    "assetID": 101,
    "contactID": 10,
    "id": 10,
    "fullName": "Иванов Иван",
    "email": "ivanov@example.com",
    "phone": "+79001234567",
    "position": "Инженер",
    "description": null,
    "archived": null
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: контакты не найдены.
- 400 BadRequest: некорректный запрос.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetContactsList`.
- 206 PartialContent: при использовании заголовка Range.

### `GET /Assets/{assetID}/contacts/{contactID}`

## Пример запроса:
`GET /Assets/101/contacts/10`
            
## Пример успешного ответа (200):
```json
{
  "assetID": 101,
  "contactID": 10,
  "id": 10,
  "fullName": "Иванов Иван",
  "email": "ivanov@example.com",
  "phone": "+79001234567",
  "position": "Инженер",
  "description": null,
  "deleted": null,
  "archived": null
}
```
            
## Негативные сценарии:
- 204 NoContent: контакт не найден.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetContactGet`.

### `POST /Assets/{assetID}/contacts/{contactID}`

## Пример запроса:
`POST /Assets/101/contacts/10`
            
## Пример успешного ответа (201):
```json
[
  {
    "assetID": 101,
    "contactID": 10,
    "id": 10
  }
]
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetContactAdd`.
- 409 Conflict: контакт уже привязан или объект недоступен.

### `DELETE /Assets/{assetID}/contacts/{contactID}`

## Пример запроса:
`DELETE /Assets/101/contacts/10`
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetContactDelete`.
- 409 Conflict: связь не найдена или объект недоступен.

### `GET /Assets/{assetID}/districts`

## Пример запроса:
`GET /Assets/101/districts`
            
## Пример успешного ответа (200):
```json
{
  "5": {
    "parentID": 1,
    "name": "Центральный район"
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: участки не найдены.
- 400 BadRequest: некорректный идентификатор объекта.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetDistrictsList`.
- 206 PartialContent: при использовании заголовка Range.

### `DELETE /Assets/{assetID}/full`

## Пример запроса:
`DELETE /Assets/101/full`
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetDeleteFull`.
- 409 Conflict: конфликт при удалении.

### `GET /Assets/{assetID}/locations/actual`

## Пример запроса:
`GET /Assets/101/locations/actual`
            
## Пример успешного ответа (200):
```json
{
  "id": 42,
  "address": "г. Москва, ул. Примерная, д. 1",
  "coordinate": "55.7558:37.6173",
  "description": "Офис",
  "deleted": null,
  "timeZone": {
    "id": 1,
    "utcOffsetMinutes": 180
  },
  "country": {
    "id": 1,
    "twoSymbolCode": "RU"
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: локация не найдена.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetLocationsGet`.

### `PUT /Assets/{assetID}/publish`

## Пример запроса:
`PUT /Assets/101/publish`
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetPublish`.
- 409 Conflict: конфликт при публикации.

### `GET /Assets/{assetID}/skills`

## Пример запроса:
`GET /Assets/101/skills`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "id": 1,
    "name": "Электромонтаж"
  },
  "2": {
    "id": 2,
    "name": "Сварка"
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: навыки не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetSkillList`.
- 206 PartialContent: при использовании заголовка Range.

### `GET /Assets/{assetID}/tags`

## Пример запроса:
`GET /Assets/101/tags`
            
## Пример успешного ответа (200):
```json
[
  "Сервисное обслуживание",
  "Критичное"
]
```
            
## Негативные сценарии:
- 204 NoContent: теги не найдены.
- 400 BadRequest: некорректный идентификатор объекта.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTagsList`.
- 206 PartialContent: при использовании заголовка Range.

### `PUT /Assets/{assetID}/unpublish`

## Пример запроса:
`PUT /Assets/101/unpublish`
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetUnpublish`.
- 409 Conflict: конфликт при снятии с публикации.

### `GET /Assets/{assetID}/workTypes`

## Пример запроса:
`GET /Assets/101/workTypes`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "workClassID": 2,
    "name": "Техническое обслуживание",
    "description": "Плановое ТО оборудования",
    "parentID": null,
    "hasChildren": false
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: виды работ не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetWorkTypesList`.
- 206 PartialContent: при использовании заголовка Range.

### `DELETE /Assets/{id}/avatar`

## Пример запроса:
`DELETE /Assets/101/avatar`
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAvatarDelete`.

### `PUT /Assets/{id}/avatar/upload/fromBody`

## Пример запроса:
`PUT /Assets/101/avatar/upload/fromBody`
            
```json
{
  "fileName": "avatar.jpg",
  "contentType": "image/jpeg",
  "content": "/9j/4AAQSkZJRg..."
}
```
            
## Пример успешного ответа (200):
```json
{
  "fileName": "avatar.jpg",
  "publicUrl": "https://storage.example.com/avatar.jpg"
}
```
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат изображения или размер менее 128×128.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAvatarUpload`.

### `PUT /Assets/{id}/avatar/upload/fromForm`

## Пример запроса:
`PUT /Assets/101/avatar/upload/fromForm`
            
Multipart/form-data с полем изображения.
            
## Пример успешного ответа (200):
```json
{
  "fileName": "avatar.jpg",
  "publicUrl": "https://storage.example.com/avatar.jpg"
}
```
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат изображения или размер менее 128×128.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetAvatarUpload`.

## Companies

### `GET /Companies`

## Пример запроса:
`GET /Companies?searchText=ромашка&isEmployer=true`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "id": 1,
    "name": "ООО Ромашка",
    "sortOrder": 0,
    "erpID": "ERP-001",
    "code": "ROM",
    "registrationTypeID": 3,
    "registrationTypeShortNameRu": "ООО",
    "registrationTypeNameRu": "Общество с ограниченной ответственностью",
    "tin": "7701234567",
    "iec": "770101001",
    "isEmployer": true,
    "isContractorHolder": false,
    "isOurCompany": false,
    "isVATTaxpayer": true,
    "customerOrgUnit": { "id": 10, "name": "Отдел закупок" },
    "staffOrgUnit": { "id": 11, "name": "Сервис" },
    "counters": { "assets": 25, "users": 5 }
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: компании не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompaniesList`.
- 206 PartialContent: при использовании заголовка Range.

### `POST /Companies`

## Пример запроса:
`POST /Companies`
            
```json
[
  {
    "name": "ООО Ромашка",
    "registrationTypeID": 3,
    "tin": "7701234567",
    "iec": "770101001",
    "isEmployer": true,
    "email": "info@romashka.ru",
    "phone": "+74951234567"
  }
]
```
            
## Пример успешного ответа (201):
```json
[1]
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyAdd`.
- 409 Conflict: конфликт при создании компании.

### `PUT /Companies`

## Пример запроса:
`PUT /Companies`
            
```json
[
  {
    "id": 1,
    "name": "ООО Ромашка (обновлено)",
    "registrationTypeID": 3,
    "tin": "7701234567",
    "email": "new@romashka.ru"
  }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyUpdate`.
- 409 Conflict: конфликт при обновлении компании.

### `DELETE /Companies`

## Пример запроса:
`DELETE /Companies`
            
```json
[1, 2, 3]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyDelete`.
- 409 Conflict: конфликт при удалении компаний.

### `HEAD /Companies`

## Пример запроса:
`HEAD /Companies?searchText=ромашка`
            
## Пример успешного ответа (200):
Заголовок `Content-Range` с общим количеством записей, удовлетворяющих фильтру.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompaniesList`.

### `POST /Companies/contacts`

## Пример запроса:
`POST /Companies/contacts`
            
```json
[
  {
    "companyID": 1,
    "data": [101, 102]
  }
]
```
            
## Пример успешного ответа (201):
```json
[
  {
    "companyID": 1,
    "contactID": 101
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: контакты не были добавлены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyContactAdd`.
- 409 Conflict: конфликт при добавлении контактов.

### `DELETE /Companies/contacts`

## Пример запроса:
`DELETE /Companies/contacts`
            
```json
[
  {
    "companyID": 1,
    "data": [101, 102]
  }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyContactDelete`.
- 409 Conflict: конфликт при удалении контактов.

### `GET /Companies/dadata/find`

## Пример запроса:
`GET /Companies/dadata/find?inn=7701234567`
            
## Пример успешного ответа (200):
```json
{
  "name": "ООО Ромашка",
  "fullName": "Общество с ограниченной ответственностью «Ромашка»",
  "tin": "7701234567",
  "iec": "770101001",
  "psrn": "1027700132195",
  "registeredOffice": "г. Москва, ул. Примерная, д. 1",
  "registrationTypeID": 3
}
```
            
## Негативные сценарии:
- 204 NoContent: компания по ИНН не найдена.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyAdd`.

### `PUT /Companies/restore`

## Пример запроса:
`PUT /Companies/restore`
            
```json
[1, 2]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyRestore`.
- 409 Conflict: конфликт при восстановлении компаний.

### `GET /Companies/{companyID}/attachment/{attachmentID}`

## Пример запроса:
`GET /Companies/1/attachment/501?thumbnailSize=128`
            
## Пример успешного ответа (200):
```json
{
  "attachmentID": 501,
  "fileName": "document.pdf",
  "description": "Устав компании",
  "isUploaded": true,
  "isProtected": false,
  "size": 102400,
  "created": "2024-01-15T10:00:00Z",
  "publicUrl": "https://storage.example.com/file.pdf",
  "thumbnailUrl": "https://storage.example.com/thumb/501_128.jpg"
}
```
            
## Негативные сценарии:
- 204 NoContent: вложение не найдено.
- 400 BadRequest: некорректный thumbnailSize.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyAttachmentGet`.
- 500 InternalServerError: ошибка сервера.

### `GET /Companies/{companyID}/attachments`

## Пример запроса:
`GET /Companies/1/attachments?thumbnailSize=128`
            
## Пример успешного ответа (200):
```json
{
  "501": {
    "fileName": "document.pdf",
    "description": "Устав компании",
    "isUploaded": true,
    "isProtected": false,
    "size": 102400,
    "created": "2024-01-15T10:00:00Z",
    "publicUrl": "https://storage.example.com/file.pdf",
    "thumbnailUrl": null
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: вложения не найдены.
- 400 BadRequest: некорректный thumbnailSize.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyAttachmentList`.
- 206 PartialContent: при использовании заголовка Range.

### `GET /Companies/{companyID}/attachments/{attachmentID}`

## Пример запроса:
`GET /Companies/1/attachments/501?noRedirect=false`
            
## Пример успешного ответа (307):
Редирект на временную ссылку для скачивания файла.
            
## Негативные сценарии:
- 400 BadRequest: некорректный thumbnailSize.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyAttachmentDownload`.
- 404 NotFound: вложение не найдено.

### `GET /Companies/{companyID}/attributes`

## Пример запроса:
`GET /Companies/1/attributes`
            
## Пример успешного ответа (200):
```json
[
  {
    "attribute": { "id": 2, "name": "Номер договора" },
    "values": ["Д-001"],
    "isPublic": true,
    "attributeType": { "id": 1, "name": "Строка", "code": "String" },
    "measurementUnit": null,
    "listOfValues": null,
    "domain": null
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: атрибуты не найдены.
- 400 BadRequest: некорректный запрос.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyGet`.
- 206 PartialContent: при использовании заголовка Range.

### `POST /Companies/{companyID}/attributes`

## Пример запроса:
`POST /Companies/1/attributes`
            
```json
[
  {
    "attributeID": 2,
    "values": ["Значение атрибута"],
    "isPublic": true
  }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyUpdate`.

### `GET /Companies/{companyID}/bankAccounts`

## Пример запроса:
`GET /Companies/1/bankAccounts?searchText=сбер`
            
## Пример успешного ответа (200):
```json
{
  "10": {
    "companyID": 1,
    "companyBankAccountID": 10,
    "checkingAccount": "40702810100000001234",
    "companyName": "ООО Ромашка",
    "isDefault": true,
    "bank": {
      "id": 1,
      "name": "ПАО Сбербанк",
      "bic": "044525225",
      "correspondingAccount": "30101810400000000225"
    },
    "currency": {
      "id": 1,
      "shortName": "RUB",
      "asciiCode": "RUB"
    }
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: банковские счета не найдены.
- 400 BadRequest: некорректный запрос.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyBankAccountList`.
- 206 PartialContent: при использовании заголовка Range.

### `POST /Companies/{companyID}/bankAccounts`

## Пример запроса:
`POST /Companies/1/bankAccounts`
            
```json
[
  {
    "bankID": 1,
    "checkingAccount": "40702810100000001234",
    "currencyID": 1,
    "isDefault": true
  }
]
```
            
## Пример успешного ответа (201):
```json
[
  {
    "companyID": 1,
    "bankID": 1,
    "companyBankAccountID": 10
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: счета не были добавлены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyBankAccountAdd`.
- 409 Conflict: конфликт при добавлении счетов.

### `PUT /Companies/{companyID}/bankAccounts`

## Пример запроса:
`PUT /Companies/1/bankAccounts`
            
```json
[
  {
    "companyBankAccountID": 10,
    "checkingAccount": "40702810100000009999",
    "isDefault": false
  }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyBankAccountUpdate`.
- 409 Conflict: конфликт при обновлении счетов.

### `DELETE /Companies/{companyID}/bankAccounts`

## Пример запроса:
`DELETE /Companies/1/bankAccounts`
            
```json
[10, 11]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyBankAccountDelete`.
- 409 Conflict: конфликт при удалении счетов.

### `DELETE /Companies/{companyID}/bankAccounts/{bankAccountID}`

## Пример запроса:
`DELETE /Companies/1/bankAccounts/10`
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyBankAccountDelete`.
- 409 Conflict: конфликт при удалении счёта.

### `GET /Companies/{companyID}/contacts`

## Пример запроса:
`GET /Companies/1/contacts?searchText=иванов`
            
## Пример успешного ответа (200):
```json
{
  "101": {
    "companyID": 1,
    "contactID": 101,
    "fullName": "Иванов Иван Иванович",
    "email": "ivanov@example.com",
    "phone": "+79001234567",
    "position": "Менеджер",
    "description": "Основной контакт",
    "archived": null
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: контакты не найдены.
- 400 BadRequest: некорректный запрос.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyContactsList`.
- 206 PartialContent: при использовании заголовка Range.

### `GET /Companies/{companyID}/contacts/{contactID}`

## Пример запроса:
`GET /Companies/1/contacts/101`
            
## Пример успешного ответа (200):
```json
{
  "companyID": 1,
  "contactID": 101,
  "fullName": "Иванов Иван Иванович",
  "email": "ivanov@example.com",
  "phone": "+79001234567",
  "position": "Менеджер",
  "description": "Основной контакт",
  "deleted": null,
  "archived": null
}
```
            
## Негативные сценарии:
- 204 NoContent: контакт не найден.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyContactGet`.

### `POST /Companies/{companyID}/contacts/{contactID}`

## Пример запроса:
`POST /Companies/1/contacts/101`
            
## Пример успешного ответа (201):
```json
[
  {
    "companyID": 1,
    "contactID": 101
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: контакт не был добавлен.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyContactAdd`.
- 409 Conflict: конфликт при добавлении контакта.

### `DELETE /Companies/{companyID}/contacts/{contactID}`

## Пример запроса:
`DELETE /Companies/1/contacts/101`
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyContactDelete`.
- 409 Conflict: конфликт при удалении контакта.

### `GET /Companies/{companyID}/locations/actual`

## Пример запроса:
`GET /Companies/1/locations/actual`
            
## Пример успешного ответа (200):
```json
{
  "id": 42,
  "address": "г. Москва, ул. Примерная, д. 1",
  "coordinate": "55.7558:37.6173",
  "description": "Офис",
  "country": {
    "id": 1,
    "twoSymbolCode": "RU",
    "name": "Россия"
  },
  "timeZone": {
    "id": 1,
    "utcOffsetMinutes": 180,
    "name": "Москва"
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: компания не найдена или локация не задана.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyLocationGet`.

### `GET /Companies/{id}`

## Пример запроса:
`GET /Companies/1`
            
## Пример успешного ответа (200):
```json
{
  "id": 1,
  "name": "ООО Ромашка",
  "fullName": "Общество с ограниченной ответственностью «Ромашка»",
  "email": "info@romashka.ru",
  "phone": "+74951234567",
  "siteUrl": "https://romashka.ru",
  "registeredOffice": "г. Москва, ул. Примерная, д. 1",
  "tin": "7701234567",
  "iec": "770101001",
  "psrn": "1027700132195",
  "vatRate": 20,
  "isEmployer": true,
  "location": {
    "id": 42,
    "address": "г. Москва, ул. Примерная, д. 1",
    "coordinate": "55.7558:37.6173"
  },
  "counters": { "assets": 25, "users": 5 }
}
```
            
## Негативные сценарии:
- 204 NoContent: компания не найдена или недоступна.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyGet`.

### `DELETE /Companies/{id}`

## Пример запроса:
`DELETE /Companies/1`
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyDelete`.
- 409 Conflict: конфликт при удалении компании.

## CompanyAttachments

### `POST /CompanyAttachments`

## Пример запроса:
`POST /CompanyAttachments`
            
```json
[
  {
    "companyID": 15,
    "data": [501, 502]
  }
]
```
            
## Пример успешного ответа (201):
```json
[
  { "companyID": 15, "attachmentID": 501 },
  { "companyID": 15, "attachmentID": 502 }
]
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyAttachmentAdd`.

### `DELETE /CompanyAttachments`

## Пример запроса:
`DELETE /CompanyAttachments`
            
```json
[
  {
    "companyID": 15,
    "data": [501, 502]
  }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyAttachmentDelete`.

### `POST /CompanyAttachments/upload/fromBody`

## Пример запроса:
`POST /CompanyAttachments/upload/fromBody`
            
```json
{
  "companyID": 15,
  "fileName": "contract.pdf",
  "contentType": "application/pdf",
  "content": "base64-encoded-content"
}
```
            
## Пример успешного ответа (201):
```json
{
  "companyID": 15,
  "attachmentID": 501,
  "fileName": "contract.pdf",
  "checkSum": "d41d8cd98f00b204e9800998ecf8427e",
  "isProtected": false
}
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyAttachmentUpload`.

### `POST /CompanyAttachments/upload/fromForm`

## Пример запроса:
`POST /CompanyAttachments/upload/fromForm`
            
Multipart/form-data с полями `companyID`, `fileName`, `content` и др.
            
## Пример успешного ответа (201):
```json
{
  "companyID": 15,
  "attachmentID": 501,
  "fileName": "contract.pdf",
  "checkSum": "d41d8cd98f00b204e9800998ecf8427e",
  "isProtected": false
}
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyAttachmentUpload`.

## CompanyContacts

### `POST /CompanyContacts`

## Пример запроса:
`POST /CompanyContacts`
            
```json
[
  {
    "companyID": 15,
    "data": [10, 11]
  }
]
```
            
## Пример успешного ответа (201):
```json
[
  { "companyID": 15, "contactID": 10 },
  { "companyID": 15, "contactID": 11 }
]
```
            
## Негативные сценарии:
- 204 NoContent: контакты не были привязаны.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyContactAdd`.
- 409 Conflict: конфликт при привязке контакта.
            
Устаревший endpoint; используйте `POST /Companies/contacts`.

### `DELETE /CompanyContacts`

## Пример запроса:
`DELETE /CompanyContacts`
            
```json
[
  {
    "companyID": 15,
    "data": [10, 11]
  }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyContactDelete`.
- 409 Conflict: конфликт при отвязке контакта.
            
Устаревший endpoint; используйте `DELETE /Companies/contacts`.

## CompanyListQueries

### `GET /CompanyListQueries`

## Пример запроса:
`GET /CompanyListQueries`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "name": "Мои компании",
    "searchText": "Ромашка",
    "queryString": "?searchText=Ромашка"
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: сохранённые запросы не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyListQueryList`.
- 206 PartialContent: при использовании заголовка Range.

### `POST /CompanyListQueries`

## Пример запроса:
`POST /CompanyListQueries`
            
```json
[
  {
    "name": "Мои компании",
    "queryString": "?companyID=15&searchText=Ромашка"
  }
]
```
            
## Пример успешного ответа (201):
```json
[15]
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyListQueryAdd`.

### `PUT /CompanyListQueries`

## Пример запроса:
`PUT /CompanyListQueries`
            
```json
[
  {
    "id": 15,
    "name": "Мои компании (обновлено)",
    "queryString": "?companyID=15"
  }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyListQueryUpdate`.

### `DELETE /CompanyListQueries`

## Пример запроса:
`DELETE /CompanyListQueries`
            
```json
[15, 16]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyListQueryDelete`.

### `DELETE /CompanyListQueries/remove`

## Пример запроса:
`DELETE /CompanyListQueries/remove`
            
```json
[15, 16]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyListQueryRemove`.

### `GET /CompanyListQueries/{id}`

## Пример запроса:
`GET /CompanyListQueries/1`
            
## Пример успешного ответа (200):
```json
{
  "name": "Мои компании",
  "searchText": "Ромашка",
  "filterList": {
    "companies": [{ "id": "15", "name": "ООО Ромашка" }]
  },
  "queryString": "?companyID=15&searchText=Ромашка"
}
```
            
## Негативные сценарии:
- 204 NoContent: запрос не найден.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyListQueryGet`.

### `DELETE /CompanyListQueries/{id}`

## Пример запроса:
`DELETE /CompanyListQueries/15`
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyListQueryDelete`.

### `DELETE /CompanyListQueries/{id}/remove`

## Пример запроса:
`DELETE /CompanyListQueries/15/remove`
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyListQueryRemove`.

## CompanyLocations

### `GET /CompanyLocations`

## Пример запроса:
`GET /CompanyLocations?companyID=15`
            
## Пример успешного ответа (200):
```json
{
  "42": {
    "companyID": 15,
    "location": {
      "id": 42,
      "address": "г. Москва, ул. Примерная, д. 1",
      "coordinate": "55.7558:37.6173",
      "description": "Офис",
      "dateFrom": "2024-01-01T00:00:00Z",
      "dateTill": "9999-12-31T23:59:59Z",
      "timezoneID": 1,
      "timezoneUtcOffsetMinutes": 180,
      "countryID": 1,
      "countryTwoSymbolCode": "RU"
    }
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: локации не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyLocationsList`.
- 409 Conflict: компания недоступна.
- 206 PartialContent: при использовании заголовка Range.

### `POST /CompanyLocations`

## Пример запроса:
`POST /CompanyLocations`
            
```json
{
  "companyID": 15,
  "locationID": 42,
  "dateFrom": "2024-01-01T00:00:00Z",
  "dateTill": "9999-12-31T23:59:59Z"
}
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyLocationAdd`.

### `PUT /CompanyLocations`

## Пример запроса:
`PUT /CompanyLocations`
            
```json
{
  "companyID": 15,
  "locationID": 42,
  "dateFrom": "2024-06-01T00:00:00Z",
  "dateTill": "9999-12-31T23:59:59Z"
}
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyLocationUpdate`.

### `DELETE /CompanyLocations`

## Пример запроса:
`DELETE /CompanyLocations`
            
```json
{
  "companyID": 15
}
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyLocationRemove`.

## CompanyRegistrationTypes

### `GET /CompanyRegistrationTypes`

## Пример запроса:
`GET /CompanyRegistrationTypes`
            
## Пример успешного ответа (200):
```json
{
  "1": {
    "id": 1,
    "shortNameRu": "ИП",
    "nameRu": "Индивидуальный предприниматель"
  },
  "3": {
    "id": 3,
    "shortNameRu": "ООО",
    "nameRu": "Общество с ограниченной ответственностью"
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: виды регистрации не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompanyRegistrationTypeList`.

## Districts

### `GET /Districts`

## Пример запроса:
`GET /Districts?includePath=true&parentID=-1`
            
## Пример успешного ответа (200):
```json
[
  {
    "id": 1,
    "name": "Центральный район",
    "description": "Основной участок",
    "erpID": "ERP-001",
    "parentID": null,
    "sortOrder": 1,
    "usersCount": 5,
    "assetsCount": 12,
    "taskTypesCount": 3,
    "isDefault": true,
    "hasChildren": true,
    "path": [
      { "id": 1, "name": "Центральный район" }
    ]
  }
]
```
            
## Негативные сценарии:
- 204 NoContent: участки не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `DistrictsList`.

### `POST /Districts`

## Пример запроса:
`POST /Districts`
            
```json
[
  {
    "name": "Новый участок",
    "description": "Описание участка",
    "parentID": 1,
    "sortOrder": 2
  }
]
```
            
## Пример успешного ответа (201):
```json
[5]
```
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `DistrictAdd`.
- 409 Conflict: конфликт данных при добавлении.

### `PUT /Districts`

## Пример запроса:
`PUT /Districts`
            
```json
[
  {
    "id": 5,
    "name": "Обновлённый участок",
    "description": "Новое описание"
  }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `DistrictUpdate`.
- 409 Conflict: конфликт данных при обновлении.

### `DELETE /Districts`

## Пример запроса:
`DELETE /Districts`
            
```json
[5, 6, 7]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `DistrictDelete`.
- 409 Conflict: один или несколько участков не могут быть удалены.

### `PUT /Districts/parentAndReorder`

## Пример запроса:
`PUT /Districts/parentAndReorder`
            
```json
{
  "id": 5,
  "parentID": 1,
  "sortOrder": 3
}
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `DistrictParentSortOrderUpdate`.
- 409 Conflict: конфликт данных при изменении иерархии.

### `GET /Districts/{id}`

## Пример запроса:
`GET /Districts/1`
            
## Пример успешного ответа (200):
```json
{
  "id": 1,
  "name": "Центральный район",
  "description": "Основной участок",
  "erpID": "ERP-001",
  "parentID": null,
  "sortOrder": 1,
  "usersCount": 0,
  "assetsCount": 0,
  "taskTypesCount": 0,
  "isDefault": true
}
```
            
## Негативные сценарии:
- 204 NoContent: участок не найден или недоступен.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `DistrictGet`.

### `DELETE /Districts/{id}`

## Пример запроса:
`DELETE /Districts/5`
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `DistrictDelete`.
- 409 Conflict: участок не может быть удалён.

## Locations

### `GET /Locations`

## Пример запроса:
`GET /Locations?searchText=Москва&radius=1000&pointCenter=55.7558:37.6173`
            
## Пример успешного ответа (200):
```json
{
  "42": {
    "id": 42,
    "address": "г. Москва, ул. Примерная, д. 1",
    "coordinate": "55.7558:37.6173",
    "description": "Офис",
    "deleted": null,
    "timeZone": { "id": 1, "utcOffsetMinutes": 180 },
    "country": { "id": 1, "twoSymbolCode": "RU" }
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: локации не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `LocationsList`.
- 206 PartialContent: при использовании заголовка Range.

### `POST /Locations`

## Пример запроса:
`POST /Locations`
            
```json
[
  {
    "address": "г. Москва, ул. Примерная, д. 1",
    "coordinate": "55.7558:37.6173",
    "description": "Офис",
    "countryID": 1,
    "timezoneID": 1
  }
]
```
            
## Пример успешного ответа (201):
```json
[42]
```
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `LocationAdd`.

### `PUT /Locations`

## Пример запроса:
`PUT /Locations`
            
```json
[
  {
    "id": 42,
    "address": "г. Москва, ул. Обновлённая, д. 2",
    "coordinate": "55.7558:37.6173"
  }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат запроса.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `LocationUpdate`.

### `DELETE /Locations`

## Пример запроса:
`DELETE /Locations`
            
```json
[42, 43]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `LocationDelete`.

### `HEAD /Locations`

## Пример запроса:
`HEAD /Locations?searchFor=Москва`
            
## Пример успешного ответа (200):
Пустое тело; заголовок `Content-Range` содержит общее количество записей.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `LocationsList`.

### `DELETE /Locations/remove`

## Пример запроса:
`DELETE /Locations/remove`
            
```json
[42, 43]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `LocationRemove`.

### `GET /Locations/{id}`

## Пример запроса:
`GET /Locations/42`
            
## Пример успешного ответа (200):
```json
{
  "id": 42,
  "address": "г. Москва, ул. Примерная, д. 1",
  "coordinate": "55.7558:37.6173",
  "description": "Офис",
  "deleted": null,
  "timeZone": { "id": 1, "utcOffsetMinutes": 180 },
  "country": { "id": 1, "twoSymbolCode": "RU" },
  "area": ["55.7558:37.6173", "55.7560:37.6180"]
}
```
            
## Негативные сценарии:
- 204 NoContent: локация не найдена.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `LocationGet`.

### `DELETE /Locations/{id}`

## Пример запроса:
`DELETE /Locations/42`
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `LocationDelete`.

### `DELETE /Locations/{id}/remove`

## Пример запроса:
`DELETE /Locations/42/remove`
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `LocationRemove`.

## OrgUnits

### `GET /OrgUnits`

## Пример запроса:
`GET /OrgUnits?companyID=1`
            
## Пример успешного ответа (200):
```json
{
  "10": {
    "name": "Центральный офис",
    "parentID": null,
    "hasChildren": true,
    "orgUnitType": { "id": 1, "name": "Филиал" },
    "company": { "id": 1, "name": "ООО Ромашка" }
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: организационные единицы не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `OrgUnitList`.

### `GET /OrgUnits/root`

## Пример запроса:
`GET /OrgUnits/root?companyID=1&companyID=2`
            
## Пример успешного ответа (200):
```json
{
  "10": {
    "name": "Центральный офис",
    "parentID": null,
    "hasChildren": true,
    "orgUnitType": { "id": 1, "name": "Филиал" },
    "company": { "id": 1, "name": "ООО Ромашка" },
    "manager": {
      "userID": 5,
      "firstName": "Алексей",
      "lastName": "Иванов",
      "email": "a.ivanov@example.com"
    },
    "location": {
      "id": 42,
      "address": "г. Москва, ул. Примерная, 1",
      "coordinate": "55.7558:37.6173"
    }
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: корневые организационные единицы не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `OrgUnitRootList`.

### `GET /OrgUnits/{id}/orgunits`

## Пример запроса:
`GET /OrgUnits/10/orgunits?companyID=1`
            
## Пример успешного ответа (200):
```json
{
  "11": {
    "name": "Отдел обслуживания",
    "parentID": 10,
    "hasChildren": false,
    "orgUnitType": { "id": 2, "name": "Подразделение" },
    "company": { "id": 1, "name": "ООО Ромашка" }
  }
}
```
            
## Негативные сценарии:
- 204 NoContent: дочерние организационные единицы не найдены.
- 400 BadRequest: некорректный идентификатор родительской единицы.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `OrgUnitList`.

## PreferredTechnicians

### `GET /PreferredTechnicians`

## Пример запроса:
`GET /PreferredTechnicians?assetID=101&assetID=102`
            
## Пример успешного ответа (200):
```json
{
  "assets": [
    {
      "id": 101,
      "parentID": 1,
      "name": "Насосная станция №1",
      "host": {
        "id": 50,
        "name": "Здание А"
      }
    }
  ],
  "users": [
    {
      "id": 12,
      "firstName": "Иван",
      "lastName": "Петров",
      "middleName": "Сергеевич",
      "avatarUrl": "https://example.com/avatar.jpg"
    }
  ]
}
```
            
## Негативные сценарии:
- 204 NoContent: по фильтру не найдено ни одной записи.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `PreferredTechniciansList`.

### `POST /PreferredTechnicians`

## Пример запроса:
`POST /PreferredTechnicians`
            
```json
[
  {
    "assetID": 101,
    "data": [12, 34, 56]
  }
]
```
            
## Пример успешного ответа (202):
Пустое тело ответа.
            
## Негативные сценарии:
- 400 BadRequest: некорректный формат запроса или отсутствуют обязательные поля.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `PreferredTechniciansMerge`.
