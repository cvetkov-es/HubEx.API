# ES — справочник ручек

> **Что здесь:** все ручки сервиса ES (API for managing enterprise structure in HubEx): сигнатуры, параметры, права. Типы — schemas/ES.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/ES.md`; грабли — `notes/ES.md` (если есть).

Base: `{BASE_URL}/ES`
> Примеры ответов вынесены в [../examples/ES.md](../examples/ES.md).

**Оглавление**

- AssetAttachments — строки 45–55
- AssetAttributes — строки 57–65
- AssetClasses — строки 67–79
- AssetDistricts — строки 81–85
- AssetFilter — строки 87–91
- AssetListQueries — строки 93–109
- AssetLocations — строки 111–119
- AssetSchemas — строки 121–155
- AssetSearchSettings — строки 157–167
- AssetSkills — строки 169–173
- AssetTags — строки 175–179
- AssetTemplateAttachments — строки 181–191
- AssetTemplateAttributes — строки 193–195
- AssetTemplateDistricts — строки 197–203
- AssetTemplateSkills — строки 205–211
- AssetTemplateWorkTypes — строки 213–219
- AssetTemplates — строки 221–253
- AssetTypes — строки 255–273
- AssetWorkTypes — строки 275–279
- Assets — строки 281–308
- Негативные сценарии: — строки 310–372
- Негативные сценарии: — строки 374–382
- Негативные сценарии: — строки 384–387
- Companies — строки 389–441
- CompanyAttachments — строки 443–451
- CompanyContacts — строки 453–457
- CompanyListQueries — строки 459–475
- CompanyLocations — строки 477–485
- CompanyRegistrationTypes — строки 487–489
- Districts — строки 491–505
- Locations — строки 507–525
- OrgUnits — строки 527–533
- PreferredTechnicians — строки 535–539

## AssetAttachments
- `POST /AssetAttachments` — Связывает объект и вложение · коды: 201 · примеры
  ← body: AssetActionDataOfInt[] → ResultsAssetAttachmentsPostResult[]
- `DELETE /AssetAttachments` — Помечает связку объекта и вложения как удалённую · коды: 202 · примеры
  ← body: AssetActionDataOfInt[]
- `POST /AssetAttachments/upload` — Загружает файл на файловый сервер и привязывает его к объекту (данные из формы) · коды: 201 · примеры
  ← query: AssetID?:int, Description?:str, IsPublic?:bool, IsIgnorePossibleDuplication?:bool, Roles?:int[], Coordinate?:str, FileName?:str, ContentType?:str, Uid?:uuid, ContentStream.CanRead?:bool, ContentStream.CanSeek?:bool, ContentStream.CanWrite?:bool, ContentStream.Capacity?:int, ContentStream.Length?:int, ContentStream.Position?:int, ContentStream.CanTimeout?:bool, ContentStream.ReadTimeout?:int, ContentStream.WriteTimeout?:int, Md5Hash?:str, ContentLength?:int; body: { File: file } → ResultsAssetAttachmentsUploadResult
- `POST /AssetAttachments/upload/fromBody` — Загружает файл на файловый сервер и привязывает его к объекту (данные из тела запроса) · коды: 201 · примеры
  ← body: DataAssetAttachmentsAssetBodyUploadData → ResultsAssetAttachmentsUploadResult
- `POST /AssetAttachments/upload/fromForm` — Загружает файл на файловый сервер и привязывает его к объекту (данные из формы) · коды: 201 · примеры
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
- `GET /AssetClasses` — Возвращает список классов объектов · коды: 200, 204, 206 · примеры
  → map<ResultsAssetClassesAssetClassListResult>
- `POST /AssetClasses` — Добавляет класс объектов · коды: 201, 204 · примеры
  ← body: ESAssetClassAddData[] → ResultsAssetClassesAssetClassAddResult[]
- `PUT /AssetClasses` — Обновляет классы объектов · коды: 202 · примеры
  ← body: ESAssetClassUpdateData[]
- `DELETE /AssetClasses` — Помечает классы объектов как удалённые · коды: 202 · примеры
  ← body: int[]
- `GET /AssetClasses/{id}` — Возвращает класс объекта · коды: 200, 204 · примеры
  ← path: id:int → ResultsAssetClassesAssetClassGetResult
- `DELETE /AssetClasses/{id}` — Помечает класс объектов как удалённый · коды: 202, 409 · примеры
  ← path: id:int

## AssetDistricts
- `POST /AssetDistricts` — Добавляет участки к объекту · коды: 201, 400, 409 · примеры
  ← body: AssetActionDataOfDistrictData
- `DELETE /AssetDistricts` — Исключает объект из участков · коды: 202, 400, 409 · примеры
  ← body: AssetActionDataOfShort

## AssetFilter
- `GET /AssetFilter` — Возвращает список доступных фильтров для пользователя, запросившего данные · коды: 200, 204 · примеры
  ← query: selectedOnly?:bool → ProjectionsCOMMONFilterListItemProjection[]
- `PUT /AssetFilter` — Обновляет список доступных фильтров и порядок их сортировки · коды: 202 · примеры
  ← body: COMMONUIFilterFilterData[]

## AssetListQueries
- `GET /AssetListQueries` — Возвращает список сохранённых запросов, доступных в тенанте · коды: 200, 204, 206 · примеры
  → map<ResultsAssetListQueriesAssetListQueryResult>
- `POST /AssetListQueries` — Создаёт сохранённый запрос и привязывает его к текущему пользователю · коды: 201 · примеры
  ← body: ESAssetListQueryAddData[] → int[]
- `PUT /AssetListQueries` — Изменяет сохранённый запрос · коды: 202 · примеры
  ← body: ESAssetListQueryUpdateData[]
- `DELETE /AssetListQueries` — Помечает сохранённые запросы как удалённые · коды: 202 · примеры
  ← body: int[]
- `DELETE /AssetListQueries/remove` — Физически удаляет сохранённые запросы · коды: 202 · примеры
  ← body: int[]
- `GET /AssetListQueries/{id}` — Возвращает сохранённый запрос · коды: 200, 204 · примеры
  ← path: id:int → ResultsAssetListQueriesAssetListQueryGetResult
- `DELETE /AssetListQueries/{id}` — Помечает сохранённый запрос как удалённый · коды: 202 · примеры
  ← path: id:int
- `DELETE /AssetListQueries/{id}/remove` — Физически удаляет сохранённый запрос · коды: 202 · примеры
  ← path: id:int

## AssetLocations
- `GET /AssetLocations` — Возвращает список локаций объекта · коды: 200, 204, 206, 409 · примеры
  ← query: assetID?:int, onDate?:datetime → map<ResultsAssetsAssetLocationResult>
- `POST /AssetLocations` — Добавляет локацию к объекту · коды: 202 · примеры
  ← body: ESAssetLocationMergeData
- `PUT /AssetLocations` — Обновляет срок нахождения объекта на локации · коды: 202 · примеры
  ← body: ESAssetLocationMergeData
- `DELETE /AssetLocations` — Удаляет привязку локации к объекту · коды: 202 · примеры
  ← body: DataAssetLocationsDeleteData

## AssetSchemas
- `GET /AssetSchemas/ascList/{assetID}` — Возвращает список существующих план-схем для текущего объекта и всех доступных объектов вверх по дереву · коды: 200, 204 · примеры
  ← path: assetID:int → map<ResultsAssetSchemaSchemaBase>
- `GET /AssetSchemas/asset/{assetID}` — Возвращает план-схему, привязанную к объекту, или ближайшую по дереву сверху · коды: 200, 204 · примеры
  ← path: assetID:int → ResultsAssetSchemaSchema
- `POST /AssetSchemas/asset/{assetId}` — Создаёт план-схему; объект можно задать через route или через body (приоритет у route) · коды: 201, 400, 409 · примеры
  ← path: assetId:int; body: ResultsAssetSchemaSchema → IdNameResultOfInt
- `PUT /AssetSchemas/asset/{assetId}` — Изменяет план-схему; объект можно задать через route или через body (приоритет у route) · коды: 202, 400, 409 · примеры
  ← path: assetId:int; body: ResultsAssetSchemaSchema → IdNameResultOfInt
- `GET /AssetSchemas/list` — Возвращает полный список схем тенанта · коды: 200, 204 · примеры
  → map<ResultsAssetSchemaSchemaBase>
- `GET /AssetSchemas/{schemaId}` — Возвращает план-схему по её уникальному идентификатору · коды: 200, 404 · примеры
  ← path: schemaId:int → ResultsAssetSchemaSchema
- `DELETE /AssetSchemas/{schemaId}` — Помечает план-схему как удалённую · коды: 202, 409 · примеры
  ← path: schemaId:int
- `POST /AssetSchemas/{schemaId}/bind` — Привязывает план-схему к нескольким объектам · коды: 202, 400, 409 · примеры
  ← path: schemaId:int; body: int[]
- `GET /AssetSchemas/{schemaId}/image` — Получает информацию об изображении, привязанном к план-схеме · коды: 200, 400, 404 · примеры
  ← path: schemaId:int; query: thumbnailSize?:int → ResultsAssetSchemaSchemaImage
- `DELETE /AssetSchemas/{schemaId}/image` — Удаляет текущее изображение, ассоциированное с план-схемой · коды: 202, 404, 409 · примеры
  ← path: schemaId:int
- `POST /AssetSchemas/{schemaId}/image/attach/{attachmentId}` — Привязывает ранее загруженное вложение (attachment) к план-схеме · коды: 201, 404, 409 · примеры
  ← path: schemaId:int, attachmentId:int; body: ResultsAssetSchemaImageSize → ResultsAssetSchemaSchemaBase
- `GET /AssetSchemas/{schemaId}/image/download` — Возвращает временный redirect на ссылку для скачивания изображения план-схемы · коды: 303, 400, 404 · примеры
  ← path: schemaId:int; query: thumbnailSize?:int, noRedirect?:bool
- `POST /AssetSchemas/{schemaId}/image/upload` — Загружает файл изображения на файловый сервер и привязывает его к план-схеме · коды: 201, 400, 409 · примеры
  ← path: schemaId:int; body: { ContentLength?: int, ContentStream.CanRead?: bool, ContentStream.CanSeek?: bool, ContentStream.CanTimeout?: bool, ContentStream.CanWrite?: bool, ContentStream.Capacity?: int, ContentStream.Length?: int, ContentStream.Position?: int, ContentStream.ReadTimeout?: int, ContentStream.WriteTimeout?: int, ContentType?: str, Coordinate?: str, Description?: str, File: file, FileName?: str, IsIgnorePossibleDuplication?: bool, IsPublic?: bool, Md5Hash?: str, Roles?: int[], Uid?: uuid } → ResultsAssetSchemaSchemaImageShort
- `GET /AssetSchemas/{schemaId}/points` — Возвращает полный список точек-заданий, размещённых на план-схеме · коды: 200, 204 · примеры
  ← path: schemaId:int; query: taskID?:int, assetID?:int → ResultsAssetSchemaSchemaTask[]
- `POST /AssetSchemas/{schemaId}/points` — Обновляет или добавляет точки на план-схему · коды: 200, 400, 409 · примеры
  ← path: schemaId:int; body: ResultsAssetSchemaSchemaTask[] → ResultsAssetSchemaSchemaTask[]
- `DELETE /AssetSchemas/{schemaId}/points` — Удаляет набор точек-заданий с план-схемы · коды: 202, 409 · примеры
  ← path: schemaId:int; body: int[]
- `PUT /AssetSchemas/{schemaId}/unbind` — Отвязывает несколько объектов от план-схемы · коды: 202, 400, 409 · примеры
  ← path: schemaId:int; body: int[]

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
- `POST /AssetSkills` — Добавляет навыки к объектам · коды: 201, 204, 409 · примеры
  ← body: AssetActionDataOfInt[] → ResultsAssetSkillsPostResult[]
- `DELETE /AssetSkills` — Удаляет навыки у объектов · коды: 202, 409 · примеры
  ← body: AssetActionDataOfInt[]

## AssetTags
- `POST /AssetTags` — Добавляет теги к объекту · коды: 201, 409 · примеры
  ← body: ESAssetTagAddData[] → ResultsAssetTagsAddResult[]
- `DELETE /AssetTags` — Удаляет теги у объекта · коды: 202, 400 · примеры
  ← body: ESAssetTagDeleteData[]

## AssetTemplateAttachments
- `POST /AssetTemplateAttachments` — Связывает шаблон объекта и вложение · коды: 201 · примеры
  ← body: AssetTemplateActionDataOfInt[] → ResultsAssetTemplateAttachmentsPostResult[]
- `DELETE /AssetTemplateAttachments` — Помечает связку шаблона объекта и вложения как удалённую · коды: 202 · примеры
  ← body: AssetTemplateActionDataOfInt[]
- `POST /AssetTemplateAttachments/upload` — Загружает файл и привязывает его к шаблону объекта (данные из формы) · коды: 201, 400 · примеры
  ← query: AssetTemplateID?:int, Description?:str, IsPublic?:bool, IsIgnorePossibleDuplication?:bool, Roles?:int[], Coordinate?:str, FileName?:str, ContentType?:str, Uid?:uuid, ContentStream.CanRead?:bool, ContentStream.CanSeek?:bool, ContentStream.CanWrite?:bool, ContentStream.Capacity?:int, ContentStream.Length?:int, ContentStream.Position?:int, ContentStream.CanTimeout?:bool, ContentStream.ReadTimeout?:int, ContentStream.WriteTimeout?:int, Md5Hash?:str, ContentLength?:int; body: { File: file } → ResultsAssetTemplateAttachmentsUploadResult
- `POST /AssetTemplateAttachments/upload/fromBody` — Загружает файл и привязывает его к шаблону объекта (данные из тела запроса) · коды: 201, 400 · примеры
  ← body: DataAssetTemplateAttachmentsAssetTemplateBodyUploadData → ResultsAssetTemplateAttachmentsUploadResult
- `POST /AssetTemplateAttachments/upload/fromForm` — Загружает файл и привязывает его к шаблону объекта (данные из формы) · коды: 201, 400 · примеры
  ← query: AssetTemplateID?:int, Description?:str, IsPublic?:bool, IsIgnorePossibleDuplication?:bool, Roles?:int[], Coordinate?:str, FileName?:str, ContentType?:str, Uid?:uuid, ContentStream.CanRead?:bool, ContentStream.CanSeek?:bool, ContentStream.CanWrite?:bool, ContentStream.Capacity?:int, ContentStream.Length?:int, ContentStream.Position?:int, ContentStream.CanTimeout?:bool, ContentStream.ReadTimeout?:int, ContentStream.WriteTimeout?:int, Md5Hash?:str, ContentLength?:int; body: { File: file } → ResultsAssetTemplateAttachmentsUploadResult

## AssetTemplateAttributes
- `POST /AssetTemplateAttributes` — Обновляет сведения о пользовательских полях шаблонов объектов · коды: 202 · примеры
  ← body: AssetTemplateActionDataOfMergeData[]

## AssetTemplateDistricts
- `POST /AssetTemplateDistricts` — Добавляет участки к шаблонам объектов · коды: 201, 204, 409 · примеры
  ← body: AssetTemplateActionDataOfShort[] → InterfacesEntitiesIAssetTemplateDistrictBaseEntity[]
- `DELETE /AssetTemplateDistricts` — Удаляет участки из шаблонов объектов · коды: 202, 409 · примеры
  ← body: AssetTemplateActionDataOfShort[]
- `DELETE /AssetTemplateDistricts/{id}` — Удаляет участки из шаблона объекта · коды: 202, 409 · примеры
  ← path: id:int; body: int[]

## AssetTemplateSkills
- `POST /AssetTemplateSkills` — Добавляет навыки к шаблонам объектов · коды: 201, 204, 409 · примеры
  ← body: AssetTemplateActionDataOfAddData[] → InterfacesEntitiesIAssetTemplateSkillBaseEntity[]
- `DELETE /AssetTemplateSkills` — Удаляет навыки из шаблонов объектов · коды: 202, 409 · примеры
  ← body: AssetTemplateActionDataOfInt[]
- `DELETE /AssetTemplateSkills/{id}` — Удаляет навыки из шаблона объекта · коды: 202, 409 · примеры
  ← path: id:int; body: int[]

## AssetTemplateWorkTypes
- `POST /AssetTemplateWorkTypes` — Добавляет типы работ к шаблонам объектов · коды: 201, 204, 409 · примеры
  ← body: AssetTemplateActionDataOfShort[] → EntitiesESAssetTemplateWorkTypeBaseEntity[]
- `DELETE /AssetTemplateWorkTypes` — Удаляет типы работ из шаблонов объектов · коды: 202, 409 · примеры
  ← body: AssetTemplateActionDataOfShort[]
- `DELETE /AssetTemplateWorkTypes/{id}` — Удаляет типы работ из шаблона объекта · коды: 202, 409 · примеры
  ← path: id:int; body: int[]

## AssetTemplates
- `GET /AssetTemplates` — Возвращает список шаблонов объектов · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, assetClassID?:int, assetTypeID?:int → map<ResultsAssetTemplatesListResult>
- `POST /AssetTemplates` — Добавляет шаблоны объектов · коды: 201, 409 · примеры
  ← body: ESAssetTemplateAddData[]
- `PUT /AssetTemplates` — Изменяет шаблоны объектов · коды: 202, 409 · примеры
  ← body: ESAssetTemplateUpdateData[]
- `DELETE /AssetTemplates` — Помечает шаблоны объектов как удалённые · коды: 202, 409 · примеры
  ← body: int[]
- `DELETE /AssetTemplates/avatar` — Удаляет аватарки для указанного списка шаблонов объектов · коды: 202 · примеры
  ← body: int[]
- `GET /AssetTemplates/{assetTemplateID}/attachments` — Возвращает список файлов, вложенных в шаблон объекта · коды: 200, 204, 206, 400 · примеры
  ← path: assetTemplateID:int; query: thumbnailSize?:int → map<ResultsCommonListAttachmentResult>
- `GET /AssetTemplates/{assetTemplateID}/attachments/{attachmentID}` — Возвращает TemporaryRedirect на временную ссылку для скачивания файла · коды: 307, 400, 404 · примеры
  ← path: assetTemplateID:int, attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /AssetTemplates/{assetTemplateID}/attributes` — Возвращает список пользовательских полей шаблона объекта · коды: 200, 204, 206, 400 · примеры
  ← path: assetTemplateID:int → ResultsAssetTemplatesAssetTemplateAttributeResult[]
