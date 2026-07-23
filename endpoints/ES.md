# ES — справочник ручек

> **Что здесь:** все ручки сервиса ES (API for managing enterprise structure in HubEx): сигнатуры, параметры, права. Типы — schemas/ES.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/ES.md`; грабли — `notes/ES.md` (если есть).

Base: `{BASE_URL}/ES`
> Примеры ответов вынесены в [../examples/ES.md](../examples/ES.md).

**Оглавление**

- AssetAttachments — строки 42–52
- AssetAttributes — строки 54–62
- AssetClasses — строки 64–76
- AssetDistricts — строки 78–82
- AssetFilter — строки 84–88
- AssetListQueries — строки 90–106
- AssetLocations — строки 108–116
- AssetSchemas — строки 118–154
- AssetSearchSettings — строки 156–166
- AssetSkills — строки 168–172
- AssetTags — строки 174–178
- AssetTemplateAttachments — строки 180–190
- AssetTemplateAttributes — строки 192–194
- AssetTemplateDistricts — строки 196–202
- AssetTemplateSkills — строки 204–210
- AssetTemplateWorkTypes — строки 212–218
- AssetTemplates — строки 220–252
- AssetTypes — строки 254–272
- AssetWorkTypes — строки 274–278
- Assets — строки 280–370
- Companies — строки 372–425
- CompanyAttachments — строки 427–435
- CompanyContacts — строки 437–441
- CompanyListQueries — строки 443–459
- CompanyLocations — строки 461–469
- CompanyRegistrationTypes — строки 471–473
- Districts — строки 475–489
- Locations — строки 491–509
- OrgUnits — строки 511–520
- PreferredTechnicians — строки 522–526

## AssetAttachments
- `POST /AssetAttachments` — Свзяывает объект и вложение · коды: 201
  ← body: AssetActionDataOfInt[] → ResultsAssetAttachmentsPostResult[]
- `DELETE /AssetAttachments` — Помечает связку объекта и вложения как удаленную · коды: 202
  ← body: AssetActionDataOfInt[]
- `POST /AssetAttachments/upload` — Заргужает файл на файловый сервер и привязывает его к объекту. Данные будут получены из формы. · коды: 201
  ← query: AssetID?:int, Description?:str, IsPublic?:bool, IsIgnorePossibleDuplication?:bool, Roles?:int[], Coordinate?:str, FileName?:str, ContentType?:str, Uid?:uuid, ContentStream.CanRead?:bool, ContentStream.CanSeek?:bool, ContentStream.CanWrite?:bool, ContentStream.Capacity?:int, ContentStream.Length?:int, ContentStream.Position?:int, ContentStream.CanTimeout?:bool, ContentStream.ReadTimeout?:int, ContentStream.WriteTimeout?:int, Md5Hash?:str, ContentLength?:int; body: { File: file } → ResultsAssetAttachmentsUploadResult
- `POST /AssetAttachments/upload/fromBody` — Заргужает файл на файловый сервер и привязывает его к объекту. Данные будут получены из тела запроса. · коды: 201
  ← body: DataAssetAttachmentsAssetBodyUploadData → ResultsAssetAttachmentsUploadResult
- `POST /AssetAttachments/upload/fromForm` — Заргужает файл на файловый сервер и привязывает его к объекту. Данные будут получены из формы. · коды: 201
  ← query: AssetID?:int, Description?:str, IsPublic?:bool, IsIgnorePossibleDuplication?:bool, Roles?:int[], Coordinate?:str, FileName?:str, ContentType?:str, Uid?:uuid, ContentStream.CanRead?:bool, ContentStream.CanSeek?:bool, ContentStream.CanWrite?:bool, ContentStream.Capacity?:int, ContentStream.Length?:int, ContentStream.Position?:int, ContentStream.CanTimeout?:bool, ContentStream.ReadTimeout?:int, ContentStream.WriteTimeout?:int, Md5Hash?:str, ContentLength?:int; body: { File: file } → ResultsAssetAttachmentsUploadResult

## AssetAttributes
- `POST /AssetAttributes` — Обновляет сведения о пользовательских полях объектов · коды: 202, 400 · примеры
  ← body: ESAssetAttributeActionData[]
- `DELETE /AssetAttributes` — Удаляет явно переданные пользовательские поля объектов (v2) · коды: 202, 400 · примеры
  ← body: ESAssetAttributeDeleteActionData[] → ResultsAssetAttributesAssetAttributeRejectedResult[]
- `POST /AssetAttributes/v2` — Добавляет пользовательские поля объектов (v2) · коды: 202, 400 · примеры
  ← body: ESAssetAttributeActionV2Data[] → ResultsAssetAttributesAssetAttributeRejectedResult[]
- `PUT /AssetAttributes/v2` — Обновляет пользовательские поля объектов (v2) · коды: 202, 400 · примеры
  ← body: ESAssetAttributeActionV2Data[] → ResultsAssetAttributesAssetAttributeRejectedResult[]

## AssetClasses
- `GET /AssetClasses` — Возвращает список классов объектов. · коды: 200, 500
  → map<ResultsAssetClassesAssetClassListResult>
- `POST /AssetClasses` — Добавляет класс объектов · коды: 201
  ← body: ESAssetClassAddData[] → ResultsAssetClassesAssetClassAddResult[]
- `PUT /AssetClasses` — Обновляет класс объектов данного тенанта · коды: 202
  ← body: ESAssetClassUpdateData[]
- `DELETE /AssetClasses` — Помечает классы объектов, как удаленные · коды: 202
  ← body: int[]
- `GET /AssetClasses/{id}` — Возвращает класс объекта · коды: 200
  ← path: id:int → ResultsAssetClassesAssetClassGetResult
- `DELETE /AssetClasses/{id}` — Помечает класс объектов, как удаленный · коды: 202, 409
  ← path: id:int

## AssetDistricts
- `POST /AssetDistricts` — Добавляет участки к объекту. · коды: 201, 409
  ← body: AssetActionDataOfDistrictData
- `DELETE /AssetDistricts` — Исключает объекту.из участков · коды: 202, 409
  ← body: AssetActionDataOfShort

## AssetFilter
- `GET /AssetFilter` — Возвращает список доступных фильтров для пользователя запросившего данные. · коды: 200
  ← query: selectedOnly?:bool → ProjectionsCOMMONFilterListItemProjection[]
- `PUT /AssetFilter` — Обновляет список доступных, для выполняющего операцию пользователя, фильтров и порядок их сортировки · коды: 202
  ← body: COMMONUIFilterFilterData[]

## AssetListQueries
- `GET /AssetListQueries` — Возвращает список сохраненных запросов, доступных в тенанте · коды: 200
  → map<ResultsAssetListQueriesAssetListQueryResult>[]
- `POST /AssetListQueries` — Создает сохраненный запрос и привязывает его к текущему пользователю · коды: 201
  ← body: ESAssetListQueryAddData[] → int[]
- `PUT /AssetListQueries` — Изменяет сохраненный запрос · коды: 202
  ← body: ESAssetListQueryUpdateData[]
- `DELETE /AssetListQueries` — Помечает сохраненные запросы как удаленные · коды: 202
  ← body: int[]
- `DELETE /AssetListQueries/remove` — Удаляет сохраненные запросы · коды: 202
  ← body: int[]
- `GET /AssetListQueries/{id}` — Возвращает сохраненный запрос · коды: 200
  ← path: id:int → map<ResultsAssetListQueriesAssetListQueryResult>
- `DELETE /AssetListQueries/{id}` — Помечает сохраненный запрос как удаленный · коды: 202
  ← path: id:int
- `DELETE /AssetListQueries/{id}/remove` — Удаляет сохраненный запрос · коды: 202
  ← path: id:int

## AssetLocations
- `GET /AssetLocations` — Список локаций по объекту · коды: 200, 409
  ← query: assetID?:int, onDate?:datetime
- `POST /AssetLocations` — Добавляет локацию к объекту · коды: 202
  ← body: ESAssetLocationMergeData
- `PUT /AssetLocations` — Обновление срока нахождения объекта на локации · коды: 202
  ← body: ESAssetLocationMergeData
- `DELETE /AssetLocations` — Удаление привязки локации к объекту · коды: 202
  ← body: DataAssetLocationsDeleteData

## AssetSchemas
- `GET /AssetSchemas/ascList/{assetID}` — Возвращает список существующих план-схем для текущего объекта и всех доступных объектов вверх по дереву · коды: 200, 400
  ← path: assetID:int → map<ResultsAssetSchemaSchemaBase>
- `GET /AssetSchemas/asset/{assetID}` — Возвращает план-схему привязанную к объекту или ближайшую по дереву сверху · коды: 200, 400
  ← path: assetID:int → ResultsAssetSchemaSchema
- `POST /AssetSchemas/asset/{assetId}` — Создает план-схему, объект можно задать как через route или через body
Приоритет у значения переданного через route · коды: 201, 409
  ← path: assetId:int; body: ResultsAssetSchemaSchema → IdNameResultOfInt
- `PUT /AssetSchemas/asset/{assetId}` — Изменяет план-схему, объект можно задать как через route или через body
Приоритет у значения переданного через route · коды: 202, 409
  ← path: assetId:int; body: ResultsAssetSchemaSchema → IdNameResultOfInt
- `GET /AssetSchemas/list` — Возвращает полный список схем тенанта · коды: 200, 400
  → map<ResultsAssetSchemaSchemaBase>
- `GET /AssetSchemas/{schemaID}` — Возвращает план-схему по её уникальному идентификатору · коды: 200, 400
  ← path: schemaId:int → ResultsAssetSchemaSchema
- `GET /AssetSchemas/{schemaID}/points` — Возвращает полный список точек-заданий размещённых на план-схеме · коды: 200
  ← path: schemaID:int → ResultsAssetSchemaSchemaTask[]
- `DELETE /AssetSchemas/{schemaId}` — Помечает план-схему как удаленную · коды: 202, 409
  ← path: schemaId:int
- `POST /AssetSchemas/{schemaId}/bind` — Позволяет привязать схему к нескольким объектам · коды: 409
  ← path: schemaId:int; body: int[]
- `GET /AssetSchemas/{schemaId}/image` — Получает информацию о картинке привязанной к план-схеме · коды: 200, 500
  ← path: schemaId:int; query: thumbnailSize?:int → ResultsAssetSchemaSchemaImage
- `DELETE /AssetSchemas/{schemaId}/image` — Удаляет текущее представление (картинку) ассоциированную с план-схемой · коды: 202, 409
  ← path: schemaId:int
- `POST /AssetSchemas/{schemaId}/image/attach/{attachmentId}` — Привязать картинку - attachment к план-схеме если аттачмент был загружен через common api · коды: 201, 500
  ← path: schemaId:int, attachmentId:int; body: ResultsAssetSchemaImageSize → ResultsAssetSchemaSchemaBase
- `GET /AssetSchemas/{schemaId}/image/download` — Метод получения TemporaryRedirect на временную ссылку для скачки файла прикреплённой план-схемы · коды: 303
  ← path: schemaId:int; query: thumbnailSize?:int, noRedirect?:bool
- `POST /AssetSchemas/{schemaId}/image/upload` — Метод загружает файл на файловый сервер и привязывает его к план-схеме. Данные будут получены из формы. · коды: 201, 500
  ← path: schemaId:int; body: { ContentLength?: int, ContentStream.CanRead?: bool, ContentStream.CanSeek?: bool, ContentStream.CanTimeout?: bool, ContentStream.CanWrite?: bool, ContentStream.Capacity?: int, ContentStream.Length?: int, ContentStream.Position?: int, ContentStream.ReadTimeout?: int, ContentStream.WriteTimeout?: int, ContentType?: str, Coordinate?: str, Description?: str, File: file, FileName?: str, IsIgnorePossibleDuplication?: bool, IsPublic?: bool, Md5Hash?: str, Roles?: int[], Uid?: uuid } → ResultsAssetSchemaSchemaImageShort
- `POST /AssetSchemas/{schemaId}/points` — Обновляет или добавляет точки на план-схему · коды: 200, 409
  ← path: schemaId:int; body: ResultsAssetSchemaSchemaTask[] → ResultsAssetSchemaSchemaTask[]
- `DELETE /AssetSchemas/{schemaId}/points` — Удалить набор точек-заданий с план-схемы · коды: 202, 409
  ← path: schemaId:int; body: int[]
- `PUT /AssetSchemas/{schemaId}/unbind` — Позволяет отвязать несколько объектов от схемы · коды: 200, 409
  ← path: schemaId:int; body: int[] → ResultsAssetSchemaSchemaTask[]

## AssetSearchSettings
- `GET /AssetSearchSettings` — Получение списка полей поиска объекта для текущего пользователя · коды: 200, 204 · примеры
  → ProjectionsESAssetSearchFieldSettingsProjection[]
- `POST /AssetSearchSettings/tenant` — Добавление полей поиска объекта на уровне тенанта · коды: 202 · примеры
  ← body: int[]
- `DELETE /AssetSearchSettings/tenant` — Удаление полей поиска объекта на уровне тенанта · коды: 202 · примеры
  ← body: int[]
- `POST /AssetSearchSettings/tenantMember` — Добавление полей поиска объекта для текущего пользователя · коды: 202, 409 · примеры
  ← body: int[]
- `DELETE /AssetSearchSettings/tenantMember` — Удаление полей поиска объекта для текущего пользователя · коды: 202, 409 · примеры
  ← body: int[]

## AssetSkills
- `POST /AssetSkills` — Добавляет навыки к объектам · коды: 201, 409
  ← body: AssetActionDataOfInt[] → ResultsAssetSkillsPostResult
- `DELETE /AssetSkills` — Удаялет навыки из объектов · коды: 202, 409
  ← body: AssetActionDataOfInt[]

## AssetTags
- `POST /AssetTags` — Добавляет тэги к ассету. · коды: 201, 409
  ← body: ESAssetTagAddData[] → ResultsAssetTagsAddResult[]
- `DELETE /AssetTags` — Удаляет тэги из ассету. · коды: 200, 400
  ← body: ESAssetTagDeleteData[] → ResultsAssetTagsAddResult[]

## AssetTemplateAttachments
- `POST /AssetTemplateAttachments` — Свзяывает шаблон объекта и вложение · коды: 201
  ← body: AssetTemplateActionDataOfInt[] → ResultsAssetTemplateAttachmentsPostResult[]
- `DELETE /AssetTemplateAttachments` — Помечает связку шаблона объекта и вложения как удаленную · коды: 202
  ← body: AssetTemplateActionDataOfInt[]
- `POST /AssetTemplateAttachments/upload` — Заргужает файл на файловый сервер и привязывает его к шаблону объекта. Данные будут получены из формы. · коды: 201
  ← query: AssetTemplateID?:int, Description?:str, IsPublic?:bool, IsIgnorePossibleDuplication?:bool, Roles?:int[], Coordinate?:str, FileName?:str, ContentType?:str, Uid?:uuid, ContentStream.CanRead?:bool, ContentStream.CanSeek?:bool, ContentStream.CanWrite?:bool, ContentStream.Capacity?:int, ContentStream.Length?:int, ContentStream.Position?:int, ContentStream.CanTimeout?:bool, ContentStream.ReadTimeout?:int, ContentStream.WriteTimeout?:int, Md5Hash?:str, ContentLength?:int; body: { File: file } → ResultsAssetTemplateAttachmentsUploadResult
- `POST /AssetTemplateAttachments/upload/fromBody` — Заргужает файл на файловый сервер и привязывает его к шаблону объекта. Данные будут получены из тела запроса. · коды: 201
  ← body: DataAssetTemplateAttachmentsAssetTemplateBodyUploadData → ResultsAssetTemplateAttachmentsUploadResult
- `POST /AssetTemplateAttachments/upload/fromForm` — Заргужает файл на файловый сервер и привязывает его к шаблону объекта. Данные будут получены из формы. · коды: 201
  ← query: AssetTemplateID?:int, Description?:str, IsPublic?:bool, IsIgnorePossibleDuplication?:bool, Roles?:int[], Coordinate?:str, FileName?:str, ContentType?:str, Uid?:uuid, ContentStream.CanRead?:bool, ContentStream.CanSeek?:bool, ContentStream.CanWrite?:bool, ContentStream.Capacity?:int, ContentStream.Length?:int, ContentStream.Position?:int, ContentStream.CanTimeout?:bool, ContentStream.ReadTimeout?:int, ContentStream.WriteTimeout?:int, Md5Hash?:str, ContentLength?:int; body: { File: file } → ResultsAssetTemplateAttachmentsUploadResult

## AssetTemplateAttributes
- `POST /AssetTemplateAttributes` — Обновляет сведения о пользовательских полях шаблонов объектов · коды: 202
  ← body: AssetTemplateActionDataOfMergeData[]

## AssetTemplateDistricts
- `POST /AssetTemplateDistricts` — Добавляет участки к шаблонам объектов · коды: 201, 409
  ← body: AssetTemplateActionDataOfShort[] → InterfacesEntitiesIAssetTemplateDistrictBaseEntity
- `DELETE /AssetTemplateDistricts` — Удаляет участки из шаблонов объектов · коды: 202, 409
  ← body: AssetTemplateActionDataOfShort[]
- `DELETE /AssetTemplateDistricts/{id}` — Удаляет участки из шаблона объекта · коды: 202, 409
  ← path: id:int; body: int[]

## AssetTemplateSkills
- `POST /AssetTemplateSkills` — Добавляет навыки к шаблонам объектов · коды: 201, 409
  ← body: AssetTemplateActionDataOfAddData[] → InterfacesEntitiesIAssetTemplateSkillBaseEntity
- `DELETE /AssetTemplateSkills` — Удаляет участки из шаблонов объектов · коды: 202, 409
  ← body: AssetTemplateActionDataOfInt[]
- `DELETE /AssetTemplateSkills/{id}` — Удаляет навыки из шаблона объекта · коды: 202, 409
  ← path: id:int; body: int[]

## AssetTemplateWorkTypes
- `POST /AssetTemplateWorkTypes` — Добавляет типы работ к шаблонам объектов · коды: 201, 409
  ← body: AssetTemplateActionDataOfShort[] → EntitiesESAssetTemplateWorkTypeBaseEntity
- `DELETE /AssetTemplateWorkTypes` — Удаляет типы работ из шаблонов объектов · коды: 202, 409
  ← body: AssetTemplateActionDataOfShort[]
- `DELETE /AssetTemplateWorkTypes/{id}` — Удаляет типы работ из шаблона объекта · коды: 202, 409
  ← path: id:int; body: int[]

## AssetTemplates
- `GET /AssetTemplates` — Список шаблонов ассета · коды: 200
  ← query: searchText?:str → map<ResultsAssetTemplatesListResult>
- `POST /AssetTemplates` — Добавляет шаблон объекта · коды: 201, 409
  ← body: ESAssetTemplateAddData[]
- `PUT /AssetTemplates` — Изменяет шаблон объекта · коды: 202, 409
  ← body: ESAssetTemplateUpdateData[]
- `DELETE /AssetTemplates` — Помечает шаблоны объектов как удаленные · коды: 202, 409
  ← body: int[]
- `DELETE /AssetTemplates/avatar` — Удаляет аватку для указанного списка шаблона объекта. · коды: 202
  ← body: int[]
- `GET /AssetTemplates/{assetTemplateID}/attachments` — Возвращает список файлов вложенных в шаблон объекта. · коды: 200, 400
  ← path: assetTemplateID:int; query: thumbnailSize?:int → map<ResultsCommonListAttachmentResult>
- `GET /AssetTemplates/{assetTemplateID}/attachments/{attachmentID}` — Возвращает TemporartRedirect на временную ссылку для скачки файла · коды: 307
  ← path: assetTemplateID:int, attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /AssetTemplates/{assetTemplateID}/attributes` — Возвращает список пользовательских полей шаблонов объектов · коды: 200, 400
  ← path: assetTemplateID:int → ResultsAssetTemplatesAssetTemplateAttributeResult[]
