# ES — справочник ручек

> **Что здесь:** все ручки сервиса ES (API for managing enterprise structure in HubEx): сигнатуры, параметры, права. Типы — schemas/ES.md. Сгенерировано из swagger.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/ES.md`; грабли — `notes/ES.md` (если есть).
> **Источник:** `snapshots/ES.json` · файл генерируется пайплайном — руками не править.

Base: `{BASE_URL}/ES`

## AssetAttachments
- `POST /AssetAttachments` — Свзяывает объект и вложение
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: AssetActionDataOfInt[] → ResultsAssetAttachmentsPostResult[]
- `DELETE /AssetAttachments` — Помечает связку объекта и вложения как удаленную
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: AssetActionDataOfInt[]
- `POST /AssetAttachments/upload` — Заргужает файл на файловый сервер и привязывает его к объекту. Данные будут получены из формы.
  ← query: AssetID?:int, Description?:str, IsPublic?:bool, IsIgnorePossibleDuplication?:bool, Roles?:int[], Coordinate?:str, FileName?:str, ContentType?:str, Uid?:uuid, ContentStream.CanRead?:bool, ContentStream.CanSeek?:bool, ContentStream.CanWrite?:bool, ContentStream.Capacity?:int, ContentStream.Length?:int, ContentStream.Position?:int, ContentStream.CanTimeout?:bool, ContentStream.ReadTimeout?:int, ContentStream.WriteTimeout?:int, Md5Hash?:str, ContentLength?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: { File: file } → ResultsAssetAttachmentsUploadResult
- `POST /AssetAttachments/upload/fromBody` — Заргужает файл на файловый сервер и привязывает его к объекту. Данные будут получены из тела запроса.
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataAssetAttachmentsAssetBodyUploadData → ResultsAssetAttachmentsUploadResult
- `POST /AssetAttachments/upload/fromForm` — Заргужает файл на файловый сервер и привязывает его к объекту. Данные будут получены из формы.
  ← query: AssetID?:int, Description?:str, IsPublic?:bool, IsIgnorePossibleDuplication?:bool, Roles?:int[], Coordinate?:str, FileName?:str, ContentType?:str, Uid?:uuid, ContentStream.CanRead?:bool, ContentStream.CanSeek?:bool, ContentStream.CanWrite?:bool, ContentStream.Capacity?:int, ContentStream.Length?:int, ContentStream.Position?:int, ContentStream.CanTimeout?:bool, ContentStream.ReadTimeout?:int, ContentStream.WriteTimeout?:int, Md5Hash?:str, ContentLength?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: { File: file } → ResultsAssetAttachmentsUploadResult

## AssetAttributes
- `POST /AssetAttributes` — Обновляет сведения о пользовательских полях объектов
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESAssetAttributeActionData[]
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
- `DELETE /AssetAttributes` — Удаляет явно переданные пользовательские поля объектов (v2)
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESAssetAttributeDeleteActionData[]
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
- `POST /AssetAttributes/v2` — Добавляет пользовательские поля объектов (v2)
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESAssetAttributeActionV2Data[]
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
- `PUT /AssetAttributes/v2` — Обновляет пользовательские поля объектов (v2)
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESAssetAttributeActionV2Data[]
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
- `GET /AssetClasses` — Возвращает список классов объектов.
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsAssetClassesAssetClassListResult>
- `POST /AssetClasses` — Добавляет класс объектов
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESAssetClassAddData[] → ResultsAssetClassesAssetClassAddResult[]
- `PUT /AssetClasses` — Обновляет класс объектов данного тенанта
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESAssetClassUpdateData[]
- `DELETE /AssetClasses` — Помечает классы объектов, как удаленные
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `GET /AssetClasses/{id}` — Возвращает класс объекта
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsAssetClassesAssetClassGetResult
- `DELETE /AssetClasses/{id}` — Помечает класс объектов, как удаленный
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)

## AssetDistricts
- `POST /AssetDistricts` — Добавляет участки к объекту.
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: AssetActionDataOfDistrictData
- `DELETE /AssetDistricts` — Исключает объекту.из участков
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: AssetActionDataOfShort

## AssetFilter
- `GET /AssetFilter` — Возвращает список доступных фильтров для пользователя запросившего данные.
  ← query: selectedOnly?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ProjectionsCOMMONFilterListItemProjection[]
- `PUT /AssetFilter` — Обновляет список доступных, для выполняющего операцию пользователя, фильтров и порядок их сортировки
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: COMMONUIFilterFilterData[]

## AssetListQueries
- `GET /AssetListQueries` — Возвращает список сохраненных запросов, доступных в тенанте
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsAssetListQueriesAssetListQueryResult>[]
- `POST /AssetListQueries` — Создает сохраненный запрос и привязывает его к текущему пользователю
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESAssetListQueryAddData[] → int[]
- `PUT /AssetListQueries` — Изменяет сохраненный запрос
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESAssetListQueryUpdateData[]
- `DELETE /AssetListQueries` — Помечает сохраненные запросы как удаленные
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `DELETE /AssetListQueries/remove` — Удаляет сохраненные запросы
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `GET /AssetListQueries/{id}` — Возвращает сохраненный запрос
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsAssetListQueriesAssetListQueryResult>
- `DELETE /AssetListQueries/{id}` — Помечает сохраненный запрос как удаленный
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `DELETE /AssetListQueries/{id}/remove` — Удаляет сохраненный запрос
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)

## AssetLocations
- `GET /AssetLocations` — Список локаций по объекту
  ← query: assetID?:int, onDate?:datetime; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `POST /AssetLocations` — Добавляет локацию к объекту
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESAssetLocationMergeData
- `PUT /AssetLocations` — Обновление срока нахождения объекта на локации
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESAssetLocationMergeData
- `DELETE /AssetLocations` — Удаление привязки локации к объекту
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataAssetLocationsDeleteData

## AssetSchemas
- `GET /AssetSchemas/ascList/{assetID}` — Возвращает список существующих план-схем для текущего объекта и всех доступных объектов вверх по дереву
  ← path: assetID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsAssetSchemaSchemaBase>
- `GET /AssetSchemas/asset/{assetID}` — Возвращает план-схему привязанную к объекту или ближайшую по дереву сверху
  ← path: assetID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsAssetSchemaSchema
- `POST /AssetSchemas/asset/{assetId}` — Создает план-схему, объект можно задать как через route или через body
Приоритет у значения переданного через route
  ← path: assetId:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ResultsAssetSchemaSchema → IdNameResultOfInt
- `PUT /AssetSchemas/asset/{assetId}` — Изменяет план-схему, объект можно задать как через route или через body
Приоритет у значения переданного через route
  ← path: assetId:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ResultsAssetSchemaSchema
- `GET /AssetSchemas/list` — Возвращает полный список схем тенанта
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsAssetSchemaSchemaBase>
- `GET /AssetSchemas/{schemaID}` — Возвращает план-схему по её уникальному идентификатору
  ← path: schemaId:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsAssetSchemaSchema
- `GET /AssetSchemas/{schemaID}/points` — Возвращает полный список точек-заданий размещённых на план-схеме
  ← path: schemaID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsAssetSchemaSchemaTask[]
- `DELETE /AssetSchemas/{schemaId}` — Помечает план-схему как удаленную
  ← path: schemaId:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `POST /AssetSchemas/{schemaId}/bind` — Позволяет привязать схему к нескольким объектам
  ← path: schemaId:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `GET /AssetSchemas/{schemaId}/image` — Получает информацию о картинке привязанной к план-схеме
  ← path: schemaId:int; query: thumbnailSize?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsAssetSchemaSchemaImage
- `DELETE /AssetSchemas/{schemaId}/image` — Удаляет текущее представление (картинку) ассоциированную с план-схемой
  ← path: schemaId:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `POST /AssetSchemas/{schemaId}/image/attach/{attachmentId}` — Привязать картинку - attachment к план-схеме если аттачмент был загружен через common api
  ← path: schemaId:int, attachmentId:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ResultsAssetSchemaImageSize → ResultsAssetSchemaSchemaBase
- `GET /AssetSchemas/{schemaId}/image/download` — Метод получения TemporaryRedirect на временную ссылку для скачки файла прикреплённой план-схемы
  ← path: schemaId:int; query: thumbnailSize?:int, noRedirect?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `POST /AssetSchemas/{schemaId}/image/upload` — Метод загружает файл на файловый сервер и привязывает его к план-схеме. Данные будут получены из формы.
  ← path: schemaId:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: { Description?: str, IsPublic?: bool, IsIgnorePossibleDuplication?: bool, Roles?: int[], Coordinate?: str, File: file, FileName?: str, ContentType?: str, Uid?: uuid, ContentStream.CanRead?: bool, ContentStream.CanSeek?: bool, ContentStream.CanWrite?: bool, ContentStream.Capacity?: int, ContentStream.Length?: int, ContentStream.Position?: int, ContentStream.CanTimeout?: bool, ContentStream.ReadTimeout?: int, ContentStream.WriteTimeout?: int, Md5Hash?: str, ContentLength?: int } → ResultsAssetSchemaSchemaImageShort
- `POST /AssetSchemas/{schemaId}/points` — Обновляет или добавляет точки на план-схему
  ← path: schemaId:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ResultsAssetSchemaSchemaTask[] → ResultsAssetSchemaSchemaTask[]
- `DELETE /AssetSchemas/{schemaId}/points` — Удалить набор точек-заданий с план-схемы
  ← path: schemaId:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `PUT /AssetSchemas/{schemaId}/unbind` — Позволяет отвязать несколько объектов от схемы
  ← path: schemaId:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[] → ResultsAssetSchemaSchemaTask[]

## AssetSearchSettings
- `GET /AssetSearchSettings` — Получение списка полей поиска объекта для текущего пользователя
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ProjectionsESAssetSearchFieldSettingsProjection[]
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
- `POST /AssetSearchSettings/tenant` — Добавление полей поиска объекта на уровне тенанта
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
  ## Пример запроса:
`POST /AssetSearchSettings/tenant`
            
```json
[1,2,3]
```
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTenantSearchSettingsAdd`.
- `DELETE /AssetSearchSettings/tenant` — Удаление полей поиска объекта на уровне тенанта
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
  ## Пример запроса:
`DELETE /AssetSearchSettings/tenant`
            
```json
[2,3]
```
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTenantSearchSettingsDelete`.
- `POST /AssetSearchSettings/tenantMember` — Добавление полей поиска объекта для текущего пользователя
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
  ## Пример запроса:
`POST /AssetSearchSettings/tenantMember`
            
```json
[1,2]
```
## Негативные сценарии:
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetTenantMemberSearchSettingsAdd`.
- 409 Conflict: поле поиска скрыто для компании (`SearchFieldNotAllowedForTenant`).
- `DELETE /AssetSearchSettings/tenantMember` — Удаление полей поиска объекта для текущего пользователя
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
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
- `POST /AssetSkills` — Добавляет навыки к объектам
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: AssetActionDataOfInt[] → ResultsAssetSkillsPostResult
- `DELETE /AssetSkills` — Удаялет навыки из объектов
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: AssetActionDataOfInt[]

## AssetTags
- `POST /AssetTags` — Добавляет тэги к ассету.
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESAssetTagAddData[] → ResultsAssetTagsAddResult[]
- `DELETE /AssetTags` — Удаляет тэги из ассету.
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESAssetTagDeleteData[] → ResultsAssetTagsAddResult[]

## AssetTemplateAttachments
- `POST /AssetTemplateAttachments` — Свзяывает шаблон объекта и вложение
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: AssetTemplateActionDataOfInt[] → ResultsAssetTemplateAttachmentsPostResult[]
- `DELETE /AssetTemplateAttachments` — Помечает связку шаблона объекта и вложения как удаленную
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: AssetTemplateActionDataOfInt[]
- `POST /AssetTemplateAttachments/upload` — Заргужает файл на файловый сервер и привязывает его к шаблону объекта. Данные будут получены из формы.
  ← query: AssetTemplateID?:int, Description?:str, IsPublic?:bool, IsIgnorePossibleDuplication?:bool, Roles?:int[], Coordinate?:str, FileName?:str, ContentType?:str, Uid?:uuid, ContentStream.CanRead?:bool, ContentStream.CanSeek?:bool, ContentStream.CanWrite?:bool, ContentStream.Capacity?:int, ContentStream.Length?:int, ContentStream.Position?:int, ContentStream.CanTimeout?:bool, ContentStream.ReadTimeout?:int, ContentStream.WriteTimeout?:int, Md5Hash?:str, ContentLength?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: { File: file } → ResultsAssetTemplateAttachmentsUploadResult
