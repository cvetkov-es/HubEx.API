# ES — справочник ручек

> **Что здесь:** только read-ручки (GET/HEAD) сервиса ES (API for managing enterprise structure in HubEx): сигнатуры, параметры, права. Типы — schemas/ES.md.
> **Когда сюда идти:** найти ручку и её вход/выход. Типы — `schemas/ES.md`; грабли — `notes/ES.md` (если есть).
> **Линза read-only:** здесь только GET/HEAD. Write-ручки (POST/PUT/PATCH/DELETE) и их типы в API **существуют**, но в эту линзу не входят — не делай из их отсутствия здесь вывода, что их нет в API.

Base: `{BASE_URL}/ES`
> Примеры ответов вынесены в [../examples/ES.md](../examples/ES.md).

**Оглавление**

- AssetClasses — строки 30–34
- AssetFilter — строки 36–38
- AssetListQueries — строки 40–44
- AssetLocations — строки 46–48
- AssetSchemas — строки 50–64
- AssetSearchSettings — строки 66–68
- AssetTemplates — строки 70–86
- AssetTypes — строки 88–94
- Assets — строки 96–142
- Companies — строки 144–169
- CompanyListQueries — строки 171–175
- CompanyLocations — строки 177–179
- CompanyRegistrationTypes — строки 181–183
- Districts — строки 185–189
- Locations — строки 191–197
- OrgUnits — строки 199–208
- PreferredTechnicians — строки 210–212

## AssetClasses
- `GET /AssetClasses` — Возвращает список классов объектов. · коды: 200, 500
  → map<ResultsAssetClassesAssetClassListResult>
- `GET /AssetClasses/{id}` — Возвращает класс объекта · коды: 200
  ← path: id:int → ResultsAssetClassesAssetClassGetResult

## AssetFilter
- `GET /AssetFilter` — Возвращает список доступных фильтров для пользователя запросившего данные. · коды: 200
  ← query: selectedOnly?:bool → ProjectionsCOMMONFilterListItemProjection[]

## AssetListQueries
- `GET /AssetListQueries` — Возвращает список сохраненных запросов, доступных в тенанте · коды: 200
  → map<ResultsAssetListQueriesAssetListQueryResult>[]
- `GET /AssetListQueries/{id}` — Возвращает сохраненный запрос · коды: 200
  ← path: id:int → map<ResultsAssetListQueriesAssetListQueryResult>

## AssetLocations
- `GET /AssetLocations` — Список локаций по объекту · коды: 200, 409
  ← query: assetID?:int, onDate?:datetime

## AssetSchemas
- `GET /AssetSchemas/ascList/{assetID}` — Возвращает список существующих план-схем для текущего объекта и всех доступных объектов вверх по дереву · коды: 200, 400
  ← path: assetID:int → map<ResultsAssetSchemaSchemaBase>
- `GET /AssetSchemas/asset/{assetID}` — Возвращает план-схему привязанную к объекту или ближайшую по дереву сверху · коды: 200, 400
  ← path: assetID:int → ResultsAssetSchemaSchema
- `GET /AssetSchemas/list` — Возвращает полный список схем тенанта · коды: 200, 400
  → map<ResultsAssetSchemaSchemaBase>
- `GET /AssetSchemas/{schemaID}` — Возвращает план-схему по её уникальному идентификатору · коды: 200, 400
  ← path: schemaId:int → ResultsAssetSchemaSchema
- `GET /AssetSchemas/{schemaID}/points` — Возвращает полный список точек-заданий размещённых на план-схеме · коды: 200
  ← path: schemaID:int → ResultsAssetSchemaSchemaTask[]
- `GET /AssetSchemas/{schemaId}/image` — Получает информацию о картинке привязанной к план-схеме · коды: 200, 500
  ← path: schemaId:int; query: thumbnailSize?:int → ResultsAssetSchemaSchemaImage
- `GET /AssetSchemas/{schemaId}/image/download` — Метод получения TemporaryRedirect на временную ссылку для скачки файла прикреплённой план-схемы · коды: 303
  ← path: schemaId:int; query: thumbnailSize?:int, noRedirect?:bool

## AssetSearchSettings
- `GET /AssetSearchSettings` — Получение списка полей поиска объекта для текущего пользователя · коды: 200, 204 · примеры
  → ProjectionsESAssetSearchFieldSettingsProjection[]

## AssetTemplates
- `GET /AssetTemplates` — Список шаблонов ассета · коды: 200
  ← query: searchText?:str → map<ResultsAssetTemplatesListResult>
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

## AssetTypes
- `GET /AssetTypes` — Возвращает список типов объектов · коды: 200
  → map<ResultsAssetTypesGetResult>
- `GET /AssetTypes/{id}` — Возвращает тип объекта · коды: 200, 400, 404, 409
  ← path: id:int
- `GET /AssetTypes/{id}/workTypes` — Возвращает список относящихся к типу объекта видов работ · коды: 202
  ← path: id:int → IdNameEntityOfShort[]

## Assets
- `GET /Assets` — Возращает справочник объектов                     , доступных пользователю · коды: 200
  ← query: includePath?:bool, includeTaskActuality?:bool, searchText?:str, needForAllowedTasks?:bool → map<ResultsAssetsAssetExtResult>
- `HEAD /Assets` — Возвращает заголовок запроса пользователей с количеством данных, удовлетворяющих фильтру · коды: 200
- `GET /Assets/attributes` — Возвращает список атрибутов по объектам · коды: 200
  → ResultsAssetsAssetAttributesExtResult[]
- `GET /Assets/root` — Возращает справочник корневых объектов, доступных пользователю. · коды: 200
  → map<ResultsAssetsAssetExtResult>
  Доступность объекта определяется по пересечанию участков пользователя и объека, наличию полномочия