- `GET /AssetTemplates/{assetTemplateID}/districts` — Возвращает список участков шаблонов объектов · коды: 200, 400
  ← path: assetTemplateID:int → int[]
- `GET /AssetTemplates/{assetTemplateID}/skills` — Возвращает список участков шаблонов объектов · коды: 200, 400
  ← path: assetTemplateID:int → int[]
- `GET /AssetTemplates/{assetTemplateID}/workTypes` — Возвращает список видов работ шаблонов объектов · коды: 200, 400
  ← path: assetTemplateID:int → int[]
- `GET /AssetTemplates/{id}` — Возвращает шаблон объекта · коды: 200
  ← path: id:int → ResultsAssetTemplatesGetResult
- `DELETE /AssetTemplates/{id}` — Помечает шаблон объекта как удаленный · коды: 202, 409
  ← path: id:int
- `DELETE /AssetTemplates/{id}/avatar` — Удаляет аватарку указаного шаблона объекта. · коды: 202
  ← path: id:int
- `PUT /AssetTemplates/{id}/avatar/upload/fromBody` — Загружает изображение JPG не менее 128x128 используемое в качестве аватарки для указанного шаблона объекта. Данные будут получены из тела запроса (base64). · коды: 202
  ← path: id:int; body: DataAttachmentsFromBodyUploadData → AspNetCoreResultsUploadFileResult
