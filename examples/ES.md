# ES — примеры

> **Что здесь:** блоки примеров запросов/ответов ручек сервиса ES, вынесенные из `endpoints/ES.md`. Сигнатуры и типы — там же и в `schemas/ES.md`.

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

### `HEAD /Companies`

## Пример запроса:
`HEAD /Companies?searchText=ромашка`
            
## Пример успешного ответа (200):
Заголовок `Content-Range` с общим количеством записей, удовлетворяющих фильтру.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `CompaniesList`.

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

### `HEAD /Locations`

## Пример запроса:
`HEAD /Locations?searchFor=Москва`
            
## Пример успешного ответа (200):
Пустое тело; заголовок `Content-Range` содержит общее количество записей.
            
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `LocationsList`.

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