- `GET /AssetTemplates/{assetTemplateID}/districts` — Возвращает список участков шаблона объекта · коды: 200, 204, 206, 400 · примеры
  ← path: assetTemplateID:int → map<ResultsCommonAssetDistrictResult>
- `GET /AssetTemplates/{assetTemplateID}/skills` — Возвращает список навыков шаблона объекта · коды: 200, 204, 206, 400 · примеры
  ← path: assetTemplateID:int → ResultsAssetTemplatesAssetTemplateSkillResult[]
- `GET /AssetTemplates/{assetTemplateID}/workTypes` — Возвращает список видов работ шаблона объекта · коды: 200, 204, 206, 400 · примеры
  ← path: assetTemplateID:int → ResultsAssetTemplatesAssetTemplateWorkTypeResult[]
- `GET /AssetTemplates/{id}` — Возвращает шаблон объекта · коды: 200, 204 · примеры
  ← path: id:int → ResultsAssetTemplatesGetResult
- `DELETE /AssetTemplates/{id}` — Помечает шаблон объекта как удалённый · коды: 202, 409 · примеры
  ← path: id:int
- `DELETE /AssetTemplates/{id}/avatar` — Удаляет аватарку шаблона объекта · коды: 202 · примеры
  ← path: id:int
- `PUT /AssetTemplates/{id}/avatar/upload/fromBody` — Загружает аватарку шаблона объекта (данные из тела запроса, base64) · коды: 200, 400 · примеры
  ← path: id:int; body: DataAttachmentsFromBodyUploadData → AspNetCoreResultsUploadFileResult