- `PUT /AssetTemplates/{id}/avatar/upload/fromForm` — Загружает изображение JPG не менее 128x128 используемое в качестве аватарки для указанного шаблона объекта. Данные будут получены из формы. · коды: 202
  ← path: id:int; body: { ContentLength?: int, ContentStream.CanRead?: bool, ContentStream.CanSeek?: bool, ContentStream.CanTimeout?: bool, ContentStream.CanWrite?: bool, ContentStream.Capacity?: int, ContentStream.Length?: int, ContentStream.Position?: int, ContentStream.ReadTimeout?: int, ContentStream.WriteTimeout?: int, ContentType?: str, Coordinate?: str, Description?: str, File: file, FileName?: str, IsIgnorePossibleDuplication?: bool, IsPublic?: bool, Md5Hash?: str, Roles?: int[], Uid?: uuid } → AspNetCoreResultsUploadFileResult

## AssetTypes
- `GET /AssetTypes` — Возвращает список типов объектов · коды: 200
  → map<ResultsAssetTypesGetResult>
- `POST /AssetTypes` — Добавляет тип объекта · коды: 201, 409
  ← query: relatedToAnyWorkType?:bool; body: ESAssetTypeAddData[]
- `PUT /AssetTypes` — Изменяет тип объекта · коды: 202, 409
  ← query: relatedToAnyWorkType?:bool; body: ESAssetTypeUpdateData[]