AllDistricts или AllAssets. Корневой объект - объект не имеющий объекта более высого уровня среди 
доступных пользователю.
- `GET /Assets/{assetID}` — Детальная информация по объекту · коды: 200, 400
  ← path: assetID:int → ResultsAssetsAssetDetailedInfoResult
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
- `GET /Assets/{assetID}/contacts` — Возвращает список действующих контактов для объекта · коды: 200, 400
  ← path: assetID:int; query: searchText?:str → ResultsAssetContactsListResult[]
- `GET /Assets/{assetID}/contacts/{contactID}` — Возвращает контакт объекта · коды: 200
  ← path: assetID:int, contactID:int → ResultsAssetContactsGetResult
- `GET /Assets/{assetID}/districts` — Возвращае список участков для объекта. · коды: 200, 400
  ← path: assetID:int → ResultsCommonAssetDistrictResult[]
- `GET /Assets/{assetID}/locations/actual` — Возвращает текущее местоположение объекта · коды: 200
  ← path: assetID:int → ResultsCommonLocationResult
- `GET /Assets/{assetID}/skills` — Возвращает список навыков объекта · коды: 200
  ← path: assetID:int → map<ResultsAssetSkillsAssetSkillResult>
- `GET /Assets/{assetID}/tags` — Возвращает список активных (не удаленых) тэгов по объекту. · коды: 200, 400
  ← path: assetID:int → str[]
- `GET /Assets/{assetID}/workTypes` — Возвращае список доступных по объекту видов работ. · коды: 200
  ← path: assetID:int → map<ResultsAssetsAssetWorkTypeResult>
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
- `HEAD /Companies` — Возвращает заголовок запроса доступных пользователю компаний с количеством данных, удовлетворяющих фильтру · коды: 200
  ← query: searchText?:str
- `GET /Companies/dadata/find` — Поиск информации о компании по ИНН. · коды: 200, 204
  ← query: inn?:str → ESCompanyAddData
- `GET /Companies/{CompanyID}/attachments/{attachmentID}` — Возвращает TemporartRedirect на временную ссылку для скачки файла · коды: 307
  ← path: companyID:int, attachmentID:int; query: thumbnailSize?:int, noRedirect?:bool
- `GET /Companies/{companyID}/attachment/{attachmentID}` — Прикрепленный файл к компании
<param name="companyID">Идентификатор компании</param><param name="attachmentID">Идентификатор прикрепленного файла к компании</param><param name="thumbnailSize">Размер эскиза (будет возвращен ближайший больший эскиз из доступных)</param> · коды: 200, 500
  ← path: companyID:int, attachmentID:int; query: thumbnailSize?:int → ResultsCommonGetAttachmentResult
- `GET /Companies/{companyID}/attachments` — Возвращает список файлов вложенных в компанию. · коды: 200, 400
  ← path: companyID:int; query: thumbnailSize?:int → map<ResultsCommonListAttachmentResult>
- `GET /Companies/{companyID}/attributes` — Возвращает список пользовательских атрибутов компании · коды: 200, 204, 400
  ← path: companyID:int → ResultsCompanyAttributesCompanyAttributeResult[]
- `GET /Companies/{companyID}/bankAccounts` — Возвращает список банковских счетов компании · коды: 200, 400
  ← path: companyID:int; query: searchText?:str → map<ResultsCompanyBankAccountsListResult>
- `GET /Companies/{companyID}/contacts` — Возвращает список контактов компании · коды: 200, 400
  ← path: companyID:int; query: searchText?:str → map<ResultsCompanyContactsListResult>
- `GET /Companies/{companyID}/contacts/{contactID}` — Возвращает контакт компании · коды: 200
  ← path: companyID:int, contactID:int → ResultsCompanyContactsGetResult
- `GET /Companies/{companyID}/locations/actual` — Возвращает текущее местоположение компании · коды: 200
  ← path: companyID:int → ResultsCommonLocationResult
- `GET /Companies/{id}` — Возвращает доступную пользователю компанию по идентификатору · коды: 200
  ← path: id:int → ResultsCompaniesGetResult

## CompanyListQueries
- `GET /CompanyListQueries` — Возвращает список сохраненных запросов, доступных в тенанте · коды: 200
  → map<ResultsCompanyListQueriesCompanyListQueryResult>
- `GET /CompanyListQueries/{id}` — Возвращает сохраненный запрос · коды: 200
  ← path: id:int → ResultsCompanyListQueriesCompanyListQueryGetResult

## CompanyLocations
- `GET /CompanyLocations` — Список локаций по компании · коды: 200, 409
  ← query: companyID?:int, onDate?:datetime

## CompanyRegistrationTypes
- `GET /CompanyRegistrationTypes` — Возвращает список видов регистрации компании · коды: 200
  → map<ResultsCompanyRegistrationTypesListResult>

## Districts
- `GET /Districts` — Возвращает список доступных пользователю участков. · коды: 200
  ← query: includePath?:bool → ResultsDistrictsDistrictListForTenantMemberResult[]
- `GET /Districts/{id}` — Возвращает доступный пользователю участок по идентификатору · коды: 200
  ← path: id:int → ResultsDistrictsDistrictResult

## Locations
- `GET /Locations` — Возвращает список локаций · коды: 200
  ← query: searchText?:str, searchFor?:str → map<ResultsCommonLocationResult>
- `HEAD /Locations` — Возвращает количество локаций · коды: 200
  ← query: searchFor?:str
- `GET /Locations/{id}` — Возвращает локацию с областью. · коды: 200
  ← path: id:int → map<ResultsLocationsLocationGetResult>

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