- `POST /AssetTemplateAttachments/upload/fromBody` — Заргужает файл на файловый сервер и привязывает его к шаблону объекта. Данные будут получены из тела запроса.
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataAssetTemplateAttachmentsAssetTemplateBodyUploadData → ResultsAssetTemplateAttachmentsUploadResult
- `POST /AssetTemplateAttachments/upload/fromForm` — Заргужает файл на файловый сервер и привязывает его к шаблону объекта. Данные будут получены из формы.
  ← query: AssetTemplateID?:int, Description?:str, IsPublic?:bool, IsIgnorePossibleDuplication?:bool, Roles?:int[], Coordinate?:str, FileName?:str, ContentType?:str, Uid?:uuid, ContentStream.CanRead?:bool, ContentStream.CanSeek?:bool, ContentStream.CanWrite?:bool, ContentStream.Capacity?:int, ContentStream.Length?:int, ContentStream.Position?:int, ContentStream.CanTimeout?:bool, ContentStream.ReadTimeout?:int, ContentStream.WriteTimeout?:int, Md5Hash?:str, ContentLength?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: { File: file } → ResultsAssetTemplateAttachmentsUploadResult

## AssetTemplateAttributes
- `POST /AssetTemplateAttributes` — Обновляет сведения о пользовательских полях шаблонов объектов
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: AssetTemplateActionDataOfMergeData[]