- `DELETE /AssetTypes` — Помечает типы объектов как удаленные · коды: 202, 409
  ← body: int[]
- `GET /AssetTypes/{id}` — Возвращает тип объекта · коды: 200, 400, 404, 409
  ← path: id:int
- `DELETE /AssetTypes/{id}` — Помечает тип объекта как удаленный · коды: 202, 409
  ← path: id:int
- `GET /AssetTypes/{id}/workTypes` — Возвращает список относящихся к типу объекта видов работ · коды: 202
  ← path: id:int → IdNameEntityOfShort[]
- `POST /AssetTypes/{id}/workTypes` — Привязать список видов работ к типу объекта · коды: 200
  ← path: id:int; body: int[]
- `DELETE /AssetTypes/{id}/workTypes` — Удалить привязку видов работ к типу объекта · коды: 200
  ← path: id:int; body: int[]

## AssetWorkTypes
- `POST /AssetWorkTypes` — Добавляет типы работ к ассету. · коды: 201, 409
  ← body: AssetActionDataOfShort → ProjectionsESAssetWorkTypeProjection[]
- `DELETE /AssetWorkTypes` — Отвязывает типы работ от ассета. · коды: 200
  ← body: AssetActionDataOfShort → ProjectionsESAssetWorkTypeProjection[]