- `PUT /AssetTemplates/{id}/avatar/upload/fromForm` — Загружает аватарку шаблона объекта (данные из формы) · коды: 200, 400 · примеры
  ← path: id:int; body: { ContentLength?: int, ContentStream.CanRead?: bool, ContentStream.CanSeek?: bool, ContentStream.CanTimeout?: bool, ContentStream.CanWrite?: bool, ContentStream.Capacity?: int, ContentStream.Length?: int, ContentStream.Position?: int, ContentStream.ReadTimeout?: int, ContentStream.WriteTimeout?: int, ContentType?: str, Coordinate?: str, Description?: str, File: file, FileName?: str, IsIgnorePossibleDuplication?: bool, IsPublic?: bool, Md5Hash?: str, Roles?: int[], Uid?: uuid } → AspNetCoreResultsUploadFileResult

## AssetTypes
- `GET /AssetTypes` — Возвращает список типов объектов · коды: 200, 204, 206 · примеры
  → map<ResultsAssetTypesGetResult>
- `POST /AssetTypes` — Добавляет тип объекта · коды: 201, 409 · примеры
  ← query: relatedToAnyWorkType?:bool; body: ESAssetTypeAddData[] → ResultsAssetTypesAddResult[]
- `PUT /AssetTypes` — Изменяет тип объекта · коды: 202, 409 · примеры
  ← query: relatedToAnyWorkType?:bool; body: ESAssetTypeUpdateData[]