## AssetTemplateDistricts
- `POST /AssetTemplateDistricts` — Добавляет участки к шаблонам объектов
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: AssetTemplateActionDataOfShort[] → InterfacesEntitiesIAssetTemplateDistrictBaseEntity
- `DELETE /AssetTemplateDistricts` — Удаляет участки из шаблонов объектов
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: AssetTemplateActionDataOfShort[]
- `DELETE /AssetTemplateDistricts/{id}` — Удаляет участки из шаблона объекта
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]

## AssetTemplateSkills
- `POST /AssetTemplateSkills` — Добавляет навыки к шаблонам объектов
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: AssetTemplateActionDataOfAddData[] → InterfacesEntitiesIAssetTemplateSkillBaseEntity
- `DELETE /AssetTemplateSkills` — Удаляет участки из шаблонов объектов
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: AssetTemplateActionDataOfInt[]
- `DELETE /AssetTemplateSkills/{id}` — Удаляет навыки из шаблона объекта
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]

## AssetTemplateWorkTypes
- `POST /AssetTemplateWorkTypes` — Добавляет типы работ к шаблонам объектов
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: AssetTemplateActionDataOfShort[] → EntitiesESAssetTemplateWorkTypeBaseEntity
- `DELETE /AssetTemplateWorkTypes` — Удаляет типы работ из шаблонов объектов
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: AssetTemplateActionDataOfShort[]
- `DELETE /AssetTemplateWorkTypes/{id}` — Удаляет типы работ из шаблона объекта
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]

## AssetTemplates
- `GET /AssetTemplates` — Список шаблонов ассета
  ← query: searchText?:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsAssetTemplatesListResult>
- `POST /AssetTemplates` — Добавляет шаблон объекта
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESAssetTemplateAddData[]
- `PUT /AssetTemplates` — Изменяет шаблон объекта
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESAssetTemplateUpdateData[]
- `DELETE /AssetTemplates` — Помечает шаблоны объектов как удаленные
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `DELETE /AssetTemplates/avatar` — Удаляет аватку для указанного списка шаблона объекта.
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `GET /AssetTemplates/{assetTemplateID}/attachments` — Возвращает список файлов вложенных в шаблон объекта.
  ← path: assetTemplateID:int; query: thumbnailSize?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsCommonListAttachmentResult>
- `GET /AssetTemplates/{assetTemplateID}/attachments/{attachmentID}` — Возвращает TemporartRedirect на временную ссылку для скачки файла
  ← path: assetTemplateID:int, attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `GET /AssetTemplates/{assetTemplateID}/attributes` — Возвращает список пользовательских полей шаблонов объектов
  ← path: assetTemplateID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsAssetTemplatesAssetTemplateAttributeResult[]
- `GET /AssetTemplates/{assetTemplateID}/districts` — Возвращает список участков шаблонов объектов
  ← path: assetTemplateID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → int[]
- `GET /AssetTemplates/{assetTemplateID}/skills` — Возвращает список участков шаблонов объектов
  ← path: assetTemplateID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → int[]
- `GET /AssetTemplates/{assetTemplateID}/workTypes` — Возвращает список видов работ шаблонов объектов
  ← path: assetTemplateID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → int[]
- `GET /AssetTemplates/{id}` — Возвращает шаблон объекта
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsAssetTemplatesGetResult
- `DELETE /AssetTemplates/{id}` — Помечает шаблон объекта как удаленный
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `DELETE /AssetTemplates/{id}/avatar` — Удаляет аватарку указаного шаблона объекта.
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `PUT /AssetTemplates/{id}/avatar/upload/fromBody` — Загружает изображение JPG не менее 128x128 используемое в качестве аватарки для указанного шаблона объекта. Данные будут получены из тела запроса (base64).
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataAttachmentsFromBodyUploadData
- `PUT /AssetTemplates/{id}/avatar/upload/fromForm` — Загружает изображение JPG не менее 128x128 используемое в качестве аватарки для указанного шаблона объекта. Данные будут получены из формы.
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: { Description?: str, IsPublic?: bool, IsIgnorePossibleDuplication?: bool, Roles?: int[], Coordinate?: str, File: file, FileName?: str, ContentType?: str, Uid?: uuid, ContentStream.CanRead?: bool, ContentStream.CanSeek?: bool, ContentStream.CanWrite?: bool, ContentStream.Capacity?: int, ContentStream.Length?: int, ContentStream.Position?: int, ContentStream.CanTimeout?: bool, ContentStream.ReadTimeout?: int, ContentStream.WriteTimeout?: int, Md5Hash?: str, ContentLength?: int }