## Assets
- `GET /Assets` — Возращает справочник объектов                     , доступных пользователю · коды: 200
  ← query: includePath?:bool, includeTaskActuality?:bool, searchText?:str, needForAllowedTasks?:bool → map<ResultsAssetsAssetExtResult>
- `POST /Assets` — Создает объект · коды: 201, 409
  ← body: ESAssetAddData → IdNameResultOfInt
- `PUT /Assets` — Массовое изменение объектов · коды: 202, 409
  ← body: ESAssetMassiveUpdateData
- `DELETE /Assets` — Помечает объекты как удаленные · коды: 202, 409
  ← body: int[]
- `HEAD /Assets` — Возвращает заголовок запроса пользователей с количеством данных, удовлетворяющих фильтру · коды: 200
- `GET /Assets/attributes` — Возвращает список атрибутов по объектам · коды: 200
  → ResultsAssetsAssetAttributesExtResult[]
- `DELETE /Assets/avatar` — Удаляет аватку для указанного списка объекта. · коды: 202
  ← body: int[]
- `POST /Assets/contacts` — Добавляет контактные лица для объектов · коды: 201, 409
  ← body: AssetActionDataOfInt[] → ResultsAssetContactsPostResult
- `DELETE /Assets/contacts` — Удаляет контактные лица у объектов · коды: 202, 409
  ← body: AssetActionDataOfInt[]
- `DELETE /Assets/full` — Помечает объекты и все их дочерние объекты как удаленные · коды: 202, 409
  ← body: int[]
- `PUT /Assets/restore` — Воскрешает удаленные объекты · коды: 202, 409
  ← query: withNested?:bool; body: int[]
- `GET /Assets/root` — Возращает справочник корневых объектов, доступных пользователю. · коды: 200
  → map<ResultsAssetsAssetExtResult>
  Доступность объекта определяется по пересечанию участков пользователя и объека, наличию полномочия
AllDistricts или AllAssets. Корневой объект - объект не имеющий объекта более высого уровня среди 
доступных пользователю.
- `GET /Assets/{assetID}` — Детальная информация по объекту · коды: 200, 400
  ← path: assetID:int → ResultsAssetsAssetDetailedInfoResult
- `PUT /Assets/{assetID}` — Изменяет объект · коды: 202, 409
  ← path: assetID:int; body: ESAssetUpdateData
- `DELETE /Assets/{assetID}` — Помечает объект как удаленный · коды: 202, 409
  ← path: assetID:int
- `GET /Assets/{assetID}/assignments` — Возвращает список назначений заданного объекта для пользователей · коды: 200
  ← path: assetID:int → ResultsAssetsAssetAssignmentResult[]
- `GET /Assets/{assetID}/attachments` — Возвращает список файлов вложенных в объект. · коды: 200, 400
  ← path: assetID:int; query: thumbnailSize?:int → map<ResultsCommonListAttachmentResult>