- `DELETE /AssetTypes` — Помечает типы объектов как удалённые · коды: 202, 409 · примеры
  ← body: int[]
- `GET /AssetTypes/{id}` — Возвращает тип объекта · коды: 200, 204, 400, 404, 409 · примеры
  ← path: id:int → ResultsAssetTypesGetResult
- `DELETE /AssetTypes/{id}` — Помечает тип объекта как удалённый · коды: 202, 409 · примеры
  ← path: id:int
- `GET /AssetTypes/{id}/workTypes` — Возвращает список видов работ, привязанных к типу объекта · коды: 200, 204, 206 · примеры
  ← path: id:int; query: isPublished?:bool → map<str>
- `POST /AssetTypes/{id}/workTypes` — Привязывает виды работ к типу объекта · коды: 200 · примеры
  ← path: id:int; body: int[]
- `DELETE /AssetTypes/{id}/workTypes` — Удаляет привязку видов работ к типу объекта · коды: 200 · примеры
  ← path: id:int; body: int[]

## AssetWorkTypes
- `POST /AssetWorkTypes` — Добавляет виды работ к объекту · коды: 201, 400, 409 · примеры
  ← body: AssetActionDataOfShort → ProjectionsESAssetWorkTypeProjection[]
- `DELETE /AssetWorkTypes` — Отвязывает виды работ от объекта · коды: 202, 400 · примеры
  ← body: AssetActionDataOfShort

## Assets
- `GET /Assets` — Возвращает справочник объектов, доступных пользователю · коды: 200, 204, 206, 400 · примеры
  ← query: includePath?:bool, includeTaskActuality?:bool, searchText?:str, needForAllowedTasks?:bool, parentID?:int, assetID?:int, responsiblePerson?:int, districtID?:int, workTypeID?:int, skillID?:int, companyID?:int, taskTypeID?:int, tag?:str, name?:str, isMobile?:bool, isAssigned?:bool, hasSchema?:bool, isDeleted?:bool, isPublished?:bool, warrantyFrom?:datetime, warrantyTill?:datetime, checkListID?:int, startWithAssetID?:int, assetTypeID?:int, assetClassID?:int, erpID?:str, contactID?:int, attributeValues?:str, contractID?:int → map<ResultsAssetsAssetExtResult>
- `POST /Assets` — Создает объект · коды: 201, 400, 409 · примеры
  ← body: ESAssetAddData → IdNameResultOfInt