## AssetTypes
- `GET /AssetTypes` — Возвращает список типов объектов
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsAssetTypesGetResult>
- `POST /AssetTypes` — Добавляет тип объекта
  ← query: relatedToAnyWorkType?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESAssetTypeAddData[]
- `PUT /AssetTypes` — Изменяет тип объекта
  ← query: relatedToAnyWorkType?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESAssetTypeUpdateData[]
- `DELETE /AssetTypes` — Помечает типы объектов как удаленные
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `GET /AssetTypes/{id}` — Возвращает тип объекта
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `DELETE /AssetTypes/{id}` — Помечает тип объекта как удаленный
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `GET /AssetTypes/{id}/workTypes` — Возвращает список относящихся к типу объекта видов работ
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `POST /AssetTypes/{id}/workTypes` — Привязать список видов работ к типу объекта
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `DELETE /AssetTypes/{id}/workTypes` — Удалить привязку видов работ к типу объекта
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]

## AssetWorkTypes
- `POST /AssetWorkTypes` — Добавляет типы работ к ассету.
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: AssetActionDataOfShort → ProjectionsESAssetWorkTypeProjection[]
- `DELETE /AssetWorkTypes` — Отвязывает типы работ от ассета.
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: AssetActionDataOfShort → ProjectionsESAssetWorkTypeProjection[]

## Assets
- `GET /Assets` — Возращает справочник объектов                     , доступных пользователю
  ← query: includePath?:bool, includeTaskActuality?:bool, searchText?:str, needForAllowedTasks?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsAssetsAssetExtResult>
- `POST /Assets` — Создает объект
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESAssetAddData → IdNameResultOfInt
- `PUT /Assets` — Массовое изменение объектов
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESAssetMassiveUpdateData
- `DELETE /Assets` — Помечает объекты как удаленные
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `HEAD /Assets` — Возвращает заголовок запроса пользователей с количеством данных, удовлетворяющих фильтру
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `GET /Assets/attributes` — Возвращает список атрибутов по объектам
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsAssetsAssetAttributesExtResult[]
- `DELETE /Assets/avatar` — Удаляет аватку для указанного списка объекта.
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `POST /Assets/contacts` — Добавляет контактные лица для объектов
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: AssetActionDataOfInt[] → ResultsAssetContactsPostResult
- `DELETE /Assets/contacts` — Удаляет контактные лица у объектов
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: AssetActionDataOfInt[]
- `DELETE /Assets/full` — Помечает объекты и все их дочерние объекты как удаленные
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `PUT /Assets/restore` — Воскрешает удаленные объекты
  ← query: withNested?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `GET /Assets/root` — Возращает справочник корневых объектов, доступных пользователю.
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsAssetsAssetExtResult>
- `GET /Assets/{assetID}` — Детальная информация по объекту
  ← path: assetID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsAssetsAssetDetailedInfoResult
- `PUT /Assets/{assetID}` — Изменяет объект
  ← path: assetID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESAssetUpdateData
- `DELETE /Assets/{assetID}` — Помечает объект как удаленный
  ← path: assetID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `GET /Assets/{assetID}/assignments` — Возвращает список назначений заданного объекта для пользователей
  ← path: assetID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsAssetsAssetAssignmentResult[]
- `GET /Assets/{assetID}/attachments` — Возвращает список файлов вложенных в объект.
  ← path: assetID:int; query: thumbnailSize?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsCommonListAttachmentResult>
- `GET /Assets/{assetID}/attachments/{attachmentID}` — Возвращает TemporartRedirect на временную ссылку для скачки файла
  ← path: assetID:int, attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `GET /Assets/{assetID}/attributes` — Возвращает список пользовтельских полей по объекту
  ← path: assetID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsAssetsAssetAttributeResult[]
- `GET /Assets/{assetID}/checkLists` — Возвращает список чек-листов объекта
  ← path: assetID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsAssetCheckListsGetResult[]>
- `POST /Assets/{assetID}/checkLists` — Добавляет чек-листы к объекту
  ← path: assetID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `DELETE /Assets/{assetID}/checkLists` — Помечает чек-листы у объекта как удаленные
  ← path: assetID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `POST /Assets/{assetID}/checkLists/{checkListID}` — Добавляет чек-лист к объекту
  ← path: assetID:int, checkListID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `DELETE /Assets/{assetID}/checkLists/{checkListID}` — Помечает чек-лист у объекта как удаленный
  ← path: assetID:int, checkListID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `GET /Assets/{assetID}/contacts` — Возвращает список действующих контактов для объекта
  ← path: assetID:int; query: searchText?:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsAssetContactsListResult[]
- `GET /Assets/{assetID}/contacts/{contactID}` — Возвращает контакт объекта
  ← path: assetID:int, contactID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsAssetContactsGetResult
- `POST /Assets/{assetID}/contacts/{contactID}` — Добавляет контактное лицо для объекта
  ← path: assetID:int, contactID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsAssetContactsPostResult
- `DELETE /Assets/{assetID}/contacts/{contactID}` — Удаляет контактное лицо у объекта
  ← path: assetID:int, contactID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `GET /Assets/{assetID}/districts` — Возвращае список участков для объекта.
  ← path: assetID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsCommonAssetDistrictResult[]
- `DELETE /Assets/{assetID}/full` — Помечает объект и все дочерние объекты как удаленные
  ← path: assetID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `GET /Assets/{assetID}/locations/actual` — Возвращает текущее местоположение объекта
  ← path: assetID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsCommonLocationResult
- `PUT /Assets/{assetID}/publish` — Метод публикации объекта
  ← path: assetID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `GET /Assets/{assetID}/skills` — Возвращает список навыков объекта
  ← path: assetID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsAssetSkillsAssetSkillResult>
- `GET /Assets/{assetID}/tags` — Возвращает список активных (не удаленых) тэгов по объекту.
  ← path: assetID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → str[]
- `PUT /Assets/{assetID}/unpublish` — Метод отмены публикации объекта
  ← path: assetID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `GET /Assets/{assetID}/workTypes` — Возвращае список доступных по объекту видов работ.
  ← path: assetID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsAssetsAssetWorkTypeResult>
- `DELETE /Assets/{id}/avatar` — Удаляет аватку указаного объекта.
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `PUT /Assets/{id}/avatar/upload/fromBody` — Загружает изображение JPG не менее 128x128 используемое в качестве аватарки для указанного объекта. Данные будут получены из тела запроса (base64).
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataAttachmentsFromBodyUploadData
- `PUT /Assets/{id}/avatar/upload/fromForm` — Загружает изображение JPG не менее 128x128 используемое в качестве аватарки для указанного объекта. Данные будут получены из формы.
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: { Description?: str, IsPublic?: bool, IsIgnorePossibleDuplication?: bool, Roles?: int[], Coordinate?: str, File: file, FileName?: str, ContentType?: str, Uid?: uuid, ContentStream.CanRead?: bool, ContentStream.CanSeek?: bool, ContentStream.CanWrite?: bool, ContentStream.Capacity?: int, ContentStream.Length?: int, ContentStream.Position?: int, ContentStream.CanTimeout?: bool, ContentStream.ReadTimeout?: int, ContentStream.WriteTimeout?: int, Md5Hash?: str, ContentLength?: int }
- `GET /Assets/{parentAssetID}/assets` — Возращает справочник дочерних объектов (один уровень иерархии), 
доступных пользователю.
  ← path: parentAssetID:int; query: searchText?:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsAssetsAssetExtResult>
- `GET /Assets/{parentAssetID}/assets/all` — Возращает справочник всех дочерних объектов (вниз по иерархии до самого нижнего уровня), 
доступных пользователю.
  ← path: parentAssetID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsAssetsAssetExtResult>

## Companies
- `GET /Companies` — Возвращает список доступных пользователю компаний.
  ← query: searchText?:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsCompaniesListResult>
- `POST /Companies` — Добавляет компанию
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESCompanyAddData[] → int[]
- `PUT /Companies` — Изменяет компанию
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESCompanyUpdateData[]
- `DELETE /Companies` — Помечает компании как удаленные
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `HEAD /Companies` — Возвращает заголовок запроса доступных пользователю компаний с количеством данных, удовлетворяющих фильтру
  ← query: searchText?:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `POST /Companies/contacts` — Добавляет контактные лица к компании
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: CompanyActionDataOfInt[] → ResultsCompanyContactsPostResult
- `DELETE /Companies/contacts` — Удаляет контактные лица у компании
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: CompanyActionDataOfInt[]
- `GET /Companies/dadata/find` — Поиск информации о компании по ИНН.
  ← query: inn?:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ESCompanyAddData