- `GET /Assets/{assetID}/attachments/{attachmentID}` — Возвращает TemporartRedirect на временную ссылку для скачки файла · коды: 307
  ← path: assetID:int, attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /Assets/{assetID}/attributes` — Возвращает список пользовтельских полей по объекту · коды: 200, 400
  ← path: assetID:int → ResultsAssetsAssetAttributeResult[]
- `GET /Assets/{assetID}/checkLists` — Возвращает список чек-листов объекта · коды: 200
  ← path: assetID:int → map<ResultsAssetCheckListsGetResult[]>
- `POST /Assets/{assetID}/checkLists` — Добавляет чек-листы к объекту · коды: 202
  ← path: assetID:int; body: int[]
- `DELETE /Assets/{assetID}/checkLists` — Помечает чек-листы у объекта как удаленные · коды: 202
  ← path: assetID:int; body: int[]
- `POST /Assets/{assetID}/checkLists/{checkListID}` — Добавляет чек-лист к объекту · коды: 202
  ← path: assetID:int, checkListID:int
- `DELETE /Assets/{assetID}/checkLists/{checkListID}` — Помечает чек-лист у объекта как удаленный · коды: 202
  ← path: assetID:int, checkListID:int
- `GET /Assets/{assetID}/contacts` — Возвращает список действующих контактов для объекта · коды: 200, 400
  ← path: assetID:int; query: searchText?:str → ResultsAssetContactsListResult[]
- `GET /Assets/{assetID}/contacts/{contactID}` — Возвращает контакт объекта · коды: 200
  ← path: assetID:int, contactID:int → ResultsAssetContactsGetResult
- `POST /Assets/{assetID}/contacts/{contactID}` — Добавляет контактное лицо для объекта · коды: 201, 409
  ← path: assetID:int, contactID:int → ResultsAssetContactsPostResult
- `DELETE /Assets/{assetID}/contacts/{contactID}` — Удаляет контактное лицо у объекта · коды: 202, 409
  ← path: assetID:int, contactID:int
- `GET /Assets/{assetID}/districts` — Возвращае список участков для объекта. · коды: 200, 400
  ← path: assetID:int → ResultsCommonAssetDistrictResult[]
- `DELETE /Assets/{assetID}/full` — Помечает объект и все дочерние объекты как удаленные · коды: 202, 409
  ← path: assetID:int
- `GET /Assets/{assetID}/locations/actual` — Возвращает текущее местоположение объекта · коды: 200
  ← path: assetID:int → ResultsCommonLocationResult
- `PUT /Assets/{assetID}/publish` — Метод публикации объекта · коды: 202, 409
  ← path: assetID:int
- `GET /Assets/{assetID}/skills` — Возвращает список навыков объекта · коды: 200
  ← path: assetID:int → map<ResultsAssetSkillsAssetSkillResult>
- `GET /Assets/{assetID}/tags` — Возвращает список активных (не удаленых) тэгов по объекту. · коды: 200, 400
  ← path: assetID:int → str[]
- `PUT /Assets/{assetID}/unpublish` — Метод отмены публикации объекта · коды: 202, 409
  ← path: assetID:int
- `GET /Assets/{assetID}/workTypes` — Возвращае список доступных по объекту видов работ. · коды: 200
  ← path: assetID:int → map<ResultsAssetsAssetWorkTypeResult>
- `DELETE /Assets/{id}/avatar` — Удаляет аватку указаного объекта. · коды: 202
  ← path: id:int
- `PUT /Assets/{id}/avatar/upload/fromBody` — Загружает изображение JPG не менее 128x128 используемое в качестве аватарки для указанного объекта. Данные будут получены из тела запроса (base64). · коды: 202
  ← path: id:int; body: DataAttachmentsFromBodyUploadData → AspNetCoreResultsUploadFileResult
- `PUT /Assets/{id}/avatar/upload/fromForm` — Загружает изображение JPG не менее 128x128 используемое в качестве аватарки для указанного объекта. Данные будут получены из формы. · коды: 202
  ← path: id:int; body: { ContentLength?: int, ContentStream.CanRead?: bool, ContentStream.CanSeek?: bool, ContentStream.CanTimeout?: bool, ContentStream.CanWrite?: bool, ContentStream.Capacity?: int, ContentStream.Length?: int, ContentStream.Position?: int, ContentStream.ReadTimeout?: int, ContentStream.WriteTimeout?: int, ContentType?: str, Coordinate?: str, Description?: str, File: file, FileName?: str, IsIgnorePossibleDuplication?: bool, IsPublic?: bool, Md5Hash?: str, Roles?: int[], Uid?: uuid } → AspNetCoreResultsUploadFileResult
- `GET /Assets/{parentAssetID}/assets` — Возращает справочник дочерних объектов (один уровень иерархии), 
доступных пользователю. · коды: 200
  ← path: parentAssetID:int; query: searchText?:str → map<ResultsAssetsAssetExtResult>
  Доступность объекта определяется по пересечанию участков пользователя и объека, наличию полномочия
AllDistricts или AllAssets.
- `GET /Assets/{parentAssetID}/assets/all` — Возращает справочник всех дочерних объектов (вниз по иерархии до самого нижнего уровня), 
доступных пользователю. · коды: 200
  ← path: parentAssetID:int → map<ResultsAssetsAssetExtResult>
  Доступность объекта определяется по пересечанию участков пользователя и объека, наличию полномочия
AllDistricts или AllAssets.

## Companies
- `GET /Companies` — Возвращает список доступных пользователю компаний. · коды: 200
  ← query: searchText?:str → map<ResultsCompaniesListResult>
- `POST /Companies` — Добавляет компанию · коды: 201, 409
  ← body: ESCompanyAddData[] → int[]
- `PUT /Companies` — Изменяет компанию · коды: 202, 409
  ← body: ESCompanyUpdateData[]
- `DELETE /Companies` — Помечает компании как удаленные · коды: 202, 409
  ← body: int[]
- `HEAD /Companies` — Возвращает заголовок запроса доступных пользователю компаний с количеством данных, удовлетворяющих фильтру · коды: 200
  ← query: searchText?:str
- `POST /Companies/contacts` — Добавляет контактные лица к компании · коды: 201, 409
  ← body: CompanyActionDataOfInt[] → ResultsCompanyContactsPostResult
- `DELETE /Companies/contacts` — Удаляет контактные лица у компании · коды: 202, 409
  ← body: CompanyActionDataOfInt[]
- `GET /Companies/dadata/find` — Поиск информации о компании по ИНН. · коды: 200, 204
  ← query: inn?:str → ESCompanyAddData
- `PUT /Companies/restore` — Воскрешает удаленные компании · коды: 202, 409
  ← body: int[]
- `GET /Companies/{CompanyID}/attachments/{attachmentID}` — Возвращает TemporartRedirect на временную ссылку для скачки файла · коды: 307
  ← path: companyID:int, attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /Companies/{companyID}/attachment/{attachmentID}` — Прикрепленный файл к компании