- `PUT /Assets` — Массовое изменение объектов · коды: 202, 400, 409 · примеры
  ← body: ESAssetMassiveUpdateData
- `DELETE /Assets` — Помечает объекты как удалённые · коды: 202, 409 · примеры
  ← body: int[]
- `HEAD /Assets` — Возвращает заголовок запроса с количеством объектов, удовлетворяющих фильтру · коды: 200, 206 · примеры
  ← query: checkListID?:int, parentID?:int, assetID?:int, responsiblePerson?:int, districtID?:int, workTypeID?:int, skillID?:int, companyID?:int, taskTypeID?:int, tag?:str, name?:str, isMobile?:bool, isAssigned?:bool, hasSchema?:bool, isDeleted?:bool, isPublished?:bool, warrantyFrom?:datetime, warrantyTill?:datetime, startWithAssetID?:int, assetTypeID?:int, assetClassID?:int, erpID?:str, contactID?:int, attributeValues?:str, contractID?:int
- `GET /Assets/attributes` — Возвращает список атрибутов по объектам · коды: 200, 204, 206 · примеры
  ← query: assetID?:int, attributeID?:int → ResultsAssetsAssetAttributesExtResult[]
- `DELETE /Assets/avatar` — Удаляет аватарки для списка объектов · коды: 202 · примеры
  ← body: int[]
- `POST /Assets/contacts` — Добавляет контактные лица к объектам · коды: 201, 204, 409 · примеры
  ← body: AssetActionDataOfInt[] → ResultsAssetContactsPostResult[]
- `DELETE /Assets/contacts` — Удаляет контактные лица у объектов · коды: 202, 409 · примеры
  ← body: AssetActionDataOfInt[]
- `DELETE /Assets/full` — Помечает объекты и все их дочерние объекты как удалённые · коды: 202, 409 · примеры
  ← body: int[]
- `PUT /Assets/restore` — Восстанавливает удалённые объекты · коды: 202, 409 · примеры
  ← query: withNested?:bool; body: int[]
- `GET /Assets/root` — Возращает справочник корневых объектов, доступных пользователю. · коды: 200, 204, 206
  ← query: checkListID?:int, assetID?:int, responsiblePerson?:int, districtID?:int, workTypeID?:int, skillID?:int, companyID?:int, taskTypeID?:int, tag?:str, name?:str, isMobile?:bool, isAssigned?:bool, hasSchema?:bool, isDeleted?:bool, isPublished?:bool, warrantyFrom?:datetime, warrantyTill?:datetime, assetTypeID?:int, assetClassID?:int, erpID?:str, contactID?:int → map<ResultsAssetsAssetExtResult>
  Доступность объекта определяется по пересечанию участков пользователя и объека, наличию полномочия
AllDistricts или AllAssets. Корневой объект - объект не имеющий объекта более высого уровня среди 
доступных пользователю.
            
## Негативные сценарии:
- 204 NoContent: объекты не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetsList`.
- `GET /Assets/{assetID}` — Детальная информация по объекту · коды: 200, 204 · примеры
  ← path: assetID:int → ResultsAssetsAssetDetailedInfoResult
- `PUT /Assets/{assetID}` — Изменяет объект · коды: 202, 400, 409 · примеры
  ← path: assetID:int; body: ESAssetUpdateData
- `DELETE /Assets/{assetID}` — Помечает объект как удалённый · коды: 202, 409 · примеры
  ← path: assetID:int
- `GET /Assets/{assetID}/assignments` — Возвращает список назначений объекта для пользователей · коды: 200, 204, 206, 404 · примеры
  ← path: assetID:int; query: userID?:int, validOn?:datetime → ResultsAssetsAssetAssignmentResult[]
- `GET /Assets/{assetID}/attachments` — Возвращает список файлов, вложенных в объект · коды: 200, 204, 206, 400 · примеры
  ← path: assetID:int; query: thumbnailSize?:int → map<ResultsCommonListAttachmentResult>
- `GET /Assets/{assetID}/attachments/{attachmentID}` — Возвращает TemporaryRedirect на временную ссылку для скачивания файла · коды: 307, 400, 404 · примеры
  ← path: assetID:int, attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /Assets/{assetID}/attributes` — Возвращает список пользовательских полей объекта · коды: 200, 204, 206, 400 · примеры
  ← path: assetID:int → ResultsAssetsAssetAttributeResult[]
- `GET /Assets/{assetID}/checkLists` — Возвращает список чек-листов объекта · коды: 200, 204, 206 · примеры
  ← path: assetID:int → map<ResultsAssetCheckListsGetResult[]>
- `POST /Assets/{assetID}/checkLists` — Добавляет чек-листы к объекту · коды: 202 · примеры
  ← path: assetID:int; body: int[]
- `DELETE /Assets/{assetID}/checkLists` — Помечает чек-листы объекта как удалённые · коды: 202 · примеры
  ← path: assetID:int; body: int[]
- `POST /Assets/{assetID}/checkLists/{checkListID}` — Добавляет чек-лист к объекту · коды: 202 · примеры
  ← path: assetID:int, checkListID:int
- `DELETE /Assets/{assetID}/checkLists/{checkListID}` — Помечает чек-лист объекта как удалённый · коды: 202 · примеры
  ← path: assetID:int, checkListID:int
- `GET /Assets/{assetID}/contacts` — Возвращает список действующих контактов объекта · коды: 200, 204, 206, 400 · примеры
  ← path: assetID:int; query: searchText?:str → map<ResultsAssetContactsListResult>
- `GET /Assets/{assetID}/contacts/{contactID}` — Возвращает контакт объекта · коды: 200, 204 · примеры
  ← path: assetID:int, contactID:int → ResultsAssetContactsGetResult
- `POST /Assets/{assetID}/contacts/{contactID}` — Добавляет контактное лицо к объекту · коды: 201, 409 · примеры
  ← path: assetID:int, contactID:int → ResultsAssetContactsPostResult[]