- `PUT /Companies/restore` — Воскрешает удаленные компании
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `GET /Companies/{CompanyID}/attachments/{attachmentID}` — Возвращает TemporartRedirect на временную ссылку для скачки файла
  ← path: companyID:int, attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `GET /Companies/{companyID}/attachment/{attachmentID}` — Прикрепленный файл к компании
<param name="companyID">Идентификатор компании</param><param name="attachmentID">Идентификатор прикрепленного файла к компании</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз из доступных)</param>
  ← path: companyID:int, attachmentID:int; query: thumbnailSize?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsCommonGetAttachmentResult
- `GET /Companies/{companyID}/attachments` — Возвращает список файлов вложенных в компанию.
  ← path: companyID:int; query: thumbnailSize?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsCommonListAttachmentResult>
- `GET /Companies/{companyID}/attributes` — Возвращает список пользовательских атрибутов компании
  ← path: companyID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsCompanyAttributesCompanyAttributeResult[]
- `POST /Companies/{companyID}/attributes` — Обновляет сведения о пользовательских полях в компании
  ← path: companyID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataCompanyAttributeAttributeUpdateData[]
- `GET /Companies/{companyID}/bankAccounts` — Возвращает список банковских счетов компании
  ← path: companyID:int; query: searchText?:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsCompanyBankAccountsListResult>
- `POST /Companies/{companyID}/bankAccounts` — Добавляет банковские счета компании
  ← path: companyID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESCompanyBankAccountAddData[] → ResultsCompanyBankAccountsPostResult
- `PUT /Companies/{companyID}/bankAccounts` — Обновляет банковские счета компании
  ← path: companyID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESCompanyBankAccountUpdateData[]
- `DELETE /Companies/{companyID}/bankAccounts` — Удаляет банковские счета компании
  ← path: companyID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `DELETE /Companies/{companyID}/bankAccounts/{bankAccountID}` — Удаляет банковский счёт компании
  ← path: companyID:int, bankAccountID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `GET /Companies/{companyID}/contacts` — Возвращает список контактов компании
  ← path: companyID:int; query: searchText?:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsCompanyContactsListResult>
- `GET /Companies/{companyID}/contacts/{contactID}` — Возвращает контакт компании
  ← path: companyID:int, contactID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsCompanyContactsGetResult
- `POST /Companies/{companyID}/contacts/{contactID}` — Добавляет контактное лицо к компании
  ← path: companyID:int, contactID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsCompanyContactsPostResult
- `DELETE /Companies/{companyID}/contacts/{contactID}` — Удаляет контактное лицо у компании
  ← path: companyID:int, contactID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `GET /Companies/{companyID}/locations/actual` — Возвращает текущее местоположение компании
  ← path: companyID:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsCommonLocationResult
- `GET /Companies/{id}` — Возвращает доступную пользователю компанию по идентификатору
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsCompaniesGetResult
- `DELETE /Companies/{id}` — Помечает компании как удаленные
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)

## CompanyAttachments
- `POST /CompanyAttachments` — Связывает компанию и вложение
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: CompanyActionDataOfInt[] → ResultsCompanyAttachmentsAddResult[]
- `DELETE /CompanyAttachments` — Помечает связку компании и вложения как удаленную
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: CompanyActionDataOfInt[]
- `POST /CompanyAttachments/upload/fromBody` — Загружает файл на файловый сервер и привязывает его к компании. Данные будут получены из тела запроса.
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataCompanyAttachmentCompanyBodyUploadData → ResultsCompanyAttachmentsUploadResult
- `POST /CompanyAttachments/upload/fromForm` — Загружает файл на файловый сервер и привязывает его к компании. Данные будут получены из формы.
  ← query: CompanyID?:int, Description?:str, IsPublic?:bool, IsIgnorePossibleDuplication?:bool, Roles?:int[], Coordinate?:str, FileName?:str, ContentType?:str, Uid?:uuid, ContentStream.CanRead?:bool, ContentStream.CanSeek?:bool, ContentStream.CanWrite?:bool, ContentStream.Capacity?:int, ContentStream.Length?:int, ContentStream.Position?:int, ContentStream.CanTimeout?:bool, ContentStream.ReadTimeout?:int, ContentStream.WriteTimeout?:int, Md5Hash?:str, ContentLength?:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: { File: file } → ResultsCompanyAttachmentsUploadResult