<param name="companyID">Идентификатор компании</param><param name="attachmentID">Идентификатор прикрепленного файла к компании</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз из доступных)</param> · коды: 200, 500
  ← path: companyID:int, attachmentID:int; query: thumbnailSize?:int → ResultsCommonGetAttachmentResult
- `GET /Companies/{companyID}/attachments` — Возвращает список файлов вложенных в компанию. · коды: 200, 400
  ← path: companyID:int; query: thumbnailSize?:int → map<ResultsCommonListAttachmentResult>
- `GET /Companies/{companyID}/attributes` — Возвращает список пользовательских атрибутов компании · коды: 200, 204, 400
  ← path: companyID:int → ResultsCompanyAttributesCompanyAttributeResult[]
- `POST /Companies/{companyID}/attributes` — Обновляет сведения о пользовательских полях в компании · коды: 202, 400
  ← path: companyID:int; body: DataCompanyAttributeAttributeUpdateData[]
- `GET /Companies/{companyID}/bankAccounts` — Возвращает список банковских счетов компании · коды: 200, 400
  ← path: companyID:int; query: searchText?:str → map<ResultsCompanyBankAccountsListResult>
- `POST /Companies/{companyID}/bankAccounts` — Добавляет банковские счета компании · коды: 201, 409
  ← path: companyID:int; body: ESCompanyBankAccountAddData[] → ResultsCompanyBankAccountsPostResult
- `PUT /Companies/{companyID}/bankAccounts` — Обновляет банковские счета компании · коды: 202, 409
  ← path: companyID:int; body: ESCompanyBankAccountUpdateData[]
- `DELETE /Companies/{companyID}/bankAccounts` — Удаляет банковские счета компании · коды: 202, 409
  ← path: companyID:int; body: int[]
- `DELETE /Companies/{companyID}/bankAccounts/{bankAccountID}` — Удаляет банковский счёт компании · коды: 202, 409
  ← path: companyID:int, bankAccountID:int
- `GET /Companies/{companyID}/contacts` — Возвращает список контактов компании · коды: 200, 400
  ← path: companyID:int; query: searchText?:str → map<ResultsCompanyContactsListResult>
- `GET /Companies/{companyID}/contacts/{contactID}` — Возвращает контакт компании · коды: 200
  ← path: companyID:int, contactID:int → ResultsCompanyContactsGetResult
- `POST /Companies/{companyID}/contacts/{contactID}` — Добавляет контактное лицо к компании · коды: 201, 409
  ← path: companyID:int, contactID:int → ResultsCompanyContactsPostResult
- `DELETE /Companies/{companyID}/contacts/{contactID}` — Удаляет контактное лицо у компании · коды: 202, 409
  ← path: companyID:int, contactID:int
- `GET /Companies/{companyID}/locations/actual` — Возвращает текущее местоположение компании · коды: 200
  ← path: companyID:int → ResultsCommonLocationResult
- `GET /Companies/{id}` — Возвращает доступную пользователю компанию по идентификатору · коды: 200
  ← path: id:int → ResultsCompaniesGetResult
- `DELETE /Companies/{id}` — Помечает компании как удаленные · коды: 202, 409
  ← path: id:int

## CompanyAttachments
- `POST /CompanyAttachments` — Связывает компанию и вложение · коды: 201
  ← body: CompanyActionDataOfInt[] → ResultsCompanyAttachmentsAddResult[]
- `DELETE /CompanyAttachments` — Помечает связку компании и вложения как удаленную · коды: 202
  ← body: CompanyActionDataOfInt[]
- `POST /CompanyAttachments/upload/fromBody` — Загружает файл на файловый сервер и привязывает его к компании. Данные будут получены из тела запроса. · коды: 201
  ← body: DataCompanyAttachmentCompanyBodyUploadData → ResultsCompanyAttachmentsUploadResult
- `POST /CompanyAttachments/upload/fromForm` — Загружает файл на файловый сервер и привязывает его к компании. Данные будут получены из формы. · коды: 201
  ← query: CompanyID?:int, Description?:str, IsPublic?:bool, IsIgnorePossibleDuplication?:bool, Roles?:int[], Coordinate?:str, FileName?:str, ContentType?:str, Uid?:uuid, ContentStream.CanRead?:bool, ContentStream.CanSeek?:bool, ContentStream.CanWrite?:bool, ContentStream.Capacity?:int, ContentStream.Length?:int, ContentStream.Position?:int, ContentStream.CanTimeout?:bool, ContentStream.ReadTimeout?:int, ContentStream.WriteTimeout?:int, Md5Hash?:str, ContentLength?:int; body: { File: file } → ResultsCompanyAttachmentsUploadResult