- `DELETE /Assets/{assetID}/contacts/{contactID}` — Удаляет контактное лицо у объекта · коды: 202, 409 · примеры
  ← path: assetID:int, contactID:int
- `GET /Assets/{assetID}/districts` — Возвращает список участков объекта · коды: 200, 204, 206, 400 · примеры
  ← path: assetID:int → map<ResultsCommonAssetDistrictResult>
- `DELETE /Assets/{assetID}/full` — Помечает объект и все дочерние объекты как удалённые · коды: 202, 409 · примеры
  ← path: assetID:int
- `GET /Assets/{assetID}/locations/actual` — Возвращает текущее местоположение объекта · коды: 200, 204, 206 · примеры
  ← path: assetID:int → ResultsCommonLocationResult
- `PUT /Assets/{assetID}/publish` — Публикует объект · коды: 202, 409 · примеры
  ← path: assetID:int
- `GET /Assets/{assetID}/skills` — Возвращает список навыков объекта · коды: 200, 204, 206 · примеры
  ← path: assetID:int → map<ResultsAssetSkillsAssetSkillResult>
- `GET /Assets/{assetID}/tags` — Возвращает список активных тегов объекта · коды: 200, 204, 206, 400 · примеры
  ← path: assetID:int → str[]
- `PUT /Assets/{assetID}/unpublish` — Снимает объект с публикации · коды: 202, 409 · примеры
  ← path: assetID:int
- `GET /Assets/{assetID}/workTypes` — Возвращает список доступных по объекту видов работ · коды: 200, 204, 206 · примеры
  ← path: assetID:int → map<ResultsAssetsAssetWorkTypeResult>
- `DELETE /Assets/{id}/avatar` — Удаляет аватарку объекта · коды: 202 · примеры
  ← path: id:int
- `PUT /Assets/{id}/avatar/upload/fromBody` — Загружает аватарку объекта (данные из тела запроса, base64) · коды: 200, 400 · примеры
  ← path: id:int; body: DataAttachmentsFromBodyUploadData → AspNetCoreResultsUploadFileResult
- `PUT /Assets/{id}/avatar/upload/fromForm` — Загружает аватарку объекта (данные из формы) · коды: 200, 400 · примеры
  ← path: id:int; body: { ContentLength?: int, ContentStream.CanRead?: bool, ContentStream.CanSeek?: bool, ContentStream.CanTimeout?: bool, ContentStream.CanWrite?: bool, ContentStream.Capacity?: int, ContentStream.Length?: int, ContentStream.Position?: int, ContentStream.ReadTimeout?: int, ContentStream.WriteTimeout?: int, ContentType?: str, Coordinate?: str, Description?: str, File: file, FileName?: str, IsIgnorePossibleDuplication?: bool, IsPublic?: bool, Md5Hash?: str, Roles?: int[], Uid?: uuid } → AspNetCoreResultsUploadFileResult
- `GET /Assets/{parentAssetID}/assets` — Возращает справочник дочерних объектов (один уровень иерархии), 
доступных пользователю. · коды: 200, 204, 206
  ← path: parentAssetID:int; query: searchText?:str, checkListID?:int, assetID?:int, responsiblePerson?:int, districtID?:int, workTypeID?:int, skillID?:int, companyID?:int, taskTypeID?:int, tag?:str, name?:str, isMobile?:bool, isAssigned?:bool, hasSchema?:bool, isDeleted?:bool, isPublished?:bool, warrantyFrom?:datetime, warrantyTill?:datetime, assetTypeID?:int, assetClassID?:int, erpID?:str, contactID?:int → map<ResultsAssetsAssetExtResult>
  Доступность объекта определяется по пересечанию участков пользователя и объека, наличию полномочия
AllDistricts или AllAssets.
            
## Негативные сценарии:
- 204 NoContent: объекты не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetsList`.
- `GET /Assets/{parentAssetID}/assets/all` — Возращает справочник всех дочерних объектов (вниз по иерархии до самого нижнего уровня), 
доступных пользователю. · коды: 200, 204, 206
  ← path: parentAssetID:int; query: checkListID?:int, assetID?:int, responsiblePerson?:int, districtID?:int, workTypeID?:int, skillID?:int, companyID?:int, taskTypeID?:int, tag?:str, name?:str, isMobile?:bool, isAssigned?:bool, hasSchema?:bool, isDeleted?:bool, isPublished?:bool, warrantyFrom?:datetime, warrantyTill?:datetime, assetTypeID?:int, assetClassID?:int, erpID?:str, contactID?:int → map<ResultsAssetsAssetExtResult>
  Доступность объекта определяется по пересечанию участков пользователя и объека, наличию полномочия
AllDistricts или AllAssets.
            
## Негативные сценарии:
- 204 NoContent: объекты не найдены.
- 401 Unauthorized: отсутствует или некорректен Bearer-токен.
- 403 Forbidden: недостаточно прав `AssetsList`.

## Companies
- `GET /Companies` — Возвращает список доступных пользователю компаний · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, isDeleted?:bool, taskTypeID?:int, companyID?:int, companyRegistrationTypeID?:int, isEmployer?:bool, isContractorHolder?:bool, isOurCompany?:bool, isVATTaxpayer?:bool → map<ResultsCompaniesListResult>
- `POST /Companies` — Добавляет компанию · коды: 201, 409 · примеры
  ← body: ESCompanyAddData[] → int[]
- `PUT /Companies` — Изменяет компанию · коды: 202, 409 · примеры
  ← body: ESCompanyUpdateData[]
- `DELETE /Companies` — Помечает компании как удалённые · коды: 202, 409 · примеры
  ← body: int[]
- `HEAD /Companies` — Возвращает заголовок запроса доступных пользователю компаний с количеством данных, удовлетворяющих фильтру · коды: 200, 206 · примеры
  ← query: searchText?:str, isDeleted?:bool, taskTypeID?:int, companyID?:int, companyRegistrationTypeID?:int, isEmployer?:bool, isContractorHolder?:bool, isOurCompany?:bool, isVATTaxpayer?:bool
- `POST /Companies/contacts` — Добавляет контактные лица к компаниям · коды: 201, 204, 409 · примеры
  ← body: CompanyActionDataOfInt[] → ResultsCompanyContactsPostResult[]
- `DELETE /Companies/contacts` — Удаляет контактные лица у компаний · коды: 202, 409 · примеры
  ← body: CompanyActionDataOfInt[]
- `GET /Companies/dadata/find` — Поиск информации о компании по ИНН через DaData · коды: 200, 204 · примеры
  ← query: inn?:str → ESCompanyAddData
- `PUT /Companies/restore` — Восстанавливает удалённые компании · коды: 202, 409 · примеры
  ← body: int[]
- `GET /Companies/{companyID}/attachment/{attachmentID}` — Возвращает прикреплённый файл компании · коды: 200, 204, 400, 500 · примеры
  ← path: companyID:int, attachmentID:int; query: thumbnailSize?:int → ResultsCommonGetAttachmentResult
- `GET /Companies/{companyID}/attachments` — Возвращает список файлов, вложенных в компанию · коды: 200, 204, 206, 400 · примеры
  ← path: companyID:int; query: thumbnailSize?:int → map<ResultsCommonListAttachmentResult>
- `GET /Companies/{companyID}/attachments/{attachmentID}` — Возвращает TemporaryRedirect на временную ссылку для скачивания файла · коды: 307, 400, 404 · примеры
  ← path: companyID:int, attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /Companies/{companyID}/attributes` — Возвращает список пользовательских атрибутов компании · коды: 200, 204, 206, 400 · примеры
  ← path: companyID:int → ResultsCompanyAttributesCompanyAttributeResult[]