## CompanyContacts
- `POST /CompanyContacts` — Добавляет контактные лица к компании
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: CompanyActionDataOfInt[] → ResultsCompanyContactsPostResult
- `DELETE /CompanyContacts` — Удаляет контактные лица у компании
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: CompanyActionDataOfInt[]

## CompanyListQueries
- `GET /CompanyListQueries` — Возвращает список сохраненных запросов, доступных в тенанте
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsCompanyListQueriesCompanyListQueryResult>
- `POST /CompanyListQueries` — Создает сохраненный запрос и привязывает его к текущему пользователю
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESCompanyListQueryAddData[] → int[]
- `PUT /CompanyListQueries` — Изменяет сохраненный запрос
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESCompanyListQueryUpdateData[]
- `DELETE /CompanyListQueries` — Помечает сохраненные запросы как удаленные
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `DELETE /CompanyListQueries/remove` — Удаляет сохраненные запросы
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `GET /CompanyListQueries/{id}` — Возвращает сохраненный запрос
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsCompanyListQueriesCompanyListQueryGetResult
- `DELETE /CompanyListQueries/{id}` — Помечает сохраненный запрос как удаленный
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `DELETE /CompanyListQueries/{id}/remove` — Удаляет сохраненный запрос
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)

## CompanyLocations
- `GET /CompanyLocations` — Список локаций по компании
  ← query: companyID?:int, onDate?:datetime; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `POST /CompanyLocations` — Добавляет локацию к компании
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESCompanyLocationMergeData
- `PUT /CompanyLocations` — Обновление локации у компании
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESCompanyLocationMergeData
- `DELETE /CompanyLocations` — Удаление привязки локации к компании
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataCompanyLocationsDeleteData

## CompanyRegistrationTypes
- `GET /CompanyRegistrationTypes` — Возвращает список видов регистрации компании
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsCompanyRegistrationTypesListResult>

## Districts
- `GET /Districts` — Возвращает список доступных пользователю участков.
  ← query: includePath?:bool; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsDistrictsDistrictListForTenantMemberResult[]
- `POST /Districts` — Добавляет участок
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESDistrictAddData[] → int[]
- `PUT /Districts` — Изменяет участок
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESDistrictUpdateData[]
- `DELETE /Districts` — Помечает участки как удаленные
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `PUT /Districts/parentAndReorder` — Изменяет родителя и/или сортировку участка
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: ESDistrictParentUpdateData
- `GET /Districts/{id}` — Возвращает доступный пользователю участок по идентификатору
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsDistrictsDistrictResult
- `DELETE /Districts/{id}` — Помечает участки как удаленные
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)

## Locations
- `GET /Locations` — Возвращает список локаций
  ← query: searchText?:str, searchFor?:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsCommonLocationResult>
- `POST /Locations` — Создает локации.
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataLocationsPostData[] → int[]
- `PUT /Locations` — Изменяет локации.
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: DataLocationsPutData[]
- `DELETE /Locations` — Помечает локации как удаленные.
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `HEAD /Locations` — Возвращает количество локаций
  ← query: searchFor?:str; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `DELETE /Locations/remove` — Удаляет локации.
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: int[]
- `GET /Locations/{id}` — Возвращает локацию с областью.
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → map<ResultsLocationsLocationGetResult>
- `DELETE /Locations/{id}` — Помечает локации как удаленные.
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `DELETE /Locations/{id}/remove` — Удаляет локацию.
  ← path: id:int; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)

## OrgUnits
- `GET /OrgUnits` — Возращает справочник активных (не архивных и не удаленных) организационных единиц,
доступных пользователю.
  ← query: companyID?:int[]; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `GET /OrgUnits/root` — Возращает справочник активных (не архивных и не удаленных) корневых организационных единиц,
доступных пользователю.
  ← query: companyID?:int[]; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)
- `GET /OrgUnits/{id}/orgunits` — Возращает справочник активных (не архивных и не удаленных) организационных единиц,
доступных пользователю.
  ← path: id:int; query: companyID?:int[]; header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb)

## PreferredTechnicians
- `GET /PreferredTechnicians` — Список предпочтительных исполнителей для объектa(ов)
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb) → ResultsAssetsAssetDetailedInfoResult
- `POST /PreferredTechnicians` — Добавление или удаление предпочтительного исполнителя для объекта
  ← header: X-Application-ID?:enum(1=EngineerMobile, 2=CustomerMobile, 3=MainWeb, 4=AdminWeb, 5=Api, 6=PlateWeb); body: AssetActionDataOfInt[]