## CompanyContacts
- `POST /CompanyContacts` — Добавляет контактные лица к компании · коды: 201, 409
  ← body: CompanyActionDataOfInt[] → ResultsCompanyContactsPostResult
- `DELETE /CompanyContacts` — Удаляет контактные лица у компании · коды: 202, 409
  ← body: CompanyActionDataOfInt[]

## CompanyListQueries
- `GET /CompanyListQueries` — Возвращает список сохраненных запросов, доступных в тенанте · коды: 200
  → map<ResultsCompanyListQueriesCompanyListQueryResult>
- `POST /CompanyListQueries` — Создает сохраненный запрос и привязывает его к текущему пользователю · коды: 201
  ← body: ESCompanyListQueryAddData[] → int[]
- `PUT /CompanyListQueries` — Изменяет сохраненный запрос · коды: 202
  ← body: ESCompanyListQueryUpdateData[]
- `DELETE /CompanyListQueries` — Помечает сохраненные запросы как удаленные · коды: 202
  ← body: int[]
- `DELETE /CompanyListQueries/remove` — Удаляет сохраненные запросы · коды: 202
  ← body: int[]
- `GET /CompanyListQueries/{id}` — Возвращает сохраненный запрос · коды: 200
  ← path: id:int → ResultsCompanyListQueriesCompanyListQueryGetResult
- `DELETE /CompanyListQueries/{id}` — Помечает сохраненный запрос как удаленный · коды: 202
  ← path: id:int
- `DELETE /CompanyListQueries/{id}/remove` — Удаляет сохраненный запрос · коды: 202
  ← path: id:int

## CompanyLocations
- `GET /CompanyLocations` — Список локаций по компании · коды: 200, 409
  ← query: companyID?:int, onDate?:datetime
- `POST /CompanyLocations` — Добавляет локацию к компании · коды: 202
  ← body: ESCompanyLocationMergeData
- `PUT /CompanyLocations` — Обновление локации у компании · коды: 202
  ← body: ESCompanyLocationMergeData
- `DELETE /CompanyLocations` — Удаление привязки локации к компании · коды: 202
  ← body: DataCompanyLocationsDeleteData

## CompanyRegistrationTypes
- `GET /CompanyRegistrationTypes` — Возвращает список видов регистрации компании · коды: 200
  → map<ResultsCompanyRegistrationTypesListResult>

## Districts
- `GET /Districts` — Возвращает список доступных пользователю участков. · коды: 200
  ← query: includePath?:bool → ResultsDistrictsDistrictListForTenantMemberResult[]
- `POST /Districts` — Добавляет участок · коды: 201, 409
  ← body: ESDistrictAddData[] → int[]
- `PUT /Districts` — Изменяет участок · коды: 202, 409
  ← body: ESDistrictUpdateData[]
- `DELETE /Districts` — Помечает участки как удаленные · коды: 202, 409
  ← body: int[]
- `PUT /Districts/parentAndReorder` — Изменяет родителя и/или сортировку участка · коды: 202, 409
  ← body: ESDistrictParentUpdateData
- `GET /Districts/{id}` — Возвращает доступный пользователю участок по идентификатору · коды: 200
  ← path: id:int → ResultsDistrictsDistrictResult
- `DELETE /Districts/{id}` — Помечает участки как удаленные · коды: 202, 409
  ← path: id:int

## Locations
- `GET /Locations` — Возвращает список локаций · коды: 200
  ← query: searchText?:str, searchFor?:str → map<ResultsCommonLocationResult>
- `POST /Locations` — Создает локации. · коды: 201
  ← body: DataLocationsPostData[] → int[]
- `PUT /Locations` — Изменяет локации. · коды: 202
  ← body: DataLocationsPutData[] → int[]
- `DELETE /Locations` — Помечает локации как удаленные. · коды: 202
  ← body: int[]
- `HEAD /Locations` — Возвращает количество локаций · коды: 200
  ← query: searchFor?:str
- `DELETE /Locations/remove` — Удаляет локации. · коды: 202
  ← body: int[]
- `GET /Locations/{id}` — Возвращает локацию с областью. · коды: 200
  ← path: id:int → map<ResultsLocationsLocationGetResult>
- `DELETE /Locations/{id}` — Помечает локации как удаленные. · коды: 202
  ← path: id:int
- `DELETE /Locations/{id}/remove` — Удаляет локацию. · коды: 202
  ← path: id:int

## OrgUnits
- `GET /OrgUnits` — Возращает справочник активных (не архивных и не удаленных) организационных единиц,
доступных пользователю. · коды: 200, 409
  ← query: companyID?:int[]
- `GET /OrgUnits/root` — Возращает справочник активных (не архивных и не удаленных) корневых организационных единиц,
доступных пользователю. · коды: 200, 409
  ← query: companyID?:int[]
- `GET /OrgUnits/{id}/orgunits` — Возращает справочник активных (не архивных и не удаленных) организационных единиц,
доступных пользователю. · коды: 200, 409
  ← path: id:int; query: companyID?:int[]

## PreferredTechnicians
- `GET /PreferredTechnicians` — Список предпочтительных исполнителей для объектa(ов) · коды: 200, 400
  → ResultsAssetsAssetDetailedInfoResult
- `POST /PreferredTechnicians` — Добавление или удаление предпочтительного исполнителя для объекта · коды: 202
  ← body: AssetActionDataOfInt[]