- `POST /Companies/{companyID}/attributes` — Обновляет сведения о пользовательских полях компании · коды: 202, 400 · примеры
  ← path: companyID:int; body: DataCompanyAttributeAttributeUpdateData[]
- `GET /Companies/{companyID}/bankAccounts` — Возвращает список банковских счетов компании · коды: 200, 204, 206, 400 · примеры
  ← path: companyID:int; query: searchText?:str → map<ResultsCompanyBankAccountsListResult>
- `POST /Companies/{companyID}/bankAccounts` — Добавляет банковские счета компании · коды: 201, 204, 409 · примеры
  ← path: companyID:int; body: ESCompanyBankAccountAddData[] → ResultsCompanyBankAccountsPostResult[]
- `PUT /Companies/{companyID}/bankAccounts` — Обновляет банковские счета компании · коды: 202, 409 · примеры
  ← path: companyID:int; body: ESCompanyBankAccountUpdateData[]
- `DELETE /Companies/{companyID}/bankAccounts` — Удаляет банковские счета компании · коды: 202, 409 · примеры
  ← path: companyID:int; body: int[]
- `DELETE /Companies/{companyID}/bankAccounts/{bankAccountID}` — Удаляет банковский счёт компании · коды: 202, 409 · примеры
  ← path: companyID:int, bankAccountID:int
- `GET /Companies/{companyID}/contacts` — Возвращает список контактов компании · коды: 200, 204, 206, 400 · примеры
  ← path: companyID:int; query: searchText?:str → map<ResultsCompanyContactsListResult>
- `GET /Companies/{companyID}/contacts/{contactID}` — Возвращает контакт компании · коды: 200, 204 · примеры
  ← path: companyID:int, contactID:int → ResultsCompanyContactsGetResult
- `POST /Companies/{companyID}/contacts/{contactID}` — Добавляет контактное лицо к компании · коды: 201, 204, 409 · примеры
  ← path: companyID:int, contactID:int → ResultsCompanyContactsPostResult[]
- `DELETE /Companies/{companyID}/contacts/{contactID}` — Удаляет контактное лицо у компании · коды: 202, 409 · примеры
  ← path: companyID:int, contactID:int
- `GET /Companies/{companyID}/locations/actual` — Возвращает текущее местоположение компании · коды: 200, 204, 206 · примеры
  ← path: companyID:int → ResultsCommonLocationResult
- `GET /Companies/{id}` — Возвращает доступную пользователю компанию по идентификатору · коды: 200, 204 · примеры
  ← path: id:int → ResultsCompaniesGetResult
- `DELETE /Companies/{id}` — Помечает компанию как удалённую · коды: 202, 409 · примеры
  ← path: id:int

## CompanyAttachments
- `POST /CompanyAttachments` — Связывает компанию и вложение · коды: 201 · примеры
  ← body: CompanyActionDataOfInt[] → ResultsCompanyAttachmentsAddResult[]
- `DELETE /CompanyAttachments` — Помечает связку компании и вложения как удалённую · коды: 202 · примеры
  ← body: CompanyActionDataOfInt[]
- `POST /CompanyAttachments/upload/fromBody` — Загружает файл на файловый сервер и привязывает его к компании (данные из тела запроса) · коды: 201 · примеры
  ← body: DataCompanyAttachmentCompanyBodyUploadData → ResultsCompanyAttachmentsUploadResult
- `POST /CompanyAttachments/upload/fromForm` — Загружает файл на файловый сервер и привязывает его к компании (данные из формы) · коды: 201 · примеры
  ← query: CompanyID?:int, Description?:str, IsPublic?:bool, IsIgnorePossibleDuplication?:bool, Roles?:int[], Coordinate?:str, FileName?:str, ContentType?:str, Uid?:uuid, ContentStream.CanRead?:bool, ContentStream.CanSeek?:bool, ContentStream.CanWrite?:bool, ContentStream.Capacity?:int, ContentStream.Length?:int, ContentStream.Position?:int, ContentStream.CanTimeout?:bool, ContentStream.ReadTimeout?:int, ContentStream.WriteTimeout?:int, Md5Hash?:str, ContentLength?:int; body: { File: file } → ResultsCompanyAttachmentsUploadResult

## CompanyContacts
- `POST /CompanyContacts` — Добавляет контактные лица к компании · коды: 201, 204, 409 · примеры
  ← body: CompanyActionDataOfInt[] → ResultsCompanyContactsPostResult[]
- `DELETE /CompanyContacts` — Удаляет контактные лица у компании · коды: 202, 409 · примеры
  ← body: CompanyActionDataOfInt[]

## CompanyListQueries
- `GET /CompanyListQueries` — Возвращает список сохранённых запросов, доступных в тенанте · коды: 200, 204, 206 · примеры
  → map<ResultsCompanyListQueriesCompanyListQueryResult>
- `POST /CompanyListQueries` — Создаёт сохранённый запрос и привязывает его к текущему пользователю · коды: 201 · примеры
  ← body: ESCompanyListQueryAddData[] → int[]
- `PUT /CompanyListQueries` — Изменяет сохранённый запрос · коды: 202 · примеры
  ← body: ESCompanyListQueryUpdateData[]
- `DELETE /CompanyListQueries` — Помечает сохранённые запросы как удалённые · коды: 202 · примеры
  ← body: int[]
- `DELETE /CompanyListQueries/remove` — Физически удаляет сохранённые запросы · коды: 202 · примеры
  ← body: int[]
- `GET /CompanyListQueries/{id}` — Возвращает сохранённый запрос · коды: 200, 204 · примеры
  ← path: id:int → ResultsCompanyListQueriesCompanyListQueryGetResult
- `DELETE /CompanyListQueries/{id}` — Помечает сохранённый запрос как удалённый · коды: 202 · примеры
  ← path: id:int
- `DELETE /CompanyListQueries/{id}/remove` — Физически удаляет сохранённый запрос · коды: 202 · примеры
  ← path: id:int

## CompanyLocations
- `GET /CompanyLocations` — Возвращает список локаций компании · коды: 200, 204, 206, 409 · примеры
  ← query: companyID?:int, onDate?:datetime → map<ResultsCompaniesCompanyLocationResult>
- `POST /CompanyLocations` — Добавляет локацию к компании · коды: 202 · примеры
  ← body: ESCompanyLocationMergeData
- `PUT /CompanyLocations` — Обновляет локацию у компании · коды: 202 · примеры
  ← body: ESCompanyLocationMergeData
- `DELETE /CompanyLocations` — Удаляет привязку локации к компании · коды: 202 · примеры
  ← body: DataCompanyLocationsDeleteData

## CompanyRegistrationTypes
- `GET /CompanyRegistrationTypes` — Возвращает список видов регистрации компании · коды: 200, 204 · примеры
  → map<ResultsCompanyRegistrationTypesListResult>

## Districts
- `GET /Districts` — Возвращает список доступных пользователю участков · коды: 200, 204, 206 · примеры
  ← query: includePath?:bool, parentID?:int, districtID?:int, assetID?:int, userID?:int, taskTypeID?:int → ResultsDistrictsDistrictListForTenantMemberResult[]
- `POST /Districts` — Добавляет участок · коды: 201, 409 · примеры
  ← body: ESDistrictAddData[] → int[]
- `PUT /Districts` — Изменяет участок · коды: 202, 409 · примеры
  ← body: ESDistrictUpdateData[]
- `DELETE /Districts` — Помечает участки как удалённые · коды: 202, 409 · примеры
  ← body: int[]
- `PUT /Districts/parentAndReorder` — Изменяет родителя и/или сортировку участка · коды: 202, 409 · примеры
  ← body: ESDistrictParentUpdateData
- `GET /Districts/{id}` — Возвращает доступный пользователю участок по идентификатору · коды: 200, 204 · примеры
  ← path: id:int → ResultsDistrictsDistrictResult
- `DELETE /Districts/{id}` — Помечает участок как удалённый · коды: 202, 409 · примеры
  ← path: id:int

## Locations
- `GET /Locations` — Возвращает список локаций · коды: 200, 204, 206 · примеры
  ← query: searchText?:str, searchFor?:str, radius?:float, pointCenter?:str, pointNorthEast?:str, pointSouthWest?:str → map<ResultsCommonLocationResult>
- `POST /Locations` — Создаёт локации · коды: 200, 201, 400 · примеры
  ← body: DataLocationsPostData[]
- `PUT /Locations` — Изменяет локации · коды: 202, 400 · примеры
  ← body: DataLocationsPutData[]
- `DELETE /Locations` — Помечает локации как удалённые · коды: 202 · примеры
  ← body: int[]
- `HEAD /Locations` — Возвращает количество локаций · коды: 200, 206 · примеры
  ← query: searchFor?:str
- `DELETE /Locations/remove` — Физически удаляет локации · коды: 202 · примеры
  ← body: int[]
- `GET /Locations/{id}` — Возвращает локацию с областью · коды: 200, 204 · примеры
  ← path: id:int → ResultsLocationsLocationGetResult
- `DELETE /Locations/{id}` — Помечает локацию как удалённую · коды: 202 · примеры
  ← path: id:int
- `DELETE /Locations/{id}/remove` — Физически удаляет локацию · коды: 202 · примеры
  ← path: id:int

## OrgUnits
- `GET /OrgUnits` — Возвращает справочник активных организационных единиц, доступных пользователю · коды: 200, 204, 206 · примеры
  ← query: companyID?:int[] → map<ResultsOrgUnitsOrgUnitListResult>
- `GET /OrgUnits/root` — Возвращает справочник активных корневых организационных единиц, доступных пользователю · коды: 200, 204, 206 · примеры
  ← query: companyID?:int[] → map<ResultsOrgUnitsOrgUnitListResult>
- `GET /OrgUnits/{id}/orgunits` — Возвращает дочерние организационные единицы для указанного родителя · коды: 200, 204, 206, 400 · примеры
  ← path: id:int; query: companyID?:int[] → map<ResultsOrgUnitsOrgUnitListResult>

## PreferredTechnicians
- `GET /PreferredTechnicians` — Список предпочтительных исполнителей для объекта(ов) · коды: 200, 204 · примеры
  ← query: assetID?:int, userID?:int → ResultsPreferredTechniciansPreferredTechniciansResult
- `POST /PreferredTechnicians` — Добавление или удаление предпочтительного исполнителя для объекта · коды: 202, 400 · примеры
  ← body: AssetActionDataOfInt[]
